# Inventory Analysis Query

## Business Scenario

A Supply Chain team needs visibility into inventory levels across warehouses to identify low-stock items and support replenishment planning.

## Objective

Provide current inventory balances by product and warehouse location.

## Sample SQL

```sql
SELECT 
  VEND_ITEM.VEND_ITEM_ID, 
  VEND_ITEM.VENDOR_NUM, VENDOR.VEND_NAME,
  VEND_ITEM.ITEM_NUM,
  SUM(ITEM_W.ON_HAND) AS ON_HAND,
  SUM(INV_SHP_L.TO_ALLOC_QTY) ON_SALE_QTY,
  VEND_ITEM.VENDOR_ITEM,
  VEND_ITEM.DESC_1,
  VEND_ITEM.EFFECTIVE_DATE,
  ITEM_2.DISCONTINUED_xx,
  VEND_ITEM.DISCONTINUE_DATE
FROM xxPROD_751_D.VEND_ITEM,
     xxPROD_751_D.VENDOR,
     xxPROD_751_D.ITEM_2,
     xxPROD_751_D.ITEM_W,
     xxPROD_751_D.INV_SHP_L,
     xxPROD_751_D.INV_SHP
WHERE INV_SHP_L.ITEM_NUM = VEND_ITEM.ITEM_NUM

AND INV_SHP.INV_SHP_ID = INV_SHP_L.INV_SHP_ID
AND INV_SHP.SHIPPED_DATE BETWEEN '01-JAN-9999' AND '31-MAY-9999'

AND INV_SHP_L.ITEM_NUM = ITEM_W.ITEM_NUM
AND INV_SHP_L.ITEM_NUM = ITEM_2.ITEM_NUM

AND ITEM_W.ITEM_NUM = VEND_ITEM.ITEM_NUM

AND ITEM_2.ITEM_NUM = VEND_ITEM.ITEM_NUM

AND VENDOR.VENDOR_NUM = VEND_ITEM.VENDOR_NUM

AND VEND_ITEM.VENDOR_NUM IN ('xxxx36', 'xxxx85')

AND VEND_ITEM.ITEM_NUM = 'xxxx06'
GROUP BY 
  VEND_ITEM.VEND_ITEM_ID, 
  VEND_ITEM.VENDOR_NUM, VENDOR.VEND_NAME,
  VEND_ITEM.ITEM_NUM,
  VEND_ITEM.VENDOR_ITEM,
  VEND_ITEM.DESC_1,
  VEND_ITEM.EFFECTIVE_DATE,
  ITEM_2.DISCONTINUED_xx,
  VEND_ITEM.DISCONTINUE_DATE
ORDER BY VEND_ITEM.VENDOR_NUM, VEND_ITEM.ITEM_NUM;
```

## Business Value

- Improves inventory visibility
- Supports replenishment decisions
- Reduces stockout risk
- Helps Supply Chain planning teams prioritize purchases
```


## Website Navigation

[Return to Ask Hernan Portfolio](https://hbricenor.github.io/AskHernan/portfolio.html)



