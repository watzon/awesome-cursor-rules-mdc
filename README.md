# MDC Generator for Library Best Practices

This repository contains Cursor rule files (.mdc) that provide AI-powered best practices and guidelines for various libraries and frameworks. The rules in `rules-mdc/` are the current, improved version which are more focused and comprehensive. (Note: The `rules-v0/` directory contains legacy rules and is kept for historical reference only - please use `rules-mdc/` for all new projects).

## Repository Structure

```
.
├── rules-mdc/          # Current, comprehensive rule files (recommended)
│   ├── frontend/
│   ├── backend/
│   └── ...
├── src/                # Source code for rule generation
│   ├── generate_mdc_files.py
│   ├── config.yaml
│   └── ...
└── rules-v0/           # Legacy rules (deprecated)
```

## Features

- **Configurable**: All settings can be adjusted in `src/config.yaml`
- **Parallel Processing**: Process multiple libraries simultaneously
- **Progress Tracking**: Resume from where you left off if the process is interrupted
- **Smart Glob Pattern Generation**: Automatically determines appropriate glob patterns for different libraries
- **Rate Limiting**: Configurable API rate limits to avoid throttling
- **Robust Error Handling**: Comprehensive error handling and logging

## Prerequisites

1. Python 3.8+
2. Required packages (install via `pip install -r requirements.txt`)
3. Exa API key (set as environment variable `EXA_API_KEY`)
4. LiteLLM API key (set as environment variable based on your provider)

## Configuration

The script uses a configuration file (`src/config.yaml`) with the following structure:

```yaml
paths:
  mdc_instructions: "mdc-instructions.txt"
  libraries_json: "libraries.json"
  output_dir: "rules-mdc"

api:
  llm_model: "gemini/gemini-2.0-flash"
  rate_limit_calls: 100
  rate_limit_period: 60
  max_retries: 3
  retry_min_wait: 4
  retry_max_wait: 10

processing:
  max_workers: 4
  chunk_size: 25000
```

## Usage

### Basic Usage

```bash
python src/generate_mdc_files.py
```

### Test Mode (Process Only One Library)

```bash
python src/generate_mdc_files.py --test
```

### Process Specific Categories or Libraries

```bash
python src/generate_mdc_files.py --category frontend_frameworks
python src/generate_mdc_files.py --subcategory react
python src/generate_mdc_files.py --library react
```

### Adjust Parallel Processing

```bash
python src/generate_mdc_files.py --workers 8
```

### Adjust Rate Limits

```bash
python src/generate_mdc_files.py --rate-limit 50
```

### Verbose Logging

```bash
python src/generate_mdc_files.py --verbose
```

## File Structure

The generated MDC files will be organized in the following structure:

```
rules-mdc/
├── frontend/
│   ├── react/
│   │   ├── react.mdc
│   │   ├── react-native.mdc
│   │   └── ...
│   ├── vue/
│   │   └── ...
│   └── ...
├── backend/
│   ├── python/
│   │   ├── django.mdc
│   │   ├── flask.mdc
│   │   └── ...
│   └── ...
└── ...
```

## Progress Tracking

The script maintains a progress file (`mdc_generation_progress.json`) to track which libraries have been processed. This allows you to resume the process if it's interrupted.

## Troubleshooting

- If you encounter API rate limit issues, adjust the `rate_limit_calls` in the configuration.
- If the script is using too much memory, reduce the `chunk_size` in the configuration.
- If the script is too slow, increase the `max_workers` in the configuration (but be mindful of API rate limits).

## License

MIT
