# isbusy code for Claude Code

Drives an [isbusy code](https://code.isbusy.co) light from your Claude Code
sessions: **green** ready for a prompt, **yellow** working, **red** needs you
(a permission to grant, a question to answer, a turn that failed).

```
/plugin marketplace add berkaycubuk/isbusy-code
/plugin install isbusy-code@isbusy
/isbusy-code:link XXXXX-XXXXX        # the code from code.isbusy.co/setup
```

`/isbusy-code:phone` pairs your phone (below). `/isbusy-code:status` and
`/isbusy-code:unlink` do what they say.

## Your phone and watch

`/isbusy-code:phone` pairs the isbusy code Android app. From then on a
permission prompt also reaches your phone, and through it your watch, with
**Allow**, **Deny** and **Deny with a reason**. The terminal prompt stays up
the whole time; whichever you answer first wins, and the other one goes away.
No light needed.

When Claude asks you something instead (its multiple-choice questions), the
phone shows one question at a time with its options as choices - chips on the
phone, a list on the watch - plus voice or keyboard for an answer of your own,
and **Skip**. The answers reach Claude as if picked in the terminal.

A reason reaches Claude as the reason for the denial, not as an instruction:
Claude Code treats it like any other tool result and will ask you before
acting on it.

## What it sends

For the light, only two things go to `code.isbusy.co`: the name of the event
(`start`, `prompt`, `tool`, `attention`, `stop`, `end`) and Claude Code's
session id. The hook's input - your prompts, file paths, tool names - is read
for the session id and nothing else.

With a phone paired, a permission request also goes to your phone: the tool's
name, what it wants to run or touch (the command, file or URL, cut to 700
characters), its description, and the project folder's name; for a question, the questions
and their option labels instead (not the descriptions). It is sealed
with a key that only this computer and your phone hold - it reaches the phone
inside the QR code, never through the relay - so `code.isbusy.co` passes it
on without being able to read it, and cannot forge an answer: this computer
checks the seal before it lets anything run. What the relay does see is that
a request was made, when, and when it was answered.

Everything is in one shell script: [`bin/isbusy-code`](bin/isbusy-code).
It needs `curl` and `openssl`; the phone also needs `jq`, which macOS has
built in since Sequoia.

Each light hook runs in the background and gives up after three seconds, so a
slow network never makes Claude wait. With several sessions open, the light
shows the most urgent one.

Your key lives in `~/.config/isbusy-code/key` and the phone's sealing key in
`~/.config/isbusy-code/phone` (both mode 600). `ISBUSY_CODE_URL`
points the plugin at another relay.

Made by [isbusy](https://isbusy.co). MIT licensed. `web/qrcode.js` is Kazuhiko Arase's QR Code Generator
(MIT, qrcode-generator 2.0.4 from npm).
