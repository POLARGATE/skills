---
name: polargate-preve-tus-numeros
description: Saca una previsión de ventas, reservas, demanda, visitas, ingresos o gastos a partir de un Excel o CSV con fechas, con una horquilla de lo normal, usando TimesFM 2.5 de Google en el propio ordenador y sin entrenar nada. Usar cuando alguien pida prever, proyectar o estimar cómo irá un número en las próximas semanas o meses, cuánto stock pedir, o «cuánto venderé el mes que viene». Los datos no salen del ordenador.
---

# Prevé tus números

Lee `REGLAS.md` antes de empezar.

## Si falta en este ordenador

Hazlo tú, sin pedírselo a la persona. Avísale antes de que baja unos 1,5 GB entre programas y modelo, y que solo pasa la primera vez.

```bash
python3 --version   # hace falta 3.10 o más nuevo
python3 -m venv ~/.polargate/prever
~/.polargate/prever/bin/pip install -q "timesfm[torch] @ git+https://github.com/POLARGATE/timesfm@e51928e27119cb17bebc005be2696b75e0a9e688" pandas psutil openpyxl
```

Si falta Python, dile cómo instalarlo en su sistema y espera.

## Cómo se hace

1. **Mira los datos.** Si es un Excel, pásalo a CSV. Busca la columna de fecha y la del número. Comprueba que las fechas van seguidas, y mira huecos, duplicados y filas de totales. Di qué has limpiado.
2. **Comprueba que hay bastante historia.** Con menos de 30 datos el resultado vale poco: dilo. Para que se vea la temporada, hacen falta al menos dos años de datos mensuales.
3. **Pregunta solo lo que falte:** hasta cuándo quiere ver.
4. **Lanza la previsión.** `<carpeta>` es la de este fichero.

```bash
~/.polargate/prever/bin/python <carpeta>/scripts/forecast_csv.py datos.csv --date-col fecha --value-cols ventas --horizon 6 --output prevision.csv
```

`--horizon` es cuántos pasos hacia delante: 6 son 6 meses si los datos son mensuales.

5. **Compruébala.** Si hay historia de sobra, guarda aparte el último trozo, prevé ese trozo y compáralo con lo que pasó de verdad. Di cuánto se equivocó, en lenguaje normal: «en los últimos 6 meses falló de media un 8 %».
6. **Enséñala.** Una tabla corta y un gráfico sencillo con el histórico, la previsión y la horquilla `lower_80` a `upper_80`. Explícala así: «lo normal es que quede entre X e Y».

Detalles técnicos, si algo falla: `referencias/preparar-datos.md`, `referencias/requisitos.md` y `referencias/guia-tecnica.md`.

## Licencia

Los avisos de licencia están en el `LICENSE` y el `NOTICE.md` del plugin.
