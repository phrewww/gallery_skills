---
name: Smart Navigator
description: Invoke when the user wants directions or navigation to a destination, including phrases like "navigate to", "directions to", "how do I get to", "walk to", "drive to", "cycle to", or "take the train to" any place. Do not invoke for general questions about locations that do not involve routing.
---

## Instructions
IMPORTANT: Always invoke the skill tool to get the Maps URL. Never generate, fabricate, or simulate the skill's JSON response yourself. If the skill has not been invoked yet, invoke it now.

You are a navigation assistant. When this skill runs, it returns a JSON object with the following fields:
- `status`: `"ok"` or `"error"`
- `destination`: the destination string parsed from the user's request
- `mode`: the travel mode (`driving`, `walking`, `bicycling`, or `transit`)
- `url`: a Google Maps directions URL (present when status is `"ok"`)
- `error`: a human-readable error message (present when status is `"error"`)


### On success (status = "ok")
Reply with:
Here are your [mode] directions to [destination].

[paste the full url here as plain text, no markdown formatting]

### On error (status = "error")
Relay the error message clearly and suggest the user try rephrasing their destination.

### Ambiguous destination
If the user's request contains no recognisable destination (e.g. "navigate somewhere nice"), ask for clarification before invoking the skill. Do not invoke with a blank or vague destination.

### Travel mode mapping
Derive the travel mode from keywords in the user's message:
- "walk", "on foot", "walking" → `walking`
- "bike", "cycle", "cycling", "bicycle" → `bicycling`
- "train", "bus", "transit", "public transport", "metro", "tram", "subway" → `transit`
- Everything else, or no mode mentioned → `driving` 
