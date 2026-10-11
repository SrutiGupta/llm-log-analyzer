# LLM Log Analyzer

An AI-powered log analysis tool that helps developers identify build failures, understand root causes, and get actionable debugging suggestions using Large Language Models (LLMs).

Originally developed to simplify debugging verbose Unity build logs, this tool also supports generic application logs and Android, iOS, and Flutter build logs through configurable analysis presets.

## Features

- **AI-Powered Root Cause Analysis:** Analyzes relevant log entries and explains potential causes of failures.
- **Multiple LLM Providers:** Supports Google Gemini, OpenAI, Anthropic Claude, and AWS Bedrock.
- **Structured Reports:** Generates machine-readable JSON and human-readable Markdown analysis reports.
- **Multiple Log Presets:** Includes configurations for Unity, Android, iOS, Flutter, and generic application logs.
- **Smart Log Filtering:** Extracts relevant error information to reduce unnecessary processing.
- **Large Log Support:** Uses streaming and chunk-based processing for large logs.
- **Custom Configuration:** Supports custom error patterns, prompts, and additional context.
- **CI/CD Integration:** Can be incorporated into build and continuous integration workflows.

## Tech Stack

- **Language:** Python 3.9+
- **LLM Providers:** Google Gemini, OpenAI, Anthropic Claude, AWS Bedrock
- **CLI:** Click
- **Supporting Libraries:** Requests, tiktoken, LangChain Text Splitters, Boto3

## Repository

GitHub: https://github.com/SrutiGupta/llm-log-analyzer

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/SrutiGupta/llm-log-analyzer.git
cd llm-log-analyzer
```

### 2. Set up a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## API Configuration

Choose a supported LLM provider and configure its API credentials.

**Google Gemini (default provider):**

PowerShell:

```powershell
$env:GOOGLE_API_KEY="your_gemini_api_key"
```

**OpenAI:**

```powershell
$env:OPENAI_API_KEY="your_openai_api_key"
```

**Anthropic Claude:**

```powershell
$env:ANTHROPIC_API_KEY="your_anthropic_api_key"
```

**AWS Bedrock:**

Configure the credentials and environment variables required by your AWS Bedrock setup.

```powershell
$env:AWS_BEARER_TOKEN_BEDROCK="your_aws_bearer_token"
$env:AWS_REGION="us-east-1"
```

Replace the example values with your own credentials. Never commit API keys or other secrets to GitHub.

## Usage

The examples below follow the command syntax documented by the original project. Verify the CLI entry point and options against your local installation.

### Check available providers

```bash
llm-log-analyzer --list-providers
```

### Analyze a generic application log

```bash
llm-log-analyzer application.log
```

### Analyze a Unity build log

```bash
llm-log-analyzer build.log -P unity
```

### Select a specific provider

```bash
llm-log-analyzer server.log -P generic --provider openai
```

```bash
llm-log-analyzer build.log -P unity --provider gemini
```

```bash
llm-log-analyzer build.log -P unity --provider claude
```

### Analyze other build logs

```bash
llm-log-analyzer gradle-build.log -P android
```

```bash
llm-log-analyzer xcode-build.log -P ios
```

```bash
llm-log-analyzer flutter-build.log -P flutter
```

### Customize analysis

```bash
llm-log-analyzer app.log -P generic --tail-lines 5000 --output-dir results/ --debug
```

For detailed command-line options:

```bash
llm-log-analyzer --help
```

## Analysis Presets

| Preset | Purpose |
|---|---|
| `generic` | General application and runtime logs |
| `unity` | Unity game engine build logs |
| `android` | Native Android build logs |
| `ios` | Native iOS build logs |
| `flutter` | Flutter cross-platform build logs |

Presets combine error patterns and prompts designed for different types of logs. Custom patterns and prompts can also be supplied.

## Output Reports

The analyzer's README documents two report formats:

- **`analysis.json`** — structured analysis containing information such as the root cause, relevant log lines, confidence, and suggested actions.
- **`analysis.md`** — a human-readable report summarizing the failure, analysis configuration, and recommended action items.

The exact output filenames and behavior should be confirmed by running the project.

## CI/CD Integration

The analyzer can be incorporated into automated build workflows to help investigate failures and share diagnostic reports.

Potential integrations include:

- Jenkins pipelines
- GitLab CI
- GitHub Actions

Use CI/CD secret management to provide API credentials securely. Review the exit codes and command syntax before adding the analyzer to a production pipeline.

## Troubleshooting

**API errors**
- Confirm that the selected provider's API key is configured.
- Check network connectivity and provider availability.
- Review provider usage limits and billing requirements.

**Poor analysis results**
- Confirm that the log contains useful error messages.
- Try a more suitable preset.
- Adjust filtering settings or provide additional context.

**Large logs**
- Use the available tail-line and chunk-processing options to control the amount of log data analyzed.

For additional troubleshooting information, use debug mode and consult the project documentation.

## Contributing

Contributions that improve log parsing, analysis quality, supported presets, documentation, or CI/CD integrations are welcome.

1. Create a feature branch.
2. Make and test your changes.
3. Submit a pull request with a clear description.

---

AI-assisted log analysis for more efficient debugging and root-cause investigation.
