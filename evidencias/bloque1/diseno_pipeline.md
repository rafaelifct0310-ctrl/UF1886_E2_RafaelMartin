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

#### Ver estrucutra de sale_order
```
\d sale_order
```
```
                                                 Table "public.sale_order"
            Column            |            Type             | Collation | Nullable |                Default
------------------------------+-----------------------------+-----------+----------+----------------------------------------
 id                           | integer                     |           | not null | nextval('sale_order_id_seq'::regclass)
 campaign_id                  | integer                     |           |          |
 source_id                    | integer                     |           |          |
 medium_id                    | integer                     |           |          |
 company_id                   | integer                     |           | not null |
 partner_id                   | integer                     |           | not null |
 journal_id                   | integer                     |           |          |
 partner_invoice_id           | integer                     |           | not null |
 partner_shipping_id          | integer                     |           | not null |
 fiscal_position_id           | integer                     |           |          |
 payment_term_id              | integer                     |           |          |
 pricelist_id                 | integer                     |           |          |
 currency_id                  | integer                     |           |          |
 user_id                      | integer                     |           |          |
 team_id                      | integer                     |           |          |
 create_uid                   | integer                     |           |          |
 write_uid                    | integer                     |           |          |
 access_token                 | character varying           |           |          |
 name                         | character varying           |           | not null |
 state                        | character varying           |           |          |
 client_order_ref             | character varying           |           |          |
 origin                       | character varying           |           |          |
 reference                    | character varying           |           |          |
 signed_by                    | character varying           |           |          |
 invoice_status               | character varying           |           |          |
 validity_date                | date                        |           |          |
 note                         | text                        |           |          |
 currency_rate                | numeric                     |           |          |
 amount_untaxed               | numeric                     |           |          |
 amount_tax                   | numeric                     |           |          |
 amount_total                 | numeric                     |           |          |
 locked                       | boolean                     |           |          |
 require_signature            | boolean                     |           |          |
 require_payment              | boolean                     |           |          |
 create_date                  | timestamp without time zone |           |          |
 commitment_date              | timestamp without time zone |           |          |
 date_order                   | timestamp without time zone |           | not null |
 signed_on                    | timestamp without time zone |           |          |
 write_date                   | timestamp without time zone |           |          |
 prepayment_percent           | double precision            |           |          |
 pending_email_template_id    | integer                     |           |          |
 sale_order_template_id       | integer                     |           |          |
 customizable_pdf_form_fields | jsonb                       |           |          |
 opportunity_id               | integer                     |           |          |
Indexes:
    "sale_order_pkey" PRIMARY KEY, btree (id)
    "sale_order__campaign_id_index" btree (campaign_id) WHERE campaign_id IS NOT NULL
```

```
\d sale_order_line
```
```
                                                Table "public.sale_order_line"
          Column           |            Type             | Collation | Nullable |                   Default
---------------------------+-----------------------------+-----------+----------+---------------------------------------------
 id                        | integer                     |           | not null | nextval('sale_order_line_id_seq'::regclass)
 order_id                  | integer                     |           | not null |
 sequence                  | integer                     |           |          |
 company_id                | integer                     |           |          |
 currency_id               | integer                     |           |          |
 order_partner_id          | integer                     |           |          |
 salesman_id               | integer                     |           |          |
 product_id                | integer                     |           |          |
 product_uom               | integer                     |           |          |
 linked_line_id            | integer                     |           |          |
 combo_item_id             | integer                     |           |          |
 product_packaging_id      | integer                     |           |          |
 create_uid                | integer                     |           |          |
 write_uid                 | integer                     |           |          |
 state                     | character varying           |           |          |
 display_type              | character varying           |           |          |
 virtual_id                | character varying           |           |          |
 linked_virtual_id         | character varying           |           |          |
 qty_delivered_method      | character varying           |           |          |
 invoice_status            | character varying           |           |          |
 analytic_distribution     | jsonb                       |           |          |
 name                      | text                        |           | not null |
 product_uom_qty           | numeric                     |           | not null |
 price_unit                | numeric                     |           | not null |
 discount                  | numeric                     |           |          |
 price_subtotal            | numeric                     |           |          |
 price_total               | numeric                     |           |          |
 price_reduce_taxexcl      | numeric                     |           |          |
 price_reduce_taxinc       | numeric                     |           |          |
 qty_delivered             | numeric                     |           |          |
 qty_invoiced              | numeric                     |           |          |
 qty_to_invoice            | numeric                     |           |          |
 untaxed_amount_invoiced   | numeric                     |           |          |
 untaxed_amount_to_invoice | numeric                     |           |          |
 is_downpayment            | boolean                     |           |          |
 is_expense                | boolean                     |           |          |
 create_date               | timestamp without time zone |           |          |
 write_date                | timestamp without time zone |           |          |
 technical_price_unit      | double precision            |           |          |
 price_tax                 | double precision            |           |          |
 product_packaging_qty     | double precision            |           |          |
 customer_lead             | double precision            |           | not null |
Indexes:
    "sale_order_line_pkey" PRIMARY KEY, btree (id)
    "sale_order_line__company_id_index" btree (company_id)
```
