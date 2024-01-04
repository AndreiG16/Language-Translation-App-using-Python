# Language-Translation-App-using-Python

// This is a language translation app that translates from English to German, French and Romanian.

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
