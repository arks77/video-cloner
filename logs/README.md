# Generation log — `logs/video-clone.jsonl`

One JSON object per line, appended on every generation. It is the cheapest, most accurate
source for cost estimates and for diagnosing what worked. **Never** log secrets, auth
headers, or full prompt text.

## Lifecycle

1. **On submit success:** append an entry with the request config + `jobId` and
   `status: "pending"`.
2. **On poll completion:** update that entry with the outcome (`status`, `costCharged`,
   `genTimeSec`, `outputUrl`, `error`).

## Schema

```json
{
  "timestamp": "2026-06-12T10:00:00.000Z",
  "backend": "<from adapters/active.md identity>",
  "endpoint": "<submit endpoint or sdk call>",
  "model": "<model id>",
  "jobId": "<id returned by submit>",
  "flow": "clone-ad | analyze-video | direct",
  "request": {
    "duration": 15,
    "resolution": "720p",
    "aspectRatio": "9:16",
    "audioEnabled": true,
    "inputType": "text-to-video | image-to-video | video-to-video",
    "referenceImagesCount": 1,
    "referenceVideosCount": 0,
    "referenceAudiosCount": 0,
    "promptWordCount": 180,
    "styleTemplate": "<prompt-library file used>"
  },
  "response": {
    "status": "done | failed | pending",
    "costCharged": 720,
    "genTimeSec": 240,
    "outputUrl": "<final video/image URL>",
    "error": null
  },
  "session": { "container": "video-clone — 2026-06-12", "notes": "free-form" }
}
```

## Querying for a cost estimate

Grep for the same `model` with a similar config (matching `duration`, `resolution`,
`inputType`, `referenceImagesCount`) and reuse the recorded `costCharged`. If no match,
fall back to the pricing table in `adapters/active.md`, then ask the user.
