---
title: Verwenden der Haltbarkeit | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19dfa43e83b3fe94fa75df6a2713497093a08a96
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-holdability"></a>Verwenden der Haltbarkeit
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Standardmäßig bleibt ein Resultset, das in einer Transaktion erstellt wurde, nach einem Commit der Transaktion in der Datenbank oder einem Rollback geöffnet. Bisweilen ist es aber von Nutzen, das Resultset nach einem Commit der Transaktion zu schließen. Hierzu die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die Verwendung der resultsethaltbarkeit.  
  
 Resultsethaltbarkeit kann festgelegt werden, mithilfe der [SetHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Beim Einstellen der Haltbarkeit, mit der SetHoldability-Methode, die Ergebnismenge resultsethaltbarkeit die Konstanten Hold_cursors_over_commit oder ResultSet.CLOSE_CURSORS_AT_COMMIT verwendet werden können.  
  
 Der JDBC-Treiber unterstützt auch das Festlegen der Haltbarkeit beim Erstellen eines der Statement-Objekte. Beim Erstellen der Statement-Objekte, die mit Parametern für die Resultsethaltbarkeit überladen sind, muss die Haltbarkeit des Statement-Objekts der Haltbarkeit der Verbindung entsprechen. Stimmen sie nicht überein, wird eine Ausnahme ausgelöst. Der Grund hierfür ist, dass SQL Server die Haltbarkeit nur auf Verbindungsebene unterstützt.  
  
 Die Haltbarkeit eines Resultsets handelt es sich um die Haltbarkeit von der SQLServerConnection-Objekt, das das Resultset zum Zeitpunkt der Erstellung der Resultset für nur serverseitige Cursor zugeordnet ist. Dies gilt nicht für clientseitige Cursor. Alle Resultsets mit clientseitigen Cursorn enthält immer den haltbarkeitswert Hold_cursors_over_commit auswirkt.  
  
 Wenn Servercursor mit SQL Server 2005 oder höher verbunden sind, wirkt sich das Festlegen der Haltbarkeit nur auf die Haltbarkeit neuer Resultsets aus, die erst noch für diese Verbindung erstellt werden. Das heißt, das Festlegen der Haltbarkeit hat keine Auswirkungen auf die Haltbarkeit von Resultsets, die zuvor erstellt wurden und für die Verbindung bereits geöffnet sind. Bei SQL Server 2000 wirkt sich das Festlegen der Haltbarkeit jedoch sowohl auf die Haltbarkeit vorhandener als auch neuer, noch für die Verbindung zu erstellender Resultsets aus.  
  
 Im folgenden Beispiel wird die resultsethaltbarkeit beim Ausführen einer lokalen Transaktions mit zwei getrennten Anweisungen in der `try` Block. Die Anweisungen ausgeführt werden, für die Production.ScrapReason-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank. Zunächst im Beispiel zum manuellen Transaktionsmodus gewechselt durch Festlegen des automatische Commits auf **"false"**. Sobald der Autocommit-Modus deaktiviert ist, keine SQL-Anweisungen sind nicht Commit bis die Anwendung ruft die [Commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) Methode explizit. Der Code im catch-Block führt ein Rollback der Transaktion aus, wenn eine Ausnahme ausgelöst wird.  
  
 [!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Transaktionen mit der JDBC-Treiber](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  

