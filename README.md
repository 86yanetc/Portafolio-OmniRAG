# 🏙️ OmniRAG: Ecosistema Agéntico SmartCity

**Ecosistema de Inteligencia Artificial Local (Llama-3 8B) para gestión de infraestructura urbana.**

**Nombre: Msc. Yanet Cesaire Velazquez**

## 📂 Documentación Técnica

Para conocer los detalles de arquitectura, desafíos técnicos superados (rutas, amnesia de IA, codificación) y comparativas de rendimiento:

👉 [**Descargar Informe Técnico Completo (PDF)**](./documentos/Informe_Tecnico.pdf)

Este proyecto es un caso de estudio sobre la implementación de **10 estrategias avanzadas de RAG** (Recuperación Aumentada por Generación) para resolver problemas complejos de una Ciudad Inteligente.

![9 ARQUITECTURAS RAG](./imagenes/ArquitecturaRAG.png)

Esta arquitectura representa un sistema de IA de Grado Industrial. Se basa en el desacoplamiento de responsabilidades: el **Frontend** gestiona la experiencia,el **Backend** orquesta la lógica, y los **Engines** ejecutan las estrategias específicas de RAG.

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

10. **Benchmarking PDF:** Pruebas de estrés con documentos de +200 páginas.

![ARQUITECTURA DEL SISTEMA](./imagenes/Arquitecto_Sistema.png)

Este es un proyecto a gran escala. Para mantenerlo manejable y profesional, utilizaremos una arquitectura modular donde cada tipo de RAG es un **Motor** (Engine) independiente, orquestado por FastAPI y visualizado con Streamlit, utilizando exclusivamente el 
ecosistema de **Hugging Face (Transformers, Datasets, Inference API)**.

![DIRECTORIO](./imagenes/Directorio.png)