# Laptop Recommendation System

A Flask-based chatbot application that helps users find laptop recommendations using OpenAI's GPT-3.5 model and a local laptop dataset. Users can interact with the assistant through a web chat interface, and the app uses natural language understanding to infer requirements like GPU intensity, display quality, portability, multitasking, processing speed, and budget.

## Features

- Conversational recommendation workflow via a web UI
- OpenAI GPT-3.5 powered dialogue and intent extraction
- User requirement parsing with function-calling and validation
- Laptop matching against local dataset (`laptop_data.csv`)
- Budget-based filtering and scoring logic for top recommendations
- Basic moderation checks for user and assistant responses

## Project Structure

- `app.py` - Flask web application routes, chat flow, and conversation state
- `functions.py` - OpenAI integration, conversation templates, recommendation logic, and laptop feature mapping
- `laptop_data.csv` - Dataset used for laptop filtering and recommendation scoring
- `templates/conversation_bot.html` - HTML chat interface
- `static/css/styles.css` - Page styling for the chatbot UI
- `OpenAI_API_Key.txt` - Local file containing the OpenAI API key
- `requirements.txt` - Python dependencies

## Prerequisites

- Python 3.10+ installed
- Internet access for OpenAI API calls
- OpenAI API key

## Installation

1. Clone or download the repository.
2. In the project root, create a Python environment (recommended):

```bash
python3 -m venv venv
source venv/bin/activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Add your OpenAI API key to `OpenAI_API_Key.txt` in the repository root.

> Important: Do not commit your API key to GitHub. Add `OpenAI_API_Key.txt` to `.gitignore` if you publish the repository.

## Running the App

Start the Flask server from the project root:

```bash
python app.py
```

Open a browser and navigate to:

```text
http://localhost:5001
```

## Usage

- Enter your laptop requirements in the chat box.
- The assistant will ask follow-up questions to understand your needs.
- Once enough information is collected, it will generate recommended laptops.
- Use the `End Chat` button to restart the conversation.

## How It Works

1. `app.py` initializes the conversation and renders the chat interface.
2. User input is sent to the Flask `/conversation` route.
3. The assistant uses OpenAI chat completions to decide whether it has enough information.
4. Once user requirements are extracted, the app calls the function-calling logic in `functions.py`.
5. `compare_laptops_with_user()` filters the local dataset by budget and scores laptops based on matched requirements.
6. Top recommendations are validated and then returned in a conversational response.

## Customization

- `functions.py` contains the prompt templates and recommendation scoring logic.
- `laptop_data.csv` can be updated with new laptops and specifications.
- The chat interface styling is controlled from `static/css/styles.css`.

## Notes

- The app uses GPT-3.5 (`gpt-3.5-turbo`) via the OpenAI Python SDK.
- The recommendation engine relies on the local dataset and may need calibration for new laptop descriptions.
- This repo is best suited for local testing and demo use; production deployment should secure API keys and handle environment variables safely.

## Security

- Keep `OpenAI_API_Key.txt` private.
- Do not commit secret keys to version control.
- Use environment variables or a secure secrets manager for deployed versions.

## Optional `.gitignore`

Create a `.gitignore` file with the following content to keep secrets and temporary files out of Git:

```gitignore
OpenAI_API_Key.txt
__pycache__/
*.pyc
.env
```
