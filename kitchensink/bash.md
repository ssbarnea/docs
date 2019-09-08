# Bash 101

## Bash strict mode

One of my top favorite articles around base is [unofficial-bash-strict-mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) and  I recommend anyone to read it in order to understand why they should start every new shell script with that line below, even if they plan to write only a couple of commands.

{% code-tabs %}
{% code-tabs-item title="bash-seed.sh" %}
```bash
#!/usr/bin/env bash
set -euo pipefail

# Or during development
set -euxo pipefail

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
 There are some gotchas regarding using the magic strict mode. For example out of all platforms I tested Ubuntu chokes on the use of `-o pipefail` with default shell, which is not bash. Remember to force shell for Ubuntu.
{% endhint %}

This bash strict mode also works with [zsh](https://support.apple.com/en-us/HT208050) so no need to worry about forcing the shell, especially as in newer [MacOS default shell is zsh](https://support.apple.com/en-us/HT208050), kudos goes to Apple for having the balls to do it before others.

