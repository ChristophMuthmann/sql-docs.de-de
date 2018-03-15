---
title: CREATE EVENT SESSION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EVENT SESSION
- SESSION
- EVENT SESSION
- SESSION_TSQL
- EVENT_SESSION_TSQL
- CREATE_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- CREATE EVENT SESSION statement
ms.assetid: 67683027-2b0f-47aa-b223-604731af8b4d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ede0fb6715067bba3bafb1e77863483590d5f6a7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-event-session-transact-sql"></a>CREATE EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine Sitzung für erweiterte Ereignisse, die die Quelle der Ereignisse, die Ereignissitzungsziele und die Ereignissitzungsoptionen bestimmt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE EVENT SESSION event_session_name  
ON SERVER  
{  
    <event_definition> [ ,...n]  
    [ <event_target_definition> [ ,...n] ]  
    [ WITH ( <event_session_options> [ ,...n] ) ]  
}  
;  
  
<event_definition>::=  
{  
    ADD EVENT [event_module_guid].event_package_name.event_name   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
}  
  
<predicate_expression> ::=   
{  
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }   
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]   
    [ ,...n ]  
}  
  
<predicate_factor>::=   
{  
    <predicate_leaf> | ( <predicate_expression> )  
}  
  
<predicate_leaf>::=  
{  
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>   
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )   
}  
  
<predicate_source_declaration>::=   
{  
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )  
}  
  
<value>::=   
{  
    number | 'string'  
}  
  
<event_target_definition>::=  
{  
    ADD TARGET [event_module_guid].event_package_name.target_name  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB ] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *event_session_name*  
 Der benutzerdefinierte Name für die Ereignissitzung. *event_session_name* ist alphanumerisch, kann bis zu 128 Zeichen enthalten, muss innerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eindeutig sein und muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 ADD EVENT [ *event_module_guid* ].*event_package_name*.*event_name*  
 Ist das Ereignis, das mit der Ereignissitzung zu verknüpfen ist. Dabei gilt:  
  
-   *event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *event_package_name* ist das Paket, das das Aktionsobjekt enthält.  
  
-   *event_name* ist das Ereignisobjekt.  
  
 Ereignisse werden in der sys.dm_xe_objects-Sicht als object_type 'event' angezeigt.  
  
 SET { *event_customizable_attribute*= \<value> [ ,...*n*] }  
 Ermöglicht die Festlegung anpassbarer Attribute für das Ereignis. Anpassbare Attribute werden in der sys.dm_xe_object_columns-Sicht mit column_type 'customizable' und object_name = *event_name* angezeigt.  
  
 ACTION ( { [*event_module_guid*].*event_package_name*.*action_name* [ **,**...*n*] })  
 Die Aktion, die mit der Ereignissitzung verknüpft werden soll. Dabei gilt:  
  
-   *event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *event_package_name* ist das Paket, das das Aktionsobjekt enthält.  
  
-   *action_name* ist das Aktionsobjekt.  
  
 Aktionen werden in der sys.dm_xe_objects-Sicht als object_type 'action' angezeigt.  
  
 WHERE \<predicate_expression> gibt den Prädikatausdruck an, mit dessen Hilfe bestimmt wird, ob ein Ereignis verarbeitet werden muss. Wenn \<predicate_expression> den Wert TRUE hat, wird das Ereignis von den Aktionen und Zielen für die Sitzung weiter verarbeitet. Wenn \<predicate_expression> den Wert FALSE hat, wird das Ereignis von der Sitzung gelöscht, bevor es von den Aktionen und Zielen für die Sitzung verarbeitet wird. Die Länge von Prädikatausdrücken ist auf 3000 Zeichen beschränkt, wodurch die Länge von Zeichenfolgenargumenten eingeschränkt wird. 
  
 *event_field_name*  
 Ist der Name des Ereignisfelds, das die Prädikatquelle identifiziert.  
  
 [*event_module_guid*].*event_package_name*.*predicate_source_name*  
 Ist der Name der globalen Prädikatquelle, wobei Folgendes gilt:  
  
-   *event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *event_package_name* ist das Paket, das das Prädikatobjekt enthält.  
  
-   *predicate_source_name* ist in der sys.dm_xe_objects-Sicht als object_type 'pred_source' definiert.  
  
 [*event_module_guid*].*event_package_name*.*predicate_compare_name*  
 Der Name des Prädikatobjekts, das mit dem Ereignis verknüpft werden soll. Dabei gilt Folgendes:  
  
-   *event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *event_package_name* ist das Paket, das das Prädikatobjekt enthält.  
  
-   *predicate_compare_name* ist eine globale Quelle, die in der sys.dm_xe_objects-Sicht als object_type 'pred_compare' definiert ist.  
  
 *number*  
 Ein numerischer Typ einschließlich **decimal**. Einschränkungen stellen der verfügbare physische Speicher oder eine Zahl dar, die zu groß ist, um als 64-Bit-Ganzzahl dargestellt werden zu können.  
  
 '*string*'  
 Entweder eine ANSI- oder Unicode-Zeichenfolge, die vom Prädikatvergleich verlangt wird. Für die Prädikatvergleichsfunktionen wird keine implizite Zeichenfolgentypkonvertierung ausgeführt. Die Übergabe des falschen Typs führt zu einem Fehler.  
  
 ADD TARGET [*event_module_guid*].*event_package_name*.*target_name*  
 Ist das Ziel, das mit der Ereignissitzung zu verknüpfen ist. Dabei gilt:  
  
-   *event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *event_package_name* ist das Paket, das das Aktionsobjekt enthält.  
  
-   *target_name* ist das Ziel. Ziele werden in der sys.dm_xe_objects-Sicht als object_type 'target' angezeigt.  
  
 SET { *target_parameter_name*= \<value> [, ...*n*] }  
 Legt einen Zielparameter fest. Zielparameter werden in der sys.dm_xe_object_columns-Sicht mit column_type 'customizable' und object_name = *target_name* angezeigt.  
  
> [!IMPORTANT]  
>  Wenn Sie ein Ringpufferziel verwenden, sollten Sie den max_memory-Zielparameter auf 2048 Kilobytes (KB) festlegen, um ein mögliches Abschneiden der Daten in der XML-Ausgabe zu vermeiden. Informationen zur Verwendung von unterschiedlichen Zieltypen finden Sie unter [Ziele für erweiterte Ereignisse von SQL Server](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
 WITH ( \<event_session_options> [ ,...*n*] ) gibt Optionen an, die für die Ereignissitzung verwendet werden.  
  
 MAX_MEMORY =*size* [ KB | **MB** ]  
 Gibt an, wieviel Arbeitsspeicher der Sitzung für die Ereignispufferung maximal zugeordnet werden soll. Die Standardeinstellung ist 4 MB. *size* ist eine ganze Zahl und kann in Kilobyte (KB) oder Megabyte (MB) angegeben werden.  
  
 EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS }  
 Gibt den Ereignisbeibehaltungsmodus an, der zum Behandeln von Ereignisverlusten verwendet werden soll.  
  
 **ALLOW_SINGLE_EVENT_LOSS**  
 Ein Ereignis der Sitzung darf verloren gehen. Ein einzelnes Ereignis wird nur gelöscht, wenn alle Ereignispuffer gefüllt sind. Wenn bei gefüllten Ereignispuffern nur ein Ereignis verloren geht, sind akzeptable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Leistungsmerkmale möglich, während Datenverluste im verarbeiteten Ereignisdatenstrom minimiert werden.  
  
 ALLOW_MULTIPLE_EVENT_LOSS  
 Volle Ereignispuffer, die mehrere Ereignisse enthalten, dürfen in der Sitzung verloren gehen. Die Anzahl verloren gegangener Ereignisse hängt von der Größe des Speichers, der der Sitzung zugeordnet ist, der Partitionierung des Speichers und der Größe der Ereignisse im Puffer ab. Die Option minimiert die Leistungseinbußen auf dem Server, wenn Ereignispuffer schnell gefüllt werden, jedoch große Mengen von Ereignissen in der Sitzung verloren gehen können.  
  
 NO_EVENT_LOSS  
 Verluste von Ereignissen sind nicht zulässig. Diese Option stellt sicher, dass alle ausgelösten Ereignisse beibehalten werden. Wenn diese Option verwendet wird, müssen alle Tasks, die Ereignisse auslösen, warten, bis in einem Ereignispuffer Platz verfügbar wird. Dies kann spürbare Leistungsprobleme verursachen, während die Ereignissitzung aktiv ist. Möglicherweise werden Benutzerverbindungen blockiert, während auf das Leeren von Ereignissen aus dem Puffer gewartet wird.  
  
 MAX_DISPATCH_LATENCY = { *seconds* SECONDS | **INFINITE** }  
 Gibt an, wie lange Ereignisse zwischengespeichert werden, bevor sie an Ereignissitzungsziele gesendet werden. Standardmäßig ist dieser Wert auf 30 Sekunden festgelegt.  
  
 *seconds* SECONDS  
 Die Wartezeit in Sekunden, bevor die Puffer geleert werden und ihr Inhalt an die Ziele gesendet wird. *seconds* ist eine ganze Zahl. Der Latenzzeitwert muss mindestens 1 Sekunde betragen. Mit dem Wert 0 kann jedoch eine INFINITE-Latenzzeit angegeben werden.  
  
 **INFINITE**  
 Die Puffer werden nur dann geleert und ihr Inhalt an die Ziele gesendet, wenn die Puffer voll sind oder wenn die Ereignissitzung geschlossen wird.  
  
> [!NOTE]  
>  MAX_DISPATCH_LATENCY = 0 SECONDS entspricht MAX_DISPATCH_LATENCY = INFINITE.  
  
 MAX_EVENT_SIZE =*size* [ KB | **MB** ]  
 Gibt die maximal zulässige Größe für Ereignisse an. MAX_EVENT_SIZE sollte so festgelegt werden, dass nur einzelne Ereignisse zugelassen werden, deren Wert den von MAX_MEMORY überschreitet. Ist der festgelegte Wert kleiner als der von MAX_MEMORY, wird ein Fehler ausgelöst. *size* ist eine ganze Zahl und kann in Kilobyte (KB) oder Megabyte (MB) angegeben werden. Wenn *size* in Kilobyte angegeben wird, ist die geringste zulässige Größe 64 KB. Wenn MAX_EVENT_SIZE festgelegt wird, werden zusätzlich zu MAX_MEMORY zwei Puffer von *size* erstellt. Dies bedeutet, dass der gesamte für die Ereignispufferung verwendete Arbeitsspeicher dem Wert von MAX_MEMORY + 2 * MAX_EVENT_SIZE entspricht.  
  
 MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU }  
 Gibt den Speicherort an, an dem Ereignispuffer erstellt werden.  
  
 **NONE**  
 Innerhalb der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz wird ein einzelner Satz von Puffern erstellt.  
  
 PER_NODE  
 Ein Satz von Puffern wird für jeden NUMA-Knoten erstellt.  
  
 PER_CPU  
 Ein Satz von Puffern wird für jede CPU erstellt.  
  
 TRACK_CAUSALITY = { ON | **OFF** }  
 Gibt an, ob Kausalität verfolgt wird. Wenn das Verfolgen der Kausalität aktiviert ist, können ähnliche Ereignisse auf anderen Serververbindungen korreliert werden.  
  
 STARTUP_STATE = { ON | **OFF** }  
 Gibt an, ob diese Ereignissitzung beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch gestartet werden soll.  
  
> [!NOTE]  
>  Wenn STARTUP_STATE = ON, beginnt die Ereignissitzung erst, wenn SQL Server beendet und anschließend neu gestartet wird.  
  
 ON  
 Die Ereignissitzung wird beim Start gestartet.  
  
 **OFF**  
 Die Ereignissitzung wird nicht beim Start gestartet.  
  
## <a name="remarks"></a>Remarks  
 Die Rangfolge der logischen Operatoren beginnt mit NOT (höchster Operator). Darauf folgt AND und anschließend OR.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY EVENT SESSION-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie eine Ereignissitzung mit der Bezeichnung `test_session` erstellt wird. In diesem Beispiel werden zwei Ereignisse hinzugefügt, und das Ziel 'Ereignisablaufverfolgung für Windows' wird verwendet.  
  
```  
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='test_session')  
    DROP EVENT session test_session ON SERVER;  
GO  
CREATE EVENT SESSION test_session  
ON SERVER  
    ADD EVENT sqlos.async_io_requested,  
    ADD EVENT sqlserver.lock_acquired  
    ADD TARGET package0.etw_classic_sync_target   
        (SET default_etw_session_logfile_path = N'C:\demo\traces\sqletw.etl' )  
    WITH (MAX_MEMORY=4MB, MAX_EVENT_SIZE=4MB);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  

