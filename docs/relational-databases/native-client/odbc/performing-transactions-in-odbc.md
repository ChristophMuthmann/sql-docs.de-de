---
title: Transaktionen in ODBC | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2984304ae15715e5a105fa5d6b3272f518cde28
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="performing-transactions-in-odbc"></a>Ausführen von Transaktionen in ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Transaktionen in ODBC werden auf der Verbindungsebene verwaltet. Wenn eine Anwendung eine Transaktion abschließt, führt sie für alle abgeschlossenen Arbeiten einen Commit oder Rollback über alle Anweisungshandles dieser Verbindung aus. Anwendungen müssen zum Ausführen eines Commits oder eines Rollbacks für eine Transaktion keine COMMIT- oder ROLLBACK-Anweisung übermitteln, sondern [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) aufrufen.  
  
 Eine Anwendung ruft [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) auf, um zwischen den beiden ODBC-Modi für die Verwaltung von Transaktionen zu wechseln:  
  
-   Autocommit-Modus  
  
     Für jede erfolgreich ausgeführte Anweisung wird automatisch ein Commit ausgeführt. Im Autocommit-Modus sind keine anderen Funktionen für die Verwaltung von Transaktionen erforderlich.  
  
-   Manualcommit-Modus  
  
     Alle ausgeführten Anweisungen sind in einer Transaktion enthalten, bis diese durch Aufrufen von **SQLEndTran**ausdrücklich beendet wird.  
  
 Der Autocommit-Modus ist der Standardtransaktionsmodus für ODBC. Beim Herstellen einer Verbindung befindet sich diese zunächst im Autocommit-Modus, bis **SQLSetConnectAttr** aufgerufen wird, um durch Deaktivieren des Autocommit-Modus in den Manualcommit-Modus zu wechseln. Wenn eine Anwendung Autocommit deaktiviert, startet die nächste an die Datenbank gesendete Anweisung eine Transaktion. Die Transaktion bleibt dann so lange aktiv, bis die Anwendung **SQLEndTran** mit der Option SQL_COMMIT oder mit der Option SQL_ROLLBACK aufruft. Der Befehl, der an die Datenbank nach **SQLEndTran** gesendet wird, startet die nächste Transaktion.  
  
 Wenn eine Anwendung vom Manualcommit- in den Autocommit-Modus wechselt, führt der Treiber für alle derzeit für die Verbindung geöffneten Transaktionen einen Commit aus.  
  
 ODBC-Anwendungen dürfen keine Transact-SQL-Transaktionsanweisungen, wie BEGIN TRANSACTION, COMMIT TRANSACTION oder ROLLBACK TRANSACTION, verwenden, da dies zu einem unbestimmten Verhalten des Treibers führen kann. Eine ODBC-Anwendung muss im Autocommit-Modus ausgeführt werden und darf keine Funktionen oder Anweisungen für die Verwaltung von Transaktionen verwenden oder im Manualcommit-Modus ausgeführt werden und die ODBC-Funktion **SQLEndTran** zum Ausführen eines Commits oder eines Rollbacks für Transaktionen verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Transaktionen &#40; ODBC &#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
