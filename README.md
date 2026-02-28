# **HuggingFace Organization Stats**

A single-page web application for viewing detailed statistics of any HuggingFace organization. Displays models, datasets, spaces, lifetime downloads, monthly downloads, and likes in a clean, tree-structured interface.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Demo](#demo)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Token Configuration](#token-configuration)
- [Interface Guide](#interface-guide)
- [Sorting and Filtering](#sorting-and-filtering)
- [Copy and Export](#copy-and-export)
- [Supported Organizations](#supported-organizations)
- [Technical Details](#technical-details)
- [API Endpoints Used](#api-endpoints-used)
- [Browser Support](#browser-support)
- [Limitations](#limitations)
- [License](#license)
- [Author](#author)

## Overview

HF Org Stats is a lightweight, client-side tool that fetches and presents comprehensive statistics for any public (or private, with a token) HuggingFace organization. It requires no backend server, no build step, and no dependencies beyond a modern web browser. All data is fetched directly from the HuggingFace API.

## Features

- **Organization Profile Display** -- Shows organization name, avatar, full name, and member count.
- **Aggregate Statistics** -- Total models, datasets, and spaces at a glance.
- **Lifetime Downloads** -- All-time download counts for models and datasets.
- **Monthly Downloads** -- Downloads from the last 30 days for models and datasets.
- **Likes** -- Total like counts across all repository types.
- **Tree View** -- File-explorer-style hierarchical listing of all repositories.
- **Sorting** -- Sort by all-time downloads, monthly downloads, likes, or recency.
- **Filtering** -- Search/filter repositories by name within any tab.
- **Tab Navigation** -- Switch between models, datasets, and spaces views.
- **Dark/Light Theme** -- Toggle between themes with preference saved to local storage.
- **Token Support** -- Optional HuggingFace access token for private repositories and improved rate limits.
- **Copy to Clipboard** -- Copy individual repository IDs or the entire tree output as plain text.
- **Pagination Handling** -- Automatically fetches all pages of results for organizations with large numbers of repositories.
- **Responsive Design** -- Works on desktop and mobile screens.
- **No Build Required** -- Single HTML file with inline CSS and JavaScript.

## Getting Started

### Option 1: Direct File

1. Download the `index.html` file.
2. Open it in any modern web browser.

### Option 2: Local Server

```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .
```

Then navigate to `http://localhost:8000` in your browser.

### Option 3: Deploy

Upload the single HTML file to any static hosting service such as GitHub Pages, Netlify, Vercel, or Cloudflare Pages.

## Usage

1. Enter an organization name in the input field (for example, `meta-llama`, `google`, `microsoft`).
2. Click **Fetch Stats** or press Enter.
3. View the organization profile, aggregate statistics, and detailed repository listings.
4. Use tabs to switch between Models, Datasets, and Spaces.
5. Use sort and filter controls to find specific repositories.

The organization name is stored in the URL hash, so you can bookmark or share links directly:

```
https://your-deployment.com/#meta-llama
```

## Token Configuration

A HuggingFace access token is optional but recommended for the following reasons:

- **Private Repositories** -- Access organization repositories that are not public.
- **Higher Rate Limits** -- Avoid API throttling when fetching large organizations.
- **Accurate Lifetime Stats** -- Some statistics fields require authentication to return complete data.

### Setting a Token

1. Click the **Token** button in the header.
2. Paste your HuggingFace access token (starts with `hf_`).
3. Click **Save**.

The token is stored in your browser's local storage. It is never sent to any server other than the HuggingFace API.

### Generating a Token

1. Go to [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).
2. Create a new token with `read` access.
3. Copy the token and paste it into the application.

### Clearing a Token

Click the **Clear** button in the token panel to remove the stored token.

## Interface Guide

### Profile Card

Displays the organization avatar, name (linked to the HuggingFace profile), full name if available, and member count. The three overview cards show total counts for models, datasets, and spaces, and can be clicked to switch tabs.

### Tab Bar

Three tabs for switching between repository types:

| Tab | Description |
|-----|-------------|
| Models | Machine learning models published by the organization |
| Datasets | Datasets published by the organization |
| Spaces | Gradio, Streamlit, or other interactive applications |

### Statistics Row

Shows aggregate numbers for the currently selected tab:

- **Total Count** -- Number of repositories of the selected type.
- **Downloads (All Time)** -- Cumulative downloads across all repositories (models and datasets only).
- **Downloads (Last Month)** -- Downloads in the last 30 days (models and datasets only).
- **Total Likes** -- Sum of likes across all repositories.

### Tree View

A terminal-style listing of all repositories with:

- Repository name (linked to HuggingFace)
- Pipeline tag icon (for models)
- All-time download count
- Monthly download count
- Like count
- Last modified timestamp
- Copy button for the repository ID

## Sorting and Filtering

### Sort Options for Models and Datasets

| Sort | Description |
|------|-------------|
| Downloads (All Time) | Highest lifetime downloads first |
| Downloads (Last Month) | Highest monthly downloads first |
| Most Liked | Highest like count first |
| Most Recent | Most recently modified first |

### Sort Options for Spaces

| Sort | Description |
|------|-------------|
| Most Liked | Highest like count first |
| Least Liked | Lowest like count first |

### Name Filter

Use the search field in the filter bar to filter repositories by name. Matching text is highlighted in the tree view.

## Copy and Export

### Copy Individual ID

Hover over any repository in the tree view and click the copy icon to copy the full repository ID (e.g., `meta-llama/Llama-2-7b`) to your clipboard.

### Copy Full Tree

Click the **Copy Tree** button in the tree header to copy the entire listing as formatted plain text, including aggregate statistics. The output format:

```
meta-llama -- 25 Models
├── Llama-2-70b-chat-hf (↓1.2M all ↓234.5K /mo ♥1,234)
├── Llama-2-13b-chat-hf (↓890.3K all ↓123.4K /mo ♥987)
└── Llama-2-7b (↓567.8K all ↓89.1K /mo ♥654)

Total Downloads (All Time): 12,345,678
Total Downloads (Last Month): 1,234,567
Total Likes: 9,876
```

## Supported Organizations

The homepage displays a curated list of popular organizations for quick access. Any valid HuggingFace organization or user can be queried by entering its name directly.

Pre-listed organizations include:

```
OpenMed, google, meta-llama, microsoft, Qwen, strangerzonehf,
openai, stabilityai, mistralai, black-forest-labs, strangertoolshf,
HuggingFaceFW, deepseek-ai, nvidia, allenai, strangeropshf,
apple, strangervisionhf, bigscience, EleutherAI, strangerguardhf,
huggingface, facebook, tiiuae, databricks, hugging-science
```

## Technical Details

### Architecture

- **Single HTML file** -- No external dependencies beyond CDN-loaded fonts and icons.
- **Client-side only** -- All API calls are made directly from the browser.
- **No framework** -- Vanilla JavaScript with DOM manipulation.
- **Responsive CSS** -- Custom properties (CSS variables) for theming with media queries for mobile.

### External Resources

| Resource | Source |
|----------|--------|
| Font Awesome 6.4.0 | cdnjs.cloudflare.com |
| Inter font | Google Fonts |
| JetBrains Mono font | Google Fonts |

### Data Flow

1. User enters organization name.
2. Application fetches organization profile from the HuggingFace API.
3. Application fetches all models, datasets, and spaces in parallel using `Promise.allSettled`.
4. If like counts are missing from the list endpoints, individual detail endpoints are queried in batches of 10.
5. All data is stored in a client-side state object.
6. The UI renders from the state object without further API calls until a new fetch is initiated.

### Local Storage Keys

| Key | Purpose |
|-----|---------|
| `hf_token` | HuggingFace access token |
| `hfstat_theme` | Theme preference (`light` or `dark`) |

## API Endpoints Used

| Endpoint | Purpose |
|----------|---------|
| `GET /api/organizations/{org}` | Organization profile and metadata |
| `GET /api/users/{org}/overview` | Fallback for avatar and profile data |
| `GET /api/models?author={org}` | List all models with download and like counts |
| `GET /api/datasets?author={org}` | List all datasets with download and like counts |
| `GET /api/spaces?author={org}` | List all spaces with like counts |
| `GET /api/models/{id}` | Individual model details (fallback for missing stats) |
| `GET /api/datasets/{id}` | Individual dataset details (fallback for missing stats) |

Expand parameters used: `downloadsAllTime`, `downloads`, `likes`, `lastModified`, `createdAt`.

---

## Browser Support

| Browser | Minimum Version |
|---------|----------------|
| Chrome | 80+ |
| Firefox | 78+ |
| Safari | 14+ |
| Edge | 80+ |

Requires JavaScript enabled and network access to `huggingface.co`.

## Limitations

- **Rate Limiting** -- The HuggingFace API may throttle requests for organizations with a very large number of repositories. Using a token mitigates this.
- **Spaces Downloads** -- The HuggingFace API does not provide download counts for Spaces. Only like counts are displayed.
- **Private Organizations** -- Fully private organizations require a valid access token with appropriate permissions.
- **Avatar Resolution** -- Organization avatars are resolved through multiple fallback URLs. Some organizations may display a letter fallback if no avatar is available.
- **Concurrent Requests** -- Detail fetching for missing like counts is done in sequential batches of 10 to avoid overwhelming the API.

## License

This project is open source. See the repository for license details.

## Author

Built by [prithivMLmods](https://huggingface.co/prithivMLmods)
