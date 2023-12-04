# Ad-hoc Commands
Ad-hoc commands are used for quick, one-time-use tasks.
```
# Example: Check files in all hosts belonging to the group
ansible <groupname> -a "ls"

# Update files for the group
ansible <groupname> -a "touch filez"
```
