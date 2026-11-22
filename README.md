# AI Slop Cleaner

An MCP server that improves generic AI-written text and repairs visibly synthetic-looking image details while preserving the source's meaning and composition.

## Current status

**MVP: text and image editing.** Video cleanup is planned, not implemented. The tools improve content; they do not reliably determine whether something was created by AI or prove that an image is authentic.

## Features

- **Text — `clean_text(text, instructions?)`:** removes repetitive phrasing, generic filler, awkward transitions, and unnecessary verbosity. Preserves the original language, facts, names, numbers, and links.
- **Images — `clean_image(image_base64, mime_type?, instructions?)`:** edits a supplied PNG, JPEG, or WEBP to correct visible glitches, unnatural textures, edges, and lighting. It aims for a natural photographic appearance while preserving the subject, identity, objects, pose, and composition. Returns an edited PNG as base64; the original is not changed.

Image editing is generative and may still alter details unintentionally. Review results before using them.

## Requirements

- Python 3.11+
- An OpenAI API key with access to the selected text and image models
- An MCP-compatible client

## Setup

```bash
git clone https://github.com/djdhsvsbdb-design/AI-Slop-Cleaner.git
cd AI-Slop-Cleaner
python -m venv .venv
source .venv/bin/activate
pip install -e .
export OPENAI_API_KEY="your-api-key"
python -m ai_slop_cleaner
```

On Windows PowerShell, activate the environment with `.venv\\Scripts\\Activate.ps1`.

Optional model overrides:
- `OPENAI_MODEL` (default: `gpt-4.1-mini`)
- `OPENAI_IMAGE_MODEL` (default: `gpt-image-1`)

## MCP client configuration

Example for a local stdio MCP client:

```json
{
  "mcpServers": {
    "ai-slop-cleaner": {
      "command": "python",
      "args": ["-m", "ai_slop_cleaner"],
      "env": {
        "OPENAI_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

Use your MCP client's documented configuration location. Do not commit API keys.

## Image input/output

The image tool accepts raw base64 image bytes (without a data-URL prefix) and a matching MIME type: `image/png`, `image/jpeg`, or `image/webp`. It returns `image_base64` with `mime_type: image/png`. The client must decode the base64 result to display or save the edited PNG.

## Roadmap

- [x] MCP text-cleaning tool
- [x] MCP photorealistic image-cleanup tool
- [ ] Automated tests and CI
- [ ] Video cleanup workflow
- [ ] Hosted deployment and ChatGPT connector setup

## Responsible use

Only edit content you own or have permission to modify. Do not use this project to remove attribution, copyright notices, or watermarks from someone else's work. AI-origin detection is probabilistic; this project focuses on improving content, not declaring its provenance.
