---
title: "Crea tu propio chatbot con la API de OpenAI y Gradio en Python"
datePublished: Wed Mar 22 2023 19:05:18 GMT+0000 (Coordinated Universal Time)
cuid: clfk215w500010ams7zkvhj3w
slug: crea-tu-propio-chatbot-con-la-api-de-openai-y-gradio-en-python
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/hZkOZGtlA5w/upload/b8b7ca97aff3fe83363c9b90c6177dd9.jpeg
tags: python, openai, gradio, chatgpt

---

Hoy vamos a aprender a crear una aplicación en Python utilizando la API de OpenAI y Gradio. Esta publicación será útil para las personas que quieren aprender a utilizar la API de OpenAI y crear una aplicación con una interfaz de usuario interactiva de forma rapida y sin necesidad de usar HTML, CSS y Javscript.

## Introducción

Antes de empezar, debemos entender qué es la API de OpenAI y Gradio.

[OpenAI](https://openai.com/) es una organización de investigación en inteligencia artificial. Ofrecen una API que permite acceder a modelos de inteligencia artificial avanzados para realizar diversas tareas, como responder preguntas, traducir oraciones, resumir noticias y más.

Por otro lado, [Gradio](https://gradio.app/) es una herramienta de código abierto para crear interfaces de usuario interactivas para modelos de inteligencia artificial. Ofrece una manera fácil y rápida de crear una interfaz de usuario para cualquier modelo de aprendizaje automático.

Ahora que tenemos una comprensión básica de ambas herramientas, comencemos con el tutorial.

## **Conectando a la API de OpenAI**

Para usar la API de OpenAI, necesitamos generar una clave API. Siga estos pasos para obtener su clave API:

1. Visite el sitio web de [OpenAI](https://platform.openai.com/signup) y regístrese para obtener una cuenta gratuita.
    
2. Inicie sesión en su cuenta y vaya a la página de la [API](https://platform.openai.com/account/api-keys).
    
3. Cree una nueva clave API y cópiela porque la usaremos mas adelante.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679435437209/e6cc242a-0f2c-40c8-9759-7711c29f276b.png align="center")
    

## Instalación de dependencias

En este tutorial, crearemos una aplicación de Chatbot utilizando la API de OpenAI y Gradio. Para empezar, necesitamos ubicarnos en la carpeta donde vamos a trabajar nuestro proyecto e instalar ambos paquetes en nuestra máquina. Como un paso previo a la instalación de las dependecias se puede crear un entorno virtual de python para que las librerias no tengan colision con las del sistema:

```bash
python3 -m venv venv
source venv/bin/activate
```

Luego de activar el entorno virtual, procedemos a instalar las dependencias:

```bash
pip install openai
pip install gradio
```

## Configuración de la clave API de OpenAI

Una vez que tengamos ambos paquetes instalados, podemos comenzar a escribir nuestro código.

Primero, debemos configurar la API de OpenAI para poder acceder a sus servicios. Una vez que tengamos la clave API, podemos configurarla en nuestro código de Python creando un archivo llamado `chatbot.py` utilizando el siguiente código.

```python
import openai
import os

# Obtener la clave API de OpenAI de la variable de entorno
openai.api_key = os.environ.get("OPENAI_API_KEY", None)
```

Asegúrate de configurar la variable de entorno `OPENAI_API_KEY` con tu clave API real antes de ejecutar el código, sino en la ultima sección te explico como hacerlo.

Ahora que tenemos la clave API configurada, podemos comenzar a interactuar con la API de OpenAI. En este tutorial, crearemos un chatbot que puede responder a las preguntas de los usuarios.

## Configuración del mensaje por defecto

Para crear un chatbot utilizando la API de OpenAI, necesitamos proporcionar una serie de mensajes como entrada a la API. Cada mensaje es una cadena de texto que representa el mensaje enviado por un usuario o el chatbot. Usaremos un mensaje por defecto para configurar y condicionar las respuesta GPT:

```python
messages = [
    {
        "role": "system",
        "content": "Act like a personal assistant. You can respond to questions, translate sentences, summarize news, and give recommendations."
    }
]
```

En este ejemplo, el chatbot comienza presentándose como un asistente personal y proporcionando una lista de tareas que puede realizar.

## Función de llamada a la API de OpenAI

Una vez que tenemos los mensajes de entrada preparados, podemos enviarlos a la API de OpenAI para generar una respuesta utilizando el siguiente código.

```python

def openai_process_message(user_message):
    # Set the prompt for OpenAI Api
    messages = [
        {
            "role": "system",
            "content": "Act like a personal assistant. You can respond to questions, translate sentences, summarize news, and give recommendations."
        }
    ]
    messages.append({"role": "user", "content": user_message})
    # Call the OpenAI Api to process our prompt
    openai_response = openai.ChatCompletion.create(model="gpt-3.5-turbo", messages=messages, max_tokens=2000)
    # Parse the response to get the response text for our prompt
    response_text = openai_response.choices[0].message.content
    return response_text
```

La función `openai_process_message` toma como entrada el mensaje del usuario y lo agrega a la lista de mensajes como un mensaje de usuario. A continuación, llama a la API de OpenAI para procesar los mensajes y generar una respuesta. Por último, la función devuelve la respuesta generada por la API de OpenAI.

## Creación de la UI con Gradio

A continuación, crearemos una lista de ejemplos que se utilizarán para mostrar ejemplos en la interfaz de usuario. En este caso, utilizaremos preguntas sobre la inteligencia artificial.

```python
examples = [
    "Que es la IA?",
    "Como funciona una red neuronal?",
    "pueden las maquinas aprender?",
]
```

Luego, creamos una instancia de la clase `Interface` de Gradio y le pasamos la función `openai_process_message()` como argumento. A continuación, definimos el tipo de entrada y salida que deseamos para nuestra interfaz. En este caso, utilizaremos una caja de texto para la entrada del usuario y otra para mostrar la respuesta del chatbot.

```python
# Create a Gradio interface instance
demo = gr.Interface(
    fn=openai_process_message,
    inputs=gr.Textbox(lines=5, label='Pregunta',    placeholder='Escribe tu pregunta aquí...'),
    outputs=gr.Textbox(label='Respuesta'),
    examples=examples,
    title="Chatbot OpenAI API",
)
```

Finalmente, lanzamos la interfaz de usuario utilizando el método `launch()`.

```python
if __name__ == "__main__":
    demo.launch()
```

## Corriendo nuestra aplicación

Recuerda que antes de lanzar la aplicación, debes configurar la variable de entorno "OPENAI\_API\_KEY" con tu clave de API de OpenAI. Puedes hacerlo de la siguiente manera en tu terminal:

```bash
export OPENAI_API_KEY=<tu_clave_de_api>
```

Donde &lt;tu\_clave\_de\_api&gt; debe ser reemplazada con tu clave de API real de OpenAI.

Para lanzar la aplicación, puedes simplemente ejecutar el archivo Python en tu terminal o IDE de Python:

```bash
python chatbot.py
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679438402612/e8a57a90-5afd-4d5e-9dfa-a6ef90d6bd3e.png align="center")

Con esto ya tenemos nuestra app corriendo sobre https://127.0.0.1:7860 y con la siguiente UI de forma facil y rapida:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679438572766/7cba6334-d1b2-43bb-b34c-4c60369c4151.png align="center")

## Conclusiones

Ahora tenemos una aplicación completa de preguntas y respuestas que utiliza la API de OpenAI para generar respuestas a cualquier pregunta que el usuario pueda tener. Esta aplicación es solo un ejemplo de lo que se puede hacer con la API de OpenAI y la biblioteca Gradio. Hay muchas otras aplicaciones de inteligencia artificial que se pueden crear utilizando estas herramientas.

En un proximo post voy a implementar otra UI usando el componente Chatbot de Gradio para darle un diseño mas acoorde al un chatbot y algunos otros tips a la hora de usar Gradio, por el momento es un buen punto de partida para practicar y probar estas tecnologias.

## Codigo completo

```python
# Archivo chatbot.py
import gradio as gr
import openai
import os

# Get OpenAI API Key from environment variable
openai.api_key = os.environ.get("OPENAI_API_KEY", None)

def openai_process_message(user_message):
    # Set the prompt for OpenAI Api
    messages = [
        {
            "role": "system",
            "content": "Act like a personal assistant. You can respond to questions, translate sentences, summarize news, and give recommendations."
        }
    ]
    messages.append({"role": "user", "content": user_message})
    # Call the OpenAI Api to process our prompt
    openai_response = openai.ChatCompletion.create(model="gpt-3.5-turbo", messages=messages, max_tokens=2000)
    # Parse the response to get the response text for our prompt
    response_text = openai_response.choices[0].message.content
    return response_text

examples = [
    "Que es un chatbot?",
    "podrias definir que es una IA?",
    "dime cual seria una receta para hacer salsa bechamel?",
]

demo=gr.Interface(
    fn=openai_process_message,
    inputs=gr.Textbox(lines=5, label='Pregunta',placeholder='Escribe tu pregunta'),
    outputs=gr.Textbox(label='Respuesta'),
    examples=examples,
    title="Chatbot OpenAI API",
)
if __name__ == "__main__":
    demo.launch()
```