# PDF Text Extractor

PDF Text Extractor is a simple GUI application built with Python's `tkinter` and `PyPDF2` libraries. It allows users to select a PDF file and extract the text content from it, displaying the extracted text in a text widget.

## Features

- Select and open a PDF file.
- Extract and display text content from the selected PDF file.
- User-friendly interface with error handling.

## Requirements

- Python 3.x
- `tkinter` (usually comes with Python standard library)
- `PyPDF2` library

## Installation

1. **Clone the repository:**

    ```sh
    git clone https://github.com/thenameissushant/pdf-text-extractor.git
    cd pdf-text-extractor
    ```

2. **Install the required libraries:**

    ```sh
    pip install PyPDF2
    ```

## Usage

1. **Run the script:**

    ```sh
    python pdf_text_extractor.py
    ```

2. **Using the application:**
   - Click on the "Open PDF File" button to open a file dialog.
   - Select a PDF file from your system.
   - The text content of the PDF will be extracted and displayed in the text widget.

## Code Overview

```python
import tkinter as tk
from tkinter import filedialog, messagebox
import PyPDF2

# Create main window
root = tk.Tk()
root.title("PDF Text Extractor")
root.geometry("600x400")  # Set the window size

def openFile():
    # Open file dialog to select PDF file
    filename = filedialog.askopenfilename(title="Open PDF File",
                                          initialdir=r'C:\Users\hp\Downloads',
                                          filetypes=[('PDF Files', '*.pdf')])
    if filename:
        filename_label.config(text=filename)  # Display the selected file name
        
        try:
            # Open and read the PDF file
            with open(filename, 'rb') as file:
                reader = PyPDF2.PdfFileReader(file)
                outputfile_text.delete(1.0, tk.END)  # Clear previous text
                for i in range(reader.getNumPages()):
                    page = reader.getPage(i)
                    current_text = page.extract_text()  # Use extract_text instead of extractText
                    outputfile_text.insert(tk.END, current_text)
        except Exception as e:
            messagebox.showerror("Error", f"Failed to read PDF file:\n{e}")

# Add GUI elements
filename_label = tk.Label(root, text="No File Selected", anchor="w")
outputfile_text = tk.Text(root, wrap='word')
openfile_button = tk.Button(root, text="Open PDF File", command=openFile)

# Layout GUI elements
filename_label.pack(fill='x', padx=5, pady=5)
outputfile_text.pack(expand=True, fill='both', padx=5, pady=5)
openfile_button.pack(pady=5)

# Run the main loop
root.mainloop()


#Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

#License
This project is licensed under the MIT License - see the LICENSE file for details.

#Acknowledgments
-> This project uses the PyPDF2 library for reading PDF files.
-> The GUI is built using Python's built-in tkinter library.


This README file provides an overview of your project, including installation instructions, usage guidelines, a brief code overview, and other relevant information. Feel free to customize it as needed for your specific project and preferences.
