# Skipping tasks during testing

Sometimes there are role tasks that you cannot or don't want to run during functional testing. There are two magic ansible tags that you can use to mark these: `notest` and `molecule-notest`. Keep in mind that you can also use them on blocks or even at playbook level.

