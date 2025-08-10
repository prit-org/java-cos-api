# Test Data Generator

## Summary

The Test Data Generator is a TypeScript/Node.js application that leverages AI services to create realistic synthetic test data for comprehensive application testing. The Developer/Tester has to just write in a natural language prompt about what synthetic test data they require and It generates JSON files(as per current implementation) containing structured application execution data, including processing statistics, error scenarios, timing information, and multi-step workflows that mirror production environments.

**Key Capabilities:**
- **AI-Powered Data Generation**: Creates realistic test data using AWS Bedrock, Azure OpenAI, OpenAI, or Mock providers
- **Scenario-Based Testing**: Built-in templates for various testing scenarios including manual testing, error handling, and success path validation
- **Flexible Deployment**: Works locally, in serverless functions (AWS Lambda/Azure Functions), or as a development tool
- **Zero-Setup Testing**: Mock provider allows immediate testing without AI service credentials
- **Customizable Templates**: External prompt system for domain-specific test scenarios

**Perfect For:**
- Manual testing with realistic and varied data sets
- Automated testing with diverse data scenarios
- Error handling and resilience testing
- Load and performance testing
- Integration testing with production-like data
- QA testing across different data conditions


## Features

- 🤖 **AI-Powered Generation**: Uses AWS Bedrock, Azure AI, OpenAI, or Mock providers
- 🔄 **Multi-Provider Support**: Choose from AWS, Azure, OpenAI, or Mock providers
- 🧪 **Local Testing**: Mock provider requires no credentials for testing
- � **External Prompt Templates**: Customize test scenarios via external prompt files
- 🎯 **Scenario-Based Testing**: Built-in templates for performance, errors, success paths
- �📁 **Batch File Generation**: Generate multiple JSON files at once
- 💾 **Local Storage**: Save generated files to local drives
- ⚡ **Serverless Ready**: Includes AWS Lambda and Azure Function support

## Quick Start (No Credentials Required!)

Want to test immediately without setting up AI services? Use the mock provider:

```bash
# Install dependencies
npm install

# Create a simple .env file for testing
echo "AI_PROVIDER=mock" > .env

# Generate test data immediately!
npm run generate
```

Want to customize test scenarios? Use different prompt templates:

```bash
# Generate performance testing data
echo "PROMPT_TEMPLATE=performance" >> .env
npm run generate

# Generate error scenario data  
echo "PROMPT_TEMPLATE=error-scenarios" >> .env
npm run generate

# List all available templates
npm run prompt list
```

See [LOCAL_TESTING.md](./LOCAL_TESTING.md) for detailed testing instructions and [prompts/README.md](./prompts/README.md) for prompt customization guide.

## Prerequisites

- Node.js 14+ 
- npm or yarn
- Optional: AI service credentials (AWS, Azure, or OpenAI) for production use

## Step-by-Step Setup Guide

### 1. Clone and Install

```bash
# Clone the repository (if from git)
git clone <repository-url>
cd test_data_generator

# Or if you have the folder already, navigate to it
cd test_data_generator

# Install all dependencies
npm install
```

### 2. Configure AI Provider

Copy the environment template and set up your credentials:

```bash
# Copy the template file
cp .env.template .env
```

Edit the `.env` file with your preferred AI provider:

#### Option A: Using Mock Provider (No Credentials Required)
```env
AI_PROVIDER=mock
OUTPUT_DIRECTORY=./output
DEFAULT_FILE_COUNT=3

# Prompt Template Configuration
PROMPT_TEMPLATE=default
```

## 🎯 Customizing Test Scenarios with Prompt Templates

The Test Data Generator supports external prompt templates, allowing developers and testers to customize test data generation for specific scenarios without modifying code.

### Available Built-in Templates

1. **`default`** - General purpose testing (balanced scenarios)
2. **`performance`** - High volume performance testing (100K-1M records)
3. **`error-scenarios`** - Error and failure testing (high failure rates)  
4. **`success-scenarios`** - Success path testing (minimal errors)

### Using Different Templates

```bash
# Use performance testing template
echo "PROMPT_TEMPLATE=performance" > .env
npm run generate

# Use error scenarios template  
echo "PROMPT_TEMPLATE=error-scenarios" > .env
npm run generate

# Use success scenarios template
echo "PROMPT_TEMPLATE=success-scenarios" > .env
npm run generate
```

### Managing Templates via CLI

```bash
# List all available templates
npm run prompt list

# View template content
npm run prompt show performance

# Validate a template exists
npm run prompt validate my-template

# Create a new custom template
npm run prompt create my-test-scenario
```

### Creating Custom Templates

1. **Quick Method** - Use the CLI:
   ```bash
   npm run prompt create my-scenario
   # Edit prompts/my-scenario.md
   echo "PROMPT_TEMPLATE=my-scenario" > .env
   npm run generate
   ```

2. **Manual Method** - Copy and customize:
   ```bash
   cp prompts/custom-template.md prompts/my-scenario.md
   # Edit prompts/my-scenario.md with your requirements
   ```

### Example Custom Template

Create `prompts/financial-processing.md`:
```markdown
# Financial Transaction Processing Test Data

Generate batch job data for financial transaction processing with:
- Volume: 50,000-200,000 transactions  
- Processing steps: validation, fraud_detection, compliance_check, settlement
- Error types: FRAUD_DETECTED, COMPLIANCE_VIOLATION, INSUFFICIENT_FUNDS
- Success rate: 92-98%

## Processing Steps
- transaction_validation
- fraud_detection  
- compliance_check
- settlement_processing
- audit_trail_generation

## Error Scenarios
- FRAUD_DETECTED: 1-2% of transactions
- COMPLIANCE_VIOLATION: 0.5-1% of transactions
- INSUFFICIENT_FUNDS: 2-3% of transactions

Generate realistic financial processing batch job data following this structure.
```

Then use it:
```bash
echo "PROMPT_TEMPLATE=financial-processing" > .env
npm run generate
```

### Template Benefits for Testing

- **Performance Testing**: Use `performance` template for load testing scenarios
- **Error Handling**: Use `error-scenarios` for testing error recovery
- **Happy Path**: Use `success-scenarios` for baseline performance  
- **Domain-Specific**: Create custom templates for your business domain
- **Test Matrix**: Different templates for different test phases

See [prompts/README.md](./prompts/README.md) for detailed template creation guide.

#### Option B: Using OpenAI
```env
AI_PROVIDER=openai
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_MODEL=gpt-3.5-turbo
OUTPUT_DIRECTORY=./output
DEFAULT_FILE_COUNT=3
```

#### Option C: Using AWS Bedrock
```env
AI_PROVIDER=aws
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_actual_aws_access_key
AWS_SECRET_ACCESS_KEY=your_actual_aws_secret_key
OUTPUT_DIRECTORY=./output
DEFAULT_FILE_COUNT=3
```

#### Option D: Using Azure OpenAI
```env
AI_PROVIDER=azure
AZURE_OPENAI_ENDPOINT=https://your-resource-name.openai.azure.com/
AZURE_OPENAI_API_KEY=your_actual_azure_api_key
AZURE_OPENAI_DEPLOYMENT_NAME=gpt-35-turbo
OUTPUT_DIRECTORY=./output
DEFAULT_FILE_COUNT=3
```

#### Output Configuration (Optional)
```env
OUTPUT_DIRECTORY=./output
DEFAULT_FILE_COUNT=3
```

### 3. Build the Project

```bash
npm run build
```

### 4. Generate Test Data

Choose one of these methods to generate your test data:

#### Method 1: Using the built application
```bash
# Generate 3 files (default)
npm start

# Generate specific number of files
npm start 10
```

#### Method 2: Using development mode
```bash
# Generate 5 files in development mode
npm run generate 5

# Generate default number of files
npm run generate
```

#### Method 3: Using VS Code Tasks
1. Open the project in VS Code
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
3. Type "Tasks: Run Task"
4. Select "Generate Test Data (Development)"

### 5. Find Your Generated Files

Generated files will be saved in the `output/` directory with names like:
- `batch-job-BATCH-20240807-001-1691234567890.json`
- `batch-job-BATCH-20240807-002-1691234567891.json`

## Quick Testing

To verify everything is working:

```bash
# Test with just 1 file
npm start 1

# Check the output directory
ls output/

# View a generated file
cat output/batch-job-*.json | head -20
```

## Troubleshooting

### Common Issues and Solutions

1. **"AI_PROVIDER must be one of: 'aws', 'azure', 'openai', or 'mock'" Error**
   - Check your `.env` file exists and has a valid `AI_PROVIDER` value
   - For local testing, use `AI_PROVIDER=mock` (no credentials required)

2. **"AWS credentials are required" Error**
   - Verify your AWS credentials in `.env` are correct
   - Ensure you have AWS Bedrock access enabled in your account

3. **"Azure configuration is required" Error**
   - Check your Azure OpenAI endpoint, API key, and deployment name
   - Verify your Azure OpenAI resource is deployed and accessible

4. **"Failed to connect to AI provider" Warning**
   - The app will use fallback local generation
   - Check your internet connection and API credentials
   - Verify API quotas haven't been exceeded

5. **Files not generating**
   - Check if the `output/` directory was created
   - Verify write permissions in the project directory

### Debug Mode

For detailed error information:

```bash
# Run with verbose output
DEBUG=* npm start 1

# Or use development mode for more detailed logs
npm run generate 1
```

## Example Generated Data

Each file contains realistic batch job data like this:

```json
{
  "job_id": "BATCH-20240807-001",
  "start_time": "2024-08-07T08:15:22Z",
  "end_time": "2024-08-07T09:45:17Z",
  "status": "COMPLETED",
  "records_processed": 15782,
  "records_failed": 23,
  "processing_time_ms": 5395000,
  "steps": [
    {
      "step_name": "data_extraction",
      "status": "COMPLETED",
      "duration_ms": 1250000
    }
  ],
  "errors": [
    {
      "error_code": "DATA_FORMAT_ERROR",
      "error_message": "Invalid date format in record",
      "failed_record_ids": ["REC-7723", "REC-8915"]
    }
  ]
}
```

## Advanced Usage

### Programming Interface

```typescript
import { TestDataGenerator } from './src/generators/TestDataGenerator';
import { BatchJobGenerator } from './src/generators/BatchJobGenerator';

const generator = new TestDataGenerator();

// Generate single file
const singleFile = await generator.generateSingle();

// Generate multiple files
const multipleFiles = await generator.generateMultiple(10);

// Save to specific directory
await generator.saveToDirectory('./custom-output', files);

// Work with prompt templates programmatically
const availableTemplates = BatchJobGenerator.listAvailablePrompts();
console.log('Available templates:', availableTemplates);

const isValid = BatchJobGenerator.validatePromptTemplate('performance');
console.log('Template valid:', isValid);
```

### Custom Configuration

```typescript
import { TestDataGenerator, ConfigLoader } from './src';
import { PromptLoader } from './src/utils/PromptLoader';

// Check current configuration
const config = ConfigLoader.getInstance();
console.log('Current provider:', config.getAIProvider());
console.log('Current template:', config.getPromptTemplate());

// Work with prompts programmatically
const promptLoader = PromptLoader.getInstance();
const promptContent = promptLoader.loadPrompt('performance');
console.log('Using prompt:', promptContent);

// Validate provider connection
const isValid = await generator.validateProvider();
if (!isValid) {
  console.log('Provider connection failed, using fallback generation');
}
```

### File Management

```typescript
// List all generated files
const files = await generator.listGeneratedFiles();

// Clear output directory
await generator.clearOutputDirectory();

// Get output directory path
const outputPath = generator.getOutputDirectory();
```

## Serverless Deployment

### AWS Lambda

```bash
# Package for Lambda deployment
npm run build
zip -r lambda-deployment.zip dist/ node_modules/ package.json

# Deploy using AWS CLI or SAM
```

### Azure Functions

```bash
# Install Azure Functions Core Tools
npm install -g azure-functions-core-tools@4

# Deploy
func azure functionapp publish <function-app-name>
```

### API Endpoints

Once deployed, you can call the functions via HTTP. Before making API calls, you can configure the prompt template used for data generation by setting the `PROMPT_TEMPLATE` environment variable in your serverless function configuration.

#### Configuring Prompt Templates for API

Set the prompt template in your serverless function environment:

```bash
# For AWS Lambda
aws lambda update-function-configuration \
  --function-name your-function-name \
  --environment Variables='{PROMPT_TEMPLATE=performance,AI_PROVIDER=mock}'

# For Azure Functions  
az functionapp config appsettings set \
  --name your-function-name \
  --resource-group your-resource-group \
  --settings PROMPT_TEMPLATE=error-scenarios
```

#### API Usage Examples

```bash
# Generate 5 application files (uses configured prompt template)
curl "https://your-api-endpoint/generate?count=5"

# Get JSON data directly (without saving to files)
curl "https://your-api-endpoint/generate?count=3&returnFiles=true"

# Example: Performance testing data (if PROMPT_TEMPLATE=performance is configured)
curl "https://your-api-endpoint/generate?count=10"

# Example: Error scenario data (if PROMPT_TEMPLATE=error-scenarios is configured)  
curl "https://your-api-endpoint/generate?count=5&returnFiles=true"
```

**Available Template Options:**
- `default` - General purpose testing (balanced scenarios)
- `performance` - High volume performance testing scenarios
- `error-scenarios` - Error and failure testing scenarios
- `success-scenarios` - Success path testing scenarios
- Custom templates you've created in the `prompts/` directory

## Performance Considerations

- **Rate Limiting**: 1 second delay between AI API calls to avoid rate limits
- **Batch Size**: Recommended maximum 50 files per run
- **Fallback**: Automatic local generation if AI provider fails
- **Memory Usage**: Each file ~2-5KB, 1000 files ~5MB

## File Management Tips

- Generated files are saved with unique timestamps
- Use `npm run clean` to remove compiled TypeScript files
- Output directory is configurable via `.env` file
- Files include realistic error rates (0-5% of records)

## Source Code Packaging

Create a clean source package for distribution:

```bash
# Create source package (ZIP file with only essential files)
npm run package:source
```

The source package includes:
- ✅ **Source code**: `src/`, `scripts/`, `prompts/`, `serverless/`
- ✅ **Configuration**: `package.json`, `tsconfig.json`, `.env.template`
- ✅ **Documentation**: `README.md` and all `.md` files
- ✅ **Build configs**: `.gitignore`, `.dockerignore`

The source package excludes:
- ❌ **Dependencies**: `node_modules/`
- ❌ **Build artifacts**: `dist/`, `build/`, `bin/`
- ❌ **Secrets**: `.env` files, `*.key`, `*.pem`
- ❌ **IDE settings**: `.vscode/`, `.idea/`, `.vs/`
- ❌ **System files**: `.DS_Store`, `Thumbs.db`
- ❌ **Generated data**: `output/` directory

Perfect for sharing source code or deploying to new environments!

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License - see LICENSE file for details
