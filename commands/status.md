---
description: Is this computer linked to an isbusy code light?
disable-model-invocation: true
allowed-tools: Bash(${CLAUDE_PLUGIN_ROOT}/bin/isbusy-code *)
---

!`"${CLAUDE_PLUGIN_ROOT}/bin/isbusy-code" status`

Tell the user the line above, as is, and nothing else.
