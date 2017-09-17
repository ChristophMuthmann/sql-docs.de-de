---
title: Verwenden von Anweisungen mit der JDBC-Treiber | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5e4cbbfc9d2b73d0a7c79ebc2791f588a7c8f862
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-statements-with-the-jdbc-driver"></a>Verwenden von Anweisungen mit dem JDBC-Treiber
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] dienen zum Arbeiten mit Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank in einer Vielzahl von Möglichkeiten. Mit dem JDBC-Treiber können SQL-Anweisungen für die Datenbank ausgeführt oder gespeicherte Prozeduren in der Datenbank aufgerufen werden, die sowohl Eingabe- als Ausgabeparameter verwenden. Der JDBC-Treiber unterstützt außerdem die Verwendung von SQL-Escapesequenzen, Updatezählungen, automatisch generierten Schlüsseln und die Ausführung von Updates in einer Batchoperation.  
  
 Der JDBC-Treiber umfasst drei Klassen zum Abrufen von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank:  
  
1.  [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) : SQL-Anweisungen ohne Parameter ausführen.  
  
2.  [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) - (geerbt von SQLServerStatement), für die kompilierten SQL-Anweisungen, die IN Parametern enthalten möglicherweise verwendet.  
  
3.  [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) - (geerbt von SQLServerPreparedStatement), für die Ausführung von gespeicherter Prozeduren, die möglicherweise enthalten IN-Parameter und/oder OUT-Parameter oder beides verwendet.  
  
 Die Themen in diesem Abschnitt beschreiben, wie Sie jede der drei Klassen können zum Arbeiten mit Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwenden von Anweisungen mit SQL](../../connect/jdbc/using-statements-with-sql.md)|Beschreibt, wie SQL-Anweisungen mit der JDBC-Treiber zu verwenden, um das Arbeiten mit Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.|  
|[Verwenden von Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md)|Beschreibt, wie gespeicherte Prozeduren mit dem JDBC-Treiber verwenden, arbeiten mit Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.|  
|[Verwenden mehrerer Resultsets](../../connect/jdbc/using-multiple-result-sets.md)|Beschreibt die Verwendung des JDBC-Treibers, um Daten aus mehreren Resultsets abzurufen.|  
|[Verwenden von SQL-Escapesequenzen](../../connect/jdbc/using-sql-escape-sequences.md)|Beschreibt die Verwendung von SQL-Escapesequenzen, wie z. B. Datums- und Zeitliteralen und -funktionen.|  
|[Verwenden von automatisch generierten Schlüsseln](../../connect/jdbc/using-auto-generated-keys.md)|Beschreibt die Verwendung von automatisch generierten Schlüsseln.|  
|[Ausführen von Batchvorgängen](../../connect/jdbc/performing-batch-operations.md)|Beschreibt die Verwendung des JDBC-Treibers, um Batchoperationen auszuführen.|  
|[Verarbeiten komplexer Anweisungen](../../connect/jdbc/handling-complex-statements.md)|Beschreibt die Verwendung des JDBC-Treibers, um komplexe Anweisungen auszuführen, die vielfältige Tasks ausführen und verschiedene Datentypen zurückgeben können.|  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über die JDBC-Treiber](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
