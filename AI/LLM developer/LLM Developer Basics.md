
Context window: Sending the full history is the key for maintaining context with LLMs. These models have a maximum limit on the total number of token (from both input messages and generated response) they can process in a single call. This is limit is known as context window. Context windows are normally over 100,00 tokens now but for very long task, you'll need strategies to manage this limit.

### Why prompt engineering, RAG, Tools and Find-tuning?

Transforming a basic prompt into a pipeline that's reliable and capable enough for a specific task takes a lot of work. The key developer tool kit for building and improving LLM-based products is:
1) Prompt Engineering
2) RAG
3) Fine Tuning
4) Tools use and Agents
5) Data Engineering (collection, Parsing and Curation)
6) Custom UI/UX

#### Prompting

Giving good and appropriate prompts to guide the model with clear instructions and using specific methods to improve performance.

#### RAG
Retrieval-Augmented Generation, or RAG, is about providing extra information and strapping a leash on LLMs.

#### Fine Tuning
Fine-tuning is like giving an LLM a crash course in your pet subject. Fine-Tuning can be used both for improving performance beyond the capability of off the shelf foundation State of the Art LLMs, but it is also used for helping smaller, faster, cheaper LLMs match the capability of larger models for your specific tasks.

#### Agents, Workflows and Tool Use

Why memorize when you can look it up? - the crux of Agents

LLMs are getting sharp enough to power agents—systems that think, plan, act autonomously and tap external tools to get stuff done. Think accessing calculators for math tasks, weather APIs for forecasts, or browsing the internet for you to research certain information. It’s less about stuffing the model with facts and more about teaching it to fetch what it needs and take actions if needed. These tools allow agents to handle tasks that go beyond their internal knowledge and processing capacity

#### Proprietary, Open-Weights, and Open-Source Models

Language models fall into three main categories: proprietary, open-weight, and open-source.
##### Proprietary models
like OpenAI’s GPT series and Anthropic’s Claude series, keep their capabilities behind a paywall, accessible through APIs or web interfaces.
##### Open-weight models
such as Meta’s Llama family or Alibaba’s Qwen models, offer their architectures and model weights for public use.
##### Fully open-source models
like AI2’s OLMo and Pynthia, are as transparent as they get, offering everything from pre-training data to training code.

Deciding on the best model involves assessing your specific requirements, resource availability, and budget.