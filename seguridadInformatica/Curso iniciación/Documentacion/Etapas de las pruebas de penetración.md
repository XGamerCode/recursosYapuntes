
tags: #informacion

---

![[Grafico_fases_prueba_penetracion.png]]

- 1 Pre-compromiso: 
					En este primer punto se planea con el cliente el contrato y los distintos puntos que entraran en esta prueba de penetración.
					Además se discutirán los **objetivos**, **alcance**, **estimación de tiempo** y **reglas a seguir**
- 2 Recopilación de información:
					Buscamos información sobre la empresa objetivo, el software y hardware en uso para encontrar posibles brechas de seguridad que podamos aprovechar.
- 3 Evaluación de vulnerabilidades:
					En esta etapa utilizamos la información obtenida en la etapa anterior, buscando vulnerabilidades conocidas en el sistema, tanto manualmente como haciendo uso de herramientas automatizadas. 
- 4 explotación:
					Probamos los ataques en los potenciales vectores de ataque descubiertos en el paso anterior, contra los sistemas objetivos para obtener acceso inicial.
- 5 Post-Explotación:
					En esta fase se busca obtener una escalación de privilegios, y garantizar la reentrada al sistema.
- 6 Movimiento lateral:
					Este paso consiste en, una vez obtenido el control de una maquina, repetir iterativamente los pasos anteriores con el objetivo de movernos en la red interna de host para ganar acceso a maquinas de esa red hasta alcanzar nuestro objetivo.
- 7 Prueba de concepto:
					Aquí deberemos generar la documentación que servirá como reporte de como logramos llegar a ese objetivo, detallando todos los pasos seguidos con el mayor detalle posible. 
- 8 Post-compromiso:
					En este punto deberemos limpiar todo el rastro que hayamos podido generar con todo el progreso seguido.