# 💬 Generative AI Chatbot

A simple yet powerful conversational AI chatbot built with **Streamlit** for the frontend and **LangChain** integrated with **Groq** for fast LLM inference. The chatbot maintains conversational context across multiple turns and provides helpful, low-latency responses powered by Meta's **Llama 3.1 (8B Instant)** model.

---

## 🔍 Overview

This project demonstrates how to build a production-ready conversational chatbot interface using Streamlit's chat components and LangChain's unified LLM interface, with Groq's hardware-accelerated inference engine for blazing-fast responses.

The chatbot is designed to be:
- **Lightweight** – Single-file implementation under 60 lines of code.
- **Stateless from the server's perspective** – All conversation state is held client-side using Streamlit's `session_state`.
- **Customizable** – Easy to swap models, tweak temperature, or modify the system prompt.

---

## ✨ Features

- 💬 **Interactive Chat UI** – Clean, centered chat interface with message history.
- 🤖 **Llama 3.1 (8B) via Groq** – High-speed inference powered by Groq's LPU™ technology.
- 🧠 **Conversation Memory** – Retains the full chat history during a session for contextual replies.
- 🔐 **Environment-based API Key Management** – Securely stores secrets using `.env` files.
- ⚙️ **Low Temperature (0.1)** – Produces focused, deterministic responses.
- 🎨 **Streamlit Native Components** – Uses `st.chat_message` and `st.chat_input` for a modern chat experience.

---

## 🛠 Tech Stack

| Tool | Purpose |
|------|---------|
| [Streamlit](https://streamlit.io/) | Frontend web UI framework |
| [LangChain](https://www.langchain.com/) | LLM orchestration and prompt handling |
| [LangChain-Groq](https://python.langchain.com/docs/integrations/chat/groq) | Groq integration for LangChain |
| [Groq API](https://groq.com/) | Fast LLM inference (Llama 3.1 8B Instant) |
| [python-dotenv](https://pypi.org/project/python-dotenv/) | Loads environment variables from `.env` |

---

## 📁 Project Structure

```
genai_chatbot_streamlit/
│
├── chatbot.py              # Main Streamlit application (single-file app)
├── requirements.txt        # Python dependencies
├── env_template.txt        # Template for the .env file
├── .gitignore              # Files/folders to exclude from Git
├── LICENSE                 # MIT License
└── README.md               # Project documentation
```

---

## ✅ Prerequisites

Before you begin, make sure you have the following:

- **Python 3.9+** installed on your machine.
- A **Groq API key** – Get one for free at [https://console.groq.com](https://console.groq.com).
- A working internet connection (for API calls to Groq).

---

## 📥 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/asharali31/genai-chatbot-streamlit.git
cd genai-chatbot-streamlit
```

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv venv

# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## ⚙️ Configuration

### 1. Create a `.env` file

Copy the contents of `env_template.txt` into a new file named `.env` in the project's root directory:

```bash
cp env_template.txt .env
```

### 2. Add Your Groq API Key

Open the `.env` file and replace the placeholder with your actual Groq API key:

```env
GROQ_API_KEY="your_groq_api_key_here"
```

> ⚠️ **Important:** Never commit your `.env` file or expose your API key publicly. The included `.gitignore` already excludes `.env` from version control.

---

## 🚀 Usage

To start the chatbot application, run:

```bash
streamlit run chatbot.py
```

The app will open in your default browser at:

```
http://localhost:8501
```

Type any message into the input box and press **Enter** to chat with the assistant.

---

## 🧩 How It Works

1. **Streamlit starts** and configures the page (title, icon, layout).
2. **Chat history** is initialized in `st.session_state` if not already present.
3. **Previous messages** are rendered using `st.chat_message`.
4. **User input** is captured via `st.chat_input`.
5. The user message is **appended to history** and displayed.
6. A **LangChain `ChatGroq` instance** is invoked with the system prompt + entire chat history.
7. The **assistant's response** is appended to history and displayed.
8. The cycle repeats — the model sees the full conversation on every turn.

---

## 🎨 Customization

You can easily tweak the chatbot's behavior by editing `chatbot.py`:

| What to change | How |
|----------------|-----|
| **Model** | Change `model="llama-3.1-8b-instant"` to another Groq-supported model (e.g., `llama-3.3-70b-versatile`). |
| **Creativity** | Increase `temperature` (0.0–1.0) for more creative/random responses. |
| **System prompt** | Edit the `"You're a helpful assistant."` string to give the bot a persona (e.g., *"You are a Python expert tutor."*). |
| **UI layout** | Change `layout="centered"` to `"wide"`. |
| **Page title/icon** | Modify `page_title` and `page_icon`. |

---

## 🛠 Troubleshooting

<details>
<summary><b>Error: <code>GROQ_API_KEY not found</code></b></summary>

Make sure your `.env` file exists in the same directory as `chatbot.py` and contains a valid key. Restart the Streamlit server after editing the file.

</details>

<details>
<summary><b>Error: <code>ModuleNotFoundError: No module named 'streamlit'</code></b></summary>

You haven't installed the dependencies. Run:
```bash
pip install -r requirements.txt
```

</details>

<details>
<summary><b>Slow responses</b></summary>

- Verify your internet connection.
- Check Groq's status page: [https://status.groq.com](https://status.groq.com).
- Try a smaller/faster model like `llama-3.1-8b-instant`.

</details>

---

## 🚧 Future Enhancements

- 🔄 **Streaming responses** with `st.write_stream` for real-time token display.
- 🧹 **Clear chat button** to reset conversation history.
- 📂 **Export chat history** to JSON or Markdown.
- 🎭 **Multiple personas** selectable from a sidebar.
- 📚 **RAG (Retrieval-Augmented Generation)** integration for document Q&A.
- 🔐 **Authentication** for multi-user deployments.
- ☁️ **Deploy** to Streamlit Cloud, Hugging Face Spaces, or AWS.

---

## 📄 License

This project is open-source and available under the **MIT License**. See the [LICENSE](LICENSE) file for the full license text.

---

## 🙌 Acknowledgments

- [Streamlit](https://streamlit.io/) for the beautiful UI framework.
- [LangChain](https://www.langchain.com/) for the elegant LLM abstraction.
- [Groq](https://groq.com/) for ultra-fast LLM inference.
- Meta's [Llama 3.1](https://llama.meta.com/) for the underlying model.

---

> 💡 **Tip:** This is a great starter template — extend it with RAG, agents, or function calling to build more advanced AI applications.
