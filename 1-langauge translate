import tkinter as tk
from tkinter import ttk, messagebox
from googletrans import Translator, LANGUAGES

# Initialize the translator
translator = Translator()

# Create the main application window
root = tk.Tk()
root.title("Simple Language Translator")
root.geometry("500x400")

# Function to create a language dropdown
def create_language_dropdown(row, default_lang):
    lang_var = tk.StringVar(value=default_lang)
    combobox = ttk.Combobox(root, textvariable=lang_var, values=list(LANGUAGES.values()))
    combobox.grid(row=row, column=1, pady=10, padx=10, sticky="ew")
    return lang_var

# Create labels for the UI
tk.Label(root, text="Source Language:").grid(row=0, column=0, padx=10, pady=10, sticky="w")
tk.Label(root, text="Target Language:").grid(row=1, column=0, padx=10, pady=10, sticky="w")
tk.Label(root, text="Input Text:").grid(row=2, column=0, padx=10, pady=10, sticky="nw")
tk.Label(root, text="Translation:").grid(row=4, column=0, padx=10, pady=10, sticky="nw")

# Create language dropdowns
source_lang = create_language_dropdown(0, "english")
target_lang = create_language_dropdown(1, "french")

# Create text boxes for input and output
input_text = tk.Text(root, height=5, width=40)
input_text.grid(row=2, column=1, padx=10, pady=10)

output_text = tk.Text(root, height=5, width=40, state="disabled")
output_text.grid(row=4, column=1, padx=10, pady=10)

# Function to translate text
def translate_text():
    try:
        # Get language codes from dropdown selections
        src_lang_code = [k for k, v in LANGUAGES.items() if v.lower() == source_lang.get().lower()][0]
        dest_lang_code = [k for k, v in LANGUAGES.items() if v.lower() == target_lang.get().lower()][0]
        
        # Get the text to translate
        text_to_translate = input_text.get("1.0", tk.END).strip()
        if len(text_to_translate) < 1:
            messagebox.showwarning("Warning", "Please enter text to translate")
            return
            
        # Perform the translation
        translated = translator.translate(text_to_translate, src=src_lang_code, dest=dest_lang_code)
        
        # Display the translated text
        output_text.config(state="normal")
        output_text.delete("1.0", tk.END)
        output_text.insert("1.0", translated.text)
        output_text.config(state="disabled")
    
    except Exception as e:
        messagebox.showerror("Error", f"Translation failed: {str(e)}")

# Create buttons for translation and copying text
translate_btn = tk.Button(root, text="Translate", command=translate_text)
translate_btn.grid(row=3, column=1, pady=10, sticky="e")

copy_btn = tk.Button(root, text="Copy Text", command=lambda: root.clipboard_append(output_text.get("1.0", tk.END)))
copy_btn.grid(row=5, column=1, pady=10, sticky="e")

# Run the application
root.mainloop()
