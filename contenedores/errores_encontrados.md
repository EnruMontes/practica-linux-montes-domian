# Errores que encontramos en el TP - Montes-Domian

## 1. El nombre de la red en Redis
- **Qué pasaba:** El servicio de `redis` no funcionaba bien porque estaba configurado para usar una red llamada `monitoring-network`.
- **Cómo lo arreglamos:** Nos fijamos al final del archivo y vimos que la red creada se llamaba simplemente `monitoring`. Le borramos la parte de "-network" al servicio para que coincida con la que existía.

## 2. El volumen de Grafana estaba mal
- **Qué pasaba:** Grafana estaba intentando guardar sus datos en un volumen llamado `grafana-data`.
- **Cómo lo arreglamos:** Revisamos la sección de `volumes:` y vimos que el volumen real se llamaba `grafana-storage`. Cambiamos el nombre en el servicio de Grafana para que use el volumen correcto.

## 3. Prometheus y el error con Nginx
- **Qué pasaba:** Prometheus intentaba leer métricas de Nginx en el puerto 9113 y fallaba (daba error de conexión).
- **Cómo lo arreglamos:** Vimos en la documentación que la imagen básica de Nginx no trae esas métricas activadas por defecto. Para solucionar el error, comentamos esa línea en `prometheus.yml`.
