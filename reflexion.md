# Reflexión

## Casos que fallaron y correcciones

Durante las primeras pruebas encontré varios problemas que tuve que corregir. El primero fue que el agente interpretaba mi solicitud inicial como una confirmación y llegaba a agendar una cita en el mismo mensaje. Para solucionarlo, reforcé el system prompt: primero debe consultar disponibilidad, resumir la información y esperar una confirmación explícita en un mensaje posterior.

También detecté que el workflow de agendamiento generaba citas duplicadas. El problema era que el nodo Code se ejecutaba una vez por cada cita que leía de la tabla. Cambié su modo a `runOnceForAllItems`, agregué una validación de disponibilidad justo antes de guardar y cancelé los registros de prueba que se habían duplicado.

Por último, en una prueba de horario fuera de servicio el agente respondió de forma demasiado general. Agregué una instrucción para que siempre consulte la tool de disponibilidad y explique claramente cuando un servicio terminaría después de las 20:00.

## Limitación no resuelta

Decidí usar Simple Memory porque era la alternativa más sencilla para este proyecto. Sin embargo, esta memoria se pierde cuando se reinicia n8n, por lo que el agente no conserva conversaciones entre reinicios. También dependí de la cuota gratuita y de la disponibilidad de Gemini; durante las pruebas alcancé el límite de solicitudes y un modelo alternativo presentó alta demanda temporal.

## Cambios para producción

Si este agente se utilizara con clientes reales, cambiaría Simple Memory por una memoria persistente y agregaría autenticación para que cada cliente solo pueda consultar sus propias citas. También protegería datos personales, usaría un calendario real, agregaría control de concurrencia para evitar reservas simultáneas y configuraría monitoreo, reintentos y una API con facturación para no depender de cuotas gratuitas.

## Trabajo realizado

Realicé el proyecto de forma individual. Me encargué del diseño del agente, la configuración de Gemini, la creación de las Data Tables, los workflows auxiliares, el workflow principal, las pruebas, las correcciones, las evidencias y la documentación final.
