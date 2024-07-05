# imagegpt
Create a desktop application that combines image processing (OCR using Tesseract), GUI development (PyQt5), and AI-powered text generation (using OpenAI's GPT-3).

### Imports:
- ```sys```: Provides access to system-specific parameters and functions.
- ```openai```: API library for interfacing with OpenAI's models.
- ```qtmodern.styles```, qtmodern.windows: Styling library and window components for ```PyQt5```.
- ```QApplication, QMainWindow, QLabel, QPushButton, QTextEdit, QVBoxLayout, QWidget, QLineEdit```: ```PyQt5``` components for building GUI applications.
- ```pytesseract```: Python wrapper for ```Google's Tesseract-OCR Engine```.
- ```QtCore, QtGui, QtWidgets```: Core ```PyQt5``` modules for handling GUI.
- ```Image```: From PIL (Python Imaging Library), used for image manipulation.
- ```ImageGrab```: Part of PIL, facilitates grabbing screenshots.
- ```os```: Provides functions for interacting with the operating system.

### Setting up OpenAI API Key and Tesseract Path:
- Sets the OpenAI API key for accessing GPT-3.
- Defines the default image path (```imfilepath```).
- Configures Tesseract OCR path (```pytesseract.pytesseract.tesseract_cmd```).
```python
openai.api_key = 'openai_api_key'
imfilepath = 'img_path'
try:
    pytesseract.pytesseract.tesseract_cmd = ('tesseract_path')
except Exception as e:
    print(e)
```
### ```SnippingWidget``` Class:
- ```SnippingWidget``` is a ```PyQt5``` window used for capturing a screen region (snip) using mouse events.
- It allows the user to define a rectangular region on the screen.
- Upon releasing the mouse, it captures the region as an image using ```ImageGrab```, saves it as ```"ocr.png"```, and emits a closed signal.

### ```ChatGPTApp``` Class:
- ```ChatGPTApp``` is the main application class using PyQt5.
- It sets up the GUI window with a text input ```(QLineEdit)```, a submit button ```(QPushButton)```, and a response label ```(QLabel).```
- The ```topMenu``` method creates a menu bar with options for ```saving files, capturing a screen snip (Snip), and activating automation```.
- It connects the ```SnippingWidget (snipAct.triggered.connect(self.activateSnipping))``` for capturing screen regions.
- ```on_click``` method extracts text from an image using Tesseract OCR when the input text button is clicked.
- ```get_chatgpt_response``` method generates a response using OpenAI's GPT-3 based on user input.
- ```display_response``` method updates the GUI with the generated response.
- Handles file cleanup ```(os.remove('ocr.png'))``` upon application exit or error.
### Application Entry Point

- Initializes the PyQt5 application ```(QApplication)```.
- Applies a dark theme ```(qtmodern.styles.dark(app))```.
- Creates and shows an instance of ChatGPTApp.
- Utilizes ```qtmodern.windows.ModernWindow``` for modern window styling.
- Executes the PyQt5 application ```(app.exec_())```.
