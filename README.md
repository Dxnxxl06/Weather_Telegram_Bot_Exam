🌦️ AI Weather Telegram Bot (n8n + Ollama)
Este flujo de trabajo de n8n permite a los usuarios consultar el clima de cualquier ciudad del mundo a través de un bot de Telegram. Utiliza Inteligencia Artificial local para validar entradas y generar respuestas amigables, además de persistir cada consulta en bases de datos y hojas de cálculo.

🚀 Funcionalidades
Procesamiento de Lenguaje Natural: Utiliza Ollama (Llama 3.2:3b) para validar si el texto ingresado por el usuario es una ciudad real.

Geocodificación: Convierte nombres de ciudades en coordenadas geográficas (Latitud/Longitud) mediante la API de Open-Meteo.

Datos en Tiempo Real: Obtiene información climatológica actualizada (Temperatura, viento, códigos WMO).

Generación de Respuestas IA: Crea mensajes personalizados con emojis y un tono amigable antes de enviarlos a Telegram.

Persistencia de Datos Dual: * PostgreSQL: Registra la consulta para análisis técnico o histórico.

Google Sheets: Almacena los datos para una visualización rápida y administrativa.

🛠️ Tecnologías y Nodos Utilizados
Orquestador: n8n (Versión self-hosted recomendada).

IA Local: Ollama con el modelo llama3.2:3b.

APIs Externas: * Telegram Bot API (Mensajería).

Open-Meteo (Geocoding y Weather Data).

Almacenamiento: PostgreSQL y Google Sheets.

Lógica: Nodos de JavaScript (Code) para limpieza de JSON y estructuración de prompts.

📋 Requisitos Previos
n8n instalado y funcionando.

Ollama instalado localmente con el modelo llama3.2:3b descargado.

Un Bot de Telegram (creado vía @BotFather) y su respectivo API Token.

Base de datos PostgreSQL con una tabla llamada consultas_clima.

Schema sugerido: ciudad (VARCHAR), pais (VARCHAR), temperatura (NUMERIC), chat_id (BIGINT).

Una hoja de Google Sheets con las columnas: Fecha, Ciudad, Pais, Temperatura.

⚙️ Configuración del Flujo
Importación: Copia el archivo JSON del flujo e impórtalo en tu instancia de n8n.

Credenciales: * Configura tus credenciales de Telegram.

Configura el nodo de Ollama con la URL de tu instancia local (normalmente http://localhost:11434).

Conecta tu cuenta de Google Sheets y selecciona el Document ID correspondiente.

Configura la conexión a tu base de datos Postgres.

Trigger: El flujo está configurado con un Schedule Trigger que consulta actualizaciones cada 1000 segundos (puedes ajustarlo según tu necesidad o cambiarlo por un Webhook de Telegram para respuestas instantáneas).

🧩 Estructura de la Lógica
Entrada: Se obtienen los últimos mensajes del bot mediante getUpdates.

Validación: Un agente de IA descarta mensajes que no contengan nombres de ciudades.

Enriquecimiento: Se buscan coordenadas y se hace el fetch de la API de clima.

Respuesta: La IA redacta un resumen creativo de máximo 3 líneas.

Cierre: Se envía el mensaje al usuario y se guardan los logs en SQL y Sheets.

Desarrollado con ❤️ usando n8n y Ollama.