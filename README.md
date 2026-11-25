# RF Architecture Pro v3.6

**Consola profesional de análisis de RF para alta densidad (Wi-Fi 6 / Wi-Fi 6E / Wi-Fi 7 MLO)** diseñada para ingeniería inalámbrica predictiva, dimensionamiento de capacidad, modelado espacial en planos arquitectónicos y validación regulatoria.

Desarrollado por **Ing. Gilberto Leonardo Domínguez García** — *Wireless Infrastructure Architect (RedCorp 802.11 México)*.

---

## Características Principales

### 1. Estándares Wi-Fi y Regulación Espectral por País
* **Tecnologías soportadas:**
  * **Wi-Fi 6 / 5:** 2 radios (2.4 / 5 GHz), modulación hasta 1024-QAM (MCS 10–11).
  * **Wi-Fi 6E:** 3 radios (2.4 / 5 / 6 GHz), anchos de canal hasta 160 MHz, 1024-QAM sin MLO.
  * **Wi-Fi 7 MLO:** 3 radios (2.4 / 5 / 6 GHz), anchos de canal hasta 320 MHz, 4K-QAM (MCS 12–13) y ganancia por agregación Multi-Link Operation.
* **Regulaciones integradas:** México (IFT), EE. UU. / Canadá (FCC), Europa / UK (ETSI), Brasil / LATAM 6G (ANATEL) y Japón (MIC).
* **Control de espectro:** Selección dinámica de canales con/sin DFS en 5 GHz y UNII-5 vs. UNII-5 a UNII-8 en 6 GHz.
* **Validador PSD 6 GHz LPI:** Detecta automáticamente si la EIRP configurada excede el límite legal de densidad espectral de potencia ($5\text{ dBm/MHz}$ en IFT/FCC/ANATEL o $23\text{ dBm}$ EIRP en ETSI/MIC) y ofrece un botón de corrección en un clic.

### 2. Gestión de Overhead de Airtime (Novedad v3.6)
* **Mínimo Data Rate (Basic Rate):** Selector adaptable por banda (`1–24 Mbps` en 2.4 GHz; `6–36 Mbps` en 5 y 6 GHz) para modelar el impacto de las tramas de gestión en el Airtime.
* **DTIM Interval:** Configurable (`1, 2, 3, 5`) para balancear latencia multicast/broadcast y ahorro de batería en dispositivos móviles e IoT.
* **Cantidad de SSIDs (1 a 8):** Multiplica el *Beacon & Probe Response Overhead* en función del número de SSIDs, el Basic Rate y el CCI co-canal.
* **KPI de Beacon Overhead en tiempo real:** Tarjeta dedicada que muestra el porcentaje exacto de Airtime consumido únicamente por Beacons con código de color dinámico:
  * **Verde (< 5%):** Óptimo para alta densidad.
  * **Amarillo (5% – 11.9%):** Overhead moderado.
  * **Rojo (≥ 12%):** Saturación crítica de tramas de gestión.
* **Banner de Alerta de Saturación de Beacons:** Se activa automáticamente al superar **4 SSIDs** o **12% de Beacon Overhead**, con un botón de optimización rápida que ajusta a **3 SSIDs**, **12/24 Mbps** y **DTIM 3**.

### 3. Plano Maestro CAD, Polígonos Irregulares y Control por AP
* **Importación y calibración:** Carga de planos arquitectónicos (PNG/JPG) con control de opacidad, zoom con rueda del ratón, paneo y calibración métrica de 2 puntos.
* **Polígono irregular con bloqueo de cruces:** Delimitación exacta del área de cobertura real ($m^2$) con sembrado automático de APs exclusivamente dentro del polígono.
* **Edición manual e Inspector por AP:**
  * Herramientas para **Mover**, **Añadir** y **Quitar** APs directamente sobre el plano.
  * **Inspector individual (`⚙ Editar AP`):** Permite modificar **Altura Z individual** (recalculando *Slant Path* 3D y elipse `-3 dB`), **Potencia Tx**, **Rotación/Azimut** y **encendido/apagado independiente de radios (2.4 / 5 / 6 GHz)**.
* **Modelado de antenas:** Omnidireccional (`+4 dBi`) y Sectorial HD (`+9 dBi`) en montaje **Techo (-Z)** o **Muro/Grada (Azimut)**, con Beamwidth **H × V** independiente y visualización ocultable de la elipse `-3 dB`.
* **Balanceo estricto de canales + Swap Pass:** Distribuye equitativamente los canales disponibles entre radios activos y realiza intercambios espaciales para maximizar la distancia entre APs co-canal, calculando automáticamente el **CCI** bajo umbral CCA (`-82 dBm`).

### 4. Agente Móvil "Flyer Wifi" y Modelado de Aforo
* **Sonda interactiva arrastrable:** Evalúa en tiempo real RSSI percibido, RSSI de campo del AP, SINR, MCS, Throughput neto y Airtime en cualquier coordenada `(X, Y)`.
* **Perfiles de dispositivo (Offset):** Laptop (`-3 dB`), Smartphone (`-10 dB`) y Terminal IoT/POS (`-11 dB`).
* **Aforo y postura:** Soporte de **1 a 100,000 dispositivos** (con presets y modo comparativo multi-escala) y atenuación corporal según postura (**Parada** 1.75 m, **Sentada** 1.25 m o **Mixta**).
* **Auto-Optimización RF:** Ajusta potencia, ancho de canal (20 MHz), Basic Rate y DTIM para cumplir la meta de borde de celda (`-65`, `-67` o `-69 dBm`) con mínimo CCI.

### 5. Gráficas, Portabilidad (.HDWP) y Entregables
* **5 Gráficas analíticas (Chart.js):**
  1. RSSI Ideal 2D vs. Distancia.
  2. RSSI Real 3D (con Offset de dispositivo y obstrucción corporal).
  3. Throughput Neto por Celda (Mbps).
  4. Utilización de Airtime por Celda (%) con límite de saturación (75%).
  5. Capacidad simultánea por perfil de aplicación (WhatsApp, Video HD, Stream 4K).
* **Archivos de proyecto `.HDWP` (v3.6):** Guarda y restaura todos los parámetros RF (incluyendo DTIM, Basic Rate, SSIDs, edición manual de APs, alturas Z, radios, polígono irregular y plano opcional).
* **Tabla ejecutiva y exportación:** Listado completo de APs con coordenadas `(X, Y, Z)`, radios activos, canal, sub-banda, EIRP y carga estimada, exportable a **CSV (Excel)** y **Reporte PDF** listo para impresión.

---

## Requisitos y Uso

1. **Sin instalación ni servidor:** Es una aplicación autocontenida en un único archivo `index.html`.
2. **Dependencia externa:** Requiere conexión a internet únicamente para cargar `Chart.js` desde CDN (`https://cdn.jsdelivr.net/npm/chart.js`).
3. **Flujo de trabajo recomendado:**
   1. Selecciona tecnología, país regulatorio, banda, ancho de canal, Basic Rate, DTIM y cantidad de SSIDs.
   2. Importa tu plano arquitectónico (`1. Plano`) y calibra la escala en metros (`2. Calibrar`).
   3. Traza el área de cobertura (`3. Polígono`) o presiona **Cálculo de Alta Densidad**.
   4. Ajusta APs individuales (`⚙ Editar AP`), arrastra a **Flyer Wifi** para validar cobertura y exporta tu proyecto (`.hdwp`), plan de frecuencias (`.csv`) o reporte ejecutivo (`PDF`).

---

## Autor

**Ing. Gilberto Leonardo Domínguez García**  
*Wireless Infrastructure Architect — RedCorp 802.11 México*  
© 2026
