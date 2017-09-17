---
title: Grundlegendes zu Transaktionen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64a9539296531bc0d07d79da3613eb953fefa917
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-transactions"></a>Grundlegendes zu Transaktionen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei Transaktionen handelt es sich um Gruppen von Operationen, die in logische Arbeitseinheiten zusammengefasst sind. Damit wird die Konsistenz und Integrität der einzelnen Aktionen in einer Transaktion gesteuert und gewährleistet, falls im System Fehler auftreten sollten.  
  
 Mit der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], eine lokale oder verteilte transaktionsverarbeitung möglich. Transaktionen können auch Isolationsstufen verwenden. Weitere Informationen zu den vom JDBC-Treiber unterstützten Isolationsstufen finden Sie unter [Grundlegendes zu Isolationsstufen](../../connect/jdbc/understanding-isolation-levels.md).  
  
 Anwendungen sollten Transaktionen nur entweder mit Transact-SQL-Anweisungen oder den vom JDBC-Treiber bereitgestellten Methoden steuern. Wenn für die gleiche Transaktion sowohl Transact-SQL-Anweisungen als auch JDBC-API-Methoden verwendet werden, führt dies möglicherweise zu Problemen, z. B. kann der Commit einer Transaktion nicht wie erwartet durchgeführt werden, ein unerwarteter Commit oder Rollback der Transaktion wird durchgeführt und eine neue Transaktion gestartet, oder es treten Ausnahmen wie "Fehler beim Wiederaufnehmen der Transaktion" auf.  
  
## <a name="using-local-transactions"></a>Verwenden von lokalen Transaktionen  
 Eine Transaktion wird als lokal angesehen, wenn es sich um eine Einphasentransaktion handelt, die von der Datenbank direkt verarbeitet wird. Der JDBC-Treiber unterstützt lokale Transaktionen mithilfe der verschiedenen Methoden der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse, einschließlich [SetAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [Commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md), und [Rollback](../../connect/jdbc/reference/rollback-method.md). Lokale Transaktionen werden normalerweise explizit von der Anwendung oder automatisch vom Anwendungsserver für die Java-Plattform, Enterprise Edition (Java EE) verwaltet.  
  
 Im folgende Beispiel wird eine lokale Transaktion, die aus zwei getrennten Anweisungen im besteht die `try` Block. Die Anweisungen ausgeführt werden, für die Production.ScrapReason-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank und stehen ein Commit ausgeführt, wenn keine Ausnahmen ausgelöst werden. Der Code in der `catch` -Block einen Rollback die Transaktion, wenn eine Ausnahme ausgelöst wird.  
  
 [!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]  
  
## <a name="using-distributed-transactions"></a>Verwenden von verteilten Transaktionen  
 Eine verteilte Transaktion aktualisiert Daten in mindestens zwei vernetzten Datenbanken, wobei die wichtigen Eigenschaften der Transaktionsverarbeitung (unteilbar, konsistent, isoliert und dauerhaft) gewährleistet werden. Die Unterstützung verteilter Transaktionen wurde in der optionalen API-Spezifikation von JDBC 2.0 in die JDBC-API aufgenommen. Die Verwaltung verteilter Anwendungen wird normalerweise automatisch vom JTS-Transaktions-Manager (Java Transaction Service) in einer Java EE-Anwendungsserverumgebung ausgeführt. Allerdings die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt verteilte Transaktionen Java-Transaktion API (mit jedem JTA) kompatible Transaktions-Manager.  
  
 Der JDBC-Treiber integriert sich nahtlos mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] Distributed Transaction Coordinator (MS DTC) auf "true" bieten Unterstützung von verteilten Transaktionen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. MS DTC ist eine Funktion für verteilte Transaktionen gebotenen [!INCLUDE[msCoName](../../includes/msconame_md.md)] für [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Systemen. MS DTC verwendet bewährte transaktionsverarbeitungstechnologien von [!INCLUDE[msCoName](../../includes/msconame_md.md)] , XA-Funktionen wie das vollständige verteilte Zweiphasencommit-Protokoll und die Wiederherstellung von verteilten Transaktionen zu unterstützen.  
  
 Weitere Informationen zur Verwendung von verteilten Transaktionen finden Sie unter [XA-Transaktionen](../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Transaktionen mit der JDBC-Treiber](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
