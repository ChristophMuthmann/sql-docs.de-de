---
title: 'Alternativen: SQL-Anweisungen mithilfe | Microsoft Docs'
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
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 40d0554ed5dc50f4b059de510d17608fb33077c6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="alternatives-using-sql-statements"></a>Alternativen: SQL-Anweisungen mithilfe
ADO kann auch mithilfe der Befehle als alternativen zu den integrierten Eigenschaften und Methoden zum Bearbeiten von Daten. Abhängig von Ihrem Anbieter, können alle Vorgänge, die in diesem Abschnitt aufgeführten auch verwendet werden Befehle an die Datenquelle übergeben. Beispielsweise können SQL-UPDATE-Anweisungen verwendet werden, zum Ändern von Daten ohne Verwendung der **Wert** Eigenschaft eine **Feld**. SQL-INSERT-Anweisungen können verwendet werden, um neue Datensätze zu einer Datenquelle, statt die ADO-Methode hinzufügen **AddNew**. Weitere Informationen zu den SQL- oder der Datenbearbeitungssprache Ihres Anbieters finden Sie in der Dokumentation der Datenquelle.  
  
 Beispielsweise können Sie eine SQL-Zeichenfolge, die mit einer DELETE-Anweisung in einer Datenbank übergeben, wie im folgenden Code gezeigt:  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
