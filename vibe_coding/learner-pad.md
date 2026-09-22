---
tags: Goe26, AIinRSE
title: Vibe Coding - A Useful Science Tool
---

# Vibe Coding: A Useful Science Tool

back to [main pad](https://pad.gwdg.de/kOT4kzzcTRyUNxT8OO7-wg)

## Quick Info

| Date     | 23 Sept 2026, 09:00         |
| -------- | --------------------------- |
| Duration | 1h 30m                      |
| Location | Büttner-Raum 1 (Heyne-Haus) |
| Speaker  | Dr. Till Korten             |

## Preparation

### Install Opencode

Run the installer from a terminal:

```bash
curl -fsSL https://opencode.ai/install | bash
```

Alternatively, install via package manager:

```bash
npm install -g opencode-ai
# or
brew install anomalyco/tap/opencode
```

You also need:

* A modern terminal emulator (e.g. WezTerm, Alacritty, Ghostty, Kitty, VS Code terminal, iTerm2, etc.)
* A git repository to work in (opencode is designed to be used inside a project)

### Connect to the model provider

#### GWDG academiccloud

If you indicated in the feedback form that you want to use the GWDG academiccloud, you should have gotten an API key. Please follow these steps to connect to the service:

Do not share your key with others.

1. Register the API key with opencode:
   * Run `/connect` in the opencode TUI
   * Scroll down and select **Other**
   * Enter the provider id `gwdg` (must match the id used in `opencode.json` below)
   * Enter your API key
2. Create an `opencode.json` in your project directory (model ids are the API model names from the [SAIA table](https://docs.hpc.gwdg.de/services/saia/index.html)):

```json
{
    "provider": {
        "gwdg": {
            "npm": "@ai-sdk/openai-compatible",
            "name": "GWDG Academic Cloud",
            "options": {
                "baseURL": "https://chat-ai.academiccloud.de/v1"
            },
            "models": {
                "glm-5.3-flash": {
                    "name": "GLM 5.3 Flash",
                    "limit": {
                        "context": 1000000,
                        "input": 900000,
                        "output": 32768
                    }
                },
                "deepseek-v4-flash-0731": {
                    "name": "DeepSeek V4 Flash",
                    "limit": {
                        "context": 1000000,
                        "input": 900000,
                        "output": 32768
                    }
                },
                "qwen3.8-27b": {
                    "name": "Qwen 3.8 27B",
                    "limit": {
                        "context": 262000,
                        "input": 250000,
                        "output": 32768
                    }
                }
            }
        }
    }
}
```

3. Run `/models` in the opencode TUI and select a model.

If you want to continue using the GWDG academiccloud, you can request an API key, book the LLM service at https://kisski.gwdg.de/en/leistungen/2-02-llm-service (use the same email address as for your academiccloud account).

Note:

* Recommended sampling settings per model (e.g. deepseek-v4-flash-0731: temp=1.0, top_p=1.0; glm-5.3-flash: temp=1.0, top_p=0.95; qwen3.8-27b: temp=1.0, top_p=0.95) are listed on the [models page](https://docs.hpc.gwdg.de/services/chat-ai/models/index.html). Opencode sets sensible defaults, so you usually don't need to change anything.
* The externally hosted OpenAI/Anthropic models are **not** hosted by the GWDG academiccloud, and their data is relayed to external providers. Prefer the open-weight models for data privacy.
* To see the current list of models at any time:

  ```bash
  curl -X POST https://chat-ai.academiccloud.de/v1/models \
    --header 'Accept: application/json' \
    --header 'Authorization: Bearer <api_key>' \
    --header 'Content-Type: application/json'
  ```

#### Commercial providers

* **e.g. Anthropic, OpenAI, GitHub Copilot:** Run `/connect`, select the provider, and enter your API key. Then run `/models`. No `opencode.json` configuration is needed for these providers.

### Prepare a small example project

Good projects are small, self-contained, and have a clear goal — so that you can concentrate on working with the coding agent instead of debugging. For example:

* Write a script to automate a tedious task in your daily work
* Implement a new feature in an existing codebase
* Fix a bug in a small project
* Write documentation for a project
* Implement unit tests for an existing codebase
* Migrate a legacy project to a modern language or framework
* Implement a research proposal or visualization example
* A simple data analysis task, a small simulation, or a basic machine learning model

Maybe you have a project idea that you wanted to try out but never got around to it. This is a good opportunity to do so.
