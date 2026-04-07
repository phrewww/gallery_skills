---
Name: Smart Navigator
Description: Invoke when the user wants directions or navigation to a destination. Examples: "Walk to Dam Square", "Navigate to Schiphol by train", "Drive to the Rijksmuseum", "Directions to Central Station".
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

When `run_js` returns, display the embedded map to the user.
