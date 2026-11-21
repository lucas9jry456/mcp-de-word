```markdown
# MCP de Word (`mcp-de-word`)

Servidor **MCP (Model Context Protocol)** diseñado para buscar información actualizada en internet y guardarla de forma estructurada en documentos de Microsoft Word (`.docx`).

**Repositorio:** https://github.com/lucas9jry456/mcp-de-word

---

## Descripción

Este proyecto implementa un servidor MCP que conecta un asistente de inteligencia artificial con herramientas de búsqueda web y generación de archivos `.docx`. Permite investigar temas en línea directamente desde el cliente de IA, recopilar hallazgos y exportarlos automáticamente a un documento de Word listo para editar, compartir o entregar.

---

## Requisitos

Antes de comenzar, asegúrate de contar con:

* **Git** instalado para clonar el repositorio.
* **Entorno de ejecución:** Python 3.10 o superior *(o Node.js v18+, según la implementación de tu archivo principal)*.
* **Cliente compatible con MCP:** Claude Desktop, Cursor, VS Code (con soporte MCP) u otro cliente compatible.
* **Aplicación de ofimática:** Microsoft Word, LibreOffice Writer o Google Docs para abrir y visualizar los archivos `.docx` generados.
* **Conexión a internet** activa para realizar las búsquedas web.

---

## Instalación paso a paso

1. **Clonar el repositorio:**
   Abre una terminal y descarga el proyecto desde GitHub:
   ```bash
   git clone [https://github.com/lucas9jry456/mcp-de-word.git](https://github.com/lucas9jry456/mcp-de-word.git)
   cd mcp-de-word

```

2. **Instalar las dependencias:**
* **Si el proyecto es en Python:**
```bash
python -m venv .venv
# En Windows:
.venv\Scripts\activate
# En macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt

```


* **Si el proyecto es en Node.js:**
```bash
npm install

```




3. **Configurar variables de entorno (si aplica):**
Si tu servidor requiere claves de API para el buscador o una ruta de salida específica, crea un archivo `.env` en la raíz del proyecto:
```env
API_KEY=tu_clave_aqui
OUTPUT_DIR=./documentos

```



---

## Cómo abrir y ejecutar el programa

Los servidores MCP funcionan en segundo plano comunicándose con el cliente de IA mediante entrada/salida estándar (`stdio`). Puedes abrirlo de dos maneras:

### 1. Ejecución automática desde tu cliente MCP (Recomendado)

No necesitas dejar una terminal abierta manualmente; el cliente MCP inicia el servidor de forma automática al abrirse.

1. Abre el archivo de configuración de tu cliente MCP (por ejemplo, en **Claude Desktop**: *Configuración > Desarrollador > Editar configuración*, que abre `claude_desktop_config.json`).
2. Agrega la siguiente configuración ajustando la ruta hacia tu carpeta `mcp-de-word` y el nombre de tu archivo principal (`server.py` / `main.py` / `index.js`):
```json
{
  "mcpServers": {
    "mcp-de-word": {
      "command": "python",
      "args": [
        "/RUTA/COMPLETA/A/mcp-de-word/server.py"
      ]
    }
  }
}

```


*(Nota: Si usas un entorno virtual en Python, reemplaza `"python"` por la ruta completa al ejecutable dentro de `.venv`, por ejemplo: `"/RUTA/COMPLETA/A/mcp-de-word/.venv/Scripts/python.exe"` en Windows o `"/RUTA/COMPLETA/A/mcp-de-word/.venv/bin/python"` en macOS/Linux).*
3. **Guarda el archivo y reinicia completamente tu cliente MCP.**
4. Verifica en el menú de herramientas o conectores del cliente que el servidor `mcp-de-word` aparece conectado y activo.

### 2. Ejecución manual desde la terminal (para pruebas)

Si deseas verificar que el programa arranca sin errores antes de conectarlo al cliente:

```bash
# Dentro de la carpeta mcp-de-word
python server.py

```

---

## Lista de herramientas

El servidor expone las siguientes herramientas al modelo de IA:

* **Herramienta de búsqueda web (`buscar_web` / `search_web`):** Consulta información actualizada en internet a partir de una búsqueda o pregunta y devuelve los resultados más relevantes (títulos, enlaces y extractos).
* **Herramienta de creación de Word (`crear_word` / `guardar_en_word`):** Genera un archivo `.docx` con título, subtítulos, listas y párrafos estructurados a partir de la información recopilada.

*(Ajusta los nombres exactos entre paréntesis según cómo estén definidas las funciones en tu código).*

---

## Ejemplos de uso

Una vez conectado el servidor en tu cliente MCP, puedes usarlo escribiendo instrucciones en lenguaje natural:

* **Ejemplo 1 — Investigar un tema y crear un informe:**
> *"Busca información actualizada sobre el impacto de la inteligencia artificial en la educación superior y guarda un resumen estructurado en un archivo Word llamado `ia_educacion.docx`."*


**Flujo de ejecución:** El asistente invoca la herramienta de búsqueda web, sintetiza los hallazgos y utiliza la herramienta de Word para generar el archivo `ia_educacion.docx` listo para abrir.
* **Ejemplo 2 — Crear una guía de estudio:**
> *"Investiga qué es el protocolo MCP (Model Context Protocol), cuáles son sus componentes principales y guarda una guía de estudio en `guia_mcp.docx`."*


**Flujo de ejecución:** El servidor consulta las fuentes en internet y exporta el contenido organizado directamente en `guia_mcp.docx`.

---

## Solución de problemas frecuentes

* **El servidor no aparece en el cliente MCP:** Verifica que las rutas en `claude_desktop_config.json` sean rutas absolutas y que el archivo JSON no tenga errores de formato.
* **Error de dependencias no encontradas:** Asegúrate de apuntar al ejecutable de Python dentro de tu entorno virtual (`.venv`) en la configuración del cliente.
* **No encuentro el archivo `.docx` generado:** Si no especificaste una ruta exacta en el prompt, busca el archivo en la carpeta raíz de `mcp-de-word` o en tu carpeta de usuario.

---

## Utilidad académica

### ¿Qué problema resuelve?

En el ámbito académico, la elaboración de informes, estados del arte y guías de estudio suele fragmentarse entre múltiples pestañas del navegador, motores de búsqueda y procesadores de texto. Gran parte del tiempo se invierte en tareas mecánicas de recopilación, filtrado inicial y estructuración de borradores en formato `.docx`. Este servidor MCP automatiza la transición entre la búsqueda de información en línea y la creación de un documento editable, reduciendo la fricción operativa en las fases iniciales de investigación.

### ¿Para quién está dirigido?

* **Estudiantes:** Para levantar información preliminar, estructurar apuntes de clase y preparar borradores de trabajos prácticos o revisiones bibliográficas.
* **Docentes:** Para recopilar recursos actualizados sobre una temática y generar material de apoyo o guías de lectura en formato Word de manera ágil.
* **Investigadores y ayudantes:** Para realizar exploraciones rápidas sobre conceptos emergentes y documentar hallazgos preliminares en un formato estándar.

### ¿En qué dimensión del aprendizaje aporta?

Aporta principalmente en la **gestión de la información y la síntesis documental** (alfabetización informacional y organización del conocimiento). Al delegar la recopilación inicial y el formateo básico en el flujo automatizado, el estudiante o docente puede concentrar su esfuerzo cognitivo en tareas de orden superior: evaluar críticamente la calidad de las fuentes recuperadas, contrastar argumentos, verificar datos y redactar sus propias conclusiones sobre una base ya estructurada.

---

## Declaración de uso de IA, límites conocidos y consideraciones de seguridad

### Declaración de uso de IA

Para el desarrollo de este proyecto y su documentación se utilizó asistencia de inteligencia artificial generativa como herramienta de apoyo para la redacción del archivo `README.md`, la estructuración de ejemplos y la revisión de código. El diseño funcional, la integración del repositorio y las pruebas de funcionamiento fueron realizados y verificados por el autor del proyecto.

### Límites conocidos

* **Dependencia de fuentes externas:** La calidad, actualidad y disponibilidad de la información dependen de los resultados devueltos por el motor de búsqueda utilizado y de la accesibilidad de las páginas web consultadas.
* **Riesgo de imprecisiones o sesgos:** El modelo de lenguaje puede resumir de forma incompleta o interpretar erróneamente información ambigua encontrada en la web, por lo que todo documento generado requiere revisión humana antes de su uso académico formal.
* **Formato básico de salida:** La exportación a `.docx` prioriza una estructura limpia (títulos, subtítulos, párrafos y listas), sin reemplazar diseños editoriales complejos o citación bibliográfica automática avanzada.

### Consideraciones de seguridad

* **Protección de credenciales:** Nunca se deben subir claves de API ni archivos `.env` con credenciales al repositorio público de GitHub; se recomienda incluir `.env` dentro de `.gitignore`.
* **Control de escritura de archivos:** El servidor debe operar sobre directorios de salida controlados para evitar la sobrescritura accidental de documentos importantes del sistema o del usuario.
* **Verificación de fuentes web:** Dado que el servidor consulta contenido abierto en internet, existe el riesgo de exposición a contenido no confiable o inyección indirecta de instrucciones desde páginas externas; se recomienda revisar las URLs de origen y validar el contenido antes de compartirlo.

```

```
