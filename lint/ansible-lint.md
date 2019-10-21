---
description: Some hints about using ansible-lint
---

# ansible-lint

### Accessing Ansible modules from other repos

In the unlikely case where you would end up with `ansible-lint` errors caused by the fact that it fails to find some Ansible modules which may not even be located inside your own repository, I provide this hack for you which assures is able to find `zuul_return` module which is part of `zuul` Python package.

{% code-tabs %}
{% code-tabs-item title=".pre-commit-config.yaml" %}
```yaml
  - repo: https://github.com/ansible/ansible-lint.git
    rev: v4.1.1a0
    hooks:
      - id: ansible-lint
        files: \.(yaml|yml)$
        # Helps it find zuul_return module on both zuul and on dev environments,
        # Based on https://github.com/pre-commit/pre-commit/issues/758
        entry: >
          bash -c 'env ANSIBLE_LIBRARY=`python -c "import os, zuul;
          print(os.path.dirname(zuul.__file__))"`/ansible/base/actiongeneral/
          ansible-lint --force-color -v "$@"'
        exclude: playbooks/legacy
        additional_dependencies:
          - zuul
```
{% endcode-tabs-item %}
{% endcode-tabs %}





