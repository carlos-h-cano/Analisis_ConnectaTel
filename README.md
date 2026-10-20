# Análisis ConnectaTel

## Qué problema se resuelve

Este proyecto analiza el comportamiento de uso de llamadas y mensajes de los clientes de **ConnectaTel** (operaciones en México y Colombia).  

El objetivo es:
- Identificar patrones de uso por tipo de plan y segmento de cliente.
- Detectar valores atípicos y problemas de calidad de datos.
- Segmentar a los usuarios por nivel de uso y edad.
- Generar recomendaciones accionables para optimizar la oferta de planes.


# Cómo está organizado el proyecto
├── datasets/
│   ├── plans.csv          # Planes disponibles (Básico y Premium)
│   ├── users_latam.csv    # Datos de usuarios
│   └── usage.csv          # Registros de uso (llamadas y mensajes)
├── analysis.ipynb         # Notebook principal con todo el análisis
└── README.md

### Flujo del análisis

1. **Carga de datos**  
   Lectura de `plans`, `users` y `usage`.

2. **Calidad de datos**  
   - Revisión de nulos.  
   - Corrección de sentinels (`age = -999`, `city = "?"`).  
   - Fechas fuera de rango marcadas como `NaT`.  
   - Nulos en `duration` y `length` identificados como MAR (dependen del tipo de registro).

3. **Construcción del perfil de usuario**  
   Agregación de uso por `user_id` y unión con la tabla de usuarios (`user_profile`).

4. **Análisis estadístico y visual**  
   - Resumen estadístico de variables numéricas.  
   - Histogramas por plan.  
   - Boxplots e identificación de outliers (método IQR).  
   - Decisión: mantener outliers de uso alto por ser consumo real.

5. **Segmentación**  
   - `grupo_uso`: Bajo uso / Uso medio / Alto uso.  
   - `grupo_edad`: Joven / Adulto / Adulto Mayor.

6. **Insights y recomendaciones**  
   Análisis ejecutivo orientado a stakeholders.

## Cómo reproducir el análisis

### Requisitos

- Python 3.8+
- Librerías: `pandas`, `numpy`, `matplotlib`, `seaborn`

```bash
pip install pandas numpy matplotlib seaborn
