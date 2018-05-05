---
title: Umformen | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 010504a6fe07b952f59631769bd288970c7904c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="reshaping"></a>Umformen
Ein **Recordset** erstellt eine-Klausel einer Form Befehl zugewiesen werden kann ein *Alias* Name (in der Regel mit dem AS-Schlüsselwort). Der Alias des eine geformten **Recordset** in einem ganz anderen Befehl verwiesen werden kann. D. h., Sie können wiederverwenden, oder *umformen*, eine zuvor geformten **Recordset** in einem neuen Shape-Befehl. Um dieses Feature zu unterstützen, stellt ADO eine Eigenschaft bereit, mit denen [umformen Namen](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md).  
  
 Umformen hat zwei Hauptfunktionen. Der erste Schritt besteht im Zuordnen einer vorhandenen **Recordset** mit einem neuen übergeordneten **Recordset**.  
  
## <a name="example"></a>Beispiel  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 Die zweite Funktion wird für nicht in Kapitel unterteilten den Zugriff auf vorhandene untergeordnete **Recordset** Objekte, mit der Syntax "Form" \<Recordset umformen Name > ".  
  
> [!NOTE]
>  Spalten kann nicht angefügt werden, um eine vorhandene **Recordset**, Neustrukturieren eine parametrisierte **Recordset** oder **Recordset** Objekte in alle Beteiligten COMPUTE-Klausel, oder führen Vorgänge für ein beliebiges aggregieren **Recordset** Nachfolger der **Recordset** Form wird. Die **Recordset** Form wird und die neue Form Befehl müssen beide die gleiche verwenden [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Data Shaping Example (Beispiele der Datenstrukturierung)](../../../ado/guide/data/data-shaping-example.md)
