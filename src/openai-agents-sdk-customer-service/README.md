# Customer Service Agents with OpenAI Agents SDK

This project demonstrates a multi-agent customer service system built using the `openai-agents` SDK. It features a triage agent that routes user queries to specialized agents for handling FAQs and seat bookings.

It is based on the [cookbook example](https://github.com/openai/openai-agents-python/blob/main/examples/customer_service/main.py) from the `openai-agents` SDK.

## Features

- **Triage Agent**: The entry point that understands user intent and delegates tasks.
- **FAQ Agent**: Answers questions about baggage, seats, and WiFi using a lookup tool.
- **Seat Booking Agent**: Handles seat updates for passengers.
- **Context Management**: Maintains passenger context (name, confirmation number, etc.) across the session.

## Prerequisites

- Python 3.14+
- `uv` package manager (recommended)
- OpenAI API Key
- HuggingFace Token (for the `nscale/Qwen/Qwen3-8B` model)

## Setup

1. **Install dependencies**:
   ```bash
   uv sync
   ```

2. **Environment Variables**:
   Create a `.env` file in the root or parent directory with your keys, or simply run the script and input them when prompted.
   ```env
   OPENAI_API_KEY=your_openai_key
   HF_TOKEN=your_huggingface_token
   ```

## Usage

Run the main script to start the interactive demo:

```bash
uv run main.py
```

## Example Interaction

Below is an example of a conversation flow with the agents:

> hello

[Agent updated: Triage Agent]


Hello! How can I assist you today? If you have any questions or need help with something related to flights, feel free to ask!
> i would like to know if my bag is allowed in the cabin

[Agent updated: Triage Agent]



[tool called]

[Agent updated: FAQ Agent]



[tool called]

[tool output: You are allowed to bring one bag on the plane. It must be under 50 pounds and 22 inches x 14 inches x 9 inches.]


You are allowed to bring one bag on the plane. It must weigh less than 50 pounds and fit within the dimensions of 22 inches x 14 inches x 9 inches. Be sure to confirm these details with your airline, as policies may vary slightly by carrier.
> can i update my seat?

[Agent updated: FAQ Agent]



[tool called]

[Agent updated: Triage Agent]



[tool called]

[Agent updated: Seat Booking Agent]


**Seat Booking Agent**:  
Sure! Could you please provide your confirmation number? Once I have that, I can check the available seats and proceed with the update.
> sure. it is ABC123

[Agent updated: Seat Booking Agent]


**Seat Booking Agent**:  
Thank you for the confirmation number, ABC123. Could you please let me know your desired seat number?
> i want the seat A15

[Agent updated: Seat Booking Agent]



[tool called]

[tool output: Updated seat to A15 for confirmation number ABC123]


Your seat has been successfully updated to **A15** for confirmation number **ABC123**. Let me know if you need further assistance! 😊
> thanks!

[Agent updated: Seat Booking Agent]


You're welcome! Let me know if you need anything else. 😊
