# Kling AI (kling-ai)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
