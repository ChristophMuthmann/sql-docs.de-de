---
title: Erstellen von Sichten über XML-Spalten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0225ca7a583e30cb0e237a90ca69314d5f841ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-views-over-xml-columns"></a>Erstellen von Sichten über XML-Spalten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Sie können eine Spalte vom Typ **xml** zum Erstellen von Sichten verwenden. Im folgenden Beispiel wird eine Sicht erstellt, in der mithilfe der `xml` value() **-Methode des** xml **-Datentyps der Wert aus einer Spalte vom Typ** abgerufen wird.  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 Führen Sie die folgende Abfrage für die Sicht aus:  
  
```  
SELECT *   
FROM   MyView  
```  
  
 Dies ist das Ergebnis:  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 Beachten Sie die folgenden Punkte in Bezug auf das Erstellen von Sichten mit dem **xml** -Datentyp:  
  
-   Der XML-Datentyp kann in einer materialisierten Sicht erstellt werden. Die materialisierte Sicht kann nicht auf einer xml-Datentypmethode basieren. Er kann jedoch in eine XML-Schemaauflistung umgewandelt werden, die sich von der XML-Typspalte der Basistabelle unterscheidet.  
  
-   Der **xml** -Datentyp kann nicht in verteilten partitionierten Sichten verwendet werden.  
  
-   SQL-Prädikate, die für die Sicht ausgeführt werden, werden nicht in die XQuery der Sichtdefinition verschoben.  
  
-   XML-Datentypmethoden in einer Sicht sind nicht aktualisierbar.  
  
  
