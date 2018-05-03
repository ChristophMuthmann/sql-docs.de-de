---
title: Empfangen von mehreren Recordsets | Microsoft Docs
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
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c19e7bc5f1c69bfc885375f7202c76bf296dfd88
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="receiving-multiple-recordsets"></a>Mehrere Recordsets empfangen
Die [Microsoft OLE DB-Anbieter für SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) unterstützt das Zurückgeben von mehreren **Recordset** Objekte für einen einzelnen Befehl, die mehrere SQL-Anweisungen enthält eine **Recordset**pro SQL-Anweisung. In welcher Reihenfolge die **Recordset**e zurückgegeben folgt dabei der Reihenfolge, in der die SQL-Anweisungen im Befehlstext eingefügt werden.  
  
 Microsoft OLE DB-Anbieter für SQL Server gibt auch mehrere Resultsets an ADO zurück, wenn der Befehl eine COMPUTE-Klausel enthält. Z. B. ein Befehl mit der folgenden SQL-Anweisung werden die Ergebnisse in zwei zurückgegeben **Recordset** Objekte: eines für das Rowset (*"ProductID"*, *ProductName*, *UnitPrice*), und die andere für den Durchschnittspreis aller Produkte in der Tabelle.  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 Sie können die **Recordset.NextRecordset** Methode, um die beiden Objekte aufzulisten.  
  
 Weitere Informationen finden Sie unter [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md).
