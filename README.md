# isbusy code for Claude Code

Drives an [isbusy code](https://code.isbusy.co) light from your Claude Code
sessions: **green** ready for a prompt, **yellow** working, **red** needs you
(a permission to grant, a question to answer, a turn that failed).

```
/plugin marketplace add berkaycubuk/isbusy-code
/plugin install isbusy-code@isbusy
/isbusy-code:link XXXXX-XXXXX        # the code from code.isbusy.co/setup
```

`/isbusy-code:status` and `/isbusy-code:unlink` do what they say.

## What it sends

Only two things, to `code.isbusy.co`: the name of the event (`start`,
`prompt`, `tool`, `attention`, `stop`, `end`) and Claude Code's session id.
The hook's input - your prompts, file paths, tool names - is read for the
session id and nothing else, and never leaves your computer. It is all in one
short shell script: [`bin/isbusy-code`](bin/isbusy-code).

Each hook runs in the background and gives up after three seconds, so a slow
network never makes Claude wait. With several sessions open, the light shows
the most urgent one.

Your key lives in `~/.config/isbusy-code/key` (mode 600). `ISBUSY_CODE_URL`
points the plugin at another relay.

Made by [isbusy](https://isbusy.co). MIT licensed.
