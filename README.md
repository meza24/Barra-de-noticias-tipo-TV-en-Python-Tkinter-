# Barra de noticias tipo TV en Python (Tkinter)

Este proyecto muestra una **barra de noticias estilo TV** (tipo CNN / BBC / ESPN) en la parte inferior de la pantalla usando **Python y Tkinter**.  
El texto se desplaza horizontalmente (scroll) y la barra se mantiene siempre visible por encima de otras ventanas.

---

## ✨ Características

- Barra de noticias fija en la parte inferior de la pantalla.
- Estilo similar a tickers de noticias de televisión.
- Texto en movimiento (scroll) en bucle.
- Ancho y alto configurables.
- Velocidad del scroll ajustable.
- Fuente, colores y texto totalmente personalizables.
- Funciona en cualquier sistema con Python 3 + Tkinter (Ubuntu, otras distros Linux, Windows, etc.).

---

## 🧩 Requisitos

- Python 3.x
- Tkinter (normalmente viene incluido con Python).

En Ubuntu puedes instalar/asegurarte de tener Tkinter con:

```bash
sudo apt install python3-tk
```

---

## 🚀 Instalación y uso paso a paso

### Paso 1: Crear el archivo del proyecto
Crea una carpeta para el proyecto y dentro de ella el archivo `scroll.py`:

```bash
mkdir barra-noticias
cd barra-noticias
touch scroll.py
```

### Paso 2: Copiar el código
Abre el archivo `scroll.py` con tu editor favorito y pega el siguiente código:

```python
# Comando para ejecutarlo: python3 scroll.py

import tkinter as tk

# =========================
#     CONFIGURACIÓN
# =========================
base_text = " 🔴 ÚLTIMA HORA: Hoy hay examen | Revisa tu correo institucional | Entregar máquinas ⚡ |   "

bar_width = 1500      # Ancho de la barra en píxeles
bar_height = 36       # Altura de la barra en píxeles
font_style = ("Arial", 16, "bold")  # Fuente del texto
scroll_speed = 60     # Velocidad del scroll en milisegundos

# =========================
#     CREAR VENTANA
# =========================
root = tk.Tk()
root.attributes("-topmost", True)
root.overrideredirect(True)  # Sin bordes/controles
root.config(bg="#000000")    # Fondo fuera de la barra

screen_width = root.winfo_screenwidth()
screen_height = root.winfo_screenheight()

# Posición: centrado horizontal y cerca del borde inferior
x_pos = int((screen_width - bar_width) / 2)
y_pos = screen_height - bar_height - 10    # 10 px de margen inferior

root.geometry(f"{bar_width}x{bar_height}+{x_pos}+{y_pos}")

# =========================
#     FRAME CON ESTILO TV
# =========================
frame = tk.Frame(
    root,
    bg="red",
    highlightbackground="black",   # Borde negro fino
    highlightthickness=2
)
frame.place(relwidth=1, relheight=1)

# =========================
#     RELLENAR TEXTO
# =========================
def fill_text_to_width(text, width_px, font=font_style):
    """
    Repite el texto base hasta que su ancho sea mayor
    que el de la barra, para lograr un scroll continuo.
    """
    test = tk.Label(frame, font=font)
    repeated = text
    while True:
        test.config(text=repeated)
        test.update_idletasks()
        if test.winfo_reqwidth() >= width_px * 1.6:
            # 1.6 asegura que el texto sea más largo que la barra para un scroll continuo
            break
        repeated += "   " + text
    return repeated

text = fill_text_to_width(base_text, bar_width)

# =========================
#     LABEL DEL TEXTO
# =========================
label = tk.Label(
    frame,
    text=text,
    fg="white",
    bg="red",
    font=font_style,
    anchor="w",
    padx=20  # Espacio interno tipo barra de noticias
)
label.pack(fill="both", expand=True)

# =========================
#     FUNCIÓN SCROLL
# =========================
def scroll():
    """Desplaza el texto un carácter hacia la izquierda y vuelve a llamar a la función."""
    global text
    text = text[1:] + text[0]
    label.config(text=text)
    label.after(scroll_speed, scroll)

scroll()
root.mainloop()
```

### Paso 3: Ejecutar la aplicación
En la terminal, dentro de la carpeta del proyecto, ejecuta:

```bash
python3 scroll.py
```

O si usas Windows:
```bash
python scroll.py
```

### Paso 4: Cerrar la aplicación
Para cerrar la barra de noticias:
- Presiona `Ctrl + C` en la terminal desde donde la ejecutaste
- O cierra la terminal
- O usa el administrador de tareas para finalizar el proceso de Python

---

## ⚙️ Personalización

Puedes modificar fácilmente estos parámetros al inicio del archivo `scroll.py`:

* `base_text`: texto que se va a mostrar en la barra.

  ```python
  base_text = " 🔵 INFO: Próxima entrega de proyecto | Revisa tu agenda | "
  ```

* `bar_width`: ancho de la barra (en píxeles).

  ```python
  bar_width = 1200
  ```

* `bar_height`: alto de la barra (en píxeles).

  ```python
  bar_height = 30
  ```

* `font_style`: fuente, tamaño y estilo del texto.

  ```python
  font_style = ("DejaVu Sans", 14, "bold")
  ```

* `scroll_speed`: tiempo entre pasos del scroll (en ms).
  Valores más bajos → scroll más rápido.
  Valores más altos → scroll más lento.

  ```python
  scroll_speed = 80
  ```

* **Colores**: Puedes cambiar los colores modificando:
  - `bg="red"` en el Frame (color de fondo de la barra)
  - `fg="white"` en el Label (color del texto)
  - `bg="red"` en el Label (debe coincidir con el del Frame)

---

## 🐛 Solución de problemas

### Error: "No module named 'tkinter'"
**Solución en Ubuntu/Debian:**
```bash
sudo apt update
sudo apt install python3-tk
```

**Solución en Windows:**
- Al instalar Python, asegúrate de marcar la opción "tcl/tk and IDLE"
- O reinstala Python marcando esa opción

### Error: La barra no se ve completa
- Ajusta el `bar_width` según la resolución de tu pantalla
- Para pantallas más pequeñas, usa valores entre 800-1200

### La barra aparece en posición incorrecta
- Verifica la resolución de tu pantalla
- Ajusta las variables `x_pos` y `y_pos` en el código

---

## 💡 Ideas de uso

* Mostrar recordatorios personales (tareas, exámenes, entregas).
* Simular tickers de noticias en presentaciones.
* Dashboard casero tipo "sala de control".
* Visual para proyectos de domótica o monitores de sistema.
* Demostraciones en clases de programación o interfaces gráficas.
* Mostrar información en tiempo real (precios, noticias, clima).

---


## 🔄 Próximos pasos

Una vez que funcione la versión básica, puedes:
1. Modificar el texto y colores según tus necesidades
2. Experimentar con diferentes velocidades de scroll
3. Cambiar la posición en la pantalla
4. Integrar con APIs para mostrar información en tiempo real
