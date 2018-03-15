---
title: ALTER QUEUE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/01/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_QUEUE_TSQL
- ALTER QUEUE
dev_langs:
- TSQL
helpviewer_keywords:
- number of queue readers
- modifying queues
- ALTER QUEUE statement
- queue readers [SQL Server]
- queues [Service Broker], modifying
- unavailable queues [SQL Server]
- activation stored procedures [Service Broker]
ms.assetid: d54aa325-8761-4cd4-8da7-acf33df12296
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f97bd0a341ecc5e960c94c4c8bdabe30b572fd9
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-queue-transact-sql"></a>ALTER QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften einer Warteschlange.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER QUEUE <object>   
   queue_settings  
   | queue_action  
[ ; ]  
  
<object> : :=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        queue_name  
}   
  
<queue_settings> : :=  
WITH  
   [ STATUS = { ON | OFF } [ , ] ]  
   [ RETENTION = { ON | OFF } [ , ] ]  
   [ ACTIVATION (  
       { [ STATUS = { ON | OFF } [ , ] ]   
         [ PROCEDURE_NAME = <procedure> [ , ] ]  
         [ MAX_QUEUE_READERS = max_readers [ , ] ]  
         [ EXECUTE AS { SELF | 'user_name'  | OWNER } ]  
       |  DROP }  
          ) [ , ]]  
         [ POISON_MESSAGE_HANDLING (  
          STATUS = { ON | OFF } )  
         ]   
  
<queue_action> : :=  
   REBUILD [ WITH <query_rebuild_options> ]  
   | REORGANIZE [ WITH (LOB_COMPACTION = { ON | OFF } ) ]  
   | MOVE TO { file_group | "default" }  
  
<procedure> : :=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        stored_procedure_name  
}  
  
<queue_rebuild_options> : :=  
{  
   ( MAXDOP = max_degree_of_parallelism )  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name* (Objekt)  
 Der Name der Datenbank, die die zu ändernde Warteschlange enthält. Wenn *database_name* nicht bereitgestellt wird, wird standardmäßig die aktuelle Datenbank verwendet.  
  
 *schema_name* (Objekt)  
 Der Name des Schemas, zu dem die neue Warteschlange gehört. Wenn *schema_name* nicht angegeben wird, wird standardmäßig das Standardschema für den aktuellen Benutzer verwendet.  
  
 *queue_name*  
 Der Name der zu ändernden Warteschlange.  
  
 STATUS (Warteschlange)  
 Gibt an, ob die Warteschlange verfügbar ist (ON) oder nicht (OFF). Ist die Warteschlange nicht verfügbar, können der Warteschlange keine Nachrichten hinzugefügt oder aus ihr entfernt werden.  
  
 RETENTION  
 Gibt die Beibehaltungseinstellung für die Warteschlange an. Ist RETENTION = ON, werden alle Nachrichten, die für Konversationen mit dieser Warteschlange gesendet oder empfangen werden, in der Warteschlange beibehalten, bis die Konversationen beendet sind. Dies ermöglicht es Ihnen, Nachrichten zu Überwachungszwecken oder zur Ausführung von kompensierenden Transaktionen beim Auftreten eines Fehlers beizubehalten.  
  
> [!NOTE]  
>  Das Festlegen von RETENTION = ON kann die Leistung reduzieren. Diese Einstellung sollte nur verwendet werden, wenn die Vereinbarung zum Servicelevel (SLA, Service Level Agreement) für die Anwendung eingehalten werden muss.  
  
 ACTIVATION  
 Gibt Informationen zur gespeicherten Prozedur an, die zum Verarbeiten von in dieser Warteschlange ankommenden Nachrichten aktiviert wird.  
  
 STATUS (Aktivierung)  
 Gibt an, ob die gespeicherten Prozedur von der Warteschlange aktiviert wird. Ist STATUS = ON, startet die Warteschlange die mit PROCEDURE_NAME angegebene gespeicherte Prozedur, wenn die Anzahl der zurzeit ausgeführten Prozeduren kleiner als MAX_QUEUE_READERS ist und wenn Nachrichten schneller in der Warteschlange ankommen, als die gespeicherten Prozeduren Nachrichten empfangen. Ist STATUS = OFF, aktiviert die Warteschlange die gespeicherte Prozedur nicht.  
  
 REBUILD [ WITH \<queue_rebuild_options> ]  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Erstellt alle Indizes für die interne Tabelle der Warteschlange neu. Verwenden Sie diese Funktion, wenn Fragmentierungsprobleme aufgrund von Überlastung auftreten. MAXDOP ist die einzige unterstützte Option zum erneuten Erstellen von Warteschlangen. REBUILD ist immer ein Offlinevorgang.  
  
 REORGANIZE [ WITH ( LOB_COMPACTION = { ON | OFF } ) ]  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Organisiert alle Indizes für die interne Tabelle der Warteschlange neu.   
Im Gegensatz zu REORGANIZE bei Benutzertabellen wird REORGANIZE bei einer Warteschlange immer als Offlinevorgang durchgeführt, da bei Warteschlangen Sperren auf Seitenebene explizit deaktiviert werden.  
  
> [!TIP]  
>  Bei der Indexfragmentierung empfiehlt es sich generell, den Index neu zu organisieren, wenn die Fragmentierung zwischen 5% und 30% beträgt. Wenn die Fragmentierung mehr als 30% beträgt, sollten Sie den Index neu erstellen. Diese Angaben stellen jedoch nur einen groben Richtwert als Ausgangspunkt für Ihre Umgebung dar. Informationen und Beispiele zur Ermittlung des Indexfragmentierungsgrads finden Sie in Artikel [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) in Beispiel G.  
  
 MOVE TO { *file_group* | "default" }  
 **Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Verschiebt die interne Tabelle der Warteschlange (mit den Indizes) in eine vom Benutzer angegebene Dateigruppe.  Die neue Dateigruppe darf nicht schreibgeschützt sein.  
  
 PROCEDURE_NAME = \<procedure>  
 Gibt den Namen der gespeicherten Prozedur an, die aktiviert werden soll, wenn die Warteschlange zu verarbeitende Nachrichten enthält. Dieser Wert muss ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner sein.  
  
 *database_name* (Prozedur)  
 Der Name der Datenbank, die die gespeicherte Prozedur enthält.  
  
 *schema_name* (Prozedur)  
 Der Name des Schemas, das der Besitzer der gespeicherten Prozedur ist.  
  
 *stored_procedure_name*  
 Der Name der gespeicherten Prozedur.  
  
 MAX_QUEUE_READERS =*max_reader*  
 Gibt die maximale Anzahl von Instanzen der gespeicherten Aktivierungsprozedur an, die von der Warteschlange gleichzeitig gestartet werden. Der Wert von *max_readers* muss eine Zahl zwischen 0 und 32767 sein.  
  
 EXECUTE AS  
 Gibt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank-Benutzerkonto an, unter dem die gespeicherte Aktivierungsprozedur ausgeführt wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss zum Zeitpunkt der Aktivierung der gespeicherten Prozedur durch die Warteschlange die Berechtigungen für diesen Benutzer überprüfen können. Handelt es sich um einen Windows-Domänenbenutzer, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit der Domäne verbunden sein und die Berechtigungen des angegebenen Benutzers überprüfen können, wenn die Prozedur aktiviert wird. Andernfalls erzeugt die Aktivierung einen Fehler. Bei einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer kann der Server immer die Berechtigungen überprüfen.  
  
 SELF  
 Gibt an, dass die gespeicherte Prozedur als der aktuelle Benutzer ausgeführt wird. (Der Datenbankprinzipal, der diese ALTER QUEUE-Anweisung ausführt.)  
  
 '*user_name*'  
 Der Name des Benutzers, als der die gespeicherte Prozedur ausgeführt wird. *user_name* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer sein, der als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner angegeben ist. Der aktuelle Benutzer muss über die IMPERSONATE-Berechtigung für den mit *user_name* angegebenen Benutzer verfügen.  
  
 OWNER  
 Gibt an, dass die gespeicherte Prozedur als der Besitzer der Warteschlange ausgeführt wird.  
  
 DROP  
 Löscht alle der Warteschlange zugeordneten Aktivierungsinformationen.  
  
 POISON_MESSAGE_HANDLING  
 Gibt an, ob die Behandlung nicht verarbeitbarer Nachrichten aktiviert ist. Der Standardwert ist ON.  
  
 Eine Warteschlange, für die die Behandlung nicht verarbeitbarer Nachrichten auf OFF festgelegt ist, wird erst nach fünf aufeinander folgenden Transaktionsrollbacks deaktiviert. Daher ist es möglich, dass von der Anwendung ein System für die Behandlung nicht verarbeitbarer Nachrichten definiert wird.  
  
## <a name="remarks"></a>Remarks  
 Wenn eine Warteschlange mit einer angegebenen gespeicherten Aktivierungsprozedur Nachrichten enthält, wird die gespeicherte Aktivierungsprozedur unmittelbar aktiviert, wenn der Aktivierungsstatus von OFF in ON geändert wird. Durch das Ändern des Aktivierungsstatus von ON zu OFF beendet der Broker das Aktivieren von Instanzen der gespeicherten Prozedur. Instanzen der gespeicherten Prozedur, die aktuell ausgeführt werden, werden jedoch nicht beendet.  
  
 Wird eine Warteschlange geändert, um eine gespeicherte Aktivierungsprozedur hinzuzufügen, wird dadurch der Aktivierungsstatus der Warteschlange nicht geändert. Wird die gespeicherte Aktivierungsprozedur für die Warteschlange geändert, hat dies keine Auswirkungen auf Instanzen der gespeicherten Aktivierungsprozedur, die aktuell ausgeführt werden.  
  
 Während des Aktivierungsprozesses überprüft [!INCLUDE[ssSB](../../includes/sssb-md.md)] die maximale Anzahl von Warteschlangenlesevorgängen für eine Warteschlange. Wenn eine Warteschlange geändert wird, sodass die maximale Anzahl von Warteschlangenlesevorgängen erhöht wird, kann [!INCLUDE[ssSB](../../includes/sssb-md.md)] daher sofort weitere Instanzen der gespeicherten Aktivierungsprozedur starten. Wird eine Warteschlange geändert, sodass die maximale Anzahl von Warteschlangenlesevorgängen verringert wird, hat dies auf die zurzeit ausgeführten Instanzen der gespeicherten Aktivierungsprozedur keine Auswirkungen. [!INCLUDE[ssSB](../../includes/sssb-md.md)] startet jedoch erst dann eine neue Instanz der gespeicherten Prozedur, wenn die Anzahl von Instanzen für die gespeicherte Aktivierungsprozedur unter den konfigurierten Maximalwert fällt.  
  
 Ist eine Warteschlange nicht verfügbar, speichert [!INCLUDE[ssSB](../../includes/sssb-md.md)] Nachrichten für Dienste, die die Warteschlange verwenden, in der Übertragungswarteschlange für die Datenbank. Die [sys.transmission_queue](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)-Katalogsicht stellt eine Sicht der Übertragungswarteschlange bereit.  
  
 Falls in einer RECEIVE-Anweisung oder einer GET CONVERSATION GROUP-Anweisung eine nicht verfügbare Warteschlange angegeben ist, tritt bei dieser Anweisung ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler auf.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Ändern einer Warteschlange wird standardmäßig dem Besitzer der Warteschlange, den Mitgliedern der festen Datenbankrollen db_ddladmin oder db_owner sowie Mitgliedern der festen Serverrolle sysadmin zugewiesen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-making-a-queue-unavailable"></a>A. Festlegen, dass eine Warteschlange nicht verfügbar ist  
 Im folgenden Beispiel wird festgelegt, dass die `ExpenseQueue`-Warteschlange nicht für den Empfang von Nachrichten verfügbar ist.  
  
```  
ALTER QUEUE ExpenseQueue WITH STATUS = OFF ;  
```  
  
### <a name="b-changing-the-activation-stored-procedure"></a>B. Ändern der gespeicherten Aktivierungsprozedur  
 Im folgenden Beispiel wird die von der Warteschlange gestartete gespeicherte Prozedur geändert. Die gespeicherte Prozedur wird als der Benutzer ausgeführt, der die `ALTER QUEUE`-Anweisung ausgeführt hat.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = new_stored_proc,  
        EXECUTE AS SELF) ;  
```  
  
### <a name="c-changing-the-number-of-queue-readers"></a>C. Ändern der Anzahl von Warteschlangenlesevorgängen  
 Im folgenden Beispiel wird die maximale Anzahl von Instanzen der gespeicherten Prozedur, die von [!INCLUDE[ssSB](../../includes/sssb-md.md)] für diese Warteschlange gestartet werden, auf `7` festgelegt.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (MAX_QUEUE_READERS = 7) ;  
```  
  
### <a name="d-changing-the-activation-stored-procedure-and-the-execute-as-account"></a>D. Ändern der gespeicherten Aktivierungsprozedur und des EXECUTE AS-Kontos  
 Im folgenden Beispiel wird die von [!INCLUDE[ssSB](../../includes/sssb-md.md)] gestartete gespeicherte Prozedur geändert. Die gespeicherte Prozedur wird als der Benutzer `SecurityAccount` ausgeführt.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = AdventureWorks2012.dbo.new_stored_proc ,  
        EXECUTE AS 'SecurityAccount') ;  
```  
  
### <a name="e-setting-the-queue-to-retain-messages"></a>E. Festlegen, dass Nachrichten in der Warteschlange aufbewahrt werden  
 Im folgenden Beispiel wird festgelegt, dass Nachrichten in der Warteschlange aufbewahrt werden. Die Warteschlange bewahrt alle Nachrichten auf, die von Diensten gesendet bzw. von diesen empfangen werden, die diese Warteschlange verwenden. Die Aufbewahrung endet, wenn die Konversation, in der die Nachrichten enthalten sind, beendet wurde.  
  
```  
ALTER QUEUE ExpenseQueue WITH RETENTION = ON ;  
```  
  
### <a name="f-removing-activation-from-a-queue"></a>F. Entfernen der Aktivierung aus einer Warteschlange  
 Im folgenden Beispiel werden alle Aktivierungsinformationen aus der Warteschlange entfernt.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (DROP) ;  
```  
  
### <a name="g-rebuilding-queue-indexes"></a>G. Erneutes Erstellen von Indizes  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel werden Warteschlangenindizes neu erstellt.  
  
```  
ALTER QUEUE ExpenseQueue REBUILD WITH (MAXDOP = 2)   
```  
  
### <a name="h-reorganizing-queue-indexes"></a>H. Neuorganisieren von Warteschlangenindizes  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Im folgenden Beispiel werden Warteschlangenindizes neu erstellt.  
  
```  
ALTER QUEUE ExpenseQueue REORGANIZE   
```  
  
### <a name="i-moving-queue-internal-table-to-another-filegroup"></a>I: Verschieben der internen Tabelle einer Warteschlange in eine andere Dateigruppe  
  
**Gilt für**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER QUEUE ExpenseQueue MOVE TO [NewFilegroup]   
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
  
