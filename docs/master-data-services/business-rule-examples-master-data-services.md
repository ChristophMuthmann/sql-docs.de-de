---
title: Beispiele für Geschäftsregeln (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/05/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3974b9be-4b7c-4a37-ab26-1a36ef455744
caps.latest.revision: 21
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6cd8e4f68f0167b9179d4108c59755da5619787e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="business-rule-examples-master-data-services"></a>Beispiele für Geschäftsregeln (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel zeigt Beispiele von Geschäftsregeln für [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. Sie finden diese Beispiele in den Beispielmodellen, die in Ihrer Installation von [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]enthalten sind.   
  
Anweisungen dazu, wie Sie die Beispielmodelle bereitstellen, finden Sie unter [Master Data Services – Installation und Konfiguration](../master-data-services/master-data-services-installation-and-configuration.md).  
  
  
## <a name="business-rule-examples"></a>Beispiele für Geschäftsregeln  
Beispielmodell |Entität  |Geschäftsregelname| Description  
---------|---------|---------|-----------|  
Customer    | Customer   | Person pmt-Begriffe| Gibt Standardzahlungsbedingungen für Kunden an.          
In der folgenden Geschäftsregel wird die `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), then the `defaults to` [rule action](../master-data-services/business-rule-conditions-master-data-services.md) is applied to the PaymentTerms attribute. Andernfalls wird keine Aktion ausgeführt.  
```  
If  
    CustomerType is equal to 2  
Then  
    PaymentTerms defaults to CASH  
Else  
    None      
```  
  
**--------------------------------------------------**  
  
Beispielmodell  |Entität  |Geschäftsregelname|Description    
---------|---------|---------|---------------  
Customer     | Customer    | Org pmt-Begriffe | Gibt die Standardzahlungsbedingungen für Organisationen an.         
In der folgenden Geschäftsregel wird die `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), then the `defaults to` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the PaymentTerms attribute. Andernfalls wird keine Aktion ausgeführt.  
```  
If  
    CustomerType is equal to 1  
Then  
    PaymentTerms defaults to 210Net30  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Beispielmodell  |Entität  |Geschäftsregelname| Description    
---------|---------|---------|-----------  
Product     |  Product       | DaysToManufacture |Gibt den Bereich der Tage bis zur Herstellung für die Herstellung vor Ort an.          
In der folgenden Geschäftsregel wird die `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), then the `must be between` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the DaysToManufacture attribute. Andernfalls wird keine Aktion ausgeführt.  
```  
If  
    InHouseManufacture is equal to Y  
Then  
    DaysToManufacture must be between 1 and 10  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Beispielmodell  |Entität  |Geschäftsregelname|Description    
---------|---------|---------|-------------  
Product     |Product         |Erforderliche Felder| Gibt die erforderlichen Attribute für die Elemente der Entität „Product“ an.           
In der folgenden Geschäftsregel wird unter allen Umständen die `is required` [validation action](../master-data-services/business-rule-actions-master-data-services.md) is taken for the specified attributes. Die Attributwerte dürfen nicht Null oder leer sein.  
```  
If  
    None  
Then  
    Name is required  
    ProductSubCategory is required  
    Color is required  
    StandardCost is required  
    SafetyStockLevel is required  
    ReorderPoint is required  
    InHouseManufacture is required  
    SellStartDate is required  
    FinishedGoodIndicator is required  
    ProductLine is required  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Beispielmodell  |Entität  |Geschäftsregelname|Description    
---------|---------|---------|-----------  
Product     | Product        |  Standardkosten| Erfordert, dass die Standardkosten größer als 0 sind.        
In der folgenden Geschäftsregel wird unter allen Umständen die `must be greater than` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the StandardCost attribute of products.  
```  
If  
    None  
Then  
    StandardCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Beispielmodell  |Entität  |Geschäftsregelname|Description    
---------|---------|---------|------------  
Product     | Product        | FG MSRP-Kosten|Gibt an, dass der vom Hersteller empfohlene Preis (MSRP) und die Händlerkosten größer als 0 sein müssen, wenn das Produkt ein Endprodukt ist.           
  
In der folgenden Geschäftsregel wird die `is equal` [rule condition](../master-data-services/business-rule-conditions-master-data-services.md), the `must be greater than` [rule action](../master-data-services/business-rule-actions-master-data-services.md) is applied to the MSRP and DealerCost attributes.  
```  
If  
    FinishedGoodIndicator is equal to Y  
Then  
    MSRP must be greater than 0  
    DealerCost must be greater than 0  
Else  
    None  
```  
  
**--------------------------------------------------**  
  
  
Beispielmodell  |Entität  |Geschäftsregelname|Description    
---------|---------|---------|------------  
Product     | Product        |  Standardname| Gibt den Standardnamen des Produkts basierend auf den Werten der Farb- und Klassenattribute an. Wenn der Farbattributwert nicht YLO ist, und das Klassenattribut nicht NA, dann ist der Standardname „Gelb NA“         
In der folgenden Geschäftsregel wird die `defaults to` [Regelaktion](../master-data-services/business-rule-actions-master-data-services.md) auf das Namensattribut angewendet, wenn die Farb- und Klassenattribute die`is equal`-Regelbedingung nicht erfüllen.  
```  
If  
    (Color is equal to YLO AND Class is equal to NA) is not true  
Then  
    Name defaults to Yellow NA  
Else  
    Name defaults to Other  
```  
  
**--------------------------------------------------**  
  
  
**So zeigen Sie die Geschäftsregelbeispiele in den Beispielmodellen an**  
1. Navigieren Sie zur [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] -Website, die Sie nach der Installation von MDS eingerichtet haben, und klicken Sie auf das Feld **Systemverwaltung** .   
Anweisungen zum Einrichten der Website finden Sie unter [Master Data Services – Installation und Konfiguration](../master-data-services/master-data-services-installation-and-configuration.md).  
2. Klicken Sie auf das Beispielmodell, das die Geschäftsregel enthält, so wie in den obigen Tabellen aufgeführt, und klicken Sie anschließend auf **Entitäten**.  
3. Klicken Sie auf die Entität, für welche die Regel gilt, so wie in den obigen Tabellen aufgeführt, und klicken Sie anschließend auf **Geschäftsregeln**.  
4. Klicken Sie auf den Namen der Geschäftsregel, die Sie anzeigen möchten. Die Benutzeroberfläche wird erweitert, um die Anweisungen **If**, **Then** und **Else** anzuzeigen.  
  
 
  
  
  
  

