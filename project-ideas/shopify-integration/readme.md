# Shopify Integration.

Data Model of [Shopify Config](/project-ideas/shopify-integration/shopify-config) entities. 


* Call services for processing data downloaded from Shopify must need ShopifyConfigId and related ProdutStoreId. Consider making it part of request preprossing, before the real service is called. 

* ShopifyServiceConfig are good candidates for service specific preprocessing.

   ```java
   String skipOrdersTags = EntityUtilProperties.getPropertyValue("ShopifyServiceConfig", productStoreId + ".skip.order.import.tags", delegator);
   ```

## Architecture

Transformation --> Data Mapping --> Store

1.  Transform data from Shopfiy resource schema to HotWax Commerce resource schema
2.  Process data for HotWax type mapping 

**Task 1:** 
Write JOLT transformation to map Shopify order json to HotWax Order JSON. 

### **Skip processing filters** 

The data sync process ensure, no duplicate record is created. The sync process should also allow configuration for content based skipping of objects e.g Orders tagged Re-Curate should be not be synched with HC. 
The data sync pipeline should preferably filter objects and only process data sync for select set of orders. 


https://github.com/hotwax/press-release-faq/tree/main/integration/shopify
https://github.com/hotwax/press-release-faq/blob/main/auditing/audit-and-correct-shopify-pre-order-details.md
https://github.com/hotwax/press-release-faq/blob/main/auditing/shopify-graphql-api-log-auditing.md
https://github.com/hotwax/press-release-faq/blob/main/import/pos-sales-inventory.md
