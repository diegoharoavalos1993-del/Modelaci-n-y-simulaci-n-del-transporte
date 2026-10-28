# Simulación 3D de Intersección Semaforizada

Simulación interactiva y visual en 3D de una intersección semaforizada en cruz con calles de un solo sentido, desarrollada bajo la metodología del **Highway Capacity Manual (HCM 2010)**.

---

## 📁 Archivos del Proyecto

- **`index.html`** / **`simulacion-semaforo-responsive.html`**: Versión principal responsive, optimizada tanto para computadoras de escritorio como para tablets y dispositivos móviles (con controles táctiles de rotación y zoom).
- **`simulacion-semaforo.html`**: Versión estándar de la simulación.

---

## 🚀 Cómo Ejecutar

1. Simplemente haz doble clic en **`index.html`** o **`simulacion-semaforo-responsive.html`** para abrirlo en cualquier navegador web moderno (Google Chrome, Edge, Safari, Firefox).
2. No requiere servidores externos ni instalación de dependencias adicionales.

---

## 🎮 Controles y Navegación 3D

- **Rotación 360°**: 
  - *En PC*: Haz clic izquierdo sobre el canvas y arrastra el ratón.
  - *En Móvil*: Desliza con 1 dedo sobre la calzada 3D.
- **Zoom In / Out**: 
  - *En PC*: Rueda del ratón (*scroll*).
  - *En Móvil*: Gesto de pellizco con 2 dedos (*pinch-to-zoom*).
- **Presets de Cámara Rápida**:
  - `🔄 Isométrica`: Vista angular oblicua por defecto.
  - `⬆ Cenital`: Vista en planta superior.
  - `🚗 Calle N-S` y `🚗 Calle E-O`: Perspectivas a nivel de calzada.
- **Pestañas para Móviles**: En pantallas pequeñas, alterna fácilmente entre `🎮 Vista 3D y Resultados` y `⚙️ Parámetros y Ajustes`.

---

## 🚦 Parámetros y Funcionalidades

### ⏱ Tiempos del Semáforo
- **Ciclo Total ($C$)**: Se calcula automáticamente sumando los verdes, ámbares y despejes todo rojo:
  $$C = V_{NS} + V_{EO} + 2 \times \text{Ámbar} + 2 \times \text{Todo Rojo}$$
- Tiempos de verde independientes para Norte-Sur ($V_{NS}$) y Este-Oeste ($V_{EO}$).
- Intervalos de ámbar y todo rojo ajustables.
- Velocidad de simulación ajustable ($1\times$ a $15\times$).

### 🚗 Volúmenes y Capacidad
- Volúmenes independientes por acceso ($50$ a $2200\text{ veh/h}$): Norte $\to$ Sur, Sur $\to$ Norte, Este $\to$ Oeste, Oeste $\to$ Este.
- Flujo de saturación base por carril ($1200$ a $2000\text{ veh/h/carril}$).
- **Carriles por Acceso (1 a 3)**: Al aumentar el número de carriles, la calzada 3D se ensancha dinámicamente y los vehículos forman filas paralelas, incrementando la capacidad y descargando simultáneamente.

### 📈 Metodología de Nivel de Servicio (HCM 2010)
- Cálculo en tiempo real de la demora media por vehículo ($d = d_1 + d_2$):
  - **$d_1$ (Demora Uniforme)**: Modelo simplificado de Webster considerando la relación verde/ciclo ($g/C$) y el grado de saturación ($X = v/c$).
  - **$d_2$ (Demora Incremental)**: Ecuación HCM 2010 para colas aleatorias y sobre-saturación.
- Asignación de Nivel de Servicio (**NDS A a F**):
  - **A**: $d \le 10\text{ s/veh}$
  - **B**: $10 < d \le 20\text{ s/veh}$
  - **C**: $20 < d \le 35\text{ s/veh}$
  - **D**: $35 < d \le 55\text{ s/veh}$
  - **E**: $55 < d \le 80\text{ s/veh}$
  - **F**: $d > 80\text{ s/veh}$ o $v/c > 1.0$ (animación de alerta en rojo).

---

## 📊 Telemetría en Tiempo Real

1. **Semáforo Activo**: Bombilla iluminada (🟢/🟡/🔴), nombre de fase y segundero regresivo.
2. **Ciclo Semafórico**: Tiempo transcurrido ($t / C$) con barra de progreso porcentual.
3. **NDS General**: Demora promedio ponderada ($\bar{d}$) y relación $v/c$ promedio de la intersección.
4. **4 Tarjetas de Acceso**: Estado semafórico por calle, demora por acceso ($d$), grado de saturación ($v/c$), NDS y vehículos acumulados en cola.
