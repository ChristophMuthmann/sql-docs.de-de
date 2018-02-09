---
title: Grenzen eines Recordsets | Microsoft Docs
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
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96473d512ed586ebdb155e3422f6559294c2616d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="boundaries-of-a-recordset"></a>Grenzen eines Recordsets
**Recordset** unterstützt die **BOF** und **EOF** Eigenschaften jeweils dem Anfang und Ende des Datasets abgrenzen. Sie können sich vorstellen **BOF** und **EOF** als "phantom" Datensätze, die am Anfang und Ende positioniert sind die **Recordset**. Zählen von **BOF** und **EOF**, unser Beispiel **Recordset** würde wie folgt aussehen:  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|Onkel Bobs Trockenbirnen|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|Manjimup Dried Apples|53.0000|  
|74|Longlife Tofu|10.0000|  
|EOF|||  
  
 Wenn ein Cursor hinter dem letzten Datensatz bewegt **EOF** festgelegt ist, um **"true"**ist, andernfalls ist der Wert **"false"**. Auf ähnliche Weise, wenn der Cursor wird vor dem ersten Datensatz **BOF** festgelegt ist, um **"true"**ist, andernfalls der Wert ist **"false"**. Diese Eigenschaften werden häufig zum Aufzählen der Datensätze aus dem Dataset verwendet, wie im folgenden JScript-Codefragment veranschaulicht.  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 Wenn beide **BOF** und **EOF** sind **"true"**, **Recordset** Objekt leer ist. Beide Eigenschaften werden **"false"** für eine neu geöffnete nicht leere **Recordset** Objekt. Können Sie die **BOF** und **EOF** Eigenschaften zusammen, um festzustellen, wo eine **Recordset** Objekt ist leer oder nicht, wie im folgenden JScript-Codefragment gezeigt.  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 Dieses Schema eignet sich für alle Typen von Cursor und ist unabhängig von der zugrunde liegenden Anbieter. Wenn Sie versuchen, um zu bestimmen, die überprüft, der eine **Recordset** Objekt, indem Sie überprüfen, ob die **RecordCount** Eigenschaftswert ist 0 (null) oder nicht, Sie müssen die entsprechende Vorsichtsmaßnahmen eine entsprechende Cursor und den Anbieter verwenden, unterstützt die Anzahl der Datensätze im Resultset zurückgeben.  
  
 Wenn Sie den letzten verbleibenden Datensatz im Löschen der **Recordset** Objekt ist, wird der Cursor in einem unbestimmten Zustand verbleibt. Die **BOF** und **EOF** Eigenschaften netzwerkverbindungsfehlers **"false"** , bis Sie versuchen, den aktuellen Datensatz neu positionieren, je nach Anbieter. Weitere Informationen finden Sie unter [löschen Datensätze, verwenden Sie die Methode Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md).
