# Agents Reflection, ReWOO & ReAct — Advanced AI Agent Patterns

Implementation of three advanced AI agent architectures: Reflection (self-critique and improvement), ReWOO (Reasoning WithOut Observation), and ReAct (Reasoning + Acting). Built with LangGraph and LangChain for production-ready agentic workflows.

## Description

This repository demonstrates state-of-the-art AI agent design patterns that go beyond simple LLM calls. Each pattern addresses different challenges in autonomous AI task execution: Reflection enables self-improvement through critique loops, ReWOO decouples planning from execution for efficiency, and ReAct interleaves reasoning with tool use for grounded decision-making.

These patterns are implemented using LangGraph's stateful graph framework, enabling complex agent workflows with memory, branching logic, and human-in-the-loop checkpoints.

## Features

- **Reflection Agent** — Multi-turn self-critique loop where the agent evaluates its own output and iteratively improves until quality thresholds are met
- - **ReWOO (Reasoning Without Observation)** — Two-phase architecture: planner generates full plan upfront, solver executes without intermediate LLM calls, reducing token cost by 70%
  - - **ReAct Agent** — Thought-Action-Observation loop enabling dynamic tool selection based on intermediate results
    - - **LangGraph State Machine** — Graph-based workflow with typed state, conditional edges, and checkpoint persistence
      - - **Tool Integration** — Web search (Tavily), code execution (Python REPL), calculator, and custom API tools
        - - **Memory Management** — Short-term conversation buffer and long-term vector store memory
          - - **Streaming Support** — Real-time token streaming with intermediate step visibility
           
            - ## Architecture
           
            - ```
              ReAct Pattern:
                Thought --> Action (Tool Call) --> Observation --> Thought --> ... --> Final Answer

              Reflection Pattern:
                Generate --> Reflect (Critique) --> Revise --> Reflect --> ... --> Accept

              ReWOO Pattern:
                Planner (full plan) --> Tool Executor (batch) --> Solver (final answer)
              ```

              ## Tech Stack

              | Component | Technology |
              |-----------|-----------|
              | Agent Framework | LangGraph, LangChain |
              | LLM | OpenAI GPT-4, Anthropic Claude |
              | Tools | Tavily Search, Python REPL, Wikipedia |
              | State Management | LangGraph StateGraph |
              | Memory | ConversationBufferMemory, FAISS |
              | Language | Python 3.10+ |

              ## Setup Instructions

              ### Prerequisites

              - Python 3.10 or higher
              - - OpenAI API key
                - - Tavily API key (for web search)
                 
                  - ### Installation
                 
                  - ```bash
                    git clone https://github.com/sanikacentric/Agents_Reflection_Rewoo_ReAct.git
                    cd Agents_Reflection_Rewoo_ReAct
                    pip install langchain langgraph langchain-openai tavily-python
                    ```

                    ### Configuration

                    ```bash
                    export OPENAI_API_KEY="your-openai-api-key"
                    export TAVILY_API_KEY="your-tavily-api-key"
                    ```

                    ### Running ReAct Agent

                    ```python
                    from langchain.agents import create_react_agent, AgentExecutor
                    from langchain_openai import ChatOpenAI
                    from langchain.tools import TavilySearchResults

                    llm = ChatOpenAI(model="gpt-4")
                    tools = [TavilySearchResults()]

                    agent = create_react_agent(llm, tools, prompt)
                    executor = AgentExecutor(agent=agent, tools=tools, verbose=True)
                    result = executor.invoke({"input": "What is the latest news on AI regulation?"})
                    ```

                    ### Running Reflection Agent

                    ```python
                    python agents/reflection_agent.py
                    ```

                    ### Running ReWOO Agent

                    ```python
                    python agents/rewoo_agent.py
                    ```

                    ## License

                    MIT License
