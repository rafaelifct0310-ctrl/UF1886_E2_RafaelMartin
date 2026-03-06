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

#### Ver estructura de sale_order
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
#### Ver estructura de sale_order_line
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
#### Datos disponibles
```
SELECT id, name, partner_id, date_order, amount_total, state FROM sale_order LIMIT 10;
```
```
 id |  name  | partner_id |         date_order         | amount_total | state
----+--------+------------+----------------------------+--------------+-------
  1 | S00001 |         10 | 2026-02-05 13:13:00        |      1740.00 | draft
  2 | S00002 |         12 | 2026-02-05 13:13:00        |      2947.50 | draft
  3 | S00003 |         12 | 2026-03-05 13:13:43        |       377.50 | draft
  5 | S00005 |         10 | 2026-02-05 13:13:00        |       405.00 | draft
 19 | S00019 |          8 | 2026-02-05 13:13:00        |      1740.00 | sent
  6 | S00006 |         16 | 2026-03-05 13:13:43        |       750.00 | sale
  8 | S00008 |         11 | 2026-03-05 13:13:43        |       462.00 | sale
  4 | S00004 |         11 | 2026-03-05 13:13:43        |      2240.00 | sale
  7 | S00007 |         11 | 2026-03-05 13:13:43        |      1706.00 | sale
  9 | S00009 |         11 | 2026-02-26 13:13:43.712546 |       654.00 | sale
(10 rows)

```
```
SELECT id, order_id, product_id, name, product_uom_qty, price_unit, price_subtotal FROM sale_order_line LIMIT 10;
```
```
id | order_id | product_id |                       name                        | product_uom_qty | price_unit | price_subtotal
----+----------+------------+---------------------------------------------------+-----------------+------------+----------------
  1 |        1 |         32 | [FURN_6667] Pantallas de bloque acústico (Madera) |            3.00 |     295.00 |         885.00
  2 |        1 |          6 | [FURN_8888] Lámpara de oficina                    |            5.00 |     145.00 |         725.00
  3 |        1 |          5 | [FURN_7777] Silla de oficina                      |            2.00 |      65.00 |         130.00
  4 |        2 |          3 | Diseño interior virtual                           |           24.00 |      75.00 |        1800.00
  5 |        2 |          4 | Área de casa virtual                              |           30.00 |      38.25 |        1147.50
  6 |        3 |          3 | Diseño interior virtual                           |           10.00 |      30.75 |         307.50
  7 |        3 |          5 | [FURN_7777] Silla de oficina                      |            1.00 |      70.00 |          70.00
 12 |        5 |          6 | [FURN_8888] Lámpara de oficina                    |            1.00 |     405.00 |         405.00
 40 |       19 |         32 | [FURN_6667] Pantallas de bloque acústico (Madera) |            3.00 |     295.00 |         885.00
 41 |       19 |          6 | [FURN_8888] Lámpara de oficina                    |            5.00 |     145.00 |         725.00
(10 rows)

```

#### Crear Schema Staging y tabla destino

- Conectado al psql del contenedor:
```
CREATE SCHEMA IF NOT EXISTS staging;

CREATE TABLE IF NOT EXISTS staging.sales_clean (
    id                  SERIAL PRIMARY KEY,
    sale_order_id       INTEGER,
    order_name          VARCHAR(100),
    partner_name        VARCHAR(255),
    partner_email       VARCHAR(255),
    product_name        VARCHAR(255),
    product_code        VARCHAR(100),
    qty_ordered         NUMERIC(16,4)  DEFAULT 0,
    unit_price          NUMERIC(16,4)  DEFAULT 0,
    price_subtotal      NUMERIC(16,4)  DEFAULT 0,
    order_date          DATE,
    order_state         VARCHAR(50),
    currency_name       VARCHAR(10),
    etl_load_date       TIMESTAMP      DEFAULT NOW(),
    etl_source          VARCHAR(100)   DEFAULT 'hop_pipeline_v1'
);
```

- Verificar creación
```
\dt staging.*
\d staging.sales_clean
```
```
           List of relations
 Schema  |    Name     | Type  | Owner
---------+-------------+-------+-------
 staging | sales_clean | table | user
(1 row)

                                              Table "staging.sales_clean"
     Column     |            Type             | Collation | Nullable |                     Default
----------------+-----------------------------+-----------+----------+-------------------------------------------------
 id             | integer                     |           | not null | nextval('staging.sales_clean_id_seq'::regclass)
 sale_order_id  | integer                     |           |          |
 order_name     | character varying(100)      |           |          |
 partner_name   | character varying(255)      |           |          |
 partner_email  | character varying(255)      |           |          |
 product_name   | character varying(255)      |           |          |
 product_code   | character varying(100)      |           |          |
 qty_ordered    | numeric(16,4)               |           |          | 0
 unit_price     | numeric(16,4)               |           |          | 0
 price_subtotal | numeric(16,4)               |           |          | 0
 order_date     | date                        |           |          |
 order_state    | character varying(50)       |           |          |
 currency_name  | character varying(10)       |           |          |
 etl_load_date  | timestamp without time zone |           |          | now()
 etl_source     | character varying(100)      |           |          | 'hop_pipeline_v1'::character varying
Indexes:
    "sales_clean_pkey" PRIMARY KEY, btree (id)

```
- Dar permisos
```
GRANT ALL PRIVILEGES ON SCHEMA staging TO odoo;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA staging TO odoo;
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA staging TO odoo;
```

- Verificar

```
SELECT COUNT(*) FROM staging.sales_clean;
```

```
count
-------
     0
(1 row)
```

#### Configuración conexión
````
SELECT
    so.id                        AS sale_order_id,
    so.name                      AS order_name,
    rp.name                      AS partner_name,
    rp.email                     AS partner_email,
    pt.name                      AS product_name,
    pt.default_code              AS product_code,
    sol.product_uom_qty          AS qty_ordered,
    sol.price_unit               AS unit_price,
    sol.price_subtotal           AS price_subtotal,
    so.date_order                AS order_date,
    so.state                     AS order_state,
    rc.name                      AS currency_name
FROM
    sale_order so
    JOIN sale_order_line sol  ON sol.order_id = so.id
    JOIN res_partner rp       ON rp.id = so.partner_id
    JOIN product_product pp   ON pp.id = sol.product_id
    JOIN product_template pt  ON pt.id = pp.product_tmpl_id
    JOIN res_currency rc      ON rc.id = so.currency_id
WHERE
    so.state IN ('sale', 'done')
ORDER BY so.date_order ASC;
```
