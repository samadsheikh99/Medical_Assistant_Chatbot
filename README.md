Medical Diagnosis Assistant Chatbot
Overview
The Medical Diagnosis Assistant Chatbot is a web-based application designed to provide medical diagnosis assistance by leveraging a fine-tuned large language model (LLM) for processing user-provided symptoms and generating potential diagnoses. The project integrates a FastAPI backend for handling API requests, a Streamlit frontend for user interaction, and utilizes the unsloth library for efficient model inference. The chatbot maintains per-session conversation history to provide context-aware responses, enhancing the user experience. The application is deployed using ngrok for public access, making it accessible via a web browser.
This project is intended for educational and research purposes, demonstrating how to combine modern AI frameworks, web APIs, and user interfaces to create an interactive medical assistant tool.
Features

Per-Session Context Awareness: Maintains conversation history for each user session, allowing the model to consider previous interactions when generating responses.
Fine-Tuned Language Model: Uses a pre-trained model (abdulsamad99/medical-fine-tuning) optimized for medical diagnosis, loaded with 4-bit quantization for efficient inference.
FastAPI Backend: Provides a robust API endpoint (/diagnose) to process symptom inputs and return diagnoses with optional reasoning output.
Streamlit Frontend: Offers a user-friendly interface for entering symptoms, viewing conversation history, and toggling reasoning visibility.
Regex-Based Response Parsing: Extracts <think> and <response> sections from model outputs to separate reasoning and diagnosis for better interpretability.
GPU Acceleration: Leverages CUDA-enabled GPUs for fast model inference using the unsloth and transformers libraries.
Public Deployment with ngrok: Exposes both FastAPI and Streamlit servers to the internet via ngrok tunnels for easy access.

Technologies Used

Python Libraries:
unsloth: For efficient loading and inference of the fine-tuned language model.
transformers: For tokenizer and model management.
langchain: For creating a chain to process inputs and format outputs.
fastapi, uvicorn: For building and serving the API.
streamlit: For the interactive web interface.
pyngrok: For creating public URLs for local servers.
torch: For GPU-accelerated model inference.
Others: requests, httpx, python-multipart, pydantic, sentencepiece, protobuf, datasets, huggingface_hub, hf_transfer.


Model: abdulsamad99/medical-fine-tuning from Hugging Face, fine-tuned for medical diagnosis.
Hardware: CUDA-compatible GPU for model inference.



Install Dependencies:Ensure you have Python 3.8+ and a CUDA-compatible GPU. Install the required packages:
pip install unsloth bitsandbytes accelerate xformers==0.0.29.post3 peft trl==0.15.2 triton cut_cross_entropy
pip install sentencepiece protobuf datasets huggingface_hub hf_transfer
pip install fastapi uvicorn nest-asyncio pydantic[dotenv]
pip install streamlit requests httpx python-multipart
pip install langchain langchain-community langchain-huggingface
pip install pyngrok


Set Up Hugging Face and ngrok Tokens:

Replace HF_TOKEN in the code with your Hugging Face access token.
Replace NGROK_TOKEN with your ngrok authentication token.
Obtain tokens from:
Hugging Face: https://huggingface.co/settings/tokens
ngrok: https://dashboard.ngrok.com/get-started/your-authtoken




Run the Application:Execute the main script to start both the FastAPI backend and Streamlit frontend:
python main.py

The script will:

Load the fine-tuned model on the GPU.
Start the FastAPI server on port 8000.
Start the Streamlit app on port 8501.
Create ngrok tunnels for public access to both servers.

Output will include public URLs for the FastAPI (/diagnose) and Streamlit interfaces.


Usage

Access the Streamlit Interface:

Open the Streamlit public URL (e.g., https://<ngrok-id>.ngrok-free.app) in a browser.
Enter symptoms or questions in the text area.
Click "Get Diagnosis" to receive a diagnosis and optional reasoning.
Use "Show reasoning" checkbox to view the model's <think> output.
Start a new session or clear the chat history using the provided buttons.


API Usage:

Send a POST request to the FastAPI endpoint (<public_url>/diagnose) with JSON payload:{
  "symptom": "I have a fever and cough.",
  "session_id": "unique-session-id"
}


Response format:{
  "diagnosis": "Possible flu or respiratory infection.",
  "think": "Analyzing symptoms: fever and cough suggest..."
}




Session Management:

Each session is identified by a unique session_id (generated automatically in Streamlit or provided in API requests).
Conversation history is stored in memory for each session, limited to the last 3 turns for context.



How It Works

Input Processing:

User inputs symptoms via the Streamlit interface or FastAPI endpoint.
The session_id ensures context is maintained across interactions.


Prompt Construction:

The langchain pipeline formats the input with conversation history (if any) and the current symptom.
The prompt includes a <think> tag to trigger model reasoning.


Model Inference:

The fine-tuned model (abdulsamad99/medical-fine-tuning) generates a response using 4-bit quantization for efficiency.
Generation parameters: max_new_tokens=450, temperature=0.7, top_p=0.9.


Response Parsing:

Regular expressions extract <think> (reasoning) and <response> (diagnosis) sections from the model's output.
If tags are missing, the entire output is treated as the diagnosis.


Output Delivery:

Streamlit displays the diagnosis and optional reasoning in a conversational format.
FastAPI returns a JSON response with both fields.



Limitations

Educational Use Only: The model is not a substitute for professional medical advice. Diagnoses are generated based on patterns in the training data and may not be accurate.
Session Storage: Conversation history is stored in memory and cleared when the application restarts.
Model Constraints: Limited to 512-token input length and 450-token output length to balance performance and response quality.
Dependency on ngrok: Public URLs depend on ngrok's free tier, which may have limitations or downtime.
GPU Requirement: Requires a CUDA-compatible GPU for model inference.

Future Improvements

Persist session history to a database for durability.
Add support for multi-turn clarification questions to refine diagnoses.
Implement authentication for API access.
Enhance the Streamlit UI with more interactive features (e.g., symptom suggestions, severity sliders).
Fine-tune the model further with a larger medical dataset for improved accuracy.

Contributing
Contributions are welcome! Please:

Fork the repository.
Create a feature branch (git checkout -b feature/your-feature).
Commit changes (git commit -m 'Add your feature').
Push to the branch (git push origin feature/your-feature).
Open a pull request.



Built with unsloth, transformers, and langchain for efficient LLM integration.
Powered by Hugging Face for model hosting and tokenization.
Enabled by ngrok for public deployment.
Inspired by the need for accessible, AI-driven medical assistance tools.
