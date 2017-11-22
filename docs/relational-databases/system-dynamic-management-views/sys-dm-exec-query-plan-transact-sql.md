---
title: Sys. dm_exec_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 72042c7136360436b91ff065362ed8462fab1259
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecqueryplan-transact-sql"></a>sys.dm_exec_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt für den vom Planhandle angegebenen Batch den Showplan im XML-Format zurück. Der vom Planhandle angegebene Plan ist möglicherweise zwischengespeichert oder wird gerade ausgeführt.  
  
 Das XML-Schema für den Showplan ist veröffentlicht und auf [dieser Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)verfügbar. Es ist auch verfügbar im Verzeichnis, in dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_exec_query_plan ( plan_handle )  
```  
  
## <a name="arguments"></a>Argumente  
 *plan_handle*  
 Identifiziert eindeutig einen Abfrageplan für einen Batch, der zwischengespeichert ist oder gerade ausgeführt wird.  
  
 *plan_handle* ist **varbinary(64)** *plan_handle* kann von den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
 [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
 [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**DBID**|**smallint**|ID der Kontextdatenbank, die gültig war, als die diesem Plan entsprechende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung kompiliert wurde. Für Ad-hoc-Anweisungen und vorbereitete SQL-Anweisungen, die ID der Datenbank, in der die Anweisungen kompiliert wurden.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
|**ObjectID**|**int**|ID des Objekts (z. B. gespeicherte Prozedur oder benutzerdefinierte Funktion) für diesen Abfrageplan. Für Ad-hoc- und vorbereitete Batches entspricht diese Spalte dem Wert **NULL**.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
|**Anzahl**|**smallint**|Gespeicherte Prozedur mit ganzer Zahl. Eine Gruppe von Prozeduren für die **orders** -Anwendung kann z. B. die Namen **orderproc;1**, **orderproc;2**usw. haben. Für Ad-hoc- und vorbereitete Batches entspricht diese Spalte dem Wert **NULL**.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
|**verschlüsselt**|**bit**|Zeigt an, ob die entsprechende Prozedur verschlüsselt ist.<br /><br /> 0 = nicht verschlüsselt<br /><br /> 1 = verschlüsselt<br /><br /> NULL-Werte sind in der Spalte nicht zulässig.|  
|**query_plan**|**xml**|Enthält eine zur Kompilierzeit erstellte Showplandarstellung des Abfrageausführungsplans, der mit *plan_handle*angegeben ist. Der Showplan liegt im XML-Format vor. Ein Plan generiert für jeden Batch, die, z. B. ad-hoc-enthält [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, Aufrufe von gespeicherten Prozeduren und benutzerdefinierten Funktionsaufrufe.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
  
## <a name="remarks"></a>Hinweise  
 Unter den folgenden Bedingungen wird keine Showplanausgabe in der **query_plan** -Spalte der zurückgegebenen Tabelle für **sys.dm_exec_query_plan**zurückgegeben:  
  
-   Falls der mit *plan_handle* angegebene Abfrageplan aus dem Plancache entfernt wurde, enthält die **query_plan** -Spalte der zurückgegebenen Tabelle den Wert NULL. Diese Bedingung kann z. B. auftreten, wenn es eine Zeitverzögerung zwischen der Erfassung des Planhandles und seiner Verwendung mit **sys.dm_exec_query_plan**gibt.  
  
-   Einige [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen nicht zwischengespeichert, wie z. B. für Massenvorgänge oder Anweisungen mit Zeichenfolgenliteralen, die größer als 8 KB groß. XML-Showpläne für diese Anweisungen können mit **sys.dm_exec_query_plan** nur abgerufen werden, wenn der Batch gerade ausgeführt wird, da sie im Cache nicht vorhanden sind.  
  
-   Wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch oder eine gespeicherte Prozedur enthält einen Aufruf für eine benutzerdefinierte Funktion oder einen Aufruf für eine dynamische SQL, z. B. mit EXEC (*Zeichenfolge*), wird der kompilierte XML-Showplan für die benutzerdefinierte Funktion nicht in der Tabelle enthalten ist zurückgegebenes **dm_exec_query_plan** für den Batch oder die gespeicherte Prozedur. Stattdessen müssen Sie einen separaten Aufruf von **sys.dm_exec_query_plan** für das Planhandle erstellen, das der benutzerdefinierten Funktion entspricht.  
  
 Wenn bei einer Ad-hoc-Abfrage einfache oder erzwungene Parametrisierung verwendet wird, ist in der Spalte **query_plan** nur der Anweisungstext enthalten, nicht der tatsächliche Abfrageplan. Rufen Sie zum Zurückgeben des Abfrageplans **sys.dm_exec_query_plan** für das Planhandle der vorbereiteten parametrisierten Abfrage auf. Können Sie bestimmen, ob die Abfrage parametrisiert wurde die **Sql** Spalte die [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) Sicht oder der Textspalte der [Sys. dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)-verwaltungssicht.  
  
 Aufgrund einer Beschränkung der im **xml** -Datentyp zulässigen Anzahl geschachtelter Ebenen kann **sys.dm_exec_query_plan** keine Abfragepläne zurückgeben, die 128 oder mehr Ebenen geschachtelter Elemente aufweisen. In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verhinderte diese Bedingung das Zurückgeben des Abfrageplans, wobei der Fehler 6335 generiert wurde. In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 und höheren Versionen der **Query_plan** Spalte gibt NULL zurück. Sie können die [Sys. dm_exec_text_query_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md) dynamische Verwaltungsfunktion, um die Ausgabe des Abfrageplans im Textformat zurückgeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen von **sys.dm_exec_query_plan**muss ein Benutzer Mitglied der festen Serverrolle **sysadmin** sein oder über die VIEW SERVER STATE-Berechtigung auf dem Server verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Verwendung der dynamischen Verwaltungssicht **sys.dm_exec_query_plan** gezeigt.  
  
 Führen Sie zum Anzeigen der XML-Showpläne die folgenden Abfragen im Abfrage-Editor von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], klicken Sie dann auf **"ShowPlanXml"** in der **Query_plan** Spalte der zurückgegebenen Tabelle **sys.dm_ Exec_query_plan**. Der XML-Showplan zeigt an, der [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Zusammenfassungsbereich. Um den XML-Showplan in einer Datei zu speichern, Maustaste **"ShowPlanXml"** in der **Query_plan** Spalte, klicken Sie auf **Ergebnisse speichern unter**, nennen Sie die Datei im Format \< *File_name*> .sqlplan, z. B. MyXMLShowplan.sqlplan.  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. Abrufen des zwischengespeicherten Abfrageplans für eine langsam ausgeführte Transact-SQL-Abfrage oder einen langsam ausgeführten Transact-SQL-Batch  
 Abfragepläne für unterschiedliche Typen von [!INCLUDE[tsql](../../includes/tsql-md.md)] Batches z. B. ad-hoc-Batches, gespeicherte Prozeduren und benutzerdefinierte Funktionen werden in einem Bereich des Arbeitsspeichers, der als Plancache bezeichnet zwischengespeichert. Jeder zwischengespeicherte Abfrageplan wird durch einen eindeutigen Bezeichner identifiziert, der Planhandle genannt wird. Sie können angeben, dass dieses planhandle mit der **dm_exec_query_plan** dynamische Verwaltungsansicht, um den Ausführungsplan für eine bestimmte abzurufen [!INCLUDE[tsql](../../includes/tsql-md.md)] Abfrage oder einen Batch.  
  
 Wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage oder ein -Batch für lange Zeit mit einer bestimmten Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, können Sie den Ausführungsplan für diese Abfrage oder diesen Batch abrufen, um die Ursache der Verzögerung zu ermitteln. Im folgenden Beispiel wird das Abrufen des XML-Showplans für eine langsam ausgeführte Abfrage oder einen Batch gezeigt.  
  
> [!NOTE]  
>  Ersetzen Sie zum Ausführen dieses Beispiels die Werte für *session_id* und *plan_handle* mit den Werten Ihres Servers.  
  
 Rufen Sie zunächst die Serverprozess-ID (SPID) für den Prozess ab, der die Abfrage oder den Batch ausführt, indem Sie die gespeicherte Prozedur `sp_who` verwenden:  
  
```  
USE master;  
GO  
exec sp_who;  
GO  
```  
  
 Das von `sp_who` zurückgegebene Resultset gibt die SPID `54`an. Verwenden Sie die SPID nun mit der dynamischen Verwaltungssicht `sys.dm_exec_requests` , um das Planhandle mithilfe der folgenden Abfrage abzurufen:  
  
```  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 In der von **sys.dm_exec_requests** zurückgegebenen Tabelle wird angezeigt, dass das Planhandle für die langsam ausgeführte Abfrage oder den Batch `0x06000100A27E7C1FA821B10600`lautet. Geben Sie diesen Wert als *plan_handle* -Argument mit `sys.dm_exec_query_plan` an, um den Ausführungsplan im XML-Format wie folgt abzurufen. Der Ausführungsplan im XML-Format für die langsam ausgeführte Abfrage oder den Batch ist in der **query_plan** -Spalte der von `sys.dm_exec_query_plan`zurückgegebenen Tabelle enthalten.  
  
```  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. Abrufen jedes einzelnen Abfrageplans aus dem Plancache  
 Wenn Sie eine Momentaufnahme aller im Plancache gespeicherten Abfragen abrufen möchten, rufen Sie die Planhandles aller Abfragepläne im Cache ab, indem Sie die dynamische Verwaltungssicht `sys.dm_exec_cached_plans` abfragen. Die Planhandles sind in der `plan_handle` -Spalte von `sys.dm_exec_cached_plans`gespeichert. Verwenden Sie dann den CROSS APPLY-Operator, um die Planhandles wie folgt an `sys.dm_exec_query_plan` zu übergeben. Die XML-Showplanausgabe für jeden aktuell im Plancache gespeicherten Plan wird in der `query_plan` -Spalte der zurückgegebenen Tabelle angezeigt.  
  
```  
USE master;  
GO  
SELECT * FROM sys.dm_exec_cached_plans cp CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Abrufen jedes einzelnen Abfrageplans aus dem Plancache, für den der Server eine Abfragestatistik erfasst hat  
 Wenn Sie eine Momentaufnahme aller im Plancache gespeicherten Abfragen abrufen möchten, für die der Server eine Statistik erfasst hat, rufen Sie die Planhandles dieser Pläne im Cache ab, indem Sie die dynamische Verwaltungssicht `sys.dm_exec_query_stats` abfragen. Die Planhandles sind in der `plan_handle` -Spalte von `sys.dm_exec_query_stats`gespeichert. Verwenden Sie dann den CROSS APPLY-Operator, um die Planhandles wie folgt an `sys.dm_exec_query_plan` zu übergeben. Die XML-Showplanausgabe für jeden aktuell im Plancache gespeicherten Plan, für den der Server eine Statistik erfasst hat, wird in der `query_plan` -Spalte der zurückgegebenen Tabelle angezeigt.  
  
```  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats qs CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Abrufen von Informationen zu den fünf Abfragen mit dem höchsten durchschnittlichen CPU-Zeitaufwand  
 Im folgenden Beispiel werden die Pläne und die durchschnittliche CPU-Zeit für die fünf Abfragen mit der höchsten durchschnittlichen CPU-Zeit zurückgegeben.  
  
```  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [Sys. dm_exec_query_stats &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [Sys. dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Sp_who &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [Referenz zu logischen und physischen Showplanoperatoren](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [Sys. dm_exec_text_query_plan &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  

