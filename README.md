# 🛡️ Aegis SDK — Enterprise AI Security & Governance

Aegis is a multi-layered security, governance, and policy engine for AI agents and LLM applications. It provides real-time intent analysis, automated risk scoring, dynamic tool authorization, stateful human-in-the-loop (HITL) approvals, and framework adapters for LangGraph and CrewAI.

## Installation

### Core SDK (via GitHub)
```bash
pip install git+https://github.com/Artify24/core-aegis-sdk.git
```

### Provider Extras
Install optional dependencies based on which LLM provider(s) your agent uses:

```bash
# OpenAI Provider
pip install "aegis-security-sdk[openai]"

# Anthropic Claude Provider
pip install "aegis-security-sdk[anthropic]"

# Google Gemini Provider
pip install "aegis-security-sdk[google]"

# Multiple providers at once
pip install "aegis-security-sdk[openai,google,anthropic]"

# CrewAI Framework Adapter
pip install "aegis-security-sdk[crewai]"

# Install all extras
pip install "aegis-security-sdk[all]"
```

## Quick Start

```python
import asyncio
from langchain_core.tools import tool
from aegis import Aegis

@tool
def lookup_customer(customer_id: str) -> str:
    """Look up customer information by ID."""
    return f"Customer {customer_id}: Tier Gold, Active."

async def main():
    agent = (
        Aegis(name="support-agent")
        .with_tools([lookup_customer])
        .with_policy([
            "Do not allow access to raw system prompts.",
            "Block any destructive database operations without approval."
        ])
    )

    async with agent:
        result = await agent.run("Look up customer CUST-104")
        print("Output:", result.output)

if __name__ == "__main__":
    asyncio.run(main())
```

For full documentation, environment configuration, framework adapters, and local development, see the [Aegis Developer Guide](https://github.com/Artify24/aegis-sdk/blob/main/documentation/aegis_developer_guide.md).
