## Testing CopilotKit Genrative UI & AG-UI

1. The Python Backend (FastAPI)
Your FastAPI server will act as a Remote Endpoint. Its job is to provide the "intelligence" (tools and agents) that the React frontend will call.

Install the SDK: You'll need copilotkit and fastapi (plus uvicorn to run it).

The SDK Bridge: CopilotKit provides a specific integration for FastAPI called add_fastapi_endpoint.

Defining Actions: Instead of JS functions, you'll define Python functions as Action objects. You'll give them a name, description, and parameter types (similar to OpenAI tool definitions).

The Integration: You pass your FastAPI app and your list of Action objects into the bridge function. This creates a specific route (usually /copilotkit) that the frontend can talk to.

2. The React Frontend
Since your runtime is now a standalone Python server, your React setup is simplified.

Runtime URL: In your <CopilotKit> provider, you won't point to a local /api/copilotkit file. Instead, you'll point it to your FastAPI URL:
runtimeUrl="http://localhost:8000/copilotkit"

Generative UI Hook: You still use useCopilotAction in React. Even though the "logic" is in Python, the rendering happens in React.

The Connection: 1.  User asks a question.
2.  The React app asks the Python backend: "What should I do?"
3.  Python backend responds: "Run the show_chart action with these data parameters."
4.  React app sees that action is registered in useCopilotAction and renders your component.