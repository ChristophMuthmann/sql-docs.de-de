---
title: Binden von Parametern ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- binding parameters [ODBC]
ms.assetid: 7538a82b-b08b-4c8f-9809-e4ccea16db11
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fedc7d179a3c40c0859b8b1bed4a9c77f1e8c565
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="binding-parameters-odbc"></a>Binden von Parametern ODBC
Jeder Parameter in einer SQL­Anweisung muss zugeordnet sein oder *gebunden,* einer Variablen in der Anwendung, bevor die Anweisung ausgeführt wird. Wenn die Anwendung eine Variable auf einen Parameter bindet, wird diese Variable beschrieben – Adresse, C-Datentyp usw. – an den Treiber. Es beschreibt auch die Parameter selbst – SQL-Daten Datentyp, Genauigkeit und So weiter. Der Treiber speichert diese Informationen in der Struktur, die sie für diese Anweisung verwaltet und verwendet die Informationen zum Abrufen des Werts aus der Variablen ein, wenn die Anweisung ausgeführt wird.  
  
 Parameter können gebunden oder erneut zu einem beliebigen Zeitpunkt vor der Ausführung einer Anweisung gebunden werden. Wenn ein Parameter neu ist, nachdem eine Anweisung ausgeführt wird, gilt die Bindung nicht erst die Anweisung erneut ausgeführt wird. Um einen Parameter an eine andere Variable binden, wird eine Anwendung einfach den Parameter mit der neuen Variablen; die vorherige Bindung wird automatisch freigegeben.  
  
 Eine Variable bleibt auf einen Parameter gebunden, bis eine andere Variable an den Parameter gebunden ist, bis alle Parameter durch den Aufruf ungebunden sind **SQLFreeStmt** mit der Option SQL_RESET_PARAMS oder bis die Anweisung aufgehoben wird. Aus diesem Grund muss die Anwendung sicher sein, dass die Variablen nicht erst freigegeben werden, nachdem diese aufgehoben wurden. Weitere Informationen finden Sie unter [Allocating und Freigeben von Puffern](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Da parameterbindungen nur Informationen, die in der Struktur, die vom Treiber für die Anweisung verwaltet gespeichert sind, können sie in beliebiger Reihenfolge festgelegt werden. Sie sind jedoch auch unabhängig von der SQL-Anweisung, die ausgeführt wird. Nehmen wir beispielsweise an eine Anwendung bindet die drei Parameter und führt dann die folgende SQL-Anweisung:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Wenn die Anwendung dann führt die SQL-Anweisung sofort aus  
  
```  
SELECT * FROM Orders WHERE OrderID = ?, OpenDate = ?, Status = ?  
```  
  
 über das Anweisungshandle die parameterbindungen für die **einfügen** Anweisung werden verwendet, da die Bindungen in der Anweisung Struktur gespeichert sind. In den meisten Fällen wird einem schlechten Programmierstil es sollte vermieden werden. Stattdessen sollte die Anwendung aufrufen **SQLFreeStmt** mit der Option SQL_RESET_PARAMS, trennen alle alten Parameter und dann binden Sie neue.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Binden von Parametermarkierungen](../../../odbc/reference/develop-app/binding-parameter-markers.md)  
  
-   [Binden von Parametern anhand des Namens (benannte Parameter)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)  
  
-   [Offsets der Parameterbindung](../../../odbc/reference/develop-app/parameter-binding-offsets.md)  
  
-   [Describing Parameters (Beschreiben von Parametern)](../../../odbc/reference/develop-app/describing-parameters.md)
