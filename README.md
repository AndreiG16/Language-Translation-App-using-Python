# Language-Translation-App-using-Python

This is a language translation app that translates from English to German, French and Romanian.

# Install necessary libraries
!pip install torch torchvision torchaudio
!pip install transformers ipywidgets g r a d i o --upgrade
!pip install sentencepiece
!pip install sacremoses

# Import required libraries
import gradio as gr
from transformers import pipeline

# Define translation pipelines for different languages
translation_pipelines = {
    "German": pipeline(task="translation", model="Helsinki-NLP/opus-mt-en-de"),
    "French": pipeline(task="translation", model="Helsinki-NLP/opus-mt-en-fr"),
    "Romanian": pipeline(task="translation", model="Helsinki-NLP/opus-mt-en-ro"),
}

# Define functions for translation to German, French, and Romanian
def translate_to_german(text):
    try:
        return translation_pipelines["German"](text)[0]['translation_text']
    except Exception as e:
        return f"Error during translation: {str(e)}"

def translate_to_french(text):
    try:
        return translation_pipelines["French"](text)[0]['translation_text']
    except Exception as e:
        return f"Error during translation: {str(e)}"

def translate_to_romanian(text):
    try:
        return translation_pipelines["Romanian"](text)[0]['translation_text']
    except Exception as e:
        return f"Error during translation: {str(e)}"

# Define a general translation function based on target language
def translate_transformers(text, target_language):
    if target_language == "German":
        return translate_to_german(text)
    elif target_language == "French":
        return translate_to_french(text)
    elif target_language == "Romanian":
        return translate_to_romanian(text)
    else:
        return "Invalid target language"

# Define supported languages for the UI dropdown
languages = [("German", "German"), ("French", "French"), ("Romanian", "Romanian")]

# Create the Gradio interface
interface = gr.Interface(
    fn=translate_transformers,
    inputs=[gr.Textbox(lines=2, placeholder='Text to translate'), gr.Dropdown(languages, label="Target Language")],
    outputs=gr.Textbox(),  # Use Gradio Textbox for output
    live=True,
    title='Language Translation App',
    description='Translate text from English to the selected language.'
)

# Launch the Gradio interface
interface.launch()

// Explanation of the code:

1. Library Installations: Installs the required libraries (torch, torchvision, torchaudio, transformers, ipywidgets, gradio, sentencepiece, sacremoses) using the pip install command.
2. Library Imports: Imports necessary libraries including Gradio for creating the user interface and Transformers for translation pipelines.
3. Translation Pipelines: Defines translation pipelines for German, French, and Romanian using the Hugging Face Transformers library.
4. Translation Functions: Defines functions (translate_to_german, translate_to_french, translate_to_romanian) to handle translations for specific languages.
5. General Translation Function: Defines a general translation function (translate_transformers) that takes text and a target language as input and selects the appropriate translation function based on the target language.
6. Supported Languages: Defines a list of supported languages for the UI dropdown.
7. Gradio Interface: Creates a Gradio interface with a textbox for input text, a dropdown for selecting the target language, and a textbox for displaying the translated text. The interface is launched using interface.launch().

This script sets up a simple language translation web application where users can input text in English and choose a target language for translation using a dropdown menu. The translated text is then displayed on the web page.
