---
title: Behandeln von Fehlern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cfcb29aa70f9bfb56c793f6fa5d1d8b31d45f8bf
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="handling-errors"></a>Behandeln von Fehlern
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Bei Verwendung der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], alle werden datenbankfehlerbedingungen an Ihre Java-Anwendung als Ausnahmen mithilfe der [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) Klasse. Die folgenden Methoden der SQLServerException-Klasse werden von "java.SQL.SqlException" und "java.lang.Throwable" geerbt; Sie können verwendet werden, um bestimmte Informationen zurückgegeben werden sollen, und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] aufgetretenen Fehler:  
  
-   GetSQLState gibt den normalen X / Open- oder SQL99-Statuscode der Ausnahme zurück.  
  
-   GetErrorCode gibt die jeweilige datenbankfehlernummer zurück.  
  
-   GetMessage gibt den vollständigen Text der Ausnahme zurück. Der Text der Fehlermeldung beschreibt das Problem und enthält häufig Platzhalter für Informationen wie Objektnamen, die in die angezeigte Fehlermeldung eingefügt werden.  
  
-   GetNextException gibt das nächste SQLServerException-Objekt oder Null zurück, wenn es sind keine weiteren Ausnahmeobjekte mehr zurückgegeben.  
  
 Im folgenden Beispiel wird eine offene Verbindung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] -Beispieldatenbank an die Funktion übergeben und eine fehlerhafte SQL­Anweisung erstellt, die nicht mit eine FROM-Klausel verfügt. Anschließend werden die Anweisung ausgeführt und eine SQL-Ausnahme verarbeitet.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Diagnostizieren von Problemen mit dem JDBC-Treiber](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
