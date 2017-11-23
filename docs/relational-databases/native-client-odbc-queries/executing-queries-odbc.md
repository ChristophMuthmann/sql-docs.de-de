---
title: "Ausführen von Abfragen (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ab0b9697c92b32cdc7184a07bde0bcef05aa796
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="executing-queries-odbc"></a>Ausführen von Abfragen (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Nachdem eine ODBC-Anwendung ein Verbindungshandle initialisiert und eine Verbindung zu einer Datenquelle hergestellt hat, weist sie dem Verbindungshandle ein oder mehrere Anweisungshandles zu. Die Anwendung kann dann ausführen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anweisungen über das Anweisungshandle. Die übliche Reihenfolge bei der Ausführung einer SQL-Anweisung ist:  
  
1.  Festlegen aller erforderlichen Anweisungsattribute.  
  
2.  Erstellen der Anweisung.  
  
3.  Ausführen der Anweisung.  
  
4.  Abrufen der Resultsets.  
  
 Erst nachdem eine Anwendung alle Zeilen in sämtlichen von der SQL-Anweisung zurückgegebenen Resultsets abgerufen hat, kann sie eine weitere Abfrage über dasselbe Anweisungshandle ausführen. Eine Anwendung fest, dass es nicht erforderlich ist, um alle Zeilen in einem bestimmten Resultset abzurufen, können sie den Rest des Resultsets durch den Aufruf eines Abbrechen [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) oder [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md).  
  
 Wenn Sie in einer ODBC-Anwendung dieselbe SQL-Anweisung mehrfach mit unterschiedlichen Daten ausführen müssen, verwenden Sie bei der Erstellung der SQL-Anweisung eine Parametermarkierung in Form eines Fragezeichens (?):  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 Jede parametermarkierung kann dann an eine Programmvariable gebunden werden, durch den Aufruf [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md).  
  
 Nachdem alle SQL-Anweisungen ausgeführt und ihre Resultsets verarbeitet wurden, gibt die Anwendung das Anweisungshandle frei.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt mehrere Anweisungshandles pro Verbindungshandle. Transaktionen werden auf Verbindungsebene verwaltet, d. h. alle über sämtliche Anweisungshandles auf einem einzelnen Verbindungshandle ausgeführten Aufgaben werden als Bestandteil derselben Transaktion verwaltet.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Zuordnen eines Anweisungshandles](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [Erstellen eine SQL-Anweisung &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [Erstellen von SQL-Anweisungen für Cursor](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [Verwenden von Anweisungsparametern](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [Ausführen von Anweisungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [Freigeben eines Anweisungshandles](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
