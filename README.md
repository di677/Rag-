# 🤖 RAG Chatbot using n8n

A Retrieval-Augmented Generation (RAG) chatbot built with **n8n**, **OpenAI**, and **Pinecone**. Users can submit documents through a form, which are stored as embeddings in a vector database. A chat agent then answers questions using the knowledge from those documents.

---

## 📸 Workflow Screenshot

![RAG Chatbot Workflow](https://github.com/user-attachments/assets/28e45d05-ac32-4edf-b888-3dfa92bb353e)



---

## 📌 Overview

This project has **two workflows** inside one n8n canvas:

1. **Data Ingestion Flow**: uploads and stores documents in a vector database.
2. **Chatbot Flow**: answers user questions by retrieving relevant data from the vector database.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** | Workflow automation platform |
| **OpenAI Embeddings** | Converts text into vector embeddings |
| **OpenAI Chat Model** | Generates answers (LLM) |
| **Pinecone** | Vector database for storing and searching embeddings |
| **Simple Memory** | Keeps conversation history |

---

## 🔄 Workflow Explanation

### 1️⃣ Data Ingestion Flow (Top Section)

```
On Form Submission → Pinecone Vector Store (Insert)
                        ├── Embeddings OpenAI
                        └── Default Data Loader
```

| Node | Description |
|------|-------------|
| **On form submission** | Trigger. The user uploads a file or text through a form. |
| **Default Data Loader** | Loads and splits the document into chunks. |
| **Embeddings OpenAI** | Converts each chunk into a vector embedding. |
| **Pinecone Vector Store** | Stores the embeddings in the Pinecone index. |

### 2️⃣ Chatbot Flow (Bottom Section)

```
When chat message received → AI Agent
                               ├── Chat Model: OpenAI Chat Model
                               ├── Memory: Simple Memory
                               └── Tool: Answer questions with a vector store
                                          ├── Pinecone Vector Store1
                                          │       └── Embeddings OpenAI1
                                          └── OpenAI Chat Model1
```

| Node | Description |
|------|-------------|
| **When chat message received** | Trigger. Starts when the user sends a chat message. |
| **AI Agent** | Main brain. Decides when to use the tool to answer. |
| **OpenAI Chat Model** | LLM that generates the response. |
| **Simple Memory** | Remembers previous messages in the session. |
| **Answer questions with a vector store** | Tool that retrieves relevant information from Pinecone. |
| **Pinecone Vector Store1** | Searches for the most similar document chunks. |
| **Embeddings OpenAI1** | Converts the user's question into an embedding for searching. |
| **OpenAI Chat Model1** | Uses the retrieved context to form the final answer. |

---

## ⚙️ How It Works

1. 📄 The user submits a document through the form.
2. ✂️ The document is split into chunks.
3. 🔢 Each chunk is converted into embeddings using OpenAI.
4. 💾 The embeddings are stored in Pinecone.
5. 💬 The user asks a question in the chat.
6. 🔍 The question is converted into an embedding and matched with similar chunks in Pinecone.
7. 🧠 The AI Agent uses the retrieved context and the LLM to generate an accurate answer.

---

## 🚀 Setup Instructions

### Prerequisites

- An [n8n](https://n8n.io/) account (cloud or self-hosted)
- An [OpenAI](https://platform.openai.com/) API key
- A [Pinecone](https://www.pinecone.io/) account with an index created

### Steps

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo-name>.git
   ```
2. Open n8n and go to **Workflows → Import from File**.
3. Select the exported workflow `.json` file from this repo.
4. Add your credentials:
   - OpenAI API key
   - Pinecone API key
5. Set your Pinecone **index name** in both Pinecone nodes.
6. Click **Execute workflow** and upload a document through the form.
7. Click **Open chat** and start asking questions.

---

## 💡 Example Usage

**Upload:** a PDF or text document through the form.

**Ask:**
> What is the main topic of the uploaded document?

**Bot:** answers using the content retrieved from your document.

---

## 📁 Project Structure

```
├── README.md
├── RAG Chatbot.json        # Exported n8n workflow
└── screenshots/
    └── workflow.png        # Workflow screenshot
```

---

## 🔮 Future Improvements

- Support for multiple file formats (PDF, DOCX, CSV)
- Deploy the chatbot on a website or WhatsApp / Telegram
- Add source citations to the answers
- Add authentication to the upload form

---

## 👩‍💻 Author

**Your Name**
GitHub: [@your-username](https://github.com/your-username)

---

⭐ If you like this project, give it a star!
