# MiroFish Development Setup

MiroFish is a complex multi-process application. This guide outlines the steps to set up a local development environment.

---

## 🛠 Prerequisites

- **Python**: 3.11+
- **Node.js**: 18+ (for frontend)
- **Conda**: Recommended for environment management.
- **Docker**: For running external dependencies.
- **Zep Cloud API Key**: For knowledge graph persistence.
- **LLM API Key**: OpenAI compatible (e.g., Qwen-plus, GPT-4).

---

## ⚙️ Environment Configuration

Create a `.env` file in the project root by copying `.env.example`:

```bash
# LLM Configuration
LLM_API_KEY=your_llm_api_key
LLM_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1  # Example for Qwen
LLM_MODEL_NAME=qwen-plus

# Zep Cloud Configuration
ZEP_API_KEY=your_zep_api_key

# Backend Settings
FLASK_ENV=development
UPLOAD_FOLDER=./uploads
```

---

## 🐍 Backend Setup

We use `uv` for fast package management.

1.  **Create Conda Environment**:
    ```bash
    conda create -n MiroFish python=3.11
    conda activate MiroFish
    ```

2.  **Install Dependencies**:
    ```bash
    pip install uv
    uv pip install -r requirements.txt
    ```

3.  **Run Development Server**:
    ```bash
    python run.py
    ```
    The API will be available at `http://localhost:5000`.

---

## ⚛️ Frontend Setup

1.  **Install Dependencies**:
    ```bash
    cd frontend
    npm install
    ```

2.  **Run Development Server**:
    ```bash
    npm run dev
    ```
    The frontend will be available at `http://localhost:5173`.

---

## 🐳 Docker Services

MiroFish can be deployed using Docker for consistent environments and simplified dependency management.

```bash
# Build and start all services
docker-compose up --build
```

---

## 📦 Dependency Management

When adding new Python packages, use `uv`:
```bash
uv pip compile pyproject.toml -o requirements.txt
```
This ensures a reproducible environment for all developers.
