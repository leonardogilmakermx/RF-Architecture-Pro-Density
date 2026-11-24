# RF Architecture Pro — Consola Profesional de Análisis de RF para Alta Densidad (v3.2)

Herramienta web interactiva de ingeniería y simulación RF diseñada para el dimensionamiento, optimización y auditoría de redes Wi-Fi de alta densidad (arenas, centros de convenciones, estadios, auditorios y recintos masivos) en las bandas de **2.4 GHz**, **5 GHz** y **6 GHz**.

**Autor:** Ing. Gilberto Leonardo Domínguez García — *Wireless Infrastructure Architect*  
**Organización:** RedCorp 802.11 México  

---

## Características Principales

### 1. Regulación de Frecuencias por País y Validador PSD 6 GHz LPI
* **Dominios regulatorios integrados:** México (**IFT**), EE. UU. / Canadá (**FCC**), Europa / UK (**ETSI**), Brasil / LATAM 6G (**ANATEL**) y Japón (**MIC**).
* **5 GHz (DFS y No-DFS):** Filtra automáticamente los canales permitidos por país y ancho de canal (`20`, `40`, `80` y `160 MHz`), permitiendo incluir o excluir canales DFS.
* **6 GHz (UNII-5 vs. Espectro Completo):** Diferencia entre países limitados a **UNII-5** (canales `1–93`, 24 canales @ 20 MHz) y países con espectro completo **UNII-5 a UNII-8** (canales `1–233`, 59 canales @ 20 MHz).
* **Validador PSD en 6 GHz LPI:** Detecta en tiempo real si el EIRP configurado excede el límite legal de densidad espectral de potencia (ej. $5\text{ dBm/MHz} \implies 18\text{ dBm EIRP}$ en $20\text{ MHz}$ para IFT/FCC/ANATEL; $23\text{ dBm EIRP}$ en ETSI/MIC) e incluye un botón de ajuste automático de un clic.

### 2. Modelado de Antenas Sectoriales de Doble Plano (`H × V`)
* **Montaje Techo hacia el Piso (`-Z`):** Proyecta la huella real en forma de **elipse `-3 dB`** ($r_H = h_{\text{ef}} \cdot \tan(BW_H/2)$ y $r_V = h_{\text{ef}} \cdot \tan(BW_V/2)$) con rotación configurable y cálculo parabólico combinado en ambos planos ortogonales.
* **Montaje Muro / Grada Lateral:** Proyecta el abanico direccional según el ángulo de **Azimut (`0°–360°`)**, separando la apertura horizontal ($BW_H$) y vertical ($BW_V$).
* **Control de limpieza visual:** Casilla `Haz -3 dB` en la barra de herramientas para ocultar o mostrar las líneas punteadas y etiquetas de distancia tanto en el plano de trabajo como al exportar a PDF.

### 3. Edición Manual de APs e Inspector Individual (`⚙ Editar AP`)
Además del sembrado automático por capacidad y cobertura, la consola permite ajustar el diseño manualmente dentro del polígono válido:
* **Herramientas en plano:** **Mover AP**, **Añadir AP** (validado dentro del área delimitada), **Quitar AP** y restaurar a **Auto-Sembrado**.
* **Control Individual de Radios:** En modo **Wi-Fi 7 (MLO)** habilita 3 radios independientes (`2.4 / 5 / 6 GHz`); en **Wi-Fi 6 / 5 (Estándar)** habilita 2 radios (`2.4 / 5 GHz`). Apagar un radio excluye al AP del mapa de calor, la asignación de canales y el CCI de esa banda.
* **Parámetros individuales por AP:**
  * **Altura Z (`0.5 m` a `45 m`):** Para recintos con techos a distinto nivel (mezzanines, gradas, camerinos, pista principal), recalculando dinámicamente el *Slant Path* 3D y la elipse `-3 dB`.
  * **Potencia Tx (`1` a `30 dBm`)** y **Rotación / Azimut (`0°` a `360°`)**.

### 4. Balanceo Estricto de Canales + Refinamiento Espacial (*Swap Pass*) + CCI 3D
* **Fase 1 (Asignación Balanceada):** Reparte equitativamente los canales disponibles entre los radios activos (evitando desbalances y asegurando distribuciones óptimas como `4-4-3` en 2.4 GHz o `2-2-3` en 5 GHz).
* **Fase 2 (*Swap Pass*):** Ejecuta pasadas de intercambio entre pares de APs para maximizar la distancia 3D mínima entre vecinos co-canal sin alterar el balance.
* **Cálculo automático de CCI:** Evalúa la contención co-canal real usando un umbral de detección de señal (`-82 dBm` CCA-SD ajustado por ancho de canal), ganancia de antena, aislamiento lateral y atenuación por densidad humana.

### 5. Agente Móvil "Flyer Wifi" y Telemetría en Tiempo Real
* **Perfiles de dispositivo con offset real:**
  * Laptop / MacBook (`-3 dB` Offset)
  * Smartphone / Celular (`-10 dB` Offset)
  * Terminal IoT / POS (`-11 dB` Offset)
* **Métricas en vivo:** RSSI percibido, RSSI bruto del AP, SINR, CCI, Throughput neto, utilización de Airtime y modulación exacta (**`MCS 10-11 (1024-QAM)`** para Wi-Fi 6/5 y **`MCS 12-13 (4K-QAM)`** para Wi-Fi 7 MLO).
* **5 Gráficas analíticas:** RSSI Ideal 2D, RSSI Real 3D, Throughput Neto por Celda, Utilización de Airtime y Capacidad de Dispositivos Simultáneos (WhatsApp, HD Video y 4K Stream).

### 6. Flujo CAD, Persistencia `.hdwp` y Reportes Ejecutivos PDF/CSV
* **Plano Maestro CAD:** Importación de planos arquitectónicos, control de opacidad, calibración métrica en 2 clics, trazado de polígonos irregulares con bloqueo de cruces, zoom y paneo.
* **Proyectos Portables (`.hdwp` v3.2):** Guarda e importa todos los parámetros RF, país regulatorio, polígono irregular, APs editados manualmente (con sus alturas Z, radios, Tx y rotación) y plano opcional.
* **Exportación Profesional:**
  * **CSV (Excel):** Tabla ejecutiva completa con coordenadas `(X, Y, Z)`, radios activos, canal, sub-banda, EIRP, rotación y dimensiones de la elipse `-3 dB`.
  * **Reporte PDF Optimizado:** Impresión directa con alto contraste garantizado en el lienzo (`#090d16`), ejes `X/Y` siempre visibles, gráficas sin recortes y tabla ejecutiva compacta sin saltos de línea irregulares.

---

## Guía Rápida de Uso

1. **Abrir la aplicación:** Ejecuta `index.html` directamente en cualquier navegador moderno (Chrome, Edge, Firefox) sin necesidad de servidor ni instalación.
2. **Importar y calibrar el plano:** Haz clic en `1. Plano` para cargar la imagen del recinto y usa `2. Calibrar` marcando dos puntos con distancia conocida en metros.
3. **Delimitar el área:** Selecciona `3. Polígono`, traza el perímetro del recinto y cierra el polígono para generar el sembrado automático de APs.
4. **Ajustar parámetros RF:** Selecciona País, Tecnología, Banda, Ancho de Canal, Antena (`H × V`) y Aforo, o pulsa **⚡ AUTO-OPTIMIZAR A META**.
5. **Ajuste fino (Toque Humano):** Usa `⚙ Editar AP`, `✥ Mover`, `➕ Añadir` y `🗑 Quitar` para adaptar los equipos a la arquitectura real y apagar radios redundantes (ej. en 2.4 GHz para terminales POS).
6. **Guardar y reportar:** Exporta el proyecto en `.hdwp`, descarga la tabla en `.csv` o genera el reporte ejecutivo en PDF.

---

## Novedades de la Versión 3.2
* **Motor de impresión PDF de alto contraste:** Fondo oscuro renderizado directamente en `<canvas>` y `print-color-adjust: exact` para preservar ejes `X/Y`, canales y etiquetas al exportar.
* **Tabla ejecutiva compacta:** Reglas `white-space: nowrap` en columnas críticas (`ID AP`, coordenadas, radios, potencia y carga) para evitar saltos de línea en PDF.
* **Presets genéricos:** Limpieza de etiquetas en el selector de aforo (hasta 100,000 dispositivos) y nombres sugeridos de proyecto `.hdwp`.

---

## Licencia y Autoría
Proyecto desarrollado por **Ing. Gilberto Leonardo Domínguez García** (*RedCorp 802.11 México*). Todos los derechos reservados © 2026.
