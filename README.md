# Trabajo Práctico Final - Administración de Sistemas Linux

**Materia:** Arquitectura y Sistemas Operativos
**Integrantes:** Montes, Enrico y Domian, Mateo
**Fecha de Entrega:** 04 Diciembre 2025

---

## Descripción del Proyecto
Este repositorio contiene la entrega final del trabajo práctico de administración de sistemas. El objetivo fue simular un entorno de trabajo real utilizando virtualización con Vagrant, control de versiones con Git, y despliegue de servicios tanto en contenedores (Docker) como en infraestructura tradicional (LAMP).

Todo el trabajo fue realizado de forma colaborativa en una máquina virtual Ubuntu (Jammy 64).

---

## Proceso de Resolución

### 1. Configuración del Entorno
Arrancamos configurando el `Vagrantfile` para aprovisionar automáticamente las herramientas básicas (Git, Docker, LVM). Tuvimos que corregir el script de aprovisionamiento inicial para agregar el repositorio de `fastfetch` que fallaba por defecto.

### 2. Desafío Docker (Debug)
Esta fue la parte más interesante. El `docker-compose.yml` original tenía varios errores intencionales.
- Tuvimos que unificar los nombres de las redes (de `monitoring-network` a `monitoring`).
- Corregimos el mapeo de volúmenes en Grafana.
- Desactivamos el scraping de Nginx en Prometheus porque la imagen base no soportaba métricas, lo que causaba falsos positivos de error.

### 3. Implementación LAMP (Bonus)
Para el ejercicio extra, levantamos un servidor web tradicional. Creamos una base de datos MySQL llamada `tp_final_db` y configuramos un `index.html` con estilos CSS personalizados. También programamos un script PHP para validar que la conexión a la base de datos fuera exitosa.

---

## Conclusiones
Realizar este TP nos permitió entender la diferencia entre trabajar en "mi máquina" y gestionar un servidor real. Aprendimos que:
1.  **La automatización es clave:** Usar scripts y Vagrant nos ahorró mucho tiempo al poder destruir y recrear la VM sin perder nada.
2.  **Los permisos importan:** Entendimos por qué es peligroso usar `chmod 777` y cómo usar grupos para colaborar de forma segura.
3.  **Docker vs Virtualización:** Vimos en la práctica cómo Docker levanta servicios en segundos (como Grafana y Prometheus) comparado con lo que tarda una VM completa.

---

**Estado del Proyecto:** Finalizado y entregado.
