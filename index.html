from flask import Flask, render_template, request
import google.generativeai as genai
import os
from datetime import datetime

app = Flask(__name__)

# Configuration for file uploads
UPLOAD_FOLDER = 'static/uploads/'
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER

# Ensure the upload folder exists
if not os.path.exists(UPLOAD_FOLDER):
    os.makedirs(UPLOAD_FOLDER)

# Configure the Google Gemini API
genai.configure(api_key="AIzaSyCz7Ls9eJI1tFTvCeCPntIOmvatsEM4kcU")


def upload_file_to_gemini(file_path):
    """Uploads a file to the Gemini API for analysis."""
    mime_type = None

    # Set mime type for PDF or Word documents
    if file_path.endswith('.pdf'):
        mime_type = 'application/pdf'
    elif file_path.endswith('.doc') or file_path.endswith('.docx'):
        mime_type = 'application/msword'
    else:
        raise ValueError("Unsupported file format. Only PDF and DOC/DOCX are allowed.")

    # Upload the file to Gemini
    file = genai.upload_file(file_path, mime_type=mime_type)
    print(f"Uploaded file '{file.display_name}' as: {file.uri}")
    return file


def analyze_file(file_path):
    """Analyzes a given file using Gemini AI."""
    generation_config = {
        "temperature": 1,
        "top_p": 0.95,
        "top_k": 40,
        "max_output_tokens": 8192,
        "response_mime_type": "text/plain",
    }

    model = genai.GenerativeModel(
        model_name="gemini-1.5-flash-8b",
        generation_config=generation_config,
        system_instruction="You are expert in generating reviews. A user will provide a file ,"
                           " you should analyze it and Generate review and also express personal"
                           " review and compare different perspectives."
    )

    # Upload the file
    uploaded_file = upload_file_to_gemini(file_path)

    # Create a chat session and analyze the file
    chat_session = model.start_chat(
        history=[
            {
                "role": "user",
                "parts": [uploaded_file],
            }
        ]
    )

    response = chat_session.send_message("Please analyze this file and provide feedback.")
    return response.text


@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        # Collect form data
        user_details = {
            'name': request.form['name'],

            'timestamp': datetime.now()
        }

        # Handle file upload
        file = request.files['resume']
        if file:
            file_path = os.path.join(app.config['UPLOAD_FOLDER'], file.filename)
            file.save(file_path)

            # Analyze file using Gemini API
            analysis_result = analyze_file(file_path)

            # Render the results with analysis suggestions
            return render_template('Results.html', suggestions=analysis_result)

    return render_template('index.html')


if __name__ == '__main__':
    app.run(debug=True)
