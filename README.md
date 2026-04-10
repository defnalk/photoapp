# My Photos

A personal photo archive that stores your images on GitHub — no backend, no accounts beyond GitHub, no dependencies.

## How it works

Everything runs from a single `index.html` file opened in your browser. Photos are stored in a private GitHub repository using the [GitHub Contents API](https://docs.github.com/en/rest/repos/contents). Your credentials stay in `localStorage` on your machine and are only sent to `api.github.com`.

## Getting started

1. Open `index.html` in any modern browser
2. Follow the onboarding wizard — it walks you through creating a GitHub account, a private repo, and a personal access token
3. Start uploading photos

That's it. No install, no server, no build step.

## Features

- **Guided setup** — step-by-step onboarding designed for non-technical users
- **Drag-and-drop upload** — supports JPG, PNG, WEBP, and GIF with per-file progress bars
- **Gallery view** — responsive grid with lazy-loaded images
- **Lightbox** — click any photo to view fullscreen, download, or delete
- **Plain-English errors** — no status codes or API jargon shown to the user
- **Offline credentials** — token and username stored in `localStorage`, never sent to any third party
- **Zero dependencies** — vanilla HTML, CSS, and JS in a single file

## Tech details

| | |
|---|---|
| **Storage** | GitHub Contents API (`PUT`/`GET`/`DELETE` on `/repos/{owner}/myphotos/contents/photos/`) |
| **Auth** | GitHub personal access token with `repo` scope, sent via `Authorization: Bearer` header |
| **Upload** | Files are read as base64 via `FileReader` and pushed with a commit message |
| **Delete** | Uses the file's SHA from the listing response |
| **Persistence** | `localStorage` key `myphotos` stores `{ token, username, setupDone }` |

## Limitations

- GitHub API has a [rate limit](https://docs.github.com/en/rest/rate-limit) of 5,000 requests/hour for authenticated users
- Individual file uploads are limited to 100 MB via the Contents API
- The listing endpoint returns up to 1,000 files per directory
- Images are served from `raw.githubusercontent.com` which may be slow for very large files
