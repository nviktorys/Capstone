# Sustainable Shopping Assistant - Capstone Project

## Overview
A multi-agent system that helps people shop more sustainably by automatically researching products and evaluating how eco-friendly the brands actually are.

## The Problem
Consumers face a common challenge when trying to buy sustainable products - every brand claims to be "green" or "eco-friendly," but actually figuring out which ones are legitimate takes forever. Shoppers have to check multiple websites, read through sustainability reports, and try to verify claims. It's exhausting, and honestly, most people give up and just buy whatever's convenient.

## The Solution
This project implements a system with three AI agents that work together:
1. One agent finds products based on what you're looking for
2. Another agent researches each brand's sustainability practices using real sources
3. A third agent combines everything and recommends the best option

The agent then scores brands on a 1-5 scale across four categories: environmental impact, ethical practices, animal welfare, and sustainability initiatives.

## How It Works

The system uses Google's Agent Development Kit (ADK) with Gemini 2.0. Here's the setup:

**Shopping Agent**: Searches for products using Google Search API, configured to find 6 options from UK retailers with prices and reviews.

**Sustainability Agent**: Takes the brands from the shopping results and researches them. It looks for:
- Environmental stuff (carbon footprint, waste management, packaging)
- Ethical practices (labor rights, fair trade, supply chain transparency)
- Animal welfare (cruelty-free certification, testing policies)
- Sustainability initiatives (actual programs, not just marketing)

**Root Agent**: Coordinates everything. Calls the shopping agent first, gets the brands, passes them to the sustainability agent, then combines it all into one recommendation.

## Tech Stack
- Google ADK for the agent framework
- Gemini 2.0 Flash (fast and efficient)
- Python 3.12
- Jupyter notebook for development
- Google Search API for both agents

The configuration is kept simple:
- 500 token limit to keep responses focused
- Built-in retry logic for when APIs act up
- All async so it doesn't take forever

## Example

Here's what it looks like when you run a query:

```python
await query("Sustainable toiletries under £30")
```

Output:
```
SUSTAINABLE SHOPPING RECOMMENDATION - PRODUCT DETAILS
────────────────────────────────────────────────────────────
  Brand:    Faith in Nature

SUSTAINABILITY SCORES
────────────────────────────────────────────────────────────
  Environmental Impact:        4/5
  Ethical Practices:           5/5
  Animal Welfare:              5/5
  Sustainability Initiatives:  4/5

  OVERALL SUSTAINABILITY:      4.5/5   EXCELLENT

EVALUATION SUMMARY
────────────────────────────────────────────────────────────
  Faith in Nature has cruelty-free certification from PETA,
  uses natural ingredients, and is transitioning to 100%
  recycled packaging. They're transparent about their supply
  chain and have strong ethical sourcing practices.
```

The system also logs everything to a file so you can see what searches it ran and how it came to its conclusions.

## Future Improvements

Potential next steps for development:

1. Integrate with actual sustainability databases (B Corp, Fair Trade certifications, etc.)
2. Show price history so you can see if something's actually on sale
3. Add a comparison view for the top 3 products side-by-side
4. Let users set preferences (like "I care more about animal welfare than carbon footprint")
5. Cache sustainability evaluations so repeat queries are instant

## Conclusion

This project demonstrates that multi-agent systems are really good at breaking down complex problems. Instead of one mega-prompt trying to do everything, having specialized agents that each handle one thing works much better.

The sustainability scoring isn't perfect, but it's a lot better than manually researching every brand. Being transparent about the scores and how they're calculated helps build trust.

Main takeaway: make sustainable shopping easier and more people will do it. That's the real goal.

## Links
- Code: https://github.com/nviktorys/Capstone
- Everything's in `src/agents/run_agents.ipynb`
- Setup instructions in the README
