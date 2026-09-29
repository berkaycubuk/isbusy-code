---
description: Link this computer to your isbusy code light, with the code from code.isbusy.co/setup
argument-hint: XXXXX-XXXXX
disable-model-invocation: true
allowed-tools: Bash(${CLAUDE_PLUGIN_ROOT}/bin/isbusy-code *)
---

!`"${CLAUDE_PLUGIN_ROOT}/bin/isbusy-code" link $ARGUMENTS`

Tell the user the line above, as is, and nothing else.
