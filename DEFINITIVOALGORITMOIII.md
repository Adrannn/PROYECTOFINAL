import tkinter as tk
from tkinter import filedialog
from tkinter import scrolledtext
from tkinter import messagebox
from tkinter import Menu

# Variables globales
current_file = None

def open_file():
    
    #Abre un cuadro de diálogo para seleccionar y cargar un archivo de texto en el área de texto.
    
    global current_file
    file_path = filedialog.askopenfilename(filetypes=[("Archivos de texto", "*.txt *.cpp *.cs *.py")])
    if file_path:
        current_file = file_path
        with open(file_path, 'r') as file:
            text.delete(1.0, tk.END)
            text.insert(tk.END, file.read())

def save_file():

   ## Guarda el contenido del área de texto en el archivo actual si está definido.
    
    global current_file
    if current_file:
        with open(current_file, 'w') as file:
            file.write(text.get(1.0, tk.END))

def save_file_as():
    
    #Abre un cuadro de diálogo para seleccionar la ubicación y nombre del archivo y guarda el contenido del área de texto.
    
    file_path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Archivos de texto", "*.txt")])
    if file_path:
        global current_file
        current_file = file_path
        with open(file_path, 'w') as file:
            file.write(text.get(1.0, tk.END))

def show_information():
    
   # Muestra una ventana de información sobre el programa.
    
    messagebox.showinfo("Información", "Este código crea una aplicación básica de editor de texto con una interfaz gráfica que permite abrir, guardar y editar archivos de texto. Adicionalmente, proporciona opciones de ayuda e información sobre el programa y admite archivos con extensiones (.txt, .cpp, .cs, .py, etc).")

def open_user_manual():
    
   # Abre un enlace web al manual de usuario.
    
    import webbrowser
    webbrowser.open("https://drive.google.com/file/d/16EUb3ArG2e5YfzAjQCfK2ZDUzJPkSIQl/view?usp=sharing")

def show_integrantes():
    
    #Muestra una ventana con información sobre los integrantes del grupo.
    
    messagebox.showinfo("Integrantes", "Julio Bernabe Natareno Gonzalez\nCarnet: 7690-23-10455\n\nAdrian Emiliano Atz Fuenes\nCarnet: 7690-23-17154\n\nGrupo no. 8")

def undo():
    
    #Deshace la última acción realizada en el área de texto.
    
    text.edit_undo()

def redo():
    
   # Rehace la última acción deshecha en el área de texto.
    
    text.edit_redo()

# Ventana principal
root = tk.Tk()
root.title("Editor de Texto")

# Crear el menú
menu = Menu(root)
root.config(menu=menu)

# Menú Archivo
file_menu = Menu(menu)
menu.add_cascade(label="Archivo", menu=file_menu)
file_menu.add_command(label="Abrir", command=open_file)
file_menu.add_command(label="Guardar", command=save_file)
file_menu.add_command(label="Guardar como...", command=save_file_as)
file_menu.add_separator()
file_menu.add_command(label="Salir", command=root.quit)

# Menú Editar
edit_menu = Menu(menu)
menu.add_cascade(label="Editar", menu=edit_menu)
edit_menu.add_command(label="Deshacer", command=undo)
edit_menu.add_command(label="Rehacer", command=redo)

# Menú Ayuda
help_menu = Menu(menu)
menu.add_cascade(label="Ayuda", menu=help_menu)
help_menu.add_command(label="Información", command=show_information)
help_menu.add_command(label="Manual de usuario", command=open_user_manual)
help_menu.add_command(label="Integrantes", command=show_integrantes)

# Área de texto para escribir
text = scrolledtext.ScrolledText(root, wrap=tk.WORD, undo=True)
text.pack(expand=True, fill='both')

# Ejecutar la aplicación
root.mainloop()
