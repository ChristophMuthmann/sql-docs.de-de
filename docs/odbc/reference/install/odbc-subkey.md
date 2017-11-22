---
title: "ODBC-Unterschlüssel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- registry entries for data sources [ODBC], ODBC subkey
- subkeys [ODBC], ODBC subkey
- ODBC subkey [ODBC]
ms.assetid: f9534144-8f42-4946-b0fb-638e9dcde9c8
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a01cda7280ec0a6a70bca8cf7f9fdec503c92d7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-subkey"></a>ODBC-Unterschlüssel
Die Werte unter dem Unterschlüssel ODBC angeben ODBC Ablaufverfolgungsoptionen. Diese Optionen werden festgelegt, der Registerkarte "Ablaufverfolgung" angezeigt wird, indem Sie im Dialogfeld ODBC-Datenquellenadministrator **SQLManageDataSources**. Der ODBC-Unterschlüssel selbst ist optional. Das Format der folgenden Werte ist wie in der folgenden Tabelle gezeigt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|Ablaufverfolgung|REG_SZ|**0** &#124; **1**|  
|TraceFile|REG_SZ|*Tracefile-Pfad*|  
  
 Die Werte enthalten, die in der folgenden Tabelle beschriebenen Bedeutungen.  
  
|Wert|Bedeutung|  
|-----------|-------------|  
|Ablaufverfolgung|Wenn die Trace-Wert festgelegt ist auf 1 eine Anwendung ruft **SQLAllocHandle** mit der Option SQL_HANDLE_ENV Ablaufverfolgung für die aufrufende Anwendung aktiviert ist.<br /><br /> Wenn das Trace-Schlüsselwort auf 0 festgelegt wird, wenn eine Anwendung ruft **SQLAllocHandle** mit der Option SQL_HANDLE_ENV auf die Ablaufverfolgung für die aufrufende Anwendung deaktiviert ist. Dies ist der Standardwert.<br /><br /> Eine Anwendung aktivieren oder deaktivieren die Ablaufverfolgung mit der SQL_ATTR_TRACE-Verbindungsattribut. Dadurch allerdings daher nicht auf die Daten für diesen Wert ändern.|  
|TraceFile|Wenn die Ablaufverfolgung aktiviert ist, schreibt der Treiber-Manager in der Ablaufverfolgungsdatei, die durch den Wert für die Ablaufverfolgungsdatei angegeben.<br /><br /> Wenn keine der Ablaufverfolgungsdatei angegeben wird, schreibt der Treiber-Manager zur Sql.log-Datei auf das aktuelle Laufwerk. Dies ist der Standardwert.<br /><br /> Die Ablaufverfolgung sollte nur für eine einzelne Anwendung verwendet werden, oder jede Anwendung sollte eine andere Ablaufverfolgungsdatei angeben. Andernfalls werden mindestens zwei Anwendungen versucht, öffnen Sie die gleiche Datei zur gleichen Zeit verursacht einen Fehler.<br /><br /> Eine Anwendung kann eine neue Ablaufverfolgungsdatei mit SQL_ATTR_TRACEFILE-Verbindungsattribut angeben. Dadurch allerdings daher nicht auf die Daten für diesen Wert ändern.|  
  
 Nehmen wir beispielsweise an, dass die Ablaufverfolgung aktiviert ist und die Ablaufverfolgungsdatei C:\Odbc.log. Die Werte unter dem Unterschlüssel ODBC würde wie folgt lauten:  
  
```  
Trace : REG_SZ : 1  
TraceFile : REG_SZ : C:\ODBC.LOG  
  
```
