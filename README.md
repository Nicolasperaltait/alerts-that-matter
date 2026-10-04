# Alerts That Matter

> Alertas que solo suenan por fallos reales, y controles que se verifican por su efecto.

Este repositorio documenta, de forma sanitizada, el stack de observabilidad y
visibilidad de seguridad de una infraestructura productiva personal (homelab): metricas, dashboards,
alertas y SIEM. Incluye un caso real extenso sobre un problema recurrente:
controles automatizados que informaban un resultado que no correspondia con
la realidad.

Es parte de un portfolio tecnico. **No es un laboratorio de prueba**: es una
**infraestructura productiva personal**. Un hipervisor de tipo 1 sobre un
servidor dedicado, encendido 24/7, del que dependen todos los dias la red de la
casa, los backups, la seguridad y aplicaciones en uso real. Si se apaga, se nota.

La documentacion operativa es privada. Esto es su version transformada
-decisiones, patrones y aprendizajes-, sin datos que permitan identificar o
reproducir el entorno.

Lo que busca demostrar: diseno de alertas que solo avisan de fallos reales
(sin ruido que ensene a ignorar el canal), separacion entre metricas de
infraestructura y evidencia de seguridad, y la disciplina de verificar el
efecto de un control en vez de la accion que deberia haberlo producido -una
leccion que aparecio siete veces distintas en una sola semana de trabajo.

## Por que es infraestructura productiva

| Servicio que corre 24/7 | Que pasa si se cae |
|---|---|
| DNS de toda la red de la casa | ningun equipo resuelve nombres: para quien la usa, "se corto internet" |
| Backups nocturnos y copia cifrada fuera del sitio | se pierde la proteccion de los datos y nadie lo nota hasta necesitarla |
| SIEM, metricas y alertas al telefono | los incidentes pasan sin que nadie se entere |
| Acceso remoto por malla | no hay forma de operar desde fuera de casa |
| NAS y espejo de la estacion de trabajo | se corta la sincronizacion de los archivos de trabajo |
| Aplicaciones propias en uso diario | se frena el uso real, incluido el envio de correo |
| Remoto de codigo propio | no hay donde versionar ni desde donde desplegar |

Por eso cada cambio se trata como en produccion: plan, rollback, evidencia y
verificacion de que lo que tiene que fallar, falla.

## En 30 segundos

| Indicador | Resultado |
|---|---|
| Verificaciones que informaban algo falso, en una sola semana | **7** |
| Rechazos de politica invisibles hasta construir la deteccion | **13.017** en 34 horas |
| Registro vs metrica ante 22 intentos | **6** lineas contra **23** paquetes contados |
| Formas validas de una alerta | **3**: algo fallo, algo no se hizo, algo dejo de pasar |
| Mensajes de "todo OK" en el canal de alertas | **0**, por regla |

```mermaid
flowchart LR
    A[Accion del control] -->|lo que se solia verificar| X[Exito aparente]
    A --> E[Efecto real en el sistema]
    E -->|lo que se verifica ahora| V[Exito comprobado]
    E --> F[Lo que tiene que fallar]
    F -->|tambien se verifica| V
```

## Indice

- [Ficha rapida para quien evalua](contexto.md)
- [Observabilidad, alertas y SIEM](docs/01-observabilidad-alertas-siem.md)
- [Caso de estudio: cuando un control no mide lo que dice medir](docs/casos-de-estudio/01-cuando-un-control-no-mide-lo-que-dice-medir.md)
- [Caso de estudio: 13.017 rechazos que nadie vio](docs/casos-de-estudio/02-trece-mil-rechazos-invisibles.md)

## Parte de una serie

Este repo es una pieza de un proyecto mas grande: una **infraestructura
productiva personal** (homelab), encendida 24/7 y documentada en cinco repos
independientes. Cada uno se lee solo; juntos muestran el entorno completo.

- [Zero Trust Remote Access](https://github.com/Nicolasperaltait/zero-trust-remote-access)
- [Backups That Don't Lie](https://github.com/Nicolasperaltait/backups-that-dont-lie)
- [Alerts That Matter](https://github.com/Nicolasperaltait/alerts-that-matter) (este repo)
- [Network Segmentation Playbook](https://github.com/Nicolasperaltait/network-segmentation-playbook)
- [Hypervisor as Control Plane](https://github.com/Nicolasperaltait/hypervisor-as-control-plane)

## Licencia

Ver [LICENSE.md](LICENSE.md).
