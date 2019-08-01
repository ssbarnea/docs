---
description: >-
  This article documents a pattern for loading Ansible variables specific to
  various operating systems in a maintainable way.
---

# Distro specific variables

Using `when` conditions in Ansible for adding support for multiple platforms and their versions does not scale well. As soon you need to support more than two versions it will hit you hard and make your code hard to maintain.

The trick is to load tailored presets for each platform and version when your role starts and use these values of these variables when performing tasks. Most of the time this saves you from adding conditions to tasks.

This can nicely be achieved by using an overlayed configuration file loading pattern, one that loads the more specific configs after more generic ones, overriding previously loaded values.

Doing this allows you to define overrides in a minimal number of places, more exactly at the location where the new config diverge from what the default one.

```yaml
- name: Include OS specific variables
  include_vars: "{{ item }}"
  failed_when: false
  loop:
      - "family-{{ ansible_os_family | lower }}.yml"
      - "family-{{ ansible_os_family | lower }}-{{ ansible_distribution_major_version | lower }}.yml"
      - "{{ ansible_distribution | lower }}.yml"
      - "{{ ansible_distribution | lower }}-{{ ansible_distribution_major_version | lower }}.yml"
      - "{{ ansible_distribution | lower }}-{{ ansible_distribution_version.split('.')[0:2] | join('-') | lower }}.yml"
      - "{{ ansible_distribution | lower }}-{{ ansible_distribution_version.split('.')[0:3] | join('-') | lower }}.yml"
 # pattern: v2
 
 # define variables in files like:
 # vars/family-redhat.yml # common to Fedora/RHEL/CentOS
 # vars/centos-7.yml
 # vars/family-debian.yml # common to Debian, Ubuntu,...
 # vars/ubuntu.yml # all Ubuntu versions
```

The example above is the current version which I am currently using whenever I need to load OS specific variables in ansible. 

As you can see, I included a version on it in order to better track changes. The v2 was introduced recently by adding the family suffix. This was needed in order to avoid an unexpected bug caused by the fact that, for Red Hat Enterprise Linux, Ansible populates both **ansible\_os\_family** and **ansible\_distribution** with "_**RedHat**_", meaning that 1st file and 3rd line would be the same and we would not be able to load configuration correctly.

This type of configuration loading is very easy to understand and is less-error prone than editing conditionds spread across the role. It major advantage is that it isolates config from code.

My hope for the future is that Ansible will be able to do this automaticallly if you create the special files in vars/, so you would not even need to manually load the at the start of the playbook.

