# LangChain Agents
- In agents, a language model is used as a reasoning engine to determine which actions to take and in which order.
- Agents take a self-determined, input-dependent sequence of steps before returning a user-facing output. This makes debugging these systems particularly tricky, and observability particularly important.
- Steps to use Agents:
    - Defining tools → tools to use (Vector Store and other tools)
    - Creating list of tools
    - Creating agent → basically LLM for chat, summary, or other related purpose
    - Calling tools and agent executor
        
        ```python
        from langchain.agents import create_tool_calling_agent
        from langchain.agents import AgentExecutor
        
        agent = create_tool_calling_agent(llm, tools, prompt)
        agent_executor = AgentExecutor(agent=agent, tools=tools, verbose=True)
        ```
        
    - Running agent
        
        ```python
        agent_executor.invoke({"input": "hello!"})
        ```
        
- Since, agent is stateless, ***memory*** can be added to agents to function effectively.
- **Key Concepts**:
    | Schema | Agent Action | → data class representing the action an agent should take
    → has a tool property (name of tool to be invoked) and a tool_input property (input to that tool) |
    | --- | --- | --- |
    |  | Agent Finish | → final result from an agent
    → contains return_values key-value mapping containing the final agent output key that contains output |
    |  | Intermediate Steps | → previous agent actions and corresponding outputs from this CURRENT agent run
    → important to pass to future iteration so the agent knows what work it has already done
    → types as a List[Tuple[AgentAction, Any]] |
    | Agent | Agent Inputs | → inputs to an agent are a key-value mapping
    → required key: intermediate_steps
    → PromptTemplate() takes care of transforming these pairs into a format that can best be passed into the LLM |
    |  | Agent Outputs | → next action(s) to take or the final response to send to the user (AgentActions or AgentFinish)
    → typed as Union[AgentAction, List[AgentAction], AgentFinish]
    → Output parser is responsible for taking raw LLM output & transforming it. |
    | Agent Executor |  | → an agent runtime
    → calls agent, executes the actions it chooses, passes action’s outputs back to agent, and repeats |
    | Tools |  | → functions invoked by agent
    → Tool abstraction consist of 2 components:
    1. The input schema for the tool. This tells the LLM what parameters are needed to call the tool. Without this, it will not know what the correct inputs are. These parameters should be sensibly named and described.
    2. The function to run. This is generally just a Python function that is invoked. |
    |  | Considerations | 1. Giving right tools access to the agent
    2. Describing the tools in a way i.e. helpful to the agent |
    | Tool kits |  | Mentioned in tool kits integration section |
- Built-in agents
    
    [Types | 🦜️🔗 LangChain](https://python.langchain.com/docs/modules/agents/agent_types/)
    
- Custom Tools Integrations
    
    [Tools | 🦜️🔗 LangChain](https://python.langchain.com/docs/integrations/tools/)
