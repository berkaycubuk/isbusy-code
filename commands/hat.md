---
description: Pair a Game HAT, so permission prompts reach it and its joystick answers them
argument-hint: "[ok]"
disable-model-invocation: true
allowed-tools: Bash(${CLAUDE_PLUGIN_ROOT}/bin/isbusy-code *)
---

!`"${CLAUDE_PLUGIN_ROOT}/bin/isbusy-code" hat $ARGUMENTS`

Tell the user the lines above, as is, and nothing else.
