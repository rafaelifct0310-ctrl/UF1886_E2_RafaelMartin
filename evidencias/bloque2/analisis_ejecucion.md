# Análisis de ejecución

### Resultado ETL
```
Transform Name	Copy	Input	Read	Written	Output	Updated	Rejected	Errors	Buffers Input	Buffers Output	Duration	Speed	Status
src_sales_odoo	0	 33	 0	 33	 0	 0	 0	 0	 0	 0	 0.001"	 478	Finished
trim_fields	0	 0	 33	 33	 0	 0	 0	 0	 0	 0	 0.006"	 524	Finished
replace_null	0	 0	 33	 33	 0	 0	 0	 0	 0	 0	 0.009"	 516	Finished
Select values	0	 0	 33	 33	 0	 0	 0	 0	 0	 0	 0.018"	 458	Finished
dst_staging_sales_clean	0	 0	 33	 33	 33	 0	 0	 0	 0	 0	 0.041"	 344	Finished
```
### Conculta PostgreSQL
```
docker exec -it postgres.db psql -U user -d odoo
contendor: postgres.db
owner: user
database: odoo
```