# AI Tutor using MCP + OpenAI Agents SDK

This project demonstrates how to build an **AI Tutor** powered by the **OpenAI Agents SDK** and exposed tools through an **MCP (Model Context Protocol) server** over SSE.

It includes:
- An MCP server notebook that exposes tutor tools
- A client notebook that connects an Agent to that server
- Interactive Q&A, concept explanations, summarization, flashcards, and quizzes

## Project Structure

- `MCP Server.ipynb`  
	Builds/runs the MCP server (Gradio + SSE endpoint).

- `AI_Tutor_using_MCP_Open_AI_Agents_SDK.ipynb`  
	Client notebook that creates an Agent and connects to your MCP server.

- `.env`  
	Stores environment variables (for example `OPENAI_API_KEY`).

## Prerequisites

- Python 3.10+
- Jupyter environment (VS Code notebooks or Jupyter Lab)
- OpenAI API key

## Installation

Run these in the notebooks (already included in your cells):

- `openai-agents`
- `gradio`
- `openai`
- `python-dotenv`
- `requests`
- `httpx`
- `pillow`

If you prefer terminal installation:

```bash
pip install -U openai-agents gradio openai python-dotenv requests httpx pillow
```

## Environment Setup

Create/update `.env` in the project root:

```env
OPENAI_API_KEY=your_api_key_here
```

## How to Run

### 1) Start the MCP Server

1. Open `MCP Server.ipynb`.
2. Run cells in order.
3. Confirm the server is running and exposing an SSE endpoint (for example):

```text
http://localhost:7860/gradio_api/mcp/sse
```

### 2) Run the AI Tutor Client

1. Open `AI_Tutor_using_MCP_Open_AI_Agents_SDK.ipynb`.
2. Run cells top-to-bottom.
3. Verify `MCP_BASE` matches your server URL.
4. Start the chat loop cell and ask questions like:
	 - “Explain Newton’s third law in simple terms.”
	 - “Summarize this paragraph to 30%.”
	 - “Generate 8 flashcards for photosynthesis.”
	 - “Quiz me on fractions at level 2.”

## Available Tutor Capabilities

Depending on your MCP server implementation, the client Agent is configured to use:

- `explain_concept(question, level)`
- `summarize_text(text, compression_ratio)`
- `generate_flashcards(topic, num_cards)`
- `quiz_me(topic, level, num_questions)`

## Common Issues

### MCP Timeout / ReadError

If you see errors such as tool timeout or `httpx.ReadError`:

- Make sure `MCP Server.ipynb` is running.
- Confirm `MCP_BASE` is correct and reachable in browser/HTTP.
- Increase MCP/tool timeout values in client setup.
- Retry once; transient local tunnel/server delays can happen.

### Cell keeps running after answer

If your chat loop uses `while True`, it will keep waiting for the next input.  
Type `exit` or `quit` to stop, or change your loop to one-shot behavior.

## Notes

- Keep both notebooks on the same local environment/session when possible.
- Restarting the kernel can help if connections become stale.
- Avoid running duplicate server instances on the same port.

## License

This project is for educational/demo use.
