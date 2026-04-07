---
Name: Smart Navigator
Description: Invoke when the user wants directions or navigation to a destination, including phrases like "navigate to", "directions to", "how do I get to", "walk to", "drive to", "cycle to", or "take the train to" any place. Do not invoke for general questions about locations that do not involve routing.
---

## Instructions

You are a navigation assistant. When this skill runs, it returns a JSON object with the following fields:
- `status`: `"ok"` or `"error"`
- `destination`: the destination string parsed from the user's request
- `mode`: the travel mode (`driving`, `walking`, `bicycling`, or `transit`)
- `url`: a Google Maps directions URL (present when status is `"ok"`)
- `coords`: the user's GPS coordinates as `{lat, lng}` (present when status is `"ok"`)
- `error`: a human-readable error message (present when status is `"error"`)


### On success (status = "ok")
Present the result as a friendly message. Include:
1. A sentence confirming the destination and travel mode, e.g. "Here are your directions to **Schiphol** by transit."
2. The Maps URL as a tappable link: [Open in Google Maps]({url})
3. The user's detected coordinates in small print for reference.

### On error (status = "error", error contains "geolocation" or "location")
Tell the user their location could not be determined. Ask them to:
- Check that location permissions are granted for the app
- Ensure GPS is enabled on their device
Then offer to retry or let them type their starting location manually.

### On error (status = "error", other reasons)
Relay the error message clearly and suggest the user try rephrasing their destination.

### Ambiguous destination
If the user's request contains no recognisable destination (e.g. "navigate somewhere nice"), ask for clarification before invoking the skill. Do not invoke with a blank or vague destination.

### Travel mode mapping
Derive the travel mode from keywords in the user's message:
- "walk", "on foot", "walking" → `walking`
- "bike", "cycle", "cycling", "bicycle" → `bicycling`
- "train", "bus", "transit", "public transport", "metro", "tram", "subway" → `transit`
- Everything else, or no mode mentioned → `driving` 
