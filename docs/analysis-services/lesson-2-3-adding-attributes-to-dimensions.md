---
title: "Hinzufügen von Attributen zu Dimensionen | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0642ac7688f86ce5fb23f1af50e9ced776993216
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-3---adding-attributes-to-dimensions"></a>Lektion 2 – 3 – Hinzufügen von Attributen zu Dimensionen
Nachdem Sie Dimensionen definiert haben, können Sie sie jetzt mit Attributen auffüllen, die die einzelnen Datenelemente in der Dimension darstellen. Attribute basieren normalerweise auf Feldern einer Datenquellensicht. Wenn Sie einer Dimension Attribute hinzufügen, können Sie Felder einer beliebigen Tabelle in die Datenquellensicht einschließen.  
  
In dieser Aufgabe verwenden Sie den Dimensions-Designer, um der Customer-Dimension und der Produkt-Dimension Attribute hinzuzufügen. Die Customer-Dimension schließt Attribute ein, die auf Feldern sowohl aus der Customer-Tabelle als auch aus der Geography-Tabelle basieren.  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>Hinzufügen von Attributen zur Customer-Dimension.  
  
#### <a name="to-add-attributes"></a>So fügen Sie Attribute hinzu  
  
1.  Öffnen Sie den Dimensions-Designer für die Customer-Dimension. Doppelklicken Sie dazu auf die Dimension **Customer** im Knoten **Dimensionen** des Projektmappen-Explorers.  
  
2.  Beachten Sie im Bereich **Attribute** die Attribute "Customer Key" und "Geography Key", die vom Cube-Assistenten erstellt wurden.  
  
3.  Verwenden Sie das Symbol zum Vergrößern auf der Symbolleiste der Registerkarte **Dimensionsstruktur** , um die Tabellen im Bereich **Datenquellensicht** in einer 100-Prozent-Darstellung anzuzeigen.  
  
4.  Ziehen Sie die folgenden Spalten von der **Customer** -Tabelle im Bereich **Datenquellensicht** in den Bereich **Attribute** :  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Geschlecht**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Phone**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  Ziehen Sie die folgenden Spalten von der **Geography** -Tabelle im Bereich **Datenquellensicht** in den Bereich **Attribute** :  
  
    -   **City**  
  
    -   **StateProvinceName**  
  
    -   **EnglishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  Klicken Sie im Menü Datei auf **Alle speichern**.  
  
## <a name="adding-attributes-to-the-product-dimension"></a>Hinzufügen von Attributen zur Product-Dimension.  
  
#### <a name="to-add-attributes"></a>So fügen Sie Attribute hinzu  
  
1.  Öffnen Sie den Dimensions-Designer für die Product-Dimension. Doppelklicken Sie im Projektmappen-Explorer auf die Dimension **Product** .  
  
2.  Beachten Sie im Bereich **Attribute** das Attribut "Product Key", das vom Cube-Assistenten erstellt wurde.  
  
3.  Verwenden Sie das Symbol zum Vergrößern auf der Symbolleiste der Registerkarte **Dimensionsstruktur** , um die Tabellen im Bereich **Datenquellensicht** in einer 100-Prozent-Darstellung anzuzeigen.  
  
4.  Ziehen Sie die folgenden Spalten von der **Product** -Tabelle im Bereich **Datenquellensicht** in den Bereich **Attribute** :  
  
    -   **StandardCost**  
  
    -   **Farbe**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **Größe**  
  
    -   **SizeRange**  
  
    -   **Weight**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **Class**  
  
    -   **Style**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **Status**  
  
5.  Klicken Sie im Menü Datei auf **Alle speichern**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Überprüfen von Cube- und Dimensionseigenschaften](../analysis-services/lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>Siehe auch  
[Dimensionsattributeigenschaftenverweis](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
  

