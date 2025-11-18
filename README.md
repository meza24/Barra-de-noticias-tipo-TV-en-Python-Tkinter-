Aquí tienes todo el contenido listo para pegar directamente en tu `README.md`:

````markdown
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
````

---

## 📂 Estructura del proyecto

```text
barra-noticias/
├── scroll.py      # Script principal con la barra de noticias
└── README.md      # Documentación del proyecto
```

---

## 🚀 Uso

1. Clona el repositorio o descarga los archivos:

```bash
git clone https://github.com/USUARIO/barra-noticias.git
cd barra-noticias
```

2. Ejecuta el script:

```bash
python3 scroll.py
```

La barra aparecerá en la parte inferior de la pantalla, centrada horizontalmente.

Para cerrar la barra, puedes usar `Ctrl + C` en la terminal desde donde la ejecutaste o matar el proceso de Python.

---

## 🧪 Código principal (`scroll.py`)

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

---

## 💡 Ideas de uso

* Mostrar recordatorios personales (tareas, exámenes, entregas).
* Simular tickers de noticias en presentaciones.
* Dashboard casero tipo “sala de control”.
* Visual para proyectos de domótica o monitores de sistema.
* Demostraciones en clases de programación o interfaces gráficas.

---

## 📜 Licencia

Este proyecto puede liberarse, por ejemplo, bajo la licencia **MIT**:

```text
MIT License

Copyright (c) 2025 TU_NOMBRE

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

(… resto del texto estándar de la licencia MIT …)
```

```
```
