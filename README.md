<p align="center">
  <img src="https://raw.githubusercontent.com/getbindu/create-bindu-agent/refs/heads/main/assets/light.svg" alt="bindu Logo" width="200">
</p>

<h1 align="center">medical-diagnostics-agent</h1>

<p align="center">
  <strong>A Bindu AI Agent for Multi-Specialist Medical Diagnostics</strong>
</p>

<p align="center">
  <a href="https://github.com/Paraschamoli/medical-diagnostics-agent/actions/workflows/main.yml?query=branch%3Amain">
    <img src="https://img.shields.io/github/actions/workflow/status/Paraschamoli/medical-diagnostics-agent/main.yml?branch=main" alt="Build status">
  </a>
  <a href="https://img.shields.io/github/license/Paraschamoli/medical-diagnostics-agent">
    <img src="https://img.shields.io/github/license/Paraschamoli/medical-diagnostics-agent" alt="License">
  </a>
  <a href="https://img.shields.io/badge/python-3.12+-blue.svg">
    <img src="https://img.shields.io/badge/python-3.12+-blue.svg" alt="Python 3.12+">
  </a>
</p>

---

## 📖 Overview

**Medical Diagnostics Agent (MDA)** is a sophisticated AI-powered multi-specialist medical diagnostics system built on the [Bindu Agent Framework](https://github.com/getbindu/bindu). It leverages concurrent specialist AI agents to provide comprehensive medical analysis from patient reports.

**Key Capabilities:**
- 🏥 **Multi-Specialist Analysis**: Cardiologist, Psychologist, and Pulmonologist agents
- 🔄 **Concurrent Processing**: Parallel specialist analysis for comprehensive insights
- 🧠 **Intelligent Synthesis**: Multidisciplinary team integration for final diagnosis
- 🌐 **Production-Ready**: Bindu framework with JSON-RPC API
- � **OpenRouter Integration**: Advanced LLM models with proper API key management

---

## 🚀 Quick Start

### Prerequisites

- Python 3.12+
- [uv](https://github.com/astral-sh/uv) package manager
- OpenRouter API key (free tier available)

### Installation

```bash
# Clone the repository
git clone https://github.com/Paraschamoli/medical-diagnostics-agent.git
cd medical-diagnostics-agent

# Install dependencies
uv sync

# Configure environment
cp .env.example .env
```

### Configuration

Edit `.env` and add your API keys:

| Key | Get It From | Required |
|-----|-------------|----------|
| `OPENROUTER_API_KEY` | [OpenRouter](https://openrouter.ai/keys) | ✅ Yes |
| `OPENAI_API_KEY` | [OpenAI](https://platform.openai.com/api-keys) | ⚪ Optional |

### Run the Agent

```bash
# Start the agent
uv run -m medical_diagnostics_agent

# Agent will be available at http://localhost:3773
```

### Test with Sample Medical Report

```bash
# Send a test medical report via curl
curl -X POST http://localhost:3773 \
  -H "Content-Type: application/json" \
  -d @sample_medical_rpc.json

# Get the results
curl -X POST http://localhost:3773 \
  -H "Content-Type: application/json" \
  -d @get_task_rpc.json
```

### Github Setup

```bash
# Initialize git repository and commit your code
git init -b main
git add .
git commit -m "Initial commit"

# Create repository on GitHub and push (replace with your GitHub username)
gh repo create Paraschamoli/medical-diagnostics-agent --public --source=. --remote=origin --push
```

---

## 💡 Usage

### Medical Report Analysis

The agent processes comprehensive medical reports and provides multi-specialist analysis:

**Example Medical Report:**
```
Patient presents with chest pain, heart palpitations, shortness of breath, 
dizziness, and sweating episodes over the past 3 months. Episodes last 
10-20 minutes and occur without warning, typically once or twice a week...
```

**Output Structure:**
The agent returns structured diagnosis with:
- **Specialist Analysis**: Individual insights from Cardiologist, Psychologist, and Pulmonologist
- **Integrated Diagnosis**: Multidisciplinary team synthesis
- **Health Issues**: 3 primary conditions with detailed reasoning
- **Recommendations**: Specific next steps for each identified condition

### Sample JSON-RPC Request

```json
{
  "jsonrpc": "2.0",
  "method": "message/send",
  "params": {
    "message": {
      "parts": [{
        "kind": "text",
        "text": "Patient presents with chest pain, heart palpitations, shortness of breath..."
      }]
    }
  },
  "id": "unique-request-id"
}
```

### Response Format

```json
{
  "result": {
    "history": [{
      "role": "assistant",
      "parts": [{
        "kind": "text",
        "text": "### Final Diagnosis:\n\n- **Panic Disorder**: ...\n- **GERD**: ...\n- **Anxiety-Induced Hyperventilation**: ..."
      }]
    }]
  }
}
```

---

## 🔌 API Usage

The agent exposes a RESTful JSON-RPC API when running. Default endpoint: `http://localhost:3773`

### Endpoints

- **Agent Endpoint**: `http://localhost:3773/`
- **Agent Card**: `http://localhost:3773/.well-known/agent.json`
- **DID Resolution**: `http://localhost:3773/did/resolve`

### Quick Start

For complete API documentation, request/response formats, and examples, visit:

📚 **[Bindu API Reference - Send Message to Agent](https://docs.getbindu.com/api-reference/all-the-tasks/send-message-to-agent)**

### Additional Resources

- 📖 [Full API Documentation](https://docs.getbindu.com/api-reference/all-the-tasks/send-message-to-agent)
- 📦 [Postman Collections](https://github.com/GetBindu/Bindu/tree/main/postman/collections)
- 🔧 [API Reference](https://docs.getbindu.com)

---

## 🎯 Skills

### medical-diagnostics (v1.0.0)

**Primary Capability:**
- Multi-specialist medical diagnostics using concurrent AI agents
- Comprehensive analysis from Cardiologist, Psychologist, and Pulmonologist perspectives
- Intelligent synthesis for integrated medical diagnosis

**Features:**
- Concurrent specialist agent processing
- Role-specific medical analysis prompts
- Multidisciplinary team integration
- Structured diagnosis with reasoning
- OpenRouter model integration

**Best Used For:**
- Complex medical case analysis
- Multi-system symptom evaluation
- Comprehensive diagnostic insights
- Medical education and training

**Not Suitable For:**
- Emergency medical diagnosis
- Real-time patient monitoring
- Prescription medication recommendations
- Clinical decision support (research only)

**Performance:**
- Average processing time: ~15 seconds
- Max concurrent requests: 10
- Memory per request: ~50MB

---

## 🐳 Docker Deployment

### Local Docker Setup

```bash
# Build and run with Docker Compose
docker-compose up --build

# Agent will be available at http://localhost:3773
```

### Docker Configuration

The agent runs on port `3773` and requires:
- `OPENROUTER_API_KEY` environment variable
- `OPENAI_API_KEY` environment variable (optional)

Configure these in your `.env` file before running.

### Production Deployment

```bash
# Use production compose file
docker-compose -f docker-compose.prod.yml up -d
```

---

## 🌐 Deploy to bindus.directory

Make your agent discoverable worldwide and enable agent-to-agent collaboration.

### Setup GitHub Secrets

```bash
# Authenticate with GitHub
gh auth login

# Set deployment secrets
gh secret set BINDU_API_TOKEN --body "<your-bindu-api-key>"
gh secret set DOCKERHUB_TOKEN --body "<your-dockerhub-token>"
```

Get your keys:
- **Bindu API Key**: [bindus.directory](https://bindus.directory) dashboard
- **Docker Hub Token**: [Docker Hub Security Settings](https://hub.docker.com/settings/security)

### Deploy

```bash
# Push to trigger automatic deployment
git push origin main
```

GitHub Actions will automatically:
1. Build your agent
2. Create Docker container
3. Push to Docker Hub
4. Register on bindus.directory

---

## 🛠️ Development

### Project Structure

```
medical-diagnostics-agent/
├── medical_diagnostics_agent/
│   ├── skills/
│   │   └── medical-diagnostics/
│   │       ├── skill.yaml          # Skill configuration
│   │       └── __init__.py
│   ├── agents.py                   # Multi-agent implementation
│   ├── __init__.py
│   ├── __main__.py
│   ├── main.py                     # Agent entry point
│   └── agent_config.json           # Agent configuration
├── Medical Reports/                # Sample medical reports
├── sample_medical_rpc.json         # Sample API request
├── get_task_rpc.json              # Sample task retrieval
├── tests/
│   └── test_main.py
├── .env.example
├── docker-compose.yml
├── Dockerfile.agent
└── pyproject.toml
```

### Architecture

**Multi-Agent System:**
1. **MedicalAgent Base Class**: Common functionality for all specialists
2. **Specialist Agents**: Cardiologist, Psychologist, Pulmonologist
3. **MultidisciplinaryTeam**: Synthesis agent for integrated diagnosis
4. **Bindu Integration**: Production framework with JSON-RPC API

**Key Components:**
- **Concurrent Processing**: Async execution of specialist agents
- **OpenRouter Integration**: Advanced LLM model support
- **LangChain Framework**: Prompt engineering and chain management
- **Medical Prompts**: Role-specific diagnostic templates

### Running Tests

```bash
make test              # Run all tests
make test-cov          # With coverage report
```

### Code Quality

```bash
make format            # Format code with ruff
make lint              # Run linters
make check             # Format + lint + test
```

### Pre-commit Hooks

```bash
# Install pre-commit hooks
uv run pre-commit install

# Run manually
uv run pre-commit run -a
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature` 
3. Commit your changes: `git commit -m 'Add amazing feature'` 
4. Push to the branch: `git push origin feature/amazing-feature` 
5. Open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## ⚠️ Medical Disclaimer

**IMPORTANT**: This Medical Diagnostics Agent is intended for research and educational purposes only. It is **NOT** a substitute for professional medical advice, diagnosis, or treatment.

- ❌ **Do not use** for clinical decision-making
- ❌ **Do not use** for emergency medical situations  
- ❌ **Do not use** for patient diagnosis without professional oversight
- ✅ **Use for** medical education and research
- ✅ **Use for** understanding multi-agent AI systems
- ✅ **Use for** prototype development and testing

Always consult qualified healthcare professionals for medical concerns.

---

## 🙏 Powered by Bindu

Built with the [Bindu Agent Framework](https://github.com/getbindu/bindu)

**Why Bindu?**
- 🌐 **Internet of Agents**: A2A, AP2, X402 protocols for agent collaboration
- ⚡ **Zero-config setup**: From idea to production in minutes
- 🛠️ **Production-ready**: Built-in deployment, monitoring, and scaling

**Build Your Own Agent:**
```bash
uvx cookiecutter https://github.com/getbindu/create-bindu-agent.git
```

---

## 📚 Resources

- 📖 [Full Documentation](https://Paraschamoli.github.io/medical-diagnostics-agent/)
- 💻 [GitHub Repository](https://github.com/Paraschamoli/medical-diagnostics-agent/)
- 🐛 [Report Issues](https://github.com/Paraschamoli/medical-diagnostics-agent/issues)
- 💬 [Join Discord](https://discord.gg/3w5zuYUuwt)
- 🌐 [Agent Directory](https://bindus.directory)
- 📚 [Bindu Documentation](https://docs.getbindu.com)

---

<p align="center">
  <strong>Built with 💛 by the team from Amsterdam 🌷</strong>
</p>

<p align="center">
  <a href="https://github.com/Paraschamoli/medical-diagnostics-agent">⭐ Star this repo</a> •
  <a href="https://discord.gg/3w5zuYUuwt">💬 Join Discord</a> •
  <a href="https://bindus.directory">🌐 Agent Directory</a>
</p>

#   m e d i c a l - d i a g n o s t i c s - a g e n t  
 