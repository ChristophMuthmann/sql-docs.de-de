---
title: Verwenden von Anweisungen mit SQL | Microsoft Docs
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
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 361448b1b27a735f54202a3ec6bbbec8f16ccc72
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
|[Verwenden von SQL-Anweisungen ohne Parameter](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)|Beschreibt die Verwendung von SQL-Anweisungen, die keine Parameter enthalten.|  
|[Verwenden von SQL-Anweisungen mit Parametern](../../connect/jdbc/using-an-sql-statement-with-parameters.md)|Beschreibt die Verwendung von SQL-Anweisungen, die Parameter enthalten.|  
|[Ändern von Datenbankobjekten mit SQL-Anweisungen](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md)|Beschreibt die Verwendung von SQL-Anweisungen, um Datenbankobjekte zu ändern.|  
|[Ändern von Daten mit SQL-Anweisungen](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)|Beschreibt die Verwendung von SQL-Anweisungen, um Daten in einer Datenbank zu ändern.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit dem JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
