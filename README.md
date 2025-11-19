# AI Voice Chatbot 🤖

An intelligent conversational chatbot built with Streamlit that supports voice interactions using OpenAI's Whisper (speech-to-text) and TTS (text-to-speech) models. The chatbot features two operational modes: a base AI interviewer and a PDF-based question-answering system using RAG (Retrieval Augmented Generation).

## Features

- 🎤 **Voice Input**: Record audio directly in the browser using the audio recorder
- 🔊 **Voice Output**: Automatic text-to-speech responses with natural-sounding voices
- 💬 **Chat Interface**: Clean and intuitive Streamlit chat interface
- 🔐 **Password Authentication**: Secure access with username/password authentication
- 🤖 **AI Interviewer Mode**: Conducts AI-related and behavioral interviews with adaptive follow-up questions
- 📚 **PDF Chat Mode**: Ask questions about your PDF documents using vector embeddings and semantic search
- 💾 **Conversation Memory**: Maintains chat history throughout the session

## Technologies Used

- **Frontend**: Streamlit
- **Speech-to-Text**: OpenAI Whisper API
- **Text-to-Speech**: OpenAI TTS API
- **LLM**: OpenAI GPT-3.5-turbo
- **Document Processing**: LangChain, PyPDF, Chroma (vector database)
- **Embeddings**: OpenAI Embeddings
- **Audio Recording**: audio-recorder-streamlit
- **UI Components**: streamlit-float

## Prerequisites

- Python 3.8+
- OpenAI API key
- PDF documents (optional, for PDF chat mode)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd AI-Voice-Chatbot
```

2. Install required dependencies:
```bash
pip install -r requirements.txt
```

Required packages:
- streamlit
- openai
- python-dotenv
- langchain
- langchain-community
- chromadb
- pypdf
- audio-recorder-streamlit
- streamlit-float

3. Create a `.env` file in the project root and add your OpenAI API key:
```
OPENAI_API_KEY=your_api_key_here
```

4. Create a `.streamlit/secrets.toml` file for authentication:
```toml
[passwords]
username1 = "password1"
username2 = "password2"
```

5. (Optional) For PDF chat mode, create a `docs/` folder and add your PDF files:
```bash
mkdir docs
# Add your PDF files to the docs/ folder
```

## Usage

### Running the Application

**Base Model (AI Interviewer):**
```bash
streamlit run app.py
```

**PDF Chat Mode:**
Edit `app.py` line 115 to use `pdf_chat` mode:
```python
main(answer_mode='pdf_chat')
```

Then run:
```bash
streamlit run app.py
```

### Using the Chatbot

1. Log in with your credentials
2. Click the microphone button to record your question
3. Wait for transcription and AI response
4. Listen to the audio response automatically
5. Continue the conversation naturally

## Project Structure

```
AI-Voice-Chatbot/
├── app.py                  # Main Streamlit application
├── generate_answer.py      # LLM response generation and PDF processing
├── helpers.py             # Speech-to-text and text-to-speech utilities
├── README.md              # Project documentation
├── .env                   # Environment variables (not in repo)
├── .streamlit/
│   └── secrets.toml       # Authentication credentials (not in repo)
└── docs/                  # PDF documents for RAG (optional)
    └── *.pdf
```

## How It Works

### Base Model Mode
- Uses GPT-3.5-turbo as an AI interviewer
- Evaluates candidate responses for AI-related and behavioral questions
- Provides constructive feedback and adaptive follow-up questions

### PDF Chat Mode
- Loads PDF documents from the `docs/` directory
- Splits documents into chunks and creates vector embeddings
- Uses Chroma vector database for semantic search
- Retrieves relevant context and generates accurate answers based on document content
- Maintains conversation history using ConversationBufferMemory

### Voice Processing
- **Speech-to-Text**: Audio recorded in browser → Whisper API → Text transcript
- **Text-to-Speech**: AI response text → OpenAI TTS API → Audio playback

## Configuration

### Answer Modes
- `base_model`: AI interviewer chatbot
- `pdf_chat`: Document-based Q&A system

Change the mode in `app.py` (line 115):
```python
main(answer_mode='base_model')  # or 'pdf_chat'
```

## Security Notes

- Never commit `.env` or `.streamlit/secrets.toml` files
- Use environment variables for sensitive information
- The app uses `hmac.compare_digest()` for secure password comparison
- Temporary audio files are deleted after processing

## Limitations

- Requires active internet connection for OpenAI API calls
- API usage incurs costs based on OpenAI's pricing
- PDF chat mode requires documents to be in the `docs/` folder
- Session state is cleared when the app restarts

## Future Enhancements

- [ ] Support for multiple answer modes in the UI
- [ ] File upload functionality for PDF documents
- [ ] Conversation export feature
- [ ] Multi-language support
- [ ] Custom system prompts
- [ ] Voice selection in UI


