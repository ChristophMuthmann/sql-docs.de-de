---
title: "Beispiele f&#252;r Gesch&#228;ftsregeln (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "01/05/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3974b9be-4b7c-4a37-ab26-1a36ef455744
caps.latest.revision: 21
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 19
---
# Beispiele f&#252;r Gesch&#228;ftsregeln (Master Data Services)
Dieser Artikel zeigt Beispiele von Geschäftsregeln für [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. Sie finden diese Beispiele in den Beispielmodellen, die in Ihrer Installation von [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] enthalten sind.   
  
Anweisungen dazu, wie Sie die Beispielmodelle bereitstellen, finden Sie unter [Master Data Services](../sql-server/media/master-data-services.png#deploySample).  
  
  
## Beispiele für Geschäftsregeln  
Beispielmodell |Entität  |Geschäftsregelname| Description  
---------|---------|---------|-----------|  
Customer    | Customer   | Person pmt-Begriffe| Gibt Standardzahlungsbedingungen für Kunden an.          
In der folgenden Geschäftsregel wird die `defaults to`-[Regelaktion](../master-data-services/business-rule-conditions-master-data-services.md) auf das PaymentTerms-Attribut angewendet, wenn der Attributwert CustomerType die`is equal`-[Regelbedingung](../master-data-services/business-rule-conditions-master-data-services.md) erfüllt. Andernfalls wird keine Aktion ausgeführt.  
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
In der folgenden Geschäftsregel wird die `defaults to`-[Regelaktion](../master-data-services/business-rule-actions-master-data-services.md) auf das PaymentTerms-Attribut angewendet, wenn der Attributwert CustomerType die`is equal`-[Regelbedingung](../master-data-services/business-rule-conditions-master-data-services.md) erfüllt. Andernfalls wird keine Aktion ausgeführt.  
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
In der folgenden Geschäftsregel wird die `must be between`-[Regelaktion](../master-data-services/business-rule-actions-master-data-services.md) auf das DaysToManufacture-Attribut angewendet, wenn der InHouseManufacture-Attributwert die`is equal`-[Regelbedingung](../master-data-services/business-rule-conditions-master-data-services.md) erfüllt. Andernfalls wird keine Aktion ausgeführt.  
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
In der folgenden Geschäftsregel wird unter allen Umständen die `is required`-[Überprüfungsaktion](../master-data-services/business-rule-actions-master-data-services.md) für die angegebenen Attribute verwendet. Die Attributwerte dürfen nicht Null oder leer sein.  
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
In der folgenden Geschäftsregel wird unter allen Umständen die `must be greater than`-[Regelaktion](../master-data-services/business-rule-actions-master-data-services.md) auf das StandardCost-Attribut von „Products“ angewendet.  
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
  
In der folgenden Geschäftsregel wird die `must be greater than`-[Regelaktion](../master-data-services/business-rule-actions-master-data-services.md) auf die Attribute „MSRP“ und „DealerCost“ angewendet, wenn der Wert des FinishedGoodIndicator-Attributs die`is equal`-[Regelbedingung](../master-data-services/business-rule-conditions-master-data-services.md) erfüllt.  
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
In der folgenden Geschäftsregel wird die `defaults to` [[-Regelaktion](../master-data-services/business-rule-actions-master-data-services.md)](Business%20Rule%20Conditions%20(Master%20Data%20Services).xml) auf das Namensattribut angewendet, wenn die Farb- und Klassenattribute die `is equal`-Regelbedingung nicht erfüllen.  
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
1. Navigieren Sie zur [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]-Website, die Sie nach der Installation von MDS eingerichtet haben, und klicken Sie auf das Feld **Systemverwaltung**.   
Anweisungen zum Einrichten der Website finden Sie unter [Master Data Services](../sql-server/media/master-data-services.png).  
2. Klicken Sie auf das Beispielmodell, das die Geschäftsregel enthält, so wie in den obigen Tabellen aufgeführt, und klicken Sie anschließend auf **Entitäten**.  
3. Klicken Sie auf die Entität, für welche die Regel gilt, so wie in den obigen Tabellen aufgeführt, und klicken Sie anschließend auf **Geschäftsregeln**.  
4. Klicken Sie auf den Namen der Geschäftsregel, die Sie anzeigen möchten. Die Benutzeroberfläche wird erweitert, um die Anweisungen **If**, **Then** und **Else** anzuzeigen.  
  
## Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu   
Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com).   
  
  
  
  
