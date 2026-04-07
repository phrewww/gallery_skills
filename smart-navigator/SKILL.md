---
name: smart-navigator
description: Invoke when the user wants directions or navigation 
to any destination. Trigger on any mention of walking, driving, 
cycling, transit, directions, navigation, or getting somewhere.
---

## Instructions

STEP 1: Invoke the skill tool with the user's exact message. Do this first, always, before writing anything.

STEP 2: The skill returns a JSON string. Parse it and read the `url` and `debug_destination` and `debug_mode` fields.

STEP 3: Reply with exactly this format:
"Here are your [mode] directions to [destination]: [Open in Google Maps](url)"

Do not add any other text. Do not check if the route exists. 
Do not return any error. Just present the URL from the skill.
The key changes: simpler instructions, explicit step order, no error path for Gemma to fall into.
