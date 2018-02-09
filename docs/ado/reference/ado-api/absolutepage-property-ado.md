---
title: AbsolutePage-Eigenschaft (ADO) | Microsoft Docs
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
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 677b512a88fe3b6e695bd460cb0d4dea00ed673d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="absolutepage-property-ado"></a>AbsolutePage-Eigenschaft (ADO)
Gibt an, auf der Seite zum aktuelle Datensatz befindet.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt für 32-Bit-Code oder gibt eine **lange** Wert zwischen 1 und die Anzahl der Seiten in der [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt (["PageCount"](../../../ado/reference/ado-api/pagecount-property-ado.md)), oder gibt einen der der [PositionEnum ](../../../ado/reference/ado-api/positionenum.md) Werte.  
  
 Verwenden Sie für 64-Bit-Code einen Datentyp, der für die Speicherung von 64-Bit-Wert enthält. Beispielsweise können Sie entweder **lange** oder einen anderen Wert, der 64-Bit-Länge, z. B. DBORDINAL werden kann. Verwenden Sie keine **PositionEnum** Werte, da sie auf 32-Bit-Länge beschränkt sind.  
  
## <a name="remarks"></a>Hinweise  
 Diese Eigenschaft kann verwendet werden, um die Seitenzahl zu identifizieren, auf der sich der aktuelle Datensatz befindet. Er verwendet die [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) Eigenschaft, um die Anzahl der insgesamt Rowset von logisch zu unterteilen der **Recordset** Objekt in eine Reihe von Seiten, von denen jeder die Anzahl der Datensätze, die gleich hat **PageSize** (mit Ausnahme der letzten Seite, die weniger Datensätze haben kann). Der Anbieter muss die entsprechende Funktionalität für diese Eigenschaft verfügbar sein unterstützen.  
  
-   Beim Abrufen oder Festlegen der **AbsolutePage** -Eigenschaft, die ADO verwendet die [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) Eigenschaft und die [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) -Eigenschaft wie folgt zusammen:  
  
-   Zum Abrufen der **AbsolutePage**, ADO zunächst Ruft die **AbsolutePosition**, und dann dividiert durch die **PageSize**.  
  
-   Festlegen der **AbsolutePage**, ADO wechselt die **AbsolutePosition** wie folgt: multipliziert es die **PageSize** durch die neue **AbsolutePage** Wert, und klicken Sie dann den Wert 1 hinzugefügt. Daher die aktuelle position in der **Recordset** nach dem erfolgreichen festlegen **AbsolutePage** ist der erste Datensatz in dieser Seite.  
  
 Wie die **AbsolutePosition** Eigenschaft **AbsolutePage** ist 1-basiert und entspricht 1, wenn der aktuelle Datensatz der erste Datensatz im ist die **Recordset**. Legen Sie diese Eigenschaft auf den ersten Eintrag in einer bestimmten Seite verschoben. Abrufen der Gesamtanzahl von Seiten aus der **"PageCount"** Eigenschaft.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [AbsolutePage "PageCount" und PageSize Eigenschaften Beispiel (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage "PageCount" und PageSize Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition-Eigenschaft (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 ["PageCount"-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize-Eigenschaft (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
