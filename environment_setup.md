# Environment Setup Guide

## Setting up Environment Variables

To run this application securely, you need to set up environment variables for sensitive configuration like API keys.

### 1. Create a `.env` file

Create a `.env` file in the root directory of the project (same directory as `config.py`):

```bash
# Azure OpenAI Configuration
AZURE_OPENAI_API_KEY=your_azure_openai_api_key_here
AZURE_OPENAI_ENDPOINT=https://ai-tum-dev-se-001.openai.azure.com/
AZURE_OPENAI_API_VERSION=2024-02-01
AZURE_OPENAI_DEPLOYMENT_NAME=gpt-4o

# Legacy OpenAI Configuration (if needed)
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_MODEL=gpt-4
REGION=swedencentral

# AI Parameters (optional - defaults are provided)
AI_MAX_TOKENS=4000
AI_TEMPERATURE=0.1
AI_TOP_P=1.0
AI_FREQUENCY_PENALTY=0.0
AI_PRESENCE_PENALTY=0.0

# File Paths (optional - defaults are provided)
METADATA_FILE=data/metadata.json
STATUS_LOG_FILE=data/status_log.json
IMPLEMENTED_REQUIREMENTS_FILE=../ProjectBase/implementedRequirements.csv
REQUIREMENTS_FILE=../ProjectBase/requirements.csv
CODEBASE_ROOT=../ProjectBase/CodeBase/

# Validation Settings (optional - defaults are provided)
MAX_RETRIES=3
VALIDATION_TIMEOUT=300

# Code Style Settings (optional - defaults are provided)
PYTHON_FORMATTER=black
LINTER=flake8
TEST_COMMAND=pytest

# Azure Function Settings (optional - defaults are provided)
AZURE_FUNCTION_TIMEOUT=600

# Logging (optional - defaults are provided)
LOG_LEVEL=INFO
LOG_FORMAT=%(asctime)s - %(name)s - %(levelname)s - %(message)s
```

### 2. Load Environment Variables

To load the environment variables, add this to your Python files:

```python
from dotenv import load_dotenv
load_dotenv()  # This loads the .env file
```

### 3. Security Notes

- **NEVER** commit `.env` files to version control
- The `.env` file is already added to `.gitignore`
- Only commit `.env.example` or documentation files like this one
- Keep your API keys secure and rotate them regularly

### 4. Azure Functions Local Development

For Azure Functions, you can also use `local.settings.json`:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "AZURE_OPENAI_API_KEY": "your_azure_openai_api_key_here",
    "AZURE_OPENAI_ENDPOINT": "https://ai-tum-dev-se-001.openai.azure.com/",
    "AZURE_OPENAI_API_VERSION": "2024-02-01",
    "AZURE_OPENAI_DEPLOYMENT_NAME": "gpt-4o"
  }
}
```

### 5. Production Deployment

For production deployments:

- Use Azure Key Vault or similar secret management services
- Set environment variables in your hosting platform
- Never hardcode secrets in source code
