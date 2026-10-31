# Scam-Message-Investigator
# Scam Message Investigator

A Streamlit web application that analyzes suspicious SMS, email, and chat messages for scam indicators using a locally running large language model (LLM). All analysis runs on your own machine through Ollama, so message content is never sent to an external service.

## Features

- Risk classification: Low, Medium, or High Concern
- Message type identification (for example, phishing, fake job offer, prize scam)
- Evidence-based warning signs, quoting the exact phrase from the message with an explanation
- Practical recommended safety actions
- Clear statement of limitations, since a message alone cannot be fully verified
- Prompt-injection defense: the message is treated strictly as untrusted data
- Structured JSON output from the model for reliable rendering
- Error handling for connection failures, timeouts, and malformed responses

## Tech Stack

- Python 3.11
- Streamlit (user interface)
- Requests (HTTP client)
- Ollama (local LLM runtime)
- Model: gemma3:1b

## Prerequisites

- Python 3.9 or later
- Ollama installed from https://ollama.com

## Installation

1. Clone or download this repository and open a terminal in the project folder.

2. Pull the model:

```bash
ollama pull gemma3:1b
```

3. (Optional) Create and activate a virtual environment:

```bash
python -m venv venv
venv\Scripts\activate
```

On macOS or Linux, use `source venv/bin/activate`.

4. Install dependencies:

```bash
python -m pip install -r requirements.txt
```

## Usage

1. Make sure Ollama is running in the background.
2. Start the application:

```bash
python -m streamlit run app.py
```

3. Open http://localhost:8501 in your browser.
4. Paste a suspicious message and click **Investigate Message**.

## Sample Test Messages

High concern:

```
Your SBI account will be blocked today. Click http://sbi-kyc-update.xyz to update your KYC and share the OTP to avoid suspension.
```

Low concern:

```
Your Amazon order #123 has shipped and will arrive tomorrow. Track it in the official app.
```

## Configuration

Edit these values at the top of `app.py`:

| Setting | Default | Description |
|---|---|---|
| `MODEL` | `gemma3:1b` | Ollama model used for analysis |
| `OLLAMA_URL` | `http://localhost:11434/api/chat` | Ollama chat endpoint |

Larger models such as `gemma3:4b` or `llama3.2` generally produce more accurate and consistent results.

## How It Works

1. The user pastes a message into the text area.
2. The app sends it to the local Ollama API along with a system prompt that defines the analysis criteria and the required JSON schema.
3. The request uses `format: json` and a low temperature (0.1) for consistent, parseable output.
4. The JSON response is parsed and displayed as a structured report.

## Project Structure

```
scam-message/
  app.py
  requirements.txt
  README.md
```

## Troubleshooting

| Problem | Solution |
|---|---|
| Cannot connect to Ollama | Start Ollama or run `ollama serve` |
| Model not found | Run `ollama pull gemma3:1b` |
| Invalid JSON or empty report | Retry, or switch to a larger model |
| Slow responses | Use a smaller model or a shorter message |
| `pip` not recognized | Use `python -m pip` instead |

## Limitations

- Results are AI-generated and may contain errors, especially with small models.
- The tool cannot verify links, senders, or phone numbers.
- It is an aid for awareness, not a substitute for verifying through official channels.

## Future Improvements

- Numeric risk score
- History of previous checks
- Multilingual support (Tamil, Hindi)
- URL and phone number reputation checks

 <img width="1777" height="866" alt="image" src="https://github.com/user-attachments/assets/fc55265a-c2cd-43c6-89a9-ffaabeb8dd61" />

## Disclaimer

This tool provides an automated assessment only. Always confirm suspicious messages directly with the official organization before taking any action.

## Author

Mythili K
