# Kling AI (kling-ai)

Kling AI is Kuaishou's generative video AI platform. The Kling AI Open Platform (developer API) turns text and images into video and imagery through an asynchronous **create-a-task then query-the-task** workflow, covering text-to-video, image-to-video, multi-image-to-video, video extension, lip-sync, video effects, image generation (Kolors), and Kolors virtual try-on. The API authenticates with a JWT signed from an Access Key / Secret Key pair and is billed against prepaid resource packs.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/kling-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/kling-ai/refs/heads/main/apis.yml)

## Access Model (Honest Notes)

- **Gated, key-based.** You register on the [Kling AI Open Platform](https://app.klingai.com/global/dev), obtain an **Access Key** and **Secret Key**, and generate a short-lived **JWT** (HS256) client-side for every request. The Access Key is the `iss` claim; `exp` is ~30 minutes out; `nbf` is ~5 seconds in the past. The token is sent as `Authorization: Bearer <token>`.
- **Asynchronous by design.** Nothing returns a finished video inline. You `POST` to create a task, get back a `task_id`, then poll the matching `GET .../{task_id}` endpoint (or supply a `callback_url`) until `task_status` is `succeed`. Generated asset URLs are short-lived — download them promptly.
- **Base URL:** `https://api.klingai.com` (with a `/v1` prefix for generation endpoints).
- **Prepaid billing.** Consumption draws down prepaid **resource packs**; new accounts get a small free credit grant, and failed API tasks are reported not to deduct resources.
- **Documentation caveat.** Kling's official reference pages block automated fetching (HTTP 446). The endpoint paths, JWT scheme, async task model, and model catalog here are well corroborated across Kling's docs and multiple public wrappers; the fine-grained request/response field schemas in the OpenAPI are **honestly modeled** (`endpointsModeled: true`) and should be reconciled against the live reference before code generation.

## Tags

- Video Generation
- AI Video
- Generative AI
- Text-to-Video
- Image-to-Video
- Lip Sync
- Virtual Try-On
- Image Generation

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Kling AI Text-to-Video API

Generate video from a text prompt across Kling video models (kling-v1 through kling-v2-6 and the turbo/master variants), with duration, aspect ratio, standard/professional mode, and cfg_scale. Submit a task with POST, then poll GET by task_id for the rendered video URL.

- **Human URL:** [https://app.klingai.com/global/dev/document-api/apiReference/model/textToVideo](https://app.klingai.com/global/dev/document-api/apiReference/model/textToVideo)
- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Image-to-Video API

Animate a still image into video from a start frame (and optional end frame) plus a motion prompt. Async create-then-query task pattern.

- **Human URL:** [https://app.klingai.com/global/dev/document-api/apiReference/model/imageToVideo](https://app.klingai.com/global/dev/document-api/apiReference/model/imageToVideo)
- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Multi-Image-to-Video API

Compose a video from multiple reference images (subjects/elements) plus a prompt. Async create-then-query task pattern.

- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Video Extension API

Extend a previously generated video by referencing its origin task id and an optional continuation prompt, adding seconds of coherent footage.

- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Lip-Sync API

Drive lip movement on a generated or uploaded video from supplied text (text-to-speech voice) or an audio file.

- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Video Effects API

Apply preset creative video effects (hug, kiss, squish, and other scene templates) to one or more input images.

- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Image Generation API

Generate still images from a text prompt (and optional reference image) using the Kolors image models (kling-v1 through kling-v2-1).

- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Virtual Try-On API

Kolors Virtual Try-On composites a garment image onto a person/model image to produce a realistic try-on result (model kolors-virtual-try-on-v1-5).

- **Base URL:** `https://api.klingai.com/v1`

### Kling AI Account Resource API

Query account resource-pack balances and consumption so callers can monitor remaining prepaid credits.

- **Base URL:** `https://api.klingai.com`

## Common Properties

- [Authentication](authentication/kling-ai-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/kling-ai)
- [Website](https://klingai.com)
- [Documentation](https://app.klingai.com/global/dev/document-api/quickStart/productIntroduction/overview)
- [Plans](plans/kling-ai-plans-pricing.yml)
- [Rate Limits](rate-limits/kling-ai-rate-limits.yml)
- [Fin Ops](finops/kling-ai-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
