---
title: Durch Hinzufügen mehrerer Felder | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 691ad7a1a48ea0f733db145a4a03ddd841383962
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="adding-multiple-fields-and-values"></a>Hinzufügen von mehreren Feldern und Werten
In einigen Fällen ist es möglicherweise effizienter, für die Übergabe in einem Array von Feldern und die entsprechenden Werte auf die **AddNew** -Methode, anstatt **Wert** mehrere Male für jedes neue Feld. Wenn *FieldList* ist ein Array *Werte* muss auch ein Array mit derselben Anzahl von Elementen ist andernfalls, ein Fehler auftritt. Die Reihenfolge von Feldnamen muss die Reihenfolge der Feldwerte in jedem Array entsprechen. Folgender Code übergibt ein Array von Feldern und ein Array von Werten, die **AddNew** Methode.

```
'BeginAddNew2
    Dim avarFldNames As Variant
    Dim avarFldValues As Variant

    avarFldNames = Array("CompanyName", "Phone")
    avarFldValues = Array("Sample Shipper 2", "(931) 555-6334")

    If objRs1.Supports(adAddNew) Then
        objRs1.AddNew avarFldNames, avarFldValues
    End If

    'Re-establish a Connection and update
    Set objRs1.ActiveConnection = GetNewConnection
    objRs1.UpdateBatch
'EndAddNew2
```
