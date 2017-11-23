---
title: Verwenden von Servercursorn | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d6be8e988dfa7cc388544a215a333d6eb876bf7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-server-cursors"></a>Verwenden von Servercursorn
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Wenn eine ODBC-Anwendung eine ODBC-Cursorattribute auf etwas anderes als die Standardwerte festlegt der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber fordert der Server ein API-Servercursor desselben Typs zu implementieren. Durch die Verwendung von API-Servercursorn wird auf dem Client Arbeitsspeicher freigegeben, und zudem kann der Netzwerkdatenverkehr zwischen dem Client und dem Server erheblich reduziert werden.  
  
 Ein potenzieller Nachteil von API-Servercursorn liegt darin, dass sie zurzeit nicht alle SQL-Anweisungen unterstützen. API-Servercursor können nicht verwendet werden, um Folgendes auszuführen:  
  
-   Batches oder gespeicherte Prozeduren, die mehrere Resultsets zurückgeben  
  
-   SELECT-Anweisungen, die die Klauseln COMPUTE, COMPUTE BY, FOR BROWSE oder INTO enthalten  
  
-   Eine EXECUTE-Anweisung, die auf eine remote gespeicherte Prozedur verweist  
  
 Wenn eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] besteht, führt die Ausführung einer Anweisung mit diesen Merkmalen mithilfe eines Servercursors dazu, dass der Cursor in ein Standardresultset konvertiert wird. Wenn eine Verbindung zu früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hergestellt ist, verursacht sie einen Fehler.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Cursorn](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
