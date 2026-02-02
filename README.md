# 🤖 AgendaBot – Solución Implementada

Este repositorio contiene la **implementación funcional de AgendaBot**, un bot conversacional en **Telegram** construido con **n8n Community Edition** y **Google Sheets** para la gestión de:

* 📅 Citas (Agenda)
* 📝 Tareas
* 🔁 Hábitos

El bot funciona mediante **menús numéricos y flujos guiados**, sin uso de plataformas de pago ni servicios que requieran tarjeta de crédito.

---

## 🎯 Alcance de la Solución

La solución implementa **únicamente** los siguientes módulos:

* ✅ Agenda (citas)
* ✅ Tareas
* ✅ Hábitos

❌ No incluye:

* Listas
* Reportes
* Configuración avanzada
* Módulo Administrador

---

## 🧱 Arquitectura General

```
Usuario (Telegram)
        ↓
Telegram Bot
        ↓
n8n Community Edition
        ↓
Google Sheets (AgendaBot_DB)
```

* **Telegram**: interfaz de conversación
* **n8n**: control de flujos, estados y validaciones
* **Google Sheets**: almacenamiento persistente
* **Sesiones**: control del paso actual y datos parciales

---

## 🛠️ Stack Tecnológico

* Telegram Bot API
* n8n Community Edition (self-hosted / Docker)
* Google Sheets

---

## 📊 Modelo de Datos (Google Sheets)

El bot utiliza un documento llamado **AgendaBot_DB** con las siguientes hojas:

* `CITAS`
* `TAREAS`
* `HABITOS`
* `USUARIOS`
* `SESSIONS`
* `LOGS`

> Cada interacción del usuario queda registrada para trazabilidad y control de estado.

---

## 💬 Experiencia Conversacional

* Todas las interacciones se realizan **escribiendo números**
* El bot nunca asume intención
* Cada flujo es guiado paso a paso (wizard)
* Existe opción de **cancelar o volver** en todo momento
* El bot sugiere la mejor opción cuando aplica

---

## 📅 Flujo Implementado – Agenda (Citas)

**Agendar una cita** sigue este orden:

1. Fecha (YYYY-MM-DD)
2. Hora (HH:MM)
3. Nombre del cliente
4. Motivo
5. Canal (Presencial / Virtual / Llamada)
6. Confirmación final

Los datos se almacenan en Google Sheets y el estado de la sesión se limpia al finalizar.

---

## 🧠 Manejo de Sesiones

Cada usuario tiene una sesión activa que contiene:

* Pantalla actual
* Paso del flujo
* Datos parciales
* Timestamp de última interacción

Esto permite:

* Retomar flujos
* Validar entradas
* Evitar estados inconsistentes

---

## 🚀 Cómo Ejecutar el Proyecto

### 1️⃣ Requisitos

* Docker instalado
* Cuenta de Telegram
* Bot creado con **@BotFather**
* Documento Google Sheets compartido con n8n

---

### 2️⃣ Levantar n8n

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -e GENERIC_TIMEZONE="America/Bogota" \
  -e TZ="America/Bogota" \
  -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n
```

---

### 3️⃣ Configuración en n8n

1. Importar los workflows del directorio `/n8n/workflows`
2. Configurar credenciales:

   * Telegram Bot
   * Google Sheets
3. Activar el workflow principal (`router_principal.json`)

---

## 🧪 Ejemplo de Uso

```
Usuario: 1
Bot: Perfecto, vamos con tu agenda.
Bot: ¿Qué deseas hacer?
1. Agendar una nueva cita
...
```

---

## ⚠️ Manejo de Errores

* Validación de formato en cada paso
* Mensaje global para opciones inválidas
* Cancelación segura en cualquier punto
* Limpieza automática de sesiones incompletas

---

## 📌 Notas Finales

* Proyecto desarrollado con **n8n Community**
* Sin dependencias de pago
* Enfoque educativo y demostrativo
* Preparado para ampliarse a otros módulos

---

## 👨‍💻 Autor

**Leonardo José De la cruz Ardila**

---

