---
title: Verwenden von Anweisungen mit SQL | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5cba782d32a60b2bbdcf61276db6a1989f82c50b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-statements-with-sql"></a>Verwenden von Anweisungen mit SQL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Beim Arbeiten mit Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] und Inline-SQL-Anweisungen, verschiedenen Klassen, die Sie verwenden können. Die verwendete Klasse hängt vom Typ der SQL-Anweisung ab, die ausgeführt werden soll.  
  
 Wenn die SQL-Anweisung keine IN-Parameter enthält, verwenden Sie die [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) Klasse, aber wenn Parameter vorhanden sind, verwenden die [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) Klasse.  
  
> [!NOTE]  
>  Wenn müssen Sie SQL-Anweisungen verwenden, die in- und OUT-Parameter verwenden, müssen Sie diese als gespeicherte Prozeduren implementieren und rufen sie mithilfe der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) Klasse. Weitere Informationen zum Verwenden gespeicherter Prozeduren finden Sie unter [Using-Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
 Die folgenden Abschnitte beschreiben die verschiedenen Szenarien für die Arbeit mit Daten in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe von SQL-Anweisungen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Verwenden einer SQL-Anweisung ohne Parameter](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|Beschreibt die Verwendung von SQL-Anweisungen, die keine Parameter enthalten.|  
|[Verwenden eine SQL-Anweisung mit Parametern](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|Beschreibt die Verwendung von SQL-Anweisungen, die Parameter enthalten.|  
|[Verwenden eine SQL-Anweisung zum Ändern von Datenbankobjekten](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|Beschreibt die Verwendung von SQL-Anweisungen, um Datenbankobjekte zu ändern.|  
|[Verwenden eine SQL-Anweisung zum Ändern von Daten](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|Beschreibt die Verwendung von SQL-Anweisungen, um Daten in einer Datenbank zu ändern.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit der JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

