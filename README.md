# 🩺 Medical Diagnosis Assistant Chatbot

A powerful **LLM-based medical diagnosis assistant** that uses a fine-tuned transformer model to provide **step-by-step reasoning and diagnoses** for user-reported symptoms. Built with **FastAPI**, **LangChain**, and **Streamlit**, this chatbot offers session-based memory and explainability via `<think>` tags for clinical reasoning.

---

## 🚀 Features

- 🤖 **Medical Diagnosis Generation** using a fine-tuned model on Hugging Face (`abdulsamad99/medical-fine-tuning`)
- 🧠 **Chain-of-Thought Reasoning** with `<think>` and `<response>` parsing
- 🧾 **Session-based Memory** to retain multi-turn chat history per user session
- 🌐 **FastAPI Backend** for serving diagnosis API with Ngrok tunnel
- 🖼️ **Streamlit Frontend** with real-time conversation, expandable reasoning, and session control
- 🔗 **LangChain Integration** to structure prompt, invoke model, and parse responses
- ⚡ **Unsloth** for fast, efficient LLM inference on GPU with 4-bit quantization
- 🔒 **Secure tokens** via Hugging Face and Ngrok authentication

---

## 🏗️ Tech Stack

| Layer       | Tools Used |
|-------------|------------|
| Model       | `abdulsamad99/medical-fine-tuning` (Unsloth, Hugging Face) |
| Backend     | FastAPI, LangChain, PyNgrok |
| Frontend    | Streamlit |
| Orchestration | RunnableSequence, LangChain Runnables |
| Hosting     | Ngrok tunneling for public endpoints |
| Dependencies| torch, transformers, unsloth, pydantic, uvicorn, fastapi, streamlit, langchain |

---

## 🧠 Model Details

- **Model ID**: `abdulsamad99/medical-fine-tuning`
- **Base**: LLaMA-based transformer fine-tuned for medical diagnosis using chain-of-thought formatting
- **Architecture**: LLM with Unsloth, loaded in 4-bit precision
- **Token Limit**: `MAX_SEQ_LENGTH = 512`
- **Reasoning Format**:
<think> ... step-by-step reasoning ... </think>
<response> final diagnosis </response>
## 🛠️ Installation & Setup

1. **Clone the repo**:
 ```bash
 git clone https://github.com/YOUR_USERNAME/Medical_Assistant_Chatbot.git
 cd Medical_Assistant_Chatbot
2. Install dependencies:
# Run this only outside Colab
pip install unsloth
pip install fastapi uvicorn nest-asyncio pydantic[dotenv]
pip install streamlit requests httpx python-multipart
pip install langchain langchain-community langchain-huggingface
pip install pyngrok
3. Configure Tokens:

Replace HF_TOKEN in the code with your Hugging Face token

Replace NGROK_TOKEN in the code with your Ngrok auth token
4. Run the application
5. 🧪 Example Usage
User enters:

"I have fever, cough, and shortness of breath."

The assistant replies:

"Based on symptoms, possibilities include viral infection or pneumonia."

(Click "Reasoning" to view thought process inside <think>)
6. 🧩 Architecture Overview
+-----------+         +-------------------+         +-------------------+
|  Streamlit| <-----> | FastAPI + LangChain| <-----> | Hugging Face Model|
+-----------+         +-------------------+         +-------------------+
        ↕                        ↕                          ↕
   Session ID           RunnableSequence             Unsloth 4-bit model
     Memory              Prompt + OutputParser        + LLaMA tokenizer
✅ Future Improvements
Add user authentication and patient profiles

Integrate with medical knowledge graphs

Improve diagnosis accuracy with external retrieval (RAG)

Add multilingual support

🤝 Contributing
Feel free to submit issues or pull requests. All contributions are welcome!
