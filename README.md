# BING Scraper

## Descripción

Esta aplicación es una herramienta gráfica desarrollada en Python con la biblioteca `tkinter` para buscar y descargar imágenes automáticamente desde Bing utilizando el módulo `bing-image-downloader`. El programa permite especificar un término de búsqueda y la cantidad de imágenes que se desean descargar.

## Características principales

1. **Interfaz gráfica**: 
   - Campo de entrada para especificar el término de búsqueda.
   - Campo de entrada para definir la cantidad de imágenes a descargar.
   - Botón para iniciar el proceso de descarga.

2. **Uso del módulo `bing-image-downloader`**:
   - Descarga imágenes relacionadas con un término específico.
   - Soporte para desactivar el filtro de contenido adulto.
   - Permite definir un límite máximo de imágenes a descargar.

3. **Mensajes interactivos**:
   - Confirmaciones al completar la descarga.
   - Advertencias en caso de errores o campos incompletos.

### Estructura principal

El programa se divide en las siguientes secciones:

### 1. **Importación de módulos**

```python
import os
import tkinter as tk
from tkinter import ttk, messagebox
from bing_image_downloader import downloader
```

Se importan las bibliotecas necesarias:

- `os`: para operaciones relacionadas con el sistema.
- `tkinter`: para construir la interfaz gráfica.
- `bing-image-downloader`: para descargar imágenes desde Bing.


### 2. **Función de descarga**

```python
def download_images(query, limit=300):
    downloader.download(
        query, 
        limit=limit, 
        output_dir='Downloads', 
        adult_filter_off=True, 
        force_replace=False, 
        timeout=60
    )
```

Esta función utiliza el método `download` del módulo `bing-image-downloader` para buscar y descargar imágenes:

- `query`: término de búsqueda.
- `limit`: número máximo de imágenes a descargar (por defecto 300).
- `output_dir`: carpeta donde se guardarán las imágenes (por defecto `Downloads`).
- `adult_filter_off`: desactiva el filtro de contenido adulto.
- `force_replace`: evita reemplazar imágenes previamente descargadas.
- `timeout`: tiempo máximo de espera para una conexión (en segundos).

### 3. **Gestión de la interacción**

```python
def handle_download():
    query = query_entry.get()
    limit = int(limit_entry.get())
    if query and limit:
        try:
            download_images(query, limit)
            messagebox.showinfo("Éxito", f"Se han descargado {limit} imágenes de '{query}' en la carpeta 'Descargas'")
        except Exception as e:
            messagebox.showerror("Error", f"Error al descargar imágenes: {e}")
    else:
        messagebox.showwarning("Advertencia", "Por favor, completa todos los campos")
```

Esta función valida los campos de entrada y gestiona posibles errores al ejecutar la descarga. También proporciona retroalimentación visual al usuario mediante cuadros de diálogo.

### 4. **Diseño de la interfaz gráfica**

```python
root = tk.Tk()
root.title("BING SCRAPPER")
root.geometry("500x300")
root.configure(bg="#2e2e2e")
```

Se crea una ventana principal con un fondo oscuro y dimensiones fijas.

### Estilo y Widgets

El estilo visual se personaliza usando `ttk.Style`, con configuraciones específicas para botones, etiquetas y campos de entrada.

```python
style = ttk.Style()
style.theme_use("clam")
style.configure("TButton", font=("Helvetica", 12), padding=10, background="#4a4a4a", foreground="#ffffff")
```

Widgets principales:

- Etiquetas (`ttk.Label`) para indicar los campos de entrada.
- Entradas de texto (`ttk.Entry`) para capturar el término de búsqueda y el límite de imágenes.
- Botón (`ttk.Button`) que llama a la función `handle_download` al hacer clic.

## Crear archivo ejecutable .exe

Se debe instalar la siguiente dependencia:

pip install pyinstaller

- Se crea el ejecutable .exe con el siguiente codigo en la consola:

pyinstaller --onefile --windowed bing_scrapper.py

`--onefile:` Empaqueta todo en un único archivo .exe.
`--windowed:` Elimina la consola negra de Python al ejecutar el programa.