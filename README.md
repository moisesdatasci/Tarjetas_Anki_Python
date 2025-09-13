# 📚 Crear Tarjetas de Anki con Python y Genanki

Este repositorio muestra cómo generar **mazos de Anki (`.apkg`)** de forma programática usando **Python** y la librería [`genanki`](https://github.com/kerrickstaley/genanki).

El ejemplo práctico incluye **tarjetas sobre Pandas (Python)**, pero puedes adaptarlo a cualquier tema: NumPy, Django, SQL, etc.

## 🚀 Requisitos

- Python 3.8+
- [pip](https://pip.pypa.io/en/stable/)

Instalar la librería:

```bash
pip install genanki
```

## 📂 Estructura del proyecto

```
.
├── pandas_anki.py   # Script para generar el mazo
├── README.md        # Instrucciones
└── requirements.txt # Dependencias del proyecto
```

## ✨ Ejemplo de Tarjetas

Cada tarjeta tiene un formato de 3 partes:

- **Conceptos** → Preguntas teóricas
- **Comandos** → Sintaxis básica  
- **Ejemplos** → Casos prácticos

```python
# --- CONCEPTOS ---
("¿Qué hace la función df.head() en Pandas?",
 "Muestra las primeras filas de un DataFrame.",
 "concepto"),

# --- COMANDOS ---
("Comando: ¿Cómo leer un archivo CSV en Pandas?",
 "pd.read_csv('archivo.csv')",
 "comando"),

# --- EJEMPLOS ---
("Ejemplo: ¿Cómo calcular la media de una columna 'edad'?",
 "df['edad'].mean()",
 "ejemplo"),
```

## 🛠 Script de ejemplo (`pandas_anki.py`)

```python
import genanki

# Definir el modelo de tarjeta
modelo = genanki.Model(
    1607392319,
    'Modelo Básico',
    fields=[{'name': 'Pregunta'}, {'name': 'Respuesta'}, {'name': 'Etiqueta'}],
    templates=[
        {
            'name': 'Tarjeta Básica',
            'qfmt': '<b>{{Pregunta}}</b>',
            'afmt': '{{FrontSide}}<hr id="answer">{{Respuesta}}<br><br><i>{{Etiqueta}}</i>',
        },
    ])

# Crear el mazo
mazo = genanki.Deck(
    2059400110,
    'Pandas - Conceptos, Comandos y Ejemplos'
)

# Lista de tarjetas
tarjetas = [
    # --- CONCEPTOS ---
    ("¿Qué hace la función df.head() en Pandas?",
     "Muestra las primeras filas de un DataFrame.",
     "concepto"),

    ("¿Qué hace df.tail() en Pandas?",
     "Muestra las últimas filas de un DataFrame.",
     "concepto"),

    ("¿Qué hace df.info() en Pandas?",
     "Muestra información sobre el DataFrame, como tipos de datos y valores nulos.",
     "concepto"),

    ("¿Qué hace df.describe() en Pandas?",
     "Devuelve estadísticas descriptivas de las columnas numéricas.",
     "concepto"),

    # --- COMANDOS ---
    ("Comando: ¿Cómo leer un archivo CSV en Pandas?",
     "pd.read_csv('archivo.csv')",
     "comando"),

    ("Comando: ¿Cómo mostrar las primeras 5 filas de un DataFrame?",
     "df.head()",
     "comando"),

    ("Comando: ¿Cómo seleccionar una columna llamada 'edad'?",
     "df['edad']",
     "comando"),

    ("Comando: ¿Cómo seleccionar varias columnas 'edad' y 'nombre'?",
     "df[['edad','nombre']]",
     "comando"),

    # --- EJEMPLOS ---
    ("Ejemplo: ¿Cómo calcular la media de una columna 'edad'?",
     "df['edad'].mean()",
     "ejemplo"),

    ("Ejemplo: ¿Cómo calcular la suma de la columna 'ventas'?",
     "df['ventas'].sum()",
     "ejemplo"),

    ("Ejemplo: ¿Cómo ordenar un DataFrame por la columna 'precio'?",
     "df.sort_values('precio')",
     "ejemplo"),

    ("Ejemplo: ¿Cómo contar valores únicos en la columna 'ciudad'?",
     "df['ciudad'].value_counts()",
     "ejemplo"),
]

# Agregar tarjetas al mazo
for pregunta, respuesta, etiqueta in tarjetas:
    nota = genanki.Note(
        model=modelo,
        fields=[pregunta, respuesta, etiqueta]
    )
    mazo.add_note(nota)

# Exportar el archivo .apkg
genanki.Package(mazo).write_to_file('Pandas_Anki.apkg')
print("✅ Archivo 'Pandas_Anki.apkg' generado correctamente.")
```

## ▶️ Cómo ejecutar

1. Clona este repositorio o descarga los archivos
2. Ejecuta el script:
   ```bash
   python pandas_anki.py
   ```
3. Se generará un archivo: `Pandas_Anki.apkg`
4. Importa ese archivo en la aplicación de Anki y ¡listo!

## 📌 Personalización

- Cambia el nombre del mazo en:
  ```python
  mazo = genanki.Deck(2059400110, 'Mi Nuevo Mazo')
  ```
- Agrega más tarjetas en la lista `tarjetas`
- Puedes crear carpetas por tema (Pandas, NumPy, Django) y scripts separados

## 📖 Recursos

- [Documentación oficial de Anki](https://docs.ankiweb.net/)
- [Repositorio de genanki](https://github.com/kerrickstaley/genanki)
- [Pandas en la documentación de Python](https://pandas.pydata.org/docs/)

## ✍️ Contribuciones

Las contribuciones son bienvenidas. Si tienes ideas para mejorar este proyecto:

1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/nueva-caracteristica`)
3. Commit tus cambios (`git commit -am 'Agregar nueva característica'`)
4. Push a la rama (`git push origin feature/nueva-caracteristica`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

## ⭐ ¿Te gustó el proyecto?

Si te sirve este proyecto, ¡dale una ⭐ en GitHub!
