# ⚡ Automatización y Scripts: Estándares de Flujo
Guía para el desarrollo de automatizaciones en Power Automate y Google Apps Script.

## 1. Manejo de Errores (Error Handling)
* **Timeouts:** En Power Automate, configura límites de tiempo para que un flujo no se quede "colgado" infinitamente.
* **Try/Catch en Apps Script:** Usa bloques `try { ... } catch (e) { ... }` para registrar errores en una hoja de log en lugar de que el script falle silenciosamente.

## 2. Seguridad y Credenciales
* **No Hardcoding:** Nunca escribas contraseñas o IDs sensibles directamente en el código de Apps Script. Usa `PropertiesService` para guardar configuraciones.
* **Conexiones Compartidas:** En Power Automate, usa cuentas de servicio (o cuentas genéricas de la empresa) para que el flujo no deje de funcionar si alguien cambia su contraseña personal.

## 3. Eficiencia en Google Sheets
* **Batch Operations:** En Apps Script, evita usar `getValue()` dentro de un bucle `for`. Es mejor leer todo el rango con `getValues()` una sola vez y procesarlo en memoria (JavaScript).
* **Triggers Inteligentes:** Configura disparadores (Triggers) solo cuando sea necesario (ej: al enviar un formulario) para no agotar las cuotas de ejecución diarias de Google Workspace.
