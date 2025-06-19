# 🚀 Agentic AI-Driven Stock Market Analysis Tool

[![Python](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104.1-green.svg)](https://fastapi.tiangolo.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28.1-red.svg)](https://streamlit.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An intelligent, multi-agent AI system for comprehensive stock market analysis, sentiment tracking, and portfolio management. This tool leverages advanced AI agents to process real-time financial data, perform sentiment analysis, forecast trends, and provide personalized investment recommendations.

## 🎯 Features

### 🤖 AI Agent Capabilities
- **Data Collection Agent**: Autonomous data gathering from multiple financial APIs
- **Sentiment Analysis Agent**: Real-time news and social media sentiment processing
- **Technical Analysis Agent**: Chart pattern recognition and technical indicators
- **Risk Assessment Agent**: Portfolio risk evaluation and exposure analysis
- **Recommendation Engine**: Personalized investment suggestions based on user profiles

### 📊 Core Functionality
- **Real-time Stock Data**: Live prices, volume, and market indicators via Yahoo Finance API
- **Sentiment Analysis**: News sentiment tracking from multiple sources
- **Technical Indicators**: 50+ technical analysis indicators (RSI, MACD, Bollinger Bands, etc.)
- **Portfolio Risk Management**: VaR, Sharpe ratio, beta analysis, and correlation matrices
- **Predictive Modeling**: Machine learning-based price forecasting
- **Scenario Simulation**: Stress testing and "what-if" analysis

### 🎨 Interactive Dashboard
- **Real-time Visualizations**: Interactive charts and heatmaps
- **Sentiment Heatmaps**: Visual representation of market sentiment
- **Risk Dashboards**: Portfolio risk metrics and exposure analysis
- **Scenario Modeling**: Interactive simulation tools
- **Custom Alerts**: Personalized notification system

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Data Sources  │────│   AI Agents      │────│  User Interface │
│                 │    │                  │    │                 │
│ • Yahoo Finance │    │ • Data Collector │    │ • Streamlit     │
│ • News APIs     │────│ • Sentiment      │────│ • FastAPI       │
│ • Social Media  │    │ • Technical      │    │ • Visualizations│
│ • Economic Data │    │ • Risk Analysis  │    │ • Alerts        │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                              │
                    ┌──────────────────┐
                    │   Data Storage   │
                    │                  │
                    │ • PostgreSQL     │
                    │ • Redis Cache    │
                    │ • Time Series DB │
                    └──────────────────┘
```

## 🚀 Quick Start

### Prerequisites
- Python 3.9 or higher
- PostgreSQL (optional, for persistent storage)
- Redis (optional, for caching)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/agentic-stock-analysis.git
   cd agentic-stock-analysis
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Download NLP models**
   ```bash
   python -m spacy download en_core_web_sm
   python -c "import nltk; nltk.download('vader_lexicon')"
   ```

5. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys and configuration
   ```

6. **Initialize database (optional)**
   ```bash
   alembic upgrade head
   ```

### Running the Application

#### Streamlit Dashboard
```bash
streamlit run app/main.py
```

#### FastAPI Backend
```bash
uvicorn app.api.main:app --reload --host 0.0.0.0 --port 8000
```

#### With Docker
```bash
docker-compose up -d
```

## 🔧 Configuration

### Environment Variables

Create a `.env` file with the following variables:

```env
# API Keys
OPENAI_API_KEY=your_openai_api_key
NEWS_API_KEY=your_news_api_key
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key
POLYGON_API_KEY=your_polygon_api_key

# Database Configuration
DATABASE_URL=postgresql://user:password@localhost:5432/stockdb
REDIS_URL=redis://localhost:6379/0

# Application Settings
DEBUG=True
SECRET_KEY=your_secret_key_here
ENVIRONMENT=development

# AI Agent Configuration
MAX_CONCURRENT_AGENTS=5
SENTIMENT_UPDATE_INTERVAL=300  # seconds
PRICE_UPDATE_INTERVAL=60      # seconds
```

### API Keys Required

| Service | Purpose | Required |
|---------|---------|----------|
| OpenAI | AI agent orchestration | Yes |
| News API | News sentiment analysis | Recommended |
| Alpha Vantage | Financial data backup | Optional |
| Polygon.io | Real-time market data | Optional |
| Twitter API | Social sentiment | Optional |

## 📱 Usage Examples

### Basic Stock Analysis
```python
from app.agents import StockAnalysisOrchestrator

# Initialize the orchestrator
orchestrator = StockAnalysisOrchestrator()

# Analyze a stock
analysis = orchestrator.analyze_stock("AAPL")
print(f"Current Price: ${analysis['current_price']}")
print(f"Sentiment Score: {analysis['sentiment_score']}")
print(f"Risk Rating: {analysis['risk_rating']}")
```

### Portfolio Risk Assessment
```python
from app.agents import RiskAssessmentAgent

# Assess portfolio risk
risk_agent = RiskAssessmentAgent()
portfolio = ["AAPL", "GOOGL", "MSFT", "TSLA"]
weights = [0.25, 0.25, 0.25, 0.25]

risk_metrics = risk_agent.assess_portfolio(portfolio, weights)
print(f"Portfolio VaR: {risk_metrics['var_95']}")
print(f"Sharpe Ratio: {risk_metrics['sharpe_ratio']}")
```

### Sentiment Analysis
```python
from app.agents import SentimentAnalysisAgent

# Analyze market sentiment
sentiment_agent = SentimentAnalysisAgent()
sentiment = sentiment_agent.analyze_stock_sentiment("AAPL")

print(f"News Sentiment: {sentiment['news_sentiment']}")
print(f"Social Media Sentiment: {sentiment['social_sentiment']}")
print(f"Overall Score: {sentiment['composite_score']}")
```

## 🧪 Testing

Run the test suite:
```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app --cov-report=html

# Run specific test categories
pytest tests/test_agents.py  # Agent tests
pytest tests/test_api.py     # API tests
pytest tests/test_data.py    # Data processing tests
```

## 📊 API Documentation

Once the FastAPI backend is running, visit:
- **Interactive API docs**: http://localhost:8000/docs
- **ReDoc documentation**: http://localhost:8000/redoc

### Key Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/v1/analyze/{symbol}` | GET | Get comprehensive stock analysis |
| `/api/v1/sentiment/{symbol}` | GET | Get sentiment analysis for a stock |
| `/api/v1/portfolio/risk` | POST | Calculate portfolio risk metrics |
| `/api/v1/recommendations` | GET | Get personalized recommendations |
| `/api/v1/scenarios/simulate` | POST | Run scenario simulations |

## 🚢 Deployment

### Docker Deployment
```bash
# Build and run with Docker Compose
docker-compose up -d

# Scale services
docker-compose up -d --scale api=3 --scale worker=2
```

### Cloud Deployment (AWS)
```bash
# Using AWS ECS
aws ecs create-cluster --cluster-name stock-analysis-cluster

# Deploy with Terraform (coming soon)
terraform init
terraform plan
terraform apply
```

### Environment-Specific Configurations

#### Development
```bash
export ENVIRONMENT=development
export DEBUG=True
streamlit run app/main.py
```

#### Production
```bash
export ENVIRONMENT=production
export DEBUG=False
gunicorn app.api.main:app -w 4 -k uvicorn.workers.UvicornWorker
```

## 🔍 Monitoring & Logging

### Application Metrics
- **Prometheus metrics**: http://localhost:8000/metrics
- **Health check**: http://localhost:8000/health
- **Agent performance**: Monitor via dashboard

### Logging
Logs are structured using Loguru:
```python
from loguru import logger

logger.info("Agent analysis completed", symbol="AAPL", duration=1.2)
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Setup
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and add tests
4. Run the test suite: `pytest`
5. Submit a pull request

### Code Style
- Use Black for code formatting: `black .`
- Use isort for import sorting: `isort .`
- Follow PEP 8 guidelines
- Add type hints where appropriate

## 📋 Roadmap

### Phase 1 (Current)
- [x] Basic agent architecture
- [x] Yahoo Finance integration
- [x] Streamlit dashboard
- [x] Sentiment analysis
- [ ] Technical indicators

### Phase 2
- [ ] Advanced AI agents
- [ ] Portfolio optimization
- [ ] Real-time alerts
- [ ] Mobile app support

### Phase 3
- [ ] Cryptocurrency support
- [ ] Options analysis
- [ ] Social trading features
- [ ] Advanced ML models

## ⚠️ Disclaimer

**Important**: This tool is for educational and informational purposes only. It does not constitute financial advice, investment recommendations, or trading signals. Always consult with qualified financial professionals before making investment decisions. Past performance does not guarantee future results.


## 🙏 Acknowledgments

- Yahoo Finance for providing free financial data
- OpenAI for AI capabilities
- The open-source Python community
- Financial data providers and APIs

---

**Built with ❤️ using Python, FastAPI, Streamlit, and AI**
