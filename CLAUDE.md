# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a collection of Jupyter notebooks designed to run in Google Colab for image generation and editing using various AI models (Google's Gemini/Imagen and OpenAI's GPT-Image models). The repository is primarily in Japanese.

## Repository Structure

```
google/                  # Google AI model notebooks (Apache 2.0 license)
openai/                  # OpenAI model notebooks (MIT license)
```

## Working with Notebooks

All notebooks (.ipynb files) are designed to run in Google Colab, not locally. When editing:

- Notebooks use Google Colab's `userdata.get()` to retrieve API keys securely
- Google notebooks use the `google-genai` SDK
- OpenAI notebooks use the `openai` Python package
- All notebooks include setup cells for installing dependencies

### Common API Key Patterns

**Google notebooks:**
```python
from google.colab import userdata
GOOGLE_API_KEY = userdata.get('GOOGLE_API_KEY')
```

**OpenAI notebooks:**
```python
from google.colab import userdata
client = OpenAI(api_key=userdata.get('OPENAI_API_KEY'))
```

### Google Model Patterns

Google notebooks use the `google-genai` client with models like:
- `gemini-2.0-flash-preview-image-generation` - for text + image generation
- Imagen 3 - for dedicated image generation via Vertex AI

Common pattern for multimodal generation:
```python
client = genai.Client(api_key=GOOGLE_API_KEY)
response = client.models.generate_content(
    model=MODEL_ID,
    contents=prompt,
    config=types.GenerateContentConfig(
        response_modalities=["TEXT", "IMAGE"]
    )
)
```

### OpenAI Model Patterns

OpenAI notebooks use GPT-Image-1 and GPT-Image-1.5 models for image generation/editing:

Common parameters:
- `size`: `1024x1024`, `1536x1024`, or `1024x1536`
- `quality`: `high`, `medium`, or `low`
- `background`: `transparent` or `opaque`
- Response format: `b64_json` (base64-encoded image data)

## Licensing Requirements

This repository has split licensing:
- **google/** folder: Apache License 2.0
- **openai/** folder: MIT License
- Repository default: Apache License 2.0

When adding new notebooks, ensure they are placed in the correct folder based on which API they use.

## Language and Documentation

- Primary language: Japanese
- README.md contains a table of all notebooks with Japanese descriptions
- When adding new notebooks, update README.md with Japanese descriptions
- Code comments and markdown cells are typically in Japanese
