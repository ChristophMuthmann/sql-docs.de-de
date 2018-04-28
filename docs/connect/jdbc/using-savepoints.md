---
title: Verwenden von Sicherungspunkten | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3b48eb13-32ef-4fb3-8e95-dbc9468c9a44
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dccc8739a02fa478c153bbbe1702b925942f8efd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-savepoints"></a>Verwenden von Sicherungspunkten
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Sicherungspunkte bieten einen Mechanismus, um für Abschnitte einer Transaktion einen Rollback auszuführen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie mithilfe der Anweisung "SAVE TRANSACTION Sicherungspunktname" einen Sicherungspunkt erstellen. Später können Sie die Anweisung "ROLLBACK TRANSACTION Sicherungspunktname" ausführen, um ein Rollback bis zum Sicherungspunkt auszuführen, anstatt ein Rollback bis zum Beginn der Transaktion auszuführen.  
  
 Sicherungspunkte sind vor allem in Situationen hilfreich, in denen das Auftreten von Fehlern unwahrscheinlich ist. Die Verwendung eines Sicherungspunkts, um für einen Teil einer Transaktion im Falle eines seltenen Fehlers einen Rollback auszuführen, kann effizienter sein, als jede Transaktion vor dem Ausführen einer Aktualisierung daraufhin testen zu lassen, ob die Aktualisierung gültig ist. Aktualisierungen und Rollbacks sind kostspielige Operationen. Sicherungspunkte sind also nur dann effektiv, wenn die Wahrscheinlichkeit eines Fehlers gering und die Kosten für die Vorabüberprüfung der Gültigkeit einer Aktualisierung relativ hoch sind.  
  
 Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die Verwendung von Sicherungspunkten über die [SetSavepoint](../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md) Methode der [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) Klasse. Verwenden Sie die SetSavepoint-Methode, können Sie in der aktuellen Transaktion einen benannten oder unbenannten Sicherungspunkt erstellen, und der Methodenrückgabewert ein [SQLServerSavepoint](../../connect/jdbc/reference/sqlserversavepoint-class.md) Objekt. In einer Transaktion können mehrere Sicherungspunkte erstellt werden. Um eine Transaktion zu einem bestimmten Sicherungspunkt zurückzusetzen, können Sie das SQLServerSavepoint-Objekt, das Übergeben der [Rollback (java.sql.Savepoint)](../../connect/jdbc/reference/rollback-method-java-sql-savepoint.md) Methode.  
  
 Im folgenden Beispiel wird ein Sicherungspunkt verwendet beim Ausführen einer lokalen Transaktions mit zwei getrennten Anweisungen in der `try` Block. Die Anweisungen ausgeführt werden, für die Production.ScrapReason-Tabelle in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] Beispieldatenbank und einen Sicherungspunkt wird verwendet, um die zweite Anweisung ein Rollback auszuführen. Dies führt dazu, dass nur für die erste Anweisung ein Commit in der Datenbank ausgeführt wird.  
  
 [!code[JDBC#UsingSavepoints1](../../connect/jdbc/codesnippet/Java/using-savepoints_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Transaktionen mit dem JDBC-Treiber](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
