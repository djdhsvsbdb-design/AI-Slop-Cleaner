# AI Slop Cleaner

An MCP server that helps improve low-quality or overly generic AI-generated content while preserving the author's meaning.

## Current status

**MVP: text cleanup.** Image and video analysis are planned, not implemented yet. The tool does not claim to reliably determine whether content was made by AI.

## What it does

- Rewrites text to remove repetitive phrasing, generic filler, awkward transitions, and unnecessary verbosity.
- Preserves factual claims, names, numbers, links, and the original language.
- Avoids inventing facts or adding unsupported claims.
- Returns a revised version and a concise change summary.

## Requirements

- Python 3.11+
- An OpenAI API key
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

## Tool

### `clean_text(text, instructions?)`

Returns:
- `cleaned_text`: revised text
- `changes`: short list of edits
- `notes`: caveats when facts or meaning may need human review

## Roadmap

- [x] MCP text-cleaning tool
- [ ] Tests and CI
- [ ] Image review/edit workflow (requires image-capable model and explicit user approval before destructive edits)
- [ ] Video review/edit workflow
- [ ] Hosted deployment and ChatGPT connector setup

## Responsible use

Only edit content you own or have permission to modify. Do not use this project to remove attribution, copyright notices, or watermarks from someone else's work. AI-origin detection is probabilistic; this project focuses on improving content, not declaring its provenance.
