# TRP1 – AI Content Generation Challenge

## Participant
- Name: Dagim Wondim
- Challenge: AI Content Generation (Second Challenge)

---

## Part 1: Environment Setup & API Configuration

### Environment
- OS: Windows 10
- Python 3.11
- Node.js installed
- uv CLI installed via Astral
- Virtual environment: .venv (created automatically by uv)

### Actions Taken
- Cloned repository: `git clone https://github.com/10xac/trp1-ai-artist.git`
- Created `.env` from `.env.example`
- Added Google Gemini API key for Lyria
- Installed dependencies using `uv sync`
- Verified CLI commands:
  - `uv run ai-content --help`
  - `uv run ai-content list-providers`
  - `uv run ai-content list-presets`

### Issues Encountered
- uv not initially recognized (PATH issue)
- Resolved by adding `C:\Users\Dagi\.local\bin` to PATH
- Music generation requires explicit `--prompt` flag

### Status
Environment setup completed successfully

---

## Part 2: Codebase Exploration

### Package Structure
- `src/ai_content/`
  - `providers/` → Handles AI providers (lyria, minimax, veo, imagen)
  - `pipelines/` → Orchestrates prompt → provider → output workflow
  - `presets/` → Predefined music/video styles
  - `cli.py` → Entry point for ai-content CLI

### Provider Capabilities
- Music:
  - **Lyria** → Instrumental music (Google Gemini)
  - **MiniMax** → Vocals / lyrics (AIMLAPI)
- Video:
  - **Veo** → Video generation
  - **Kling** → Video generation
- Image:
  - **Imagen** → Image generation
- Vocals supported only by MiniMax

### Preset System
- Music presets: BPM, mood, style
  - Examples: jazz (nostalgic, 95 BPM), ethiopian-jazz (mystical, 85 BPM)
- Video presets: aspect ratio, duration, theme
  - Examples: nature (16:9), urban (21:9)
- Adding a new preset:
  - Create preset definition
  - Register in loader
  - Reference by name in CLI

### CLI Commands
- `list-providers` → lists all providers
- `list-presets` → lists all presets
- `music` → generate music
  - Options: --style, --prompt, --provider, --bpm, --duration, --lyrics
- `video` → generate video
  - Options: --style, --prompt, --provider, --aspect, --duration
- Other commands: `jobs`, `jobs-stats`, `jobs-sync`

---

## Part 3: Content Generation

### Lyria Music Attempt – Success

**Command executed:**
```bash
uv run ai-content music --provider lyria --style jazz --prompt "Smooth jazz instrumental, relaxing and warm" --duration 30

MiniMax Vocals Attempt

Command executed:

uv run ai-content music --provider minimax --prompt "Ethiopian jazz fusion with vocals" --lyrics my_lyrics.txt --duration 30


Observed behavior:

Lyrics file loaded successfully

CLI connected to MiniMax

Streaming attempted for 30 seconds

Error returned:

{'name': 'ForbiddenException', 'message': 'Complete verification to using the API https://aimlapi.com/app/verification', 'data': {'kind': 'err_unverified_card'}}


Analysis:

Environment and CLI working correctly

Failure caused by provider verification requirement, not your setup

Outcome: Attempt documented properly

Veo Video Attempt

Command executed:

uv run ai-content video --provider veo --style nature --prompt "Beautiful Ethiopian landscapes with mountains, rivers, and traditional villages" --duration 5


Observed behavior:

Preset nature used

CLI connected to Veo

Streaming attempted for 5 seconds

Error returned:

429 RESOURCE_EXHAUSTED
{'error': {'code': 429, 'message': 'You exceeded your current quota, please check your plan and billing details.'}}


Analysis:

Environment and CLI fully functional

Failure caused by API quota limit, not local setup
