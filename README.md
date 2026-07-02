# 🏙️ OmniRAG: Ecosistema Agéntico SmartCity

**Ecosistema de Inteligencia Artificial Local (Llama-3 8B) para gestión de infraestructura urbana.**
*"Donde el dato se convierte en decisión: Un ecosistema agéntico diseñado para que las ciudades no solo procesen información, sino que aprendan, vean y recuerden."

**Desarrollado por: Msc. Yanet Cesaire Velazquez**

## 📂 Documentación Técnica

Para conocer los detalles de arquitectura, desafíos técnicos superados y comparativas de rendimiento:

👉 [**Descargar Informe Técnico Completo (PDF)**](./documentos/Informe_Tecnico.pdf)

*Nota: Este repositorio es un portafolio de arquitectura y diseño de sistemas de IA. El código fuente es de propiedad privada de la autora.*

Este proyecto es un caso de estudio sobre la implementación de **10 estrategias avanzadas de RAG (Recuperación Aumentada por Generación)** para resolver problemas complejos de una **"Ciudad Inteligente"**.

![9 ARQUITECTURAS RAG](./imagenes/ArquitecturaRAG.png)

## 🚀 Las 10 Estrategias Implementadas

1. **RAG Básico:** Búsqueda semántica estándar.

2. **RAG Jerárquico:** Estructura Padre-Hijo para manuales extensos.

3. **RAG con Agentes:** Toma de decisiones con herramientas en vivo.

4. **RAG de Memoria:** Persistencia histórica con SQLite.

5. **RAG Multimodal:** Análisis de imágenes con modelos BLIP.

6. **RAG con Retroalimentación:** Aprendizaje continuo por feedback humano.

7. **RAG Distribuido:** Enrutamiento inteligente a silos regionales (Europa, Asia, América).

8. **RAG Híbrido:** Precisión del 100% en códigos SKU (Vectores + Keyword).

9. **RAG Adaptativo:** Clasificador de intención (Nivel 1 vs Nivel 2).

10. **Benchmarking PDF:** Pruebas de estrés con documentos de +200 páginas (Usamos en la comparación **ChromaDB  y Faiss**).

## 🏗️ Diseño de Arquitectura 

Esta arquitectura representa un sistema de IA de Grado Industrial. Se basa en el desacoplamiento de responsabilidades: el **Frontend** gestiona la experiencia, el **Backend** orquesta la lógica, y los **Engines** ejecutan las estrategias específicas de RAG.
Todo orquestado por FastAPI y visualizado con Streamlit, utilizando exclusivamente el ecosistema de **Hugging Face (Transformers, Datasets, Inference API)**.

**CAPA DE PRESENTACIÓN (Streamlit):** Es el punto de entrada. Gestiona no solo el texto, sino el renderizado de imágenes de evidencia y las métricas de rendimiento que el backend calcula en tiempo real.

**CAPA DE ORQUESTACIÓN (FastAPI):** Funciona como un "Traffic Controller". Antes de buscar, pasa por el Memory Middleware (SQLite) para saber quién es el usuario y qué dijo antes. Luego, el Adaptive Gateway decide si la pregunta es simple o requiere análisis profundo.

**LÓGICA AGÉNTICA:** Aquí residen tus 10 estrategias. El sistema decide qué "herramienta" de recuperación usar (Híbrida para códigos SKU, Jerárquica para manuales, o Multimodal para cámaras).

**CAPA DE INFERENCIA:** Es el motor de ejecución. Utilizamos Llama-3 8B para el razonamiento y BLIP para la visión. Todo corre localmente, asegurando privacidad y soberanía de datos.

**CAPA DE DATOS:** El almacenamiento está segmentado. FAISS/ChromaDB para la velocidad de búsqueda, SQLite para la integridad de la memoria, y Silos Regionales para simular una infraestructura distribuida real.

```mermaid
graph TD
    classDef frontend fill:#E1F5FE,stroke:#01579B,stroke-width:2px,color:#000
    classDef backend fill:#F5F5F5,stroke:#424242,stroke-width:2px,color:#000
    classDef agent fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,color:#000
    classDef models fill:#FFF9C4,stroke:#FBC02D,stroke-width:2px,color:#000
    classDef storage fill:#FFEBEE,stroke:#C62828,stroke-width:2px,color:#000

    subgraph UI ["🖥️ CAPA DE PRESENTACIÓN"]
        A[Streamlit Dashboard]
        A1[Métricas de Latencia]
        A2[Interfaz de Chat]
        A3[Visor de Imágenes]
    end
    class A,A1,A2,A3 frontend

    subgraph Backend ["⚙️ BACKEND - FASTAPI"]
        B{Orquestador OmniRAG}
        B1[Clasificador Adaptativo]
        B2[Router Regional de Silos]
        B3[Middleware de Memoria]
    end
    class B,B1,B2,B3 backend

    subgraph Agents ["🧠 LÓGICA DE AGENTES"]
        C1[Búsqueda Híbrida]
        C2[Motor Jerárquico]
        C3[Agente Visual Multimodal]
        C4[Capa de Aprendizaje/Feedback]
        C5[Módulo de Benchmarking]
    end
    class C1,C2,C3,C4,C5 agent

    subgraph AI_Models ["🤖 MODELOS DE IA LOCAL"]
        D1[Llama-3 8B GGUF]
        D2[BLIP Vision Model]
        D3[HuggingFace Embeddings]
    end
    class D1,D2,D3 models

    subgraph Data ["💾 PERSISTENCIA Y DATOS"]
        E1["(FAISS / ChromaDB)"]
        E2["(SQLite - Historial)"]
        E3[CSV - Feedback DB]
        E4[Silos: EU / AS / AM]
        E5[PDF / JSON Master]
    end
    class E1,E2,E3,E4,E5 storage

    A -->|Consulta HTTP| B
    B --> B3
    B3 -->|Consulta| E2
    B --> B1
    B1 -->|Enrutamiento| C1
    B --> B2
    B2 -->|Filtro| E4

    C1 -->|Búsqueda| E1
    C2 -->|Búsqueda| E1
    C4 -->|Búsqueda| E1
    C3 -->|Analizar Imagen| D2
    D2 -->|Descripción| C3

    C1 -->|Prompt Contexto| D1
    C2 -->|Prompt Contexto| D1
    C3 -->|Prompt Contexto| D1
    C4 -->|Prompt Contexto| D1
    C5 -->|Prompt Contexto| D1
    
    D3 -->|Vectores| E1

    D1 -->|Respuesta Final| A
    E1 -->|Contexto Técnico| D1
    C4 -->|Guardar| E3

    style UI fill:#FFFFFF,stroke:#333,stroke-dasharray: 5 5
    style Backend fill:#FFFFFF,stroke:#333,stroke-dasharray: 5 5
    style Agents fill:#FFFFFF,stroke:#333,stroke-dasharray: 5 5
    style AI_Models fill:#FFFFFF,stroke:#333,stroke-dasharray: 5 5
    style Data fill:#FFFFFF,stroke:#333,stroke-dasharray: 5 5
```

## 🌲 Estructura del Directorio

A continuación se detalla la organización modular de los microservicios y bases de datos:

![DIRECTORIO](./imagenes/1_Directorio.png)

## 🌐 Microservicios con FastAPI: El Cerebro del Sistema

En este proyecto, **FastAPI** actúa como la capa de backend de alto rendimiento, encargada de gestionar la lógica de los 10 agentes RAG de forma modular. Sus principales funciones son:

**1. Orquestación Agéntica (Inference Engine)**

El microservicio central recibe las consultas del usuario y decide, mediante lógica de programación y prompts dinámicos, qué estrategia de recuperación activar (Básica, Jerárquica o Híbrida). Gestiona la comunicación directa con el modelo Llama-3 8B de forma eficiente, controlando los tiempos de generación.

**2. Enrutamiento Inteligente (Router Service)**

Implementa la lógica del RAG Adaptativo y Distribuido. Este componente analiza la intención de la pregunta y la región geográfica mencionada para dirigir la petición al silo de datos correcto (Europa, Asia, América) o al nivel de complejidad adecuado (FAQ vs. Análisis Profundo), optimizando el uso de recursos de la CPU.

**3. Procesamiento Multimodal y Visión**

Este microservicio integra el modelo de **visión BLIP**. Se encarga de la ingesta de imágenes, la extracción de metadatos técnicos y la conversión de píxeles a descripciones textuales que luego son indexadas en la base de datos vectorial para su búsqueda por lenguaje natural.

**4. Gestión de Persistencia y Memoria (State Management)**

Responsable de la conexión con SQLite y archivos de Feedback. Este servicio asegura que cada interacción se guarde correctamente, permitiendo que la IA "recuerde" el contexto del usuario y que el sistema aprenda de las correcciones humanas mediante el procesamiento de archivos CSV en tiempo real.

**5. API de Benchmarking y Métricas**

Un servicio especializado en el análisis de rendimiento. Captura las latencias de búsqueda (Retrieval) y de generación (LLM) de motores como FAISS y ChromaDB, exponiendo estos datos a través de endpoints específicos para su visualización técnica en el dashboard.

![MICROSERVICIO](./imagenes/Microservicios.png)

## 🛠️ Stack Tecnológico

**LLM: Llama-3 8B (Local/Quantized)**

**Orquestación: FastAPI & LangChain**

**Bases de Datos: FAISS, ChromaDB, SQLite**

**Visión: BLIP (Salesforce)**

**Interfaz: Streamlit (Custom CSS)**

**Embeddings: HuggingFace / sentence-transformers**

**Lenguaje de Programación: Python**

## 🖥️ Prototipo de Interfaz

He diseñado un dashboard interactivo utilizando **Streamlit** que permite al operador de la SmartCity alternar entre los 10 agentes RAG de forma fluida.

**Ejemplos: RAG Multimodal**

![INTERFAZ 1](./imagenes/2_OK.png)

![INTERFAZ 2](./imagenes/3_OK.png)

![INTERFAZ 3](./imagenes/4_OK.png)

**Ejemplos: RAG con Retroalimentación (Feedback)**

El sistema genera una respuesta con Llama 8B y permite que el usuario la vote (👍/👎).

![FEEDBACK 1](./imagenes/1_FeedBack.png)

![FEEDBACK 2](./imagenes/2_FeedBack.png)

**Ejemplos: RAG con Híbrida**

![FEEDBACK 1](./imagenes/1_Hibrido.png)
