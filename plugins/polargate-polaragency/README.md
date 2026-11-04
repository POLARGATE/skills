# PolarAgency

Una agencia entera dentro de Claude Code: 283 especialistas de IA en 18 departamentos (marketing, ventas, anuncios, diseño, producto, proyectos, atención y soporte, finanzas y más).

Le pides lo que necesitas con tus palabras («escríbeme un correo para conseguir clientes», «planifícame la campaña de noviembre») y Claude elige al especialista que toca y le pasa el trabajo. Te entrega un borrador; nada se envía ni se publica sin que lo digas.

## Instalar

En Claude Code:

```
/plugin marketplace add POLARGATE/skills
/plugin install polargate-polaragency@polargate
```

## Créditos

Basada en [agency-agents](https://github.com/msitarzewski/agency-agents), de AgentLand Contributors, con licencia MIT, a partir del commit `b37b5bb33b78`. Cambiamos: índice en español por departamentos, reglas de Polargate y reparto del trabajo entre especialistas. Los ficheros de los especialistas son los originales, en inglés.

Sustituye a «Ponle un experto»: trae sus 36 especialistas como «los más usados» y el resto por departamento. Si tenías aquella instalada, cámbiala:

```
/plugin uninstall polargate-ponle-un-experto@polargate
/plugin install polargate-polaragency@polargate
```

Es de [Polargate](https://polargate.ai) y está en la [Biblioteca](https://biblioteca.polargate.ai).
