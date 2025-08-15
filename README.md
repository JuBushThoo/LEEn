# 🤖 AI-Powered Telegram Bot

[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com/)

A modern Telegram bot powered by artificial intelligence, built on microservices architecture using Docker, PostgreSQL, and AI model integration.

## ✨ Features

- 🧠 **AI Integration** — Support for GPT-3.5/4, Llama 3, Hugging Face models
- 🐳 **Docker Containerization** — Easy deployment and scaling
- 🗄️ **PostgreSQL** — Reliable database for data persistence
- ⚡ **FastAPI Backend** — High-performance REST API
- 📊 **Logging & Monitoring** — Full system observability
- 🔒 **Security** — Secure environment variables handling
- 🚀 **CI/CD Ready** — Automated deployment pipeline

## 🏗️ Architecture

```
/project
├── bot/                  # Telegram bot code
│   ├── main.py           # Main bot script
│   ├── handlers/         # Command handlers
│   ├── middlewares/      # Middleware components
│   ├── utils/           # Utilities and helpers
│   └── requirements.txt
├── backend/              # FastAPI REST API
│   ├── main.py          # FastAPI application
│   ├── routers/         # API routes
│   ├── models/          # SQLAlchemy models
│   ├── schemas/         # Pydantic schemas
│   └── requirements.txt
├── db/                   # PostgreSQL configuration
│   └── init.sql         # Database initialization script
├── ai/                   # AI logic
│   ├── prompt_engine.py # Prompt tuning engine
│   ├── models/          # AI models
│   └── utils/           # AI utilities
├── docker-compose.yml    # Container orchestration
├── .env.example         # Environment variables example
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose
- Git
- Telegram bot token (get from [@BotFather](https://t.me/BotFather))
- OpenAI API key (optional)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/ai-telegram-bot.git
   cd ai-telegram-bot
   ```

2. **Configure environment variables**
   ```bash
   cp .env.example .env
   ```
   Edit the `.env` file:
   ```env
   # Telegram Bot
   BOT_TOKEN=your_telegram_bot_token
   
   # Database
   POSTGRES_USER=botuser
   POSTGRES_PASSWORD=secure_password
   POSTGRES_DB=telegram_bot
   DATABASE_URL=postgresql://botuser:secure_password@db:5432/telegram_bot
   
   # AI Integration
   OPENAI_API_KEY=your_openai_api_key
   AI_MODEL=gpt-3.5-turbo
   
   # Backend
   SECRET_KEY=your_secret_key
   ```

3. **Start the project**
   ```bash
   docker-compose up -d --build
   ```

4. **Check service status**
   ```bash
   docker-compose ps
   ```

## 🎯 Usage

### Bot Commands

- `/start` — Start interacting with the bot
- `/help` — Show help information
- `/ai <text>` — Query AI model
- `/stats` — Usage statistics
- `/settings` — User settings

### API Endpoints

API documentation is available at: `http://localhost:8000/docs`

- `GET /health` — Health check
- `POST /api/v1/chat` — Send message to AI
- `GET /api/v1/users/{user_id}` — Get user data
- `POST /api/v1/users` — Create user

## 🔧 Configuration

### Docker Compose Services

- **bot** — Telegram bot (Python)
- **backend** — FastAPI server
- **db** — PostgreSQL database
- **redis** — Redis for caching (optional)

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `BOT_TOKEN` | Telegram bot token | Required |
| `DATABASE_URL` | Database connection URL | `postgresql://...` |
| `OPENAI_API_KEY` | OpenAI API key | Optional |
| `LOG_LEVEL` | Logging level | `INFO` |
| `MAX_MESSAGE_LENGTH` | Maximum message length | `4000` |

## 🤖 AI Integration

### Supported Models

- **OpenAI GPT-3.5/4** — For high-quality responses
- **Llama 3** — Local deployment
- **Hugging Face Transformers** — Custom models

### AI Usage Example

```python
from ai.prompt_engine import PromptEngine

async def handle_ai_request(user_message: str):
    engine = PromptEngine(model="gpt-3.5-turbo")
    response = await engine.generate_response(
        prompt=user_message,
        max_tokens=150,
        temperature=0.7
    )
    return response
```

## 📊 Monitoring & Logging

### Logs
```bash
# View logs for all services
docker-compose logs -f

# View logs for specific service
docker-compose logs -f bot
```

### Metrics
- Number of processed messages
- AI model response time
- Resource usage

## 🚀 VPS Deployment

### 1. Server Setup

```bash
# System update
sudo apt update && sudo apt upgrade -y

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Install Docker Compose
sudo apt install docker-compose -y

# Add user to docker group
sudo usermod -aG docker $USER
```

### 2. Deployment

```bash
# Clone the project
git clone https://github.com/your-username/ai-telegram-bot.git
cd ai-telegram-bot

# Configure environment variables
cp .env.example .env
nano .env

# Start services
docker-compose -f docker-compose.prod.yml up -d
```

### 3. Nginx Configuration (Optional)

```nginx
server {
    listen 80;
    server_name yourdomain.com;
    
    location /api/ {
        proxy_pass http://localhost:8000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## 🧪 Testing

```bash
# Run tests
docker-compose exec bot python -m pytest tests/

# Test API
docker-compose exec backend python -m pytest tests/

# Check code coverage
docker-compose exec bot python -m pytest --cov=. tests/
```

## 📝 Development

### Local Development

```bash
# Install development dependencies
pip install -r requirements-dev.txt

# Run in development mode
docker-compose -f docker-compose.dev.yml up
```

### Pre-commit Hooks

```bash
# Install pre-commit
pip install pre-commit
pre-commit install

# Code formatting
black .
flake8 .
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) — Excellent library for Telegram bots
- [FastAPI](https://fastapi.tiangolo.com/) — Modern web framework for APIs
- [PostgreSQL](https://www.postgresql.org/) — Powerful object-relational database

## 📞 Support

If you have questions or issues:

- 🐛 [Create an Issue](https://github.com/your-username/ai-telegram-bot/issues)
- 💬 [Discussions](https://github.com/your-username/ai-telegram-bot/discussions)
- 📧 Email: your-email@example.com

---

⭐ Star this repo if you find it helpful!