# Identificación flujo
- Tabla de origen: 
```
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
- Tabla de destino: **sales_clean** 