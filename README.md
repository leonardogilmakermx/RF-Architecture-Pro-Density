# RF Architecture Pro - High Density Full Analysis Console 📶

**Diseñado por:** Ing. G. Leonardo Dominguez Garcia  
**Especialidad:** Wireless Infrastructure Architect | RedCorp 802.11 México

## 🚀 Descripción del Proyecto
Esta consola de análisis profesional permite realizar simulaciones predictivas de cobertura, utilización de **Airtime** y **QoE** en escenarios de alta densidad (10, 100 y 1,000 usuarios concurrentes). 

A diferencia de las calculadoras estándar de propagación, este algoritmo integra:
- **Trayectoria Slant (Real):** Cálculo de distancia hipotenusa considerando la altura del AP y del cliente.
- **Atenuación por Densidad Humana:** Modelado logarítmico de pérdida de señal según el bloque de personas.
- **Análisis de Airtime dinámico:** Impacto de la interferencia Co-Canal (CCI) y degradación por señales bajas.

## 🛠️ Especificaciones Técnicas
- **Frecuencias soportadas:** 2.4 GHz, 5.2 GHz y 6.0 GHz (Wi-Fi 6E/7 ready).
- **Métricas calculadas:** - **RSSI (Horizontal vs Real):** Visualización del desvanecimiento de señal.
  - **Throughput Neto:** Estimación de capacidad real tras descontar overhead y colisiones.
  - **Capacidad por Servicio:** Cálculo de cuántos usuarios simultáneos soporta el AP para WhatsApp, HD Video y 4K Streaming.

## 📊 Algoritmo de Cálculo (RF Logic)
El simulador utiliza la fórmula de Free Space Path Loss (FSPL) ajustada por factores de absorción biológica:

$$FSPL = 20\log_{10}(d) + 20\log_{10}(f) + 32.44$$
$$RSSI = P_{tx} - FSPL - Atten_{Human}$$

## 💻 Instalación
El proyecto es una **Consola Web Monolítica**. No requiere dependencias de servidor:
1. Clonar el repositorio.
2. Abrir `index.html` en cualquier navegador moderno.
3. (Opcional) Ejecutar en modo local para generar reportes en PDF.

## 📄 Licencia
Este software es propiedad intelectual de **RedCorp 802.11 México**. Ver archivo LICENSE para más detalles.