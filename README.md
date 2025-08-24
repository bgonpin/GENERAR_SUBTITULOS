# 📋 Manual de Empleo - Generador de Subtítulos

## 📚 Tabla de Contenidos
- [Introducción](#-introducción)
- [Funcionalidades Principales](#-funcionalidades-principales)
- [Requisitos del Sistema](#-requisitos-del-sistema)
- [Instalación](#-instalación)
- [Instrucciones de Uso](#-instrucciones-de-uso)
- [Ejemplos Prácticos](#-ejemplos-prácticos)
- [Configuración Avanzada](#️-configuración-avanzada)
- [Solución de Problemas](#-solución-de-problemas)
- [Referencia Técnica](#-referencia-técnica)

## 🎯 Introducción
Este proyecto es un **generador automático de subtítulos** para archivos de video desarrollado en Python. El script procesa videos de manera inteligente, extrayendo el audio, transcribiéndolo a texto y generando archivos de subtítulos en formato SRT (SubRip).

### ¿Qué hace exactamente?
- 🔊 **Extracción de Audio:** Usa FFmpeg para extraer audio de cualquier formato de video
- 📝 **Transcripción:** Convierte audio a texto usando modelos de IA (Whisper)
- 🌐 **Traducción (Opcional):** Traduce subtítulos a múltiples idiomas
- 📁 **Generación SRT:** Crea archivos de subtítulos compatibles con reproductores multimedia

## ⚡ Funcionalidades Principales

### Transcripción Inteligente
- **Whisper Local:** Usa modelos de OpenAI Whisper para transcripción de alta calidad
- **Ollama Integration:** Soporte para modelos de IA locales vía Ollama
- **Formato SRT:** Genera subtítulos con timestamps precisos
- **Procesamiento por Lotes:** Procesa múltiples videos automáticamente

### Traducción Multilingüe
- **Google Translate:** Traducción automática a 10+ idiomas
- **Ollama Translation:** Traducción usando modelos de lenguaje locales
- **Idiomas Soportados:** Español, Inglés, Francés, Alemán, Italiano, Portugués, Ruso, Japonés, Coreano, Chino

### Gestión Automática de Archivos
- **Carpetas Organizadas:** videos_entrada/ para entrada, videos_salida/ para salida
- **Limpieza Automática:** Elimina archivos temporales automáticamente
- **Sobrescritura Inteligente:** Pregunta antes de sobrescribir archivos existentes

## 🔧 Requisitos del Sistema

### Dependencias Obligatorias
| Software | Propósito | Instalación |
|----------|-----------|-------------|
| **Python 3.7+** | Ejecutar el script | python.org |
| **FFmpeg** | Extraer audio de videos | ffmpeg.org |

### Dependencias Opcionales
| Software | Propósito | Comando de Instalación |
|----------|-----------|----------------------|
| **OpenAI Whisper** | Transcripción local de alta calidad | `pip install openai-whisper` |
| **PyTorch** | Soporte para Whisper | `pip install torch torchvision torchaudio` |
| **Googletrans** | Traducción automática | `pip install googletrans==4.0.0rc1` |
| **Ollama** | Modelos de IA locales | ollama.ai |

## 🚀 Instalación

### 1. Instalar Dependencias Básicas
```bash
nito@linux:~$ sudo apt update
nito@linux:~$ sudo apt install ffmpeg python3 python3-pip
```

### 2. Instalar Dependencias de Python
```bash
nito@linux:~$ pip install openai-whisper torch torchvision torchaudio
nito@linux:~$ pip install googletrans==4.0.0rc1
```

### 3. Verificar Instalación
```bash
nito@linux:~$ python generar.py --help
```

## 📖 Instrucciones de Uso

**📋 Contenido del Archivo "empleo":**

### 1. Uso Básico (Recomendado)
```bash
python generar.py
```
**Qué hace:** Procesa todos los videos en la carpeta `videos_entrada/` usando Whisper local para transcripción.

### 2. Transcripción y Traducción al Español
```bash
python generar.py --translate
```
**Qué hace:** Genera subtítulos y los traduce automáticamente al español usando Google Translate.

### 3. Traducción a Otros Idiomas
```bash
# Traducción al inglés
python generar.py --translate --target-lang en

# Traducción al francés
python generar.py --translate --target-lang fr

# Traducción al alemán
python generar.py --translate --target-lang de
```

### 4. Usar Ollama para Traducción
```bash
python generar.py --translate --translation-method ollama
```
**Nota:** Requiere tener modelos de Ollama instalados y ejecutándose.

### 5. Especificar Modelo de Ollama
```bash
python generar.py --translate --translation-method ollama --translation-model mistral
```

### 6. Usar Ollama para Transcripción
> ⚠️ **Advertencia:** Ollama no está optimizado para transcripción. Se recomienda usar Whisper local.
```bash
python generar.py --use-ollama
```

### 7. Combinar Opciones
```bash
python generar.py --translate --target-lang en --translation-method ollama
```
Combina múltiples opciones para personalizar el procesamiento.

## 💡 Ejemplos Prácticos

### Ejemplo 1: Procesamiento Básico
```bash
nito@linux:~/GENERAR_SUBTITULOS$ ls videos_entrada/
01_Introduction.mp4  02_Chapter1.mp4

nito@linux:~/GENERAR_SUBTITULOS$ python generar.py

=============================================
Procesando: 01_Introduction.mp4
=============================================
Extrayendo audio de videos_entrada/01_Introduction.mp4...
✓ Audio extraído correctamente
Usando Whisper local para transcripción...
✓ Modelo cargado en CPU
Transcribiendo audio...
Creando archivo SRT: videos_salida/01_Introduction.srt

✅ ¡Subtítulos generados exitosamente!
📁 Archivo: videos_salida/01_Introduction.srt
```

### Ejemplo 2: Con Traducción
```bash
nito@linux:~/GENERAR_SUBTITULOS$ python generar.py --translate --target-lang en

=============================================
Procesando: 01_Introduction.mp4
=============================================
Extrayendo audio de videos_entrada/01_Introduction.mp4...
✓ Audio extraído correctamente
Usando Whisper local para transcripción...
Traduciendo subtítulos a en usando googletrans...
Traduciendo segmento 1/15...
Traduciendo segmento 2/15...
...
Creando archivo SRT: videos_salida/01_Introduction.srt

✅ ¡Subtítulos generados exitosamente!
🌐 Subtítulos traducidos a en usando googletrans
📁 Archivo: videos_salida/01_Introduction.srt
```

### Ejemplo 3: Archivo Específico
```bash
python generar.py --video videos_entrada/01_Introduction.mp4
```

## ⚙️ Configuración Avanzada

### Parámetros del Script
| Parámetro | Descripción | Valor por Defecto |
|-----------|-------------|-------------------|
| `-v, --video` | Procesar archivo específico | Todos los archivos |
| `-m, --model` | Modelo de Ollama para transcripción | dimavz/whisper-tiny |
| `--keep-audio` | Mantener archivo de audio temporal | false |
| `--use-ollama` | Usar Ollama para transcripción | false |
| `--use-whisper` | Usar Whisper local | true (por defecto) |
| `--translate` | Habilitar traducción | false |
| `--translation-method` | Método de traducción | googletrans |
| `--target-lang` | Idioma destino | es (español) |
| `--translation-model` | Modelo de Ollama para traducción | llama3.2 |

### Estructura de Carpetas
```
GENERAR_SUBTITULOS/
├── generar.py              # Script principal
├── empleo                  # Instrucciones de uso
├── manual.html            # Este manual
├── videos_entrada/        # 📥 Colocar videos aquí
│   ├── video1.mp4
│   └── video2.mp4
└── videos_salida/         # 📤 Subtítulos generados
    ├── video1.srt
    └── video2.srt
```

## 🔍 Solución de Problemas

### Errores Comunes

#### ❌ FFmpeg no encontrado
```
Error: Faltan dependencias: ffmpeg
```
**Solución:**
```bash
sudo apt install ffmpeg  # Ubuntu/Debian
# o
sudo yum install ffmpeg  # CentOS/RHEL
# o
brew install ffmpeg      # macOS
```

#### ❌ Whisper no instalado
```
Whisper no está instalado. Instala con: pip install openai-whisper
```
**Solución:**
```bash
pip install openai-whisper torch torchvision torchaudio
```

#### ❌ Problemas con PyTorch
```
Error en transcripción con Whisper: [PyTorch error]
```
**Solución:**
```bash
# Para CPU only (recomendado)
pip uninstall torch torchvision torchaudio
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu

# Para GPU (si tienes CUDA)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

#### 💡 Consejos Útiles
- Usa `--keep-audio` para inspeccionar archivos de audio si hay problemas
- Verifica que los videos estén en formato compatible (.mp4, .avi, .mkv, etc.)
- Asegúrate de tener suficiente espacio en disco para archivos temporales
- Para mejor rendimiento, instala PyTorch con soporte GPU

## 📚 Referencia Técnica

### Formato SRT
Los archivos SRT (SubRip) tienen la siguiente estructura:
```
1
00:00:01,500 --> 00:00:04,000
Hola, bienvenidos al tutorial

2
00:00:04,500 --> 00:00:07,200
En este video aprenderemos...
```

### Flujo de Trabajo Interno
1. **Validación:** Verifica dependencias y archivos de entrada
2. **Extracción:** FFmpeg extrae audio del video
3. **Transcripción:** Whisper convierte audio a texto con timestamps
4. **Traducción (Opcional):** Traduce segmentos usando Google Translate u Ollama
5. **Formateo:** Convierte a formato SRT con timestamps precisos
6. **Guardado:** Almacena archivo en carpeta de salida
7. **Limpieza:** Elimina archivos temporales

### Códigos de Idioma
| Código | Idioma | Código | Idioma |
|--------|--------|--------|--------|
| `es` | Español | `en` | Inglés |
| `fr` | Francés | `de` | Alemán |
| `it` | Italiano | `pt` | Portugués |
| `ru` | Ruso | `ja` | Japonés |
| `ko` | Coreano | `zh` | Chino |

---

**Generador de Subtítulos** - Documentación Técnica  
Desarrollado con Python | Última actualización: Agosto 2025  
Para más información, consulte el código fuente en `generar.py`
