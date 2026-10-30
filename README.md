# Nino Analitics — Tus análisis de laboratorio, explicados en lenguaje simple

> Agente de IA que ayuda a las personas a entender sus resultados de laboratorio y a llegar mejor preparadas a la consulta médica. **No diagnostica ni reemplaza a un profesional de la salud.**

Proyecto para el **Nebius x NVIDIA Global AI Hackathon 2026** · Track: **Best Apps and Agents**

## El problema

Mucha gente recibe sus análisis de sangre u orina como una tabla de números y abreviaturas, y a veces espera días para consultar con un médico. El resultado es ansiedad innecesaria, o lo contrario: ignorar valores que sí merecían atención.

## La solución

El usuario pega o sube sus resultados y el agente:

1. **Extrae** cada valor, su unidad y el rango de referencia.
2. **Marca** lo que está fuera de rango (alto/bajo) y qué tan lejos está.
3. **Explica** en lenguaje simple qué mide cada examen y qué podría significar un valor alterado, sin dar diagnósticos.
4. **Sugiere preguntas** concretas para llevar al médico.
5. **Se apoya en fuentes médicas actuales** mediante búsqueda web (Tavily) y las cita.

## Cómo funciona

```
Resultados (texto/archivo)
        │
        ▼
 Parser de valores ──► Comparación determinista con rangos de referencia
        │                          │
        ▼                          ▼
   Agente (Nemotron en Nebius Token Factory)
        │        ▲
        │        └── Tavily: búsqueda de fuentes médicas
        ▼
 Explicación simple + valores marcados + preguntas para el médico
```

Decisión de diseño importante: **la comparación contra los rangos de referencia se hace con código, no con el modelo**, para evitar que el LLM invente o malinterprete límites. El modelo se encarga de explicar y redactar.

## Tecnologías

- **Modelo:** NVIDIA Nemotron `[nemo, nano super]`
- **Infraestructura:** Nebius Token Factory
- **Búsqueda:** Tavily
- **App:** `[python, fastapi, cuda, uvicorn, poetry, tensores, modelos open source]`

## Instalación y uso

```bash
git clone [URL-del-repositorio]
cd ninoanalitics
cp .env.example .env   # agrega NEBIUS_API_KEY y TAVILY_API_KEY
[comando de instalación]
[comando para ejecutar]
```

Variables de entorno:

| Variable | Descripción |
|---|---|
| `NEBIUS_API_KEY` | Clave de Nebius Token Factory |
| `TAVILY_API_KEY` | Clave de Tavily |

## Seguridad y privacidad

- La herramienta es **solo informativa**: no emite diagnósticos ni recomienda tratamientos.
- Toda respuesta incluye un aviso para consultar a un profesional de la salud.
- Ante valores muy alterados, el agente recomienda atención médica oportuna en lugar de especular.
- `[Indicar cómo se manejan los datos: no se almacenan / se procesan solo en la sesión, etc.]`

## Hoja de ruta

- **Triage de síntomas:** preguntas guiadas para orientar si conviene ir a emergencias, consulta o esperar.
- **Seguimiento de factores de riesgo:** según edad, hábitos y antecedentes, qué chequeos preventivos corresponden y cada cuánto.
- Historial de resultados para ver tendencias en el tiempo.
- Soporte para más tipos de examen y más idiomas.

## Demo

`[enlace al video o capturas]`

## Autor

Joshua — ingeniero de software.

## Aviso

LabLens es un prototipo creado para un hackathon con fines educativos e informativos. No es un dispositivo médico.
