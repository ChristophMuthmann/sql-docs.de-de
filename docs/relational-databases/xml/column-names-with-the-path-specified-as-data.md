---
title: Spaltennamen, deren Pfad als data() angegeben ist | Microsoft Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: names [SQL Server], columns with
ms.assetid: 0b738e44-6108-4417-a9a4-abeb7680d899
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c10a9be79b86072e1f56c9c61560faee1463c11e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="column-names-with-the-path-specified-as-data"></a>Spaltennamen, deren Pfad als data() angegeben ist
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Wenn der als Spaltenname angegebene Pfad „data()“ ist, wird der Wert im generierten XML-Code als unteilbarer Wert behandelt. Dem XML-Code wird ein Leerzeichen hinzugefügt, wenn das nächste Element in der Serialisierung ebenfalls ein atomarer Wert ist. Dies erweist sich beim Erstellen von Listenelementen und Attributen als nützlich. Die folgende Abfrage ruft die Produktmodell-ID, den Namen des Produktmodells sowie die Liste der Produkte dieses Produktmodells ab.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID       AS "@ProductModelID",  
       Name                 AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
      FOR XML PATH (''))    AS "@ProductIDs"  
FROM  Production.ProductModel  
WHERE ProductModelID= 7   
FOR XML PATH('ProductModelData');  
```  
  
 Das geschachtelte SELECT ruft eine Liste mit Produkt-IDs ab. Als Spaltenname für die Produkt-IDs wird dabei "data()" angegeben. Da der PATH-Modus eine leere Zeichenfolge für den Namen des Zeilenelements angibt, wird kein Zeilenelement generiert. Stattdessen werden die Werte als die einem ProductIDs-Attribut zugewiesene Werte des <`ProductModelData`>-Zeilenelements des übergeordneten SELECT zurückgegeben. Dies ist das Ergebnis:  
  
 `<ProductModelData ProductModelID="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 888 889 890 891 892 893" />`  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden des PATH-Modus mit FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
