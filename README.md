# 🚀 LoopLM - Guía de instalación
Sigue estos pasos para instalar y ejecutar el entorno con los modelos personalizados en Ollama y Open WebUI.

## 1. Instalar Docker
Descarga e instala Docker desde la página oficial:
👉 https://www.docker.com/products/docker-desktop/

## 2. Instalar Open WebUI
Requisitos:
Debes tener instalado Ollama previamente en tu PC.
👉 https://ollama.com/
* Una vez instalado debes ejecutar desde la cmd:
  * ```bash
    docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
    ```
* De igual forma puedes seguir el siguiente tutorial de youtube: https://www.youtube.com/watch?v=shjlblBLLLk

## 3. Descargar los modelos desde Hugging Face
Descarga los siguientes modelos .gguf y sus respectivos Modelfile desde Hugging Face:

🔗 LLaMA 3.1 Tuned - LoopLM
https://huggingface.co/Melinnaaa/llama-3.1-tuned-looplm

🔗 Mistral V3 Tuned - LoopLM
https://huggingface.co/Melinnaaa/mistral-v3-tuned-looplm

Una vez descargados, debes copiar los archivos al contenedor de Docker donde se ejecuta Ollama.

## 4. Crear carpetas para los modelos (dentro de Docker Desktop)
  1. Abre Docker Desktop.
  
  2. Ve a la pestaña "Containers", busca el contenedor donde tienes instalado Ollama y haz clic en "Exec".
  
  3. En la terminal que se abre, ejecuta los siguientes comandos para crear las carpetas necesarias:
  ```bash
  mkdir -p /root/.ollama/models/llama3-code-explainer
  mkdir -p /root/.ollama/models/mistralV3-code-explainer
  ```

## 5. Copiar los archivos del modelo
Copia los archivos .gguf y Modelfile descargados en los pasos anteriores a las carpetas correspondientes dentro del contenedor:
* **Importante**:
  * Reemplaza [nombre_de_usuario] por el nombre de tu usuario de Windows.
  * Si los archivos están en otra ubicación distinta a Descargas, modifica la ruta en los comandos para que apunte a la carpeta correcta.
  * Asegurate que copies correctamente los modelfiles para cada modelo, ya que son diferentes.
  * Estos comandos se deben ejecutar desde la cmd de windows.
* LLama 3.1
  ```bash
  docker cp "C:\Users\[nombre_de_usuario]\Downloads\Llama3.1.gguf" open-webui:/root/.ollama/models/llama3-code-explainer/
  docker cp "C:\Users\[nombre_de_usuario]\Downloads\Modelfile" open-webui:/root/.ollama/models/llama3-code-explainer/
  ```
* Mistral V3
  ```bash
  docker cp "C:\Users\[nombre_de_usuario]\Downloads\Mistral_7B.gguf" open-webui:/root/.ollama/models/mistralV3-code-explainer/
  docker cp "C:\Users\[nombre_de_usuario]\Downloads\Modelfile" open-webui:/root/.ollama/models/mistralV3-code-explainer/
  ```
## 6. Crear los modelos personalizados en Ollama
Una vez que todo esté en su lugar, ejecuta los siguientes comandos dentro del contenedor, usando Docker Desktop (Exec):
  ```bash
  ollama create llama-3-code-explainer -f /root/.ollama/models/llama3-code-explainer/Modelfile
  ollama create Mistral-V3:7B -f /root/.ollama/models/mistralV3-code-explainer/Modelfile
  ```  
## 7. Acceder a OpenWebUI
Ahora que ya se encuentran los modelos instalados localmente, puedes acceder a OpenWebUI desde tu navegador en:

👉 http://localhost:3000

Pasos para configurar los modelos en OpenWebUI:
  1. Regístrate. Al hacerlo por primera vez, se te creará una cuenta de administrador automáticamente.
  
  2. Haz clic en tu nombre de usuario (abajo a la izquierda) y accede a Configuración.
    ![image](https://github.com/user-attachments/assets/28f89cb7-2e24-411f-ba8e-7452f5a55c68)
  
  3. Ingresa a la pestaña Ajustes de Admin.
    ![image](https://github.com/user-attachments/assets/6b47c0f2-a252-4464-b699-347b964195ea)
  
  4. Ve a la sección Modelos y haz clic en Editar sobre el modelo que desees ajustar.
    ![image](https://github.com/user-attachments/assets/54465ccc-740c-4feb-9dd5-92d263cd04ff)

  5. En el campo "Paráms Modelo", sube el prompt personalizado que se encuentra en este repositorio.
    ![image](https://github.com/user-attachments/assets/9a8b8f5b-6b56-4c4c-8bf9-4ef75ee1c86a)

  6. En la sección de Parámetros Avanzados, ajusta la temperatura a 0.
    ![image](https://github.com/user-attachments/assets/4a280fba-0afa-4144-9930-2b236a63c3d3)

  7. Haz clic en Guardar.
    ![image](https://github.com/user-attachments/assets/fe8e6cf5-42b6-428d-97e3-66a3bfdc4c4a)

  8. Repite el mismo procedimiento para el segundo modelo.


✅ ¡Listo! Ahora puedes comenzar a hacer preguntas a cualquiera de los modelos directamente desde la interfaz de OpenWebUI.
