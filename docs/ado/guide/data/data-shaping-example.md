---
title: Daten strukturieren Beispiel | Microsoft Docs
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
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e05526425f2ee5f6a2d776439f28f0fca244d4cc
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="data-shaping-example"></a>Daten strukturiert werden, Beispiel
Die folgenden Daten strukturieren Befehl veranschaulicht, wie eine hierarchische erstellen **Recordset** aus der **Kunden** und **Aufträge** Tabellen in der Northwind-Datenbank.  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 Wenn dieser Befehl verwendet wird, Öffnen einer **Recordset** Objekt (wie gezeigt in [Visual Basic-Beispiel der Strukturierung Daten](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)), einem Kapitel erstellt (**ChapOrders**) für jeden Datensatz zurückgegeben aus der **Kunden** Tabelle. In diesem Kapitel besteht aus einer Teilmenge von der **Recordset** zurückgegeben, die von der **Aufträge** Tabelle. Die **ChapOrders** Kapitel enthält die angeforderte Informationen zu den vom angegebenen Kunden aufgegebene Bestellungen. In diesem Beispiel besteht im Kapitel über das aus drei Spalten: **OrderID**, **OrderDate**, und **CustomerID**.  
  
 Die ersten beiden Einträge von der resultierenden geformten **Recordset** lauten wie folgt:  
  
|CustomerID|ContactName|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|Maria Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 In einer SHAPE-Befehl APPEND verwendet, um ein untergeordnetes Element erstellen **Recordset** im Zusammenhang mit der übergeordneten **Recordset** (wie aus den anbieterspezifischen-Befehl zurückgegeben, sofort nach dem Form-Schlüsselwort, die behandelt wurde früher) von der RELATE-Klausel. Die über- und untergeordneten in der Regel haben mindestens eine Spalte gemeinsam: der Wert der Spalte in einer Zeile des übergeordneten Elements ist identisch mit dem Wert der Spalte in allen Zeilen des untergeordneten Elements.  
  
 Es wird eine zweite Möglichkeit zum Form-Befehle verwenden: nämlich, generieren Sie ein übergeordnetes Element **Recordset** von einem untergeordneten **Recordset**. Die Datensätze in der untergeordneten **Recordset** gruppiert sind, in der Regel mithilfe der BY-Klausel und eine Zeile an der übergeordneten Tabelle hinzugefügt wird **Recordset** für jede resultierende Gruppe in das untergeordnete Element. Wenn die BY-Klausel weggelassen wird, das untergeordnete Element **Recordset** Formular wird, eine einzelne Gruppe und das übergeordnete Element **Recordset** genau eine Zeile enthält. Dies ist hilfreich zum Berechnen von Aggregaten "Gesamtsumme" über das gesamte untergeordnete **Recordset**.  
  
 Das SHAPE-Befehl-Konstrukt können Sie programmgesteuert eine geformten erstellen auch **Recordset**. Anschließend können Sie zugreifen, die Bestandteile der **Recordset** programmgesteuert oder über eine entsprechende visual-Steuerelement. Wie alle anderen ADO-Befehlstext ist ein Shape-Befehl ausgegeben. Weitere Informationen finden Sie unter [Form Befehle im allgemeinen](../../../ado/guide/data/shape-commands-in-general.md).  
  
 Unabhängig von der Art der übergeordneten **Recordset** wird gebildet, enthält es eine Kapitelspalte, die verwendet wird, besteht die Beziehung zu einer untergeordneten **Recordset**. Wenn Sie möchten, das übergeordnete Element **Recordset** Spalten, die Aggregate (SUM, MIN, MAX, usw.) enthalten kann auch über die untergeordneten Zeilen haben. Das übergeordnete Element und dem untergeordneten **Recordset** können Spalten mit einem Ausdruck auf die Zeile in der **Recordset**sowie Spalten, die neue und anfänglich sind leer.  
  
 Dieser Abschnitt beginnt mit dem folgenden Thema.  
  
-   [Visual Basic Example of Data Shaping (Visual Basic-Beispiel der Datenstrukturierung)](../../../ado/guide/data/visual-basic-example-of-data-shaping.md)
