# SUDO Privilege Escalation Cheat Sheet

## Dangerous Programs When Allowed via sudo

If any of the following binaries appear in `sudo -l`, treat it as an immediate escalation opportunity.

---

## Editors

- vi
- vim
- nano
- ed

These often allow execution of system commands from inside the editor.

---

## Viewers / Pagers

- less
- more
- man

These can sometimes spawn a shell or execute commands.

---

## Interpreters

- python
- perl
- ruby
- lua
- node

These can execute arbitrary system commands directly.

---

## System Utilities

- bash
- sh
- find
- awk
- tar
- zip
- rsync

Many of these support command execution flags or shell escapes.

---

## Why They Are Dangerous

These programs frequently support:

- `:!bash`
- `!sh`
- `shell=True`
- `--exec`
- `-e`
- command substitution
- spawning subshells

If executed with sudo privileges, any spawned shell runs as root.

---

## Quick Mental Checklist

After running:

```
sudo -l
```

Ask yourself:

1. Is the allowed binary interactive?
2. Can it execute system commands?
3. Does GTFOBins list a "Sudo" escape for it?

If yes → test escalation immediately.

---

## Pro Tip

Always check:

[https://gtfobins.github.io](https://gtfobins.github.io)

Search the binary name → review the "Sudo" section.

---

## Core Principle

Sudo + Interactive Binary = Potential Root Shell
