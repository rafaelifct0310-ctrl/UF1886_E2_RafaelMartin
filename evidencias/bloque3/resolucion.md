# Aplicación de solución
#### Solución
- Ejecutar docker compose 
  
```
2026/03/09 11:58:41 - Hop - Pipeline opened.
2026/03/09 11:58:41 - Hop - Launching pipeline [P01_load_sales]...
2026/03/09 11:58:41 - Hop - Started the pipeline execution.
2026/03/09 11:58:41 - P01_load_sales - Executing this pipeline using the Local Pipeline Engine with run configuration 'local'
2026/03/09 11:58:41 - P01_load_sales - Execution started for pipeline [P01_load_sales]
2026/03/09 11:58:41 - dst_staging_sales_clean.0 - Connected to database [odoo_pg_local] (commit=1000)
2026/03/09 11:58:42 - src_sales_odoo.0 - Finished reading query, closing connection.
2026/03/09 11:58:42 - trim_fields.0 - Finished processing (I=0, O=0, R=33, W=33, U=0, E=0)
2026/03/09 11:58:42 - src_sales_odoo.0 - Finished processing (I=33, O=0, R=0, W=33, U=0, E=0)
2026/03/09 11:58:42 - replace_null.0 - Finished processing (I=0, O=0, R=33, W=33, U=0, E=0)
2026/03/09 11:58:42 - Select values.0 - Finished processing (I=0, O=0, R=33, W=33, U=0, E=0)
2026/03/09 11:58:42 - dst_staging_sales_clean.0 - Finished processing (I=0, O=33, R=33, W=33, U=0, E=0)
2026/03/09 11:58:42 - P01_load_sales - Pipeline duration : 0.312 seconds [  0.312" ]
2026/03/09 11:58:42 - P01_load_sales - Execution finished on a local pipeline engine with run configuration 'local'


```
#### Tabla resumen
```
Incidencia: Error de conexión 
Tranform falla: Table Input
Clasificación: Conexión 
Solución rápida: Reiniciar contenedor
```
