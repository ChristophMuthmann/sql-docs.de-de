---
title: Behandeln von Fehlern | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33f9c9daa495c26b1a1e35869016f0e7382d9d1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
  
