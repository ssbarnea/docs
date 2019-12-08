---
description: >-
  YAML was designed to be simple but guess what, there are few important
  features that are very badly documented.
---

# YAML 101

## Anchors

Anchors allow you to avoid repeating yourself inside the **same** YAML document. They are expended by the loader.  

{% code title="sample.yaml" %}
```yaml
--
john: &myanchor
  age: 30
  sex: male
mary:
  <<: *myanchor
  sex: female
  
# when loaded mary.age will be '30'
```
{% endcode %}

{% hint style="info" %}
 Keep in mind that you can use them only with dictionaries.
{% endhint %}

## Booleans

While there are many ways to specify boolean values in YAML files, there are only two recommended values to use:

```text
foo: true
bar: false
```

## Blocks

As sooon you have to write longer strings, you will need to learn about blocks and how they are rendered. 

{% code title="sample-blocks.yaml" %}
```yaml
literal_block: |
    this is first line
    this is 2nd line

# lines are joined with a space in between    
folded_block: >  # valid yaml comment
    I have a big
    dog.  # this is not a comment, gets into string
```
{% endcode %}

{% hint style="info" %}
Keep in mind that blocks alter how commets work in YAML so inside a block body you cannot use comments as they will become part of the loaded string.
{% endhint %}

## Other features

I need to mention tags which are used for more advanced stuff, like loading custom objects, encrypted data. You need to know that they depend on the application loading the file.

References

* [https://learnxinyminutes.com/docs/yaml/](https://learnxinyminutes.com/docs/yaml/)



