---
name: Smart Navigator
description: Show navigation directions to a destination. Invoke for requests like walking, driving, cycling, or transit directions to any place.
---

## Instructions

Extract the destination and travel mode from the user's message, then call `run_js` with a JSON string:

```json
{"destination": "<place name>", "mode": "<driving|walking|bicycling|transit>"}
```

Travel mode mapping:
- "walk", "walking", "on foot" → `walking`
- "bike", "cycle", "bicycle" → `bicycling`
- "train", "bus", "transit", "metro", "tram", "subway" → `transit`
- Default → `driving`

When `run_js` returns, present only the `url` field as a tappable link — nothing else.
