# Sustainable Shopping Assistant

A multi-agent AI system that helps users make environmentally conscious shopping decisions by combining product search with sustainability evaluation.

## Overview

This project uses Google's Agent Development Kit (ADK) and Gemini AI to create an intelligent shopping assistant that:

- **Searches for products** based on user queries
- **Evaluates brand sustainability** using multiple criteria
- **Recommends the best option** balancing quality, price, and environmental impact

The system employs three specialized AI agents working together:
1. **Shopping Agent** - Finds and compares products from UK retailers
2. **Sustainability Evaluation Agent** - Researches and scores brands on environmental and ethical practices
3. **Root Orchestrator Agent** - Combines results to provide the optimal recommendation

## Features

- **Multi-dimensional Sustainability Scoring**
  - Environmental Impact (carbon footprint, resource usage, waste management)
  - Ethical Practices (labor rights, fair trade, community engagement)
  - Animal Welfare (cruelty-free certifications, testing policies)
  - Sustainability Initiatives (environmental programs and policies)

- **Smart Product Discovery**
  - Searches across multiple UK retailers
  - Compares prices and user ratings
  - Evaluates 6 products and returns 1 best recommendation

- **Comprehensive Evaluation**
  - External validation of sustainability claims
  - Scoring system from 1-5 for each category
  - Overall sustainability rating with detailed justification

## Getting Started

### Prerequisites

- Python 3.12 or higher
- Google API Key with access to Gemini API
- Git (for cloning the repository)

### Installation

1. **Clone the repository**
   ```powershell
   git clone https://github.com/nviktorys/Capstone.git
   cd Capstone
   ```

2. **Set up Python environment**

   Using UV (recommended):
   ```powershell
   # Install UV
   pip install uv
   
   # Install dependencies
   uv sync
   ```

   Using venv:
   ```powershell
   # Create virtual environment
   python -m venv .venv
   
   # Activate virtual environment
   .venv\Scripts\activate
   
   # Install dependencies
   pip install google-adk google-generativeai jupyter ipykernel
   ```

3. **Configure API Key**

   Create a `.env` file in the project root:
   ```bash
   GOOGLE_API_KEY=your_google_api_key_here
   ```

   Or set as environment variable:
   ```powershell
   $env:GOOGLE_API_KEY="your_google_api_key_here"
   ```

   **Note:** Get your Google API key from [Google AI Studio](https://makersuite.google.com/app/apikey)

## Usage

### Running the Notebook

1. **Start Jupyter Notebook**
   ```powershell
   # If using UV
   uv run jupyter notebook
   
   # If using venv
   jupyter notebook
   ```

2. **Open the notebook**
   - Navigate to `src/agents/run_agents.ipynb`

3. **Run cells sequentially**

   **Cell 1-2:** Import dependencies and configure model
   ```python
   # Sets up Google Gemini with retry logic and token limits
   ```

   **Cell 3:** Create Shopping Agent
   ```python
   # Finds products from UK retailers
   ```

   **Cell 4:** Create Sustainability Evaluation Agent
   ```python
   # Researches and scores brands
   ```

   **Cell 5:** Create Root Orchestrator Agent
   ```python
   # Combines shopping and sustainability results
   ```

   **Cell 6:** Create Runner
   ```python
   runner = InMemoryRunner(
       agent=root_agent,
       plugins=[LoggingPlugin()]
   )
   ```

   **Cell 7:** Execute Query
   ```python
   response = await runner.run_debug(
       "Find vegan christmas chocolate gifts."
   )
   ```

   **Cell 8:** Display Results
   ```python
   display_recommendation(response)
   ```

### Example Queries

```python
# Vegan products
response = await runner.run_debug("Find vegan christmas chocolate gifts.")

# Sustainable fashion
response = await runner.run_debug("Find sustainable winter jackets.")

# Eco-friendly home products
response = await runner.run_debug("Find eco-friendly water bottles.")

# Ethical electronics
response = await runner.run_debug("Find sustainably made wireless headphones.")
```

## Output Format

The system provides a comprehensive recommendation with:

```
PRODUCT DETAILS
  Brand:    [Brand Name]

SUSTAINABILITY SCORES
  Environmental Impact:        x/5
  Ethical Practices:           x/5
  Animal Welfare:              x/5
  Sustainability Initiatives:  x/5

  OVERALL SUSTAINABILITY:       x/5.0
  Rating:                       EXCELLENT/GOOD/FAIR/POOR

EVALUATION SUMMARY
  [Detailed explanation of scores and recommendation rationale]
```

## Project Structure

```
Capstone/
├── src/
│   └── agents/
│       ├── run_agents.ipynb    # Main notebook with agent implementation
├── .env                        # Environment variables (not in git)
├── .gitignore                  # Git ignore rules
├── pyproject.toml              # Project dependencies
├── uv.lock                     # Dependency lock file
└── README.md                   # This file
```

## Configuration

### Model Settings

Located in notebook Cell 2:

```python
model_name = "gemini-2.0-flash"          # Gemini model version

retry_config = types.HttpRetryOptions(
    attempts=5,                           # Max retry attempts
    exp_base=7,                           # Delay multiplier
    initial_delay=1,                      # Initial delay (seconds)
    http_status_codes=[429, 500, 503, 504]
)

short_config = types.GenerationConfig(
    max_output_tokens=500,                # Token limit per response
)
```

### Agent Customization

You can modify agent instructions in Cells 3-5 to:
- Change the number of product recommendations
- Adjust sustainability scoring criteria
- Target different regions (currently UK-focused)
- Add additional evaluation categories

## Testing

Example test scenarios:

1. **Vegan Products**
2. **Sustainable Fashion** 
3. **Electronics**

## Troubleshooting

### Common Issues

**"GOOGLE_API_KEY not set" error**
```powershell
# Set environment variable
$env:GOOGLE_API_KEY="your_key_here"

# Or add to .env file
echo GOOGLE_API_KEY=your_key_here > .env
```

**"Module not found" errors**
```powershell
# Reinstall dependencies
pip install google-adk google-generativeai jupyter
```

**Sustainability scores seem inaccurate**
- The agent relies on publicly available information
- Scores are subjective and based on AI interpretation

## Dependencies

Core libraries:
- `google-adk>=1.19.0` - Google Agent Development Kit
- `google-generativeai>=0.8.5` - Google Gemini API client
- `jupyter` - Interactive notebook environment
- `ipykernel` - Jupyter kernel for Python