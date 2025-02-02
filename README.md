# deepseek-r1-interface
## preparation for running the program
🤖 Deploy DeepSeek R1 Model with Google Colab (Using Ollama) + Simple Web Chatbot

💻 Google Colab Specifications
- Use GPU T4 runtime

🗒️ Requirements
- Ollama (make the model run)
- Streamlite (makes the web UI run)
- Ngrok (for tunneling the web port, so it can be public)
### 1. Install Ollama to run the model
```
!curl -fsSL https://ollama.com/install.sh | sh
```

### 2. Run Ollama as background service
```
import subprocess

process = subprocess.Popen(['ollama', 'serve'], stdout=subprocess.PIPE, stderr=subprocess.PIPE)
print(f"Ollama serve process ID: {process.pid}")
```

### 3. Pull the deepseek-r1:7b model from the Ollama repository
```
!ollama pull deepseek-r1:7b
```

### 4. Install the library for the website
```
!pip install -U langchain langchain-community
!pip install streamlit
!pip install ollama
!pip install prompt-template
!pip install langchain
!pip install langchain_experimental
!pip install sentence-transformers
!pip install pyngrok
```

### 5. Download the code for the web UI
```
!curl -X GET https://raw.githubusercontent.com/DimasF12/deepseek-r1-interface/refs/heads/main/chat.py -o chat.py
```

### 6. Save the Ngrok auth token so that the Ngrok can be used
Auth tokens can be obtained by signing up on the website -> https://ngrok.com
```
!ngrok authtoken xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### 7. Run the website using Streamlit + Ngrok
```
from pyngrok import ngrok

port = 8501

public_url = ngrok.connect(port)
print(f"Akses website nya disini -> {public_url}\n\n")

!streamlit run chat.py --server.port 8501 --server.enableCORS false
```
