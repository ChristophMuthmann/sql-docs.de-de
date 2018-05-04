---
title: Hinzufügen von Datensätzen mit AddNew | Microsoft Docs
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
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ba15d68b5fbaa749e00987b1fbfef73887dc377
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="adding-records-using-addnew-method"></a>Hinzufügen von Datensätzen mit AddNew-Methode
Dies ist die grundlegende Syntax der **AddNew** Methode:

 *Recordset*. AddNew *FieldList*, *Werte*

 Die *FieldList* und *Werte* Argumente sind optional. *Feldliste* ist ein einzelner Name oder ein Array von Namen oder die Ordnungsposition der Felder im neuen Datensatz.

 Die *Werte* Argument ist ein einzelner Wert oder ein Array von Werten für die Felder im neuen Datensatz.

 In der Regel, wenn Sie beabsichtigen, einen einzelnen Datensatz hinzuzufügen, rufen Sie die **AddNew** -Methode ohne Argumente. Rufen Sie insbesondere **AddNew**; legen die **Wert** jedes Feld im neuen Datensatz; und rufen dann **Update** oder **UpdateBatch**, oder beide. Sie können sicherstellen, dass Ihre **Recordset** unterstützt das Hinzufügen von neuen Datensätzen mit der **unterstützt** Eigenschaft mit dem **AdAddNew** Enumerationskonstante.

 Der folgende Code verwendet dieses Verfahren zum Beispiel ein neues Versandunternehmen hinzuzufügende **Recordset**. Den Wert des Felds Firmen-Nr wird von SQL Server automatisch bereitgestellt. Aus diesem Grund versucht der Code keinen Feldwert für neue Datensätze angeben.

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>Hinweise
 Da dieser Code verwendet wird, eine nicht verbundene **Recordset** mit einem clientseitigen Cursor im Batchmodus ausgeführt, müssen Sie die Verbindung der **Recordset** mit der Datenquelle mit einem neuen **Verbindung** -Objekt vor dem Aufruf können die **UpdateBatch** Methode zum Bereitstellen von Änderungen an der Datenbank. Dies erfolgt einfach mithilfe der neuen Funktion **GetNewConnection**.
