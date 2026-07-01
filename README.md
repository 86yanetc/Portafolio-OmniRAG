# 🏙️ OmniRAG: Ecosistema Agéntico SmartCity

**Ecosistema de Inteligencia Artificial Local (Llama-3 8B) para gestión de infraestructura urbana.**

Este proyecto es un caso de estudio sobre la implementación de **10 estrategias avanzadas de RAG** (Recuperación Aumentada por Generación) para resolver problemas complejos de una Ciudad Inteligente.

![9 ARQUITECTURAS RAG](./imagenes/ArquitecturaRAG.png)

Esta arquitectura representa un sistema de IA de Grado Industrial. Se basa en el desacoplamiento de responsabilidades: el **Frontend** gestiona la experiencia,el **Backend** orquesta la lógica, y los **Engines** ejecutan las estrategias específicas de RAG.

![ARQUITECTURA DEL SISTEMA](./imagenes/Arquitecto_Sistema.png)

Este es un proyecto a gran escala. Para mantenerlo manejable y profesional, utilizaremos una arquitectura modular donde cada tipo de RAG es un **Motor** (Engine) independiente, orquestado por FastAPI y visualizado con Streamlit, utilizando exclusivamente el 
ecosistema de Hugging Face (Transformers, Datasets, Inference API).

![DIRECTORIO](./imagenes/Directorio.png)