# Bitcoin Power Law

Un notebook de Jupyter que ajusta la Ley de Potencias de Bitcoin a los precios diarios y la dibuja en gráficos fáciles de leer de un vistazo.

```
precio ≈ A × (días desde el bloque génesis) ^ n
```

El bloque génesis es el día 0 (3 de enero de 2009). En un gráfico log-log esa curva se convierte en una línea recta. El notebook ajusta la línea, mide qué tan bien se sostiene y muestra dónde está el precio de hoy frente a ella. El exponente ajustado sale cerca de `n ≈ 5.6`.

Preview
<img width="1638" height="652" alt="image" src="https://github.com/user-attachments/assets/181774cb-b66d-4a0d-a41c-96d6af1964ef" />

## Archivos

| Archivo                   | Qué es                                       |
| ------------------------- | -------------------------------------------- |
| `bitcoin_power_law.ipynb` | El notebook. Ejecuta este.                   |
| `BTC_daily.csv`           | Precios de cierre diarios de BTC (`Date,Price`) |
| `requirements.txt`        | Paquetes de Python que necesita              |

Preview
<img width="1309" height="648" alt="image" src="https://github.com/user-attachments/assets/7a53d8f2-fd39-4bb7-8ade-af0156986699" />

## Cómo ejecutarlo

```bash
# 1. (opcional) crea un entorno aislado
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 2. instala los paquetes
pip install -r requirements.txt

# 3. abre el notebook
jupyter notebook bitcoin_power_law.ipynb
```

Ejecuta las celdas de arriba hacia abajo con Shift+Enter.

Al abrirlo, la primera celda revisa la última fecha del CSV. Si está atrasada, baja los días que faltan desde Yahoo Finance hasta hoy, los agrega al archivo y sigue. Si estás sin conexión, simplemente usa los datos que ya están en el CSV.

Preview
<img width="1270" height="636" alt="image" src="https://github.com/user-attachments/assets/699ae9a2-4b4b-4688-b970-eb52bc3d37d6" />

## Qué muestra cada sección

1. **Cargar los datos.** Lee los precios y cuenta los días desde el bloque génesis.
2. **Ajustar la línea.** Ajusta una línea recta a `log(precio)` frente a `log(días)`. La pendiente es el exponente `n`, el punto de corte da `A`, y `R²` dice qué tan pegados están los precios a la línea.
3. **El gráfico principal.** Los puntos de precio se reparten alrededor de una sola línea recta a lo largo de seis órdenes de magnitud.
4. **El corredor.** Una banda alrededor de la tendencia, con una línea de soporte (el percentil 1 de las diferencias pasadas) y una línea de resistencia (el percentil 99), proyectada hasta 2035. Los precios de soporte, valor justo y resistencia de hoy aparecen en la leyenda.
5. **Histograma.** Cuántos días Bitcoin cotizó a cada distancia de la tendencia, medida en desviaciones estándar. Por debajo de la tendencia es verde, por encima es rojo.
6. **Oscilador.** Las mismas distancias dibujadas en el tiempo para que veas a Bitcoin moverse por encima y por debajo de la tendencia año tras año.
7. **Bandas de percentiles.** Bandas asimétricas del 67% y 95%, ya que las diferencias son más amplias por encima de la tendencia que por debajo. También señala una regla práctica: el precio de tendencia se duplica más o menos cada vez que la edad de Bitcoin crece alrededor de un 13%.
8. **Bandas skew-normal.** Una curva ajustada para las diferencias desbalanceadas, más un acercamiento a los últimos 12 meses.
9. **Métrica de riesgo.** Para cada día, ordena la diferencia de hoy frente a todas las diferencias hasta ese día y la reduce a un puntaje de 0 a 1. 0 es lo más bajo que ha estado Bitcoin frente a la tendencia, 1 es lo más alto. Después viene una versión suavizada, y puedes cambiar la ventana `SMOOTH` a tu gusto.

## Aviso

Esto es una visualización educativa, no un consejo financiero. La ley de potencias es una tendencia descriptiva, no una ley de la naturaleza. Un `R²` alto viene en parte de que dos cosas crecen con el tiempo, el exponente es incierto (alrededor de 5.6 más o menos 0.4) y cambia con la fecha de inicio elegida, y Bitcoin solo tiene una historia corta. La línea puede doblarse o romperse.
