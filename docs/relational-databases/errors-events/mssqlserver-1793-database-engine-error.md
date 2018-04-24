---
title: MSSQLSERVER_1793 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00919111d7df7f3e6a3077a5c99e355c93abacad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|1793|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|Meldungstext|Das Löschen des Indexes '%.*ls' ist nicht möglich, da kein Partitionsschema für FILESTREAM-Daten angegeben wurde.|  
  
## <a name="explanation"></a>Erklärung  
Diese Meldung wird angezeigt, wenn Sie versuchen, einen gruppierten Index für eine Tabelle zu löschen, die FILESTREAM-Daten enthält, und eine **MOVE TO**-Klausel für die Basisdaten angeben, dabei aber keine **FILESTREAM_ON**-Klausel für die FILESTREAM-Daten bereitstellen.  
  
## <a name="user-action"></a>Benutzeraktion  
Verwenden Sie beim Löschen eines gruppierten Indexes in einer Tabelle, die FILESTREAM-Daten enthält, eine der folgenden Optionen:  
  
-   Geben Sie sowohl eine **MOVE TO**-Klausel für die Basisdaten als auch eine **FILESTREAM_ON**-Klausel für die FILESTREAM-Daten an.  
  
-   Geben Sie nicht entweder eine **MOVE TO**-Klausel für die Basisdaten oder eine **FILESTREAM_ON**-Klausel für die FILESTREAM-Daten an.  
  
Im folgenden Beispiel tritt ein Fehler auf, da ein Partitionsschema für die Basisdaten angegeben ist, jedoch nicht für die FILESTREAM-Daten.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
Das folgende Beispiel ist erfolgreich, da sowohl eine **MOVE TO**-Klausel für die Basisdaten als auch eine **FILESTREAM_ON**-Klausel für die FILESTREAM-Daten angegeben wird.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
Das folgende Beispiel ist auch erfolgreich, da weder eine **MOVE TO**-Klausel für die Basisdaten noch eine **FILESTREAM_ON**-Klausel für die FILESTREAM-Daten angegeben wird.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
