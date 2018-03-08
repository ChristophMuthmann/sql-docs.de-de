---
title: Beispiel-Recordset zum Untersuchen von Daten | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66ed865b10da98f63c087cc56191300e058403c3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="sample-recordset-for-examining-data"></a>Beispiel-Recordset zum Untersuchen von Daten
Zunächst sehen wir uns die **Recordset** -Objekt zurückgegeben, mit der folgenden SQL-Abfrage, für die Northwind-Beispieldaten Basis in Microsoft SQL Server ausgeführt wird.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 Die resultierenden **Recordset** Objekt enthält alle erzeugt in der Datenbank, die in der folgenden Tabelle gezeigt.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Onkel Bobs Trockenbirnen|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|Manjimup Dried Apples|53.0000|  
|74|Longlife Tofu|10.0000|  
  
 Wenn Sie interessiert, diese Ergebnisse selbst sind, versuchen Sie es im folgende JScript-Beispiel:  
  
-   [JScript-Beispiel zum Zurückgeben eines Recordsets](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
