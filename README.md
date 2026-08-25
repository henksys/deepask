# ask - chat with DeepSeek from the terminal. 

## Description:

Ask a question and DeepSeek answers, keeping the conversation history (if you enable history )
so follow-up questions have context. If you prefer one-shot questions, to save tokens, leave save_history option disabled)

##Usage:

Open a terminal:
$ ask "your question between the quotes"

Options:
-  -h   Show this help.
-  -r   Clear the conversation history.
-  -e   Edit the config file in $EDITOR (default: vi).
-  -s   Show current config settings.
-  -d   Restore the default config (asks for confirmation).


## Requirements to run he ask (deepseek) script:

- bash (script is #!/bin/bash)
- python3 (stdlib only: json, sys — no pip packages needed)
- curl (API calls)
- coreutils (mkdir, cat, rm, touch, printf, read) — present on any Linux/macOS
- Network access to api.deepseek.com
- DEEPSEEK_API_KEY env var set (only needed for asking questions, not for -h/-r/-e/-s/-d)
- $EDITOR optional — only used by ask -e, falls back to vi

set your deepseek API key in your ~/.bashrc with:
export DEEPSEEK_API_KEY="your-key-between-the-quotes"

So, roughly 60% Python / 40% bash — Python does all the JSON work, bash does the orchestration (flags, curl, filesystem).


## Files:

  Bash script : Place the ask bash script in '~/.local/bin/ask'
  
  Config:   ~/.config/ask/config
  History:  ~/.local/share/ask/history.jsonl (if history is enabled)

note: the config file will be auto generated when no config file is found.
the history file will be automatically created when history is enabled in the config file.

## Config parameters (set in ~/.config/ask/config):

  role              System prompt defining the AI's persona.
  model             deepseek-v4-flash (default) or deepseek-v4-pro.
  temperature       Sampling temperature (0-2); higher is more random.
  top_p             Nucleus sampling (0-1); prefer temperature or top_p, not both.
  thinking          Thinking mode: enabled or disabled.
  reasoning_effort  Reasoning effort: low, high, or max (thinking only).
  response_format   Output format: text or json_object.
  save_history      Keep conversation history for future context: y or n.

Note: comments in the config file must be on their own line,
starting with //. Do not append comments to a value line.
