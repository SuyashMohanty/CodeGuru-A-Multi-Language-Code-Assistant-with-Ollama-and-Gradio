# 🤖 CodeGuru: A Multi-Language Code Assistant with Ollama and Gradio

**CodeGuru** is a versatile, conversational AI code assistant designed to help with a wide range of programming questions. This project leverages a custom-built model named **`codeguru`** (based on Codellama) and serves it locally using **Ollama**. The user interface is a clean and simple web application built with **Gradio**, allowing for easy interaction with the model.

---
## ✨ Features

* **Custom Local LLM**: Utilizes a custom model named `codeguru` built from Codellama, tailored to act as a code teaching assistant.
* **Powered by Ollama**: The model is served locally via Ollama, making it easy to run and manage without relying on external cloud APIs.
* **Conversational Memory**: Maintains a history of the conversation, allowing the model to have context from previous prompts.
* **Simple Web Interface**: A user-friendly UI created with Gradio for easy interaction.
* **Multi-Language Support**: Capable of answering questions about various programming languages, thanks to the underlying Codellama model.

---
## ⚙️ How it Works

The application operates with a straightforward architecture:

1.  **Ollama Backend**:
    * An Ollama instance must be running locally.
    * The `codeguru` model, created from the provided `modelfile`, is served by Ollama at a local endpoint (`http://localhost:11434/api/generate`).
2.  **Gradio Frontend**:
    * The `app.py` script launches a Gradio web interface with a textbox for input and an area for text output.
3.  **User Interaction**:
    * A user enters a programming-related question into the Gradio textbox.
    * The `generate_response` function in `app.py` takes the user's prompt.
4.  **API Request and Response**:
    * The user's prompt is appended to a `history` list to maintain conversation context.
    * A POST request is sent to the Ollama API endpoint with the model name (`codeguru`) and the full conversation history as the prompt.
    * Ollama processes the prompt with the `codeguru` model and generates a response.
    * The script parses the JSON response to extract the answer and displays it in the Gradio UI.

---
## 📋 Requirements

* Python 3.x
* Ollama installed and running.
* The `codeguru` model created in Ollama.
* Required Python libraries: `requests`, `gradio`.

---
## 🛠️ Setup & Installation

1.  **Install Ollama**:
    * Follow the official instructions to [install Ollama](https://ollama.com/) on your system.

2.  **Create the `codeguru` Model**:
    * Create a file named `modelfile` with the content you provided:
        ```modelfile
        FROM codellama

        ## Set the Temperature
        PARAMETER temperature 1

        ## set system prompt
        SYSTEM """
        You are a code teaching assistant named as CodeGuru created by Suyash.
        Answer all the code realted questions being asked.
        """
        ```
    * Run the following command in your terminal to create the model in Ollama:
        ```bash
        ollama create codeguru -f ./modelfile
        ```
    * Verify the model is running by executing `ollama run codeguru` in your terminal.

3.  **Clone the repository or download the `app.py` script.**

4.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

5.  **Install the required Python libraries:**
    ```bash
    pip install requests gradio
    ```

---
## ▶️ Usage

1.  **Start the Ollama Service**:
    * Ensure the Ollama service is running in the background. Typically, it starts automatically after installation.

2.  **Run the Gradio App**:
    * Open your terminal in the project's root directory.
    * Execute the `app.py` script:
        ```bash
        python app.py
        ```
    * This will launch the Gradio web interface, usually accessible at `http://127.0.0.1:7860`. The URL will be displayed in your terminal.

3.  **Ask Questions**:
    * Open the URL in your web browser.
    * Type your programming questions into the input box and see the `CodeGuru` assistant respond.

---