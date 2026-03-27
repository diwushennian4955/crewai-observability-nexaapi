# CrewAI Observability + NexaAPI

> Build observable, cost-efficient AI agent pipelines. LoongSuite instrumentation + NexaAPI inference = the ultimate CrewAI stack.

[![NexaAPI](https://img.shields.io/badge/NexaAPI-56%2B%20Models-blue)](https://nexa-api.com)
[![PyPI](https://img.shields.io/pypi/v/nexaapi)](https://pypi.org/project/nexaapi)

## Stack

```
CrewAI (orchestration) + LoongSuite (observability) + NexaAPI (inference)
```

## Quick Start

```bash
pip install nexaapi crewai loongsuite-instrumentation-crewai
```

```python
from loongsuite.instrumentation.crewai import CrewAIInstrumentor
from nexaapi import NexaAPI
from crewai import Agent, Task, Crew, tool

# Enable observability
CrewAIInstrumentor().instrument()

client = NexaAPI(api_key='YOUR_NEXAAPI_KEY')

@tool('Image Generator')
def generate_image(prompt: str) -> str:
    """Generate an AI image for $0.003 using NexaAPI."""
    result = client.image.generate(model='flux-schnell', prompt=prompt, width=1024, height=1024)
    return result.url

creative_agent = Agent(
    role='Creative Director',
    goal='Generate multimedia content',
    backstory='Expert creative director using AI at scale.',
    tools=[generate_image],
    verbose=True
)

task = Task(description='Create a product banner image.', expected_output='Image URL', agent=creative_agent)
crew = Crew(agents=[creative_agent], tasks=[task])
result = crew.kickoff()
# All API calls are now traced by LoongSuite!
```

## Cost Comparison

| Provider | Image | 100 images |
|----------|-------|-----------|
| **NexaAPI** | **$0.003** | **$0.30** |
| Replicate | ~$0.04 | ~$4.00 |
| DALL-E 3 | $0.04-0.12 | ~$8.00 |

## Links

- 🌐 [nexa-api.com](https://nexa-api.com)
- 🐍 [pypi.org/project/nexaapi](https://pypi.org/project/nexaapi)
- 📦 [npmjs.com/package/nexaapi](https://www.npmjs.com/package/nexaapi)
- ⚡ [rapidapi.com/user/nexaquency](https://rapidapi.com/user/nexaquency)
- 🔗 [LoongSuite CrewAI](https://pypi.org/project/loongsuite-instrumentation-crewai/)

## Topics

`crewai` `observability` `loongsuite` `nexaapi` `ai-agents` `image-generation` `python` `opentelemetry`
