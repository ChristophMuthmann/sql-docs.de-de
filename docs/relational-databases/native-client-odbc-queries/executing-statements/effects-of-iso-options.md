---
title: Effekte von ISO-Optionen | Microsoft Docs
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
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a127f05771be6d1f1db46d43804a2e888c1af442
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="effects-of-iso-options"></a>Effekte von ISO-Optionen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Der ODBC-Standard orientiert sich eng am ISO-Standard, und ODBC-Anwendungen erwarten von einem ODBC-Treiber Standardverhalten. Ihr Verhalten genauer Übereinstimmung mit vornehmen, die in der ODBC-Standard definiert die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber immer die ISO-Optionen zur Verfügung, in der Version von SQL Server, mit denen sie eine Verbindung herstellt.  
  
 Wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], der Server erkennt, dass der Client verwendet die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und aktiviert mehrere Optionen.  
  
 Der Treiber gibt diese Anweisungen selbst aus; die ODBC-Anwendung fordert sie nicht an. Durch das Einstellen dieser Optionen werden ODBC-Anwendungen, die den Treiber verwenden, besser portierbar, da das Serververhalten dem ISO-Standard entspricht.  
  
 DB-Library-basierte Anwendungen aktivieren diese Optionen im Allgemeinen nicht. Standorte unterschiedliches Verhalten zwischen ODBC oder DB-Library-Clients beim Ausführen der gleichen SQL-Anweisung nicht dadurch annehmen soll, verweist auf ein Problem mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber. Sie sollten zuerst führen Sie die Anweisung in der DB-Library-Umgebung mit denselben SET-Optionen wie belegen würde die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber.  
  
 Da SET-Optionen jederzeit von Benutzern und Anwendungen aktiviert und deaktiviert werden können, sollten Entwickler von gespeicherten Prozeduren und Triggern diese mit den oben aufgeführten SET-Optionen sowohl im aktivierten als auch im deaktivierten Zustand testen. Dadurch wird sichergestellt, dass die Prozeduren und Trigger bei ihrem Aufruf korrekt ausgeführt werden, unabhängig davon, welche Optionen eine bestimmte Verbindung festgelegt hat. Wenn ein Trigger oder eine gespeicherte Prozedur eine bestimmte Einstellung für eine dieser Optionen erfordert, sollte am Anfang des Triggers bzw. der gespeicherten Prozedur eine SET-Anweisung ausgeführt werden. Die SET-Anweisung behält ihre Gültigkeit nur während der Ausführung des Triggers bzw. der gespeicherten Prozedur bei. Wenn der Trigger oder die Prozedur beendet ist, wird die ursprüngliche Einstellung wiederhergestellt.  
  
 Wenn eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hergestellt wird, wird zudem eine vierte SET-Option, CONCAT_NULL_YIELDS_NULL, aktiviert. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ist nicht dieser Optionen an If festgelegt AnsiNPW = NO angegeben ist, in der Datenquelle oder für [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) oder [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 Der ISO-Optionen, wie der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ist nicht aktiviert die QUOTED_IDENTIFIER-Option auf If QuotedID = NO angegeben ist, in der Datenquelle oder für **SQLDriverConnect** oder  **SQLBrowseConnect**.  
  
 Damit der Treiber den aktuellen Status der SET-Optionen ermitteln kann, sollten ODBC-Anwendungen die [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET-Anweisung nicht verwenden, um diese Optionen festzulegen. Sie sollten diese Optionen nur mithilfe der Datenquelle oder über die Verbindungsoptionen festlegen. Wenn die Anwendung SET-Anweisungen ausgibt, generiert der Treiber möglicherweise falsche SQL-Anweisungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Anweisungen &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
