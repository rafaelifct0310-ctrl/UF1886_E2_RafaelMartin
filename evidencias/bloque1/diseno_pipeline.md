 # Diseño pipeline
 
 ## Identificar flujo de datos
### Entrar al contenedor PostgreSQL

```
docker exec -it postgres.db psql -U user -d odoo
```
```
odoo=# \df
```
```
                                                                    List of functions
 Schema |                   Name                    | Result data type |                            Argument data types                            | Type
--------+-------------------------------------------+------------------+---------------------------------------------------------------------------+------
 public | gin_extract_query_trgm                    | internal         | text, internal, smallint, internal, internal, internal, internal          | func
 public | gin_extract_value_trgm                    | internal         | text, internal                                                            | func
 public | gin_trgm_consistent                       | boolean          | internal, smallint, text, integer, internal, internal, internal, internal | func
 ```


 #### Explorar tablas
 ##### Tablas relevantes
 ```
 \dt sale*
 \dt res*
 \dt product*
 ```
 ```
 Schema |                         Name                         | Type  | Owner
--------+------------------------------------------------------+-------+-------
 public | account_tax_sale_order_discount_rel                  | table | user
 public | account_tax_sale_order_line_rel                      | table | user
 public | product_document_sale_pdf_form_field_rel             | table | user
 public | product_template_attribute_value_sale_order_line_rel | table | user
 public | quotation_document_sale_order_rel                    | table | user
 public | quotation_document_sale_pdf_form_field_rel           | table | user
 public | sale_advance_payment_inv                             | table | user
 public | sale_advance_payment_inv_sale_order_rel              | table | user
 public | sale_mass_cancel_orders                              | table | user
 public | sale_order                                           | table | user
 public | sale_order_cancel                                    | table | user
 public | sale_order_discount                                  | table | user
 public | sale_order_line                                      | table | user

 ```

### 
