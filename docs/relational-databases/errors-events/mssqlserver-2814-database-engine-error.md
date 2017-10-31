---
title: MSSQLSERVER_2814 | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 109b5a18604b2111f3344ba216a6d3d98131d116
ms.openlocfilehash: 3bca883d9f5b13b81e021014193df43fc3f5f6e3
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="mssqlserver2814"></a>MSSQLSERVER_2814
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2814|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|PR_POSSIBLE_INFINITE_RECOMPILE|  
|Meldungstext|Es wurde ein mögliche unbegrenzte Neukompilierung für SQLHANDLE %hs, PlanHandle %hs, Startoffset %d, Endoffset %d erkannt. Die letzte Ursache für die Neukompilierung war %d.|  
  
## <a name="explanation"></a>Erklärung  
Eine oder mehrere Anweisungen haben bewirkt, dass der Abfragebatch mindestens 50 Mal neu kompiliert wurde. Die angegebene Anweisung sollte korrigiert werden, um weitere Neukompilierungen zu vermeiden.  
  
In der folgenden Tabelle werden die Ursachen für die Neukompilierung aufgelistet.  
  
|Ursachencode|Description|  
|---------------|---------------|  
|1|Schema geändert|  
|2|Statistiken geändert|  
|3|Verzögerte Kompilierung|  
|4|Festgelegte Option geändert|  
|5|Temp. Tabelle geändert|  
|6|Remote-Rowset geändert|  
|7|For Browse-Berechtigungen geändert|  
|8|Abfragebenachrichtigungsumgebung geändert|  
|9|Partitionierte Sicht geändert|  
|10|Cursoroptionen geändert|  
|11|Option (Neukompilierung) angefordert|  
  
## <a name="user-action"></a>Benutzeraktion  
  
1.  Zeigen Sie die Anweisung an, die die Neukompilierung verursacht, indem Sie die folgende Abfrage ausführen. Ersetzen Sie die Platzhalter *sql_handle*, *starting_offset*, *ending_offset* und *plan_handle* durch die in der Fehlermeldung angegebenen Werte. Die Spalten **database_name** und **object_name** haben für Ad-hoc- und vorbereitete [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen den Wert NULL.  
  
    ```sql   
    SELECT DB_NAME(st.dbid) AS database_name,  
        OBJECT_NAME(st.objectid) AS object_name,  
        st.text  
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
    WHERE qs.statement_start_offset = *starting_offset*  
    AND qs.statement_end_offset = *ending_offset*  
    AND qs.plan_handle = *plan_handle*;
    ```
  
2.  Ändern Sie auf Grundlage der Beschreibung des Ursachencodes die Anweisung, den Batch oder die Prozedur, um Neukompilierungen zu vermeiden. Eine gespeicherte Prozedur kann z. B. eine oder mehrere SET-Anweisungen enthalten. Diese Anweisungen sollten aus der Prozedur entfernt werden. Weitere Beispiele für die Ursachen von Neukompilierungen und Lösungen finden Sie unter [Batch Compilation, Recompilation, and Plan Caching Issues in SQL Server 2005 (Probleme bei der Batchkompilierung, Neukompilierung und beim Zwischenspeichern von Ausführungsplänen in SQL Server 2005)](http://go.microsoft.com/fwlink/?LinkId=69175).  
  
3.  Wenn das Problem wiederholt auftritt, wenden Sie sich an den Microsoft-Kundendienst.  
  
## <a name="see-also"></a>Siehe auch  
[SQL:StmtRecompile Event Class](../event-classes/sql-stmtrecompile-event-class.md)  
  

