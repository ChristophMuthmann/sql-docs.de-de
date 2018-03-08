---
title: "Ändern von vorhandenen Spalten in XML-Spalten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f04a60816bc02bef8ce4bb670e2ac5416608388c
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="change-existing-columns-to-xml-columns"></a>Ändern von vorhandenen Spalten in XML-Spalten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
Die ALTER TABLE-Anweisung unterstützt den **xml** -Datentyp. So können Sie z. B. eine beliebige Spalte vom Zeichenfolgentyp in den **xml** -Datentyp ändern. Beachten Sie, dass die in der Spalte enthaltenen Dokumente dazu wohlgeformt sein müssen. Außerdem werden beim Ändern des Spaltentyps vom Zeichenfolgentyp in den typisierten XML-Typ die Dokumente in der Spalte anhand der angegebenen XSD-Schemas überprüft.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max))  
GO  
INSERT INTO T   
VALUES (1, '<Root><Product ProductID="1"/></Root>')  
GO  
ALTER TABLE T   
ALTER COLUMN Col2 xml  
GO  
```  
  
 Sie können eine nicht typisierte Spalte vom Typ `xml` in eine typisierte XML-Spalte ändern. Zum Beispiel:  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T   
values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>')  
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection)  
GO  
```  
  
> [!NOTE]  
>  Das Skript wird für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank ausgeführt, da die XML-Schemaauflistung `Production.ProductDescriptionSchemaCollection`als Teil der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank erstellt wird.  
  
 Im vorherigen Beispiel werden alle in der Spalte gespeicherten Instanzen mit den XSD-Schemas der angegebenen Auflistung überprüft und typisiert. Wenn die Spalte eine oder mehrere in Bezug auf das angegebene Schema ungültige XML-Instanzen enthält, erzeugt die `ALTER TABLE` -Anweisung einen Fehler, d. h. Sie können die nicht typisierte XML-Spalte nicht in eine typisierte XML-Spalte ändern.  
  
> [!NOTE]  
>  Bei umfangreichen Tabellen kann das Ändern einer Spalte vom Typ **xml** äußerst aufwändig werden, da jedes Dokument auf Wohlgeformtheit überprüft und bei typisierten XML-Dokumenten auch eine Überprüfung durchgeführt werden muss.  
  
 Weitere Informationen zu typisierten XML-Dokumenten finden Sie unter [Vergleichen von typisiertem XML mit nicht typisiertem XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
  
