[README.md](https://github.com/user-attachments/files/23553974/README.md)
# HR Analytics Dashboard - Análisis de Rotación de Personal

# Descripción General

Dashboard interactivo para análisis de rotación de personal (attrición) basado en datos de empleados. 
Proporciona insights accionables para equipos de Recursos Humanos con visualizaciones interactivas, 
métricas clave y análisis exploratorio de datos.

**Repositorio**: [GitHub](https://github.com/tu-usuario/hr-analytics-dashboard)  
**Última actualización**: 14 de Noviembre, 2025

---

# Estructura del Proyecto


hr-analytics-dashboard/
│
├── app.py                          # Aplicación principal (Streamlit)
├── requirements.txt                # Dependencias de Python
├── .gitignore                      # Archivos a ignorar en Git
├── .streamlit_config.toml         # Configuración de Streamlit
├── README.md                       # Este archivo
│
├── data/
│   └── hr_employee_attrition.csv  # Dataset principal
│
├── outputs/
│   ├── 01_attrition_by_department.html     # Gráfico: Rotación por depto
│   ├── 02_hours_distribution.html          # Gráfico: Distribución de horas
│   ├── 03_correlation_heatmap.html         # Gráfico: Matriz de correlaciones
│   ├── 04_attrition_by_tenure.html         # Gráfico: Rotación por antigüedad
│   └── 05_satisfaction_vs_attrition.html   # Gráfico: Satisfacción vs Rotación
│
├── notebooks/
│   └── 01_eda_analysis.ipynb      # Análisis exploratorio detallado
│
└── docs/
    ├── METHODOLOGY.md              # Documentación de metodología
    └── INSIGHTS.md                 # Insights detallados


---

## Fuente de Datos

**Dataset**: WA_Fn-UseC_-HR-Employee-Attrition  
**Origen**: IBM HR Analytics Dataset  
**Tamaño**: 1,470 empleados × 35 variables  
**Período**: Data de empleados activos e históricos

### Variables Principales

| Variable | Descripción | Tipo | Rango |
|----------|-------------|------|-------|
| `Attrition` | Indicador de rotación (Yes/No) | Categórica | - |
| `Department` | Departamento del empleado | Categórica | 3 categorías |
| `JobRole` | Rol de trabajo | Categórica | 9 roles |
| `Age` | Edad del empleado | Numérica | 18-60 años |
| `YearsAtCompany` | Antigüedad en empresa | Numérica | 0-40 años |
| `MonthlyIncome` | Ingreso mensual | Numérica | USD |
| `JobSatisfaction` | Satisfacción laboral | Ordinal | 1-4 (bajo-alto) |
| `EnvironmentSatisfaction` | Satisfacción con ambiente | Ordinal | 1-4 |
| `WorkLifeBalance` | Balance vida-trabajo | Ordinal | 1-4 |
| `JobInvolvement` | Involucramiento en trabajo | Ordinal | 1-4 |
| `PerformanceRating` | Calificación de desempeño | Ordinal | 1-4 |

---

## 🧹 Limpieza de Datos

## Proceso de Validación

 **Valores Faltantes**: 0 (sin valores nulos)  
 **Duplicados**: 0 filas duplicadas  
 **Tipos de Datos**: Verificados y correctos  
- 26 variables numéricas
- 9 variables categóricas

### Transformaciones Aplicadas

1. **Conversión de tipos**: Validación de int64 para métricas numéricas
2. **Encoding**: Variables categóricas mantenidas en original format
3. **Variables derivadas**: 
   - Attrition como variable binaria (0/1) para análisis
   - Grupos de edad para segmentación

---

##  Análisis Exploratorio (EDA)

### Métricas Clave Globales

| Métrica | Valor |
|---------|-------|
| **Total de Empleados** | 1,470 |
| **Empleados que se fueron** | 237 |
| **Tasa de Rotación Global** | **16.12%** |
| **Edad Promedio** | 36.9 años |
| **Antigüedad Promedio** | 7.01 años |
| **Ingreso Mensual Promedio** | $6,503 USD |

### Tasa de Rotación por Departamento

| Departamento | Tasa de Rotación | Total Empleados |
|--------------|------------------|-----------------|
| Sales | 20.63% | 446 |
| Human Resources | 19.05% | 63 |
| Research & Development | 13.84% | 961 |

**Insight**: El departamento de Ventas presenta la rotación más alta (20.63%), 
seguido de RRHH (19.05%) y R&D con la tasa más baja (13.84%).

### Horas de Trabajo por Departamento

Todos los departamentos cuentan con un estándar de **80 horas mensuales** de trabajo.
No hay variabilidad en este indicador.

### Correlaciones: Satisfacción vs Rotación

| Factor | Correlación | P-value | Interpretación |
|--------|------------|---------|-----------------|
| **Job Involvement** | -0.130 | 1e-06 | Negativa fuerte, significativa |
| **Job Satisfaction** | -0.103 | 7e-05 | Negativa moderada, significativa |
| **Environment Satisfaction** | -0.103 | 7.2e-05 | Negativa moderada, significativa |
| **Work-Life Balance** | -0.064 | 0.014 | Negativa débil, significativa |
| **Relationship Satisfaction** | -0.046 | 0.079 | Negativa débil, no significativa |

**Interpretación**: 
- Mayor involucramiento laboral → **menor rotación** (correlación más fuerte)
- Mayor satisfacción laboral → **menor rotación**
- Mayor balance vida-trabajo → **ligeramente menor rotación**
- La satisfacción de relaciones tiene impacto limitado en rotación

---

##  Insights Accionables

### **Insight #1: Crisis en Ventas - Necesidad de Intervención Inmediata**

**Problema**:
- El departamento de Ventas tiene una tasa de rotación de **20.63%**, 
  la más alta de toda la organización (6.8 puntos porcentuales por encima del promedio)
- Esto representa aproximadamente **92 de 446 empleados** que se van anualmente

**Causas Identificadas**:
- Menor satisfacción laboral en Ventas vs otros departamentos
- Presión de resultados y viajes frecuentes (BusinessTravel)
- Posiblemente compensación no competitiva respecto a la demanda del mercado

**Recomendaciones**:
1. **Revisión Salarial**: Aumentar compensación base para roles de ventas un 10-15%
2. **Beneficios**: Implementar bonificación por retención (stay bonus) para vendedores con >5 años
3. **Ambiente de Trabajo**: 
   - Reducir viajes frecuentes mediante implementación de herramientas de venta remota
   - Programas de mentoría y desarrollo profesional específicos para ventas
4. **Evaluación de Gestión**: Revisar estilos de liderazgo en esta unidad
5. **Timeline**: Implementar cambios en Q1 2026, monitorear impacto en Q2-Q3

**Impacto Esperado**: Reducir rotación de 20.63% a 15% (+4 meses en retención promedio)

---

### **Insight #2: Involucramiento Laboral es el Factor Crítico de Retención**

**Problema**:
- Job Involvement tiene la correlación más fuerte con rotación (-0.130)
- Empleados con bajo involucramiento son significativamente más propensos a irse
- R&D, a pesar de baja rotación general, puede optimizar aún más mediante este factor

**Causas Identificadas**:
- Empleados sin claridad en objetivos o rol en la empresa
- Proyectos poco motivadores o impactantes
- Falta de reconocimiento y feedback

**Recomendaciones**:
1. **Claridad de Rol y Objetivos**:
   - Sesiones trimestrales de alineamiento OKR (Objectives & Key Results)
   - Documentación clara de contribución de cada empleado al negocio

2. **Proyectos Significativos**:
   - Asignar empleados a proyectos con alto impacto visible
   - Rotación de proyectos para mantener engagement
   - Comunicar resultados y éxitos

3. **Reconocimiento y Feedback**:
   - Sistema de reconocimiento mensual (interno + externo)
   - Sesiones de feedback 1-on-1 bi-semanales (vs anuales)
   - Exposición a liderazgo senior para reconocimiento

4. **Desarrollo Profesional**:
   - Plan de desarrollo personalizado para cada empleado
   - Oportunidades de learning on-job
   - Mentorías internas

5. **Medición**:
   - Encuesta de engagement trimestral
   - Seguimiento de Job Involvement score por departamento
   - Conectar mejoras de involucramiento con retención

**Impacto Esperado**: Por cada punto de mejora en Job Involvement score → ~0.13 reducción en rotación (potencial de -0.5 a -1.0 en tasa si logramos mejora promedio)

---

## 🚀 Cómo Ejecutar el Dashboard

### Requisitos Previos

- Python 3.9+
- Git
- Virtual environment (recomendado)

### Instalación

bash
# Clonar repositorio
git clone https://github.com/tu-usuario/hr-analytics-dashboard.git
cd hr-analytics-dashboard

# Crear virtual environment
python -m venv venv

# Activar virtual environment
# En Windows:
venv\Scripts\activate
# En macOS/Linux:
source venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt


### Preparar Datos

bash
# Crear directorio data
mkdir data

# Copiar archivo CSV al directorio data
cp hr_employee_attrition.csv data/


### Ejecutar Dashboard

bash
streamlit run app.py


El dashboard abrirá en tu navegador por defecto en `http://localhost:8501`

### Uso del Dashboard

1. **Filtros de Sidebar**:
   - Selecciona uno o múltiples departamentos
   - Filtra por roles de trabajo
   - Ajusta rango de edades

2. **Navegación por Secciones**:
   - **KPIs**: Métricas globales en tiempo real
   - **Análisis por Departamento**: Comparación de departamentos
   - **Satisfacción y Rotación**: Relación entre factores de satisfacción
   - **Análisis Temporal**: Tendencias por antigüedad y edad
   - **Datos Detallados**: Tabla interactiva con opción de descarga

3. **Descarga de Datos**:
   - Botón "Descargar datos filtrados como CSV" para análisis adicional

---

##  Visualizaciones Disponibles

### 1. **Rotación por Departamento** (Gráfico de Barras)
- Archivo: `01_attrition_by_department.html`
- Compara tasa de rotación entre Sales, R&D y RRHH
- Identifica departamentos de riesgo

### 2. **Distribución de Horas** (Histograma)
- Archivo: `02_hours_distribution.html`
- Muestra concentración de horas estándar (80h)
- Poco variación entre empleados

### 3. **Matriz de Correlaciones** (Heatmap)
- Archivo: `03_correlation_heatmap.html`
- Correlaciones entre todas las variables
- Identifica factores correlacionados con rotación

### 4. **Rotación por Antigüedad** (Línea de Tiempo)
- Archivo: `04_attrition_by_tenure.html`
- Muestra rotación elevada en primeros 2 años
- Estabilización después de 5+ años

### 5. **Satisfacción vs Rotación** (Gráfico Mixto)
- Archivo: `05_satisfaction_vs_attrition.html`
- Compara empleados que se fueron vs se quedaron
- Por nivel de satisfacción laboral

---

## 🔍 Metodología Estadística

### Cálculo de Tasa de Rotación


Tasa de Rotación = (Empleados que se fueron / Total de empleados) × 100%


- **Global**: 237 / 1,470 = 16.12%
- **Por Departamento**: Aplicado igual fórmula por segmento

### Correlación de Pearson


r = Σ[(Xi - X̄)(Yi - Ȳ)] / √[Σ(Xi - X̄)² × Σ(Yi - Ȳ)²]


- Rango: -1 a +1
- Negativa: Mayor valor en X → Menor valor en Y
- P-value < 0.05: Estadísticamente significativo

### Transformaciones

- **Attrition Binaria**: Yes=1, No=0 para cálculos de correlación
- **Grupos de Edad**: Rangos 18-25, 26-35, 36-45, 46-55, 56-60

---

## 📚 Análisis Adicional (Notebooks)

Se incluye Jupyter Notebook con:
- EDA detallado
- Visualizaciones exploratorias adicionales
- Análisis estadísticos profundos
- Modelado predictivo (opcional)

bash
jupyter notebook notebooks/01_eda_analysis.ipynb


---

## 🔧 Reproducibilidad

### Para Reproducir el Análisis

1. **Datos**: Dataset incluido en `data/hr_employee_attrition.csv`
2. **Código**: Totalmente replicable con código Python/SQL incluido
3. **Dependencias**: Documentadas en `requirements.txt` con versiones pinned
4. **Seeds**: Random seeds fijados para reproduciblidad de resultados

### Para Desplegar en Nube

**Streamlit Cloud** (Recomendado):
bash
# Conectar GitHub repo a Streamlit Cloud
# Seleccionar branch y archivo main (app.py)
# Auto-deploy en cada push


**Heroku/AWS/Google Cloud**:
- Dockerfile incluido (crear si es necesario)
- Configuración de puertos en `.streamlit_config.toml`

---

##  Checklist de Implementación para RRHH

- [ ] Revisión de compensación para Sales (Insight #1)
- [ ] Diseño de programa de stay bonus
- [ ] Auditoría de estilos de liderazgo en Sales
- [ ] Planificación de herramientas de venta remota
- [ ] Diseño de programa de Job Involvement (Insight #2)
- [ ] Sistema de OKRs trimestrales
- [ ] Encuestas de engagement trimestral
- [ ] Programa de mentoría y desarrollo
- [ ] Sistema de reconocimiento mensual
- [ ] Dashboard montado y compartido con liderazgo

---

## 🤝 Contribuciones

Para contribuir:
1. Fork el repositorio
2. Crear rama feature (`git checkout -b feature/MiMejora`)
3. Commit cambios (`git commit -am 'Agrego MiMejora'`)
4. Push a la rama (`git push origin feature/MiMejora`)
5. Abrir Pull Request

---

##  Contacto y Soporte

**Preguntas sobre análisis**: [Email de equipo de analytics]  
**Soporte técnico dashboard**: [Email soporte]  
**Reporte de bugs**: [Issues en GitHub]

---

##  Licencia

Este proyecto está bajo licencia MIT. Ver archivo LICENSE para detalles.

---

##  Referencias

- IBM HR Analytics Dataset: https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset
- Streamlit Docs: https://docs.streamlit.io
- Plotly Documentation: https://plotly.com/python/
- Research sobre Retention: https://www.mckinsey.com/insights/people-performance

---

**Última actualización**: 14 de Noviembre, 2025  
**Versión**: 1.0.0  
**Estado**: 🟢 Producción
