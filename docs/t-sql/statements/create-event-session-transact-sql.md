---
title: Erstellen einer EREIGNISSITZUNG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aaee13bce387e36c1dcb7d26f2dd983b8d36a661
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-event-session-transact-sql"></a>CREATE EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Erstellt eine Sitzung für erweiterte Ereignisse, die die Quelle der Ereignisse, die Ereignissitzungsziele und die Ereignissitzungsoptionen bestimmt.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
 Der benutzerdefinierte Name für die Ereignissitzung. *Event_session_name* ist alphanumerisch, kann bis zu 128 Zeichen sein, muss innerhalb einer Instanz eindeutig sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und Sie müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 ADD EVENT [ *Event_module_guid* ]. *Event_package_name*. *Ereignisname*  
 Ist das Ereignis, das mit der Ereignissitzung zu verknüpfen ist. Dabei gilt:  
  
-   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *Event_package_name* ist das Paket, das das Aktionsobjekt enthält.  
  
-   *Ereignisname* ist das Ereignisobjekt.  
  
 Ereignisse werden in der sys.dm_xe_objects-Sicht als object_type 'event' angezeigt.  
  
 Legen Sie { *Event_customizable_attribute*= \<Wert > [,... *n*] }  
 Ermöglicht die Festlegung anpassbarer Attribute für das Ereignis. Anpassbare Attribute werden in der dm_xe_object_columns-Sicht mit Column_type 'customizable' und Object_name = *Event_name*.  
  
 Aktion ({[*Event_module_guid*]. *Event_package_name*. *Aktionsname* [ **,**... *n*] })  
 Die Aktion, die mit der Ereignissitzung verknüpft werden soll. Dabei gilt:  
  
-   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *Event_package_name* ist das Paket, das das Aktionsobjekt enthält.  
  
-   *Aktionsname* ist das Aktionsobjekt.  
  
 Aktionen werden in der sys.dm_xe_objects-Sicht als object_type 'action' angezeigt.  
  
 WOBEI \<Prädikatausdruck > Gibt an, der Prädikatausdruck verwendet, um zu bestimmen, ob ein Ereignis verarbeitet werden sollen. Wenn \<Prädikatausdruck > ist "true", wird das Ereignis verarbeitet, indem Sie die Aktionen und Zielen für die Sitzung. Wenn \<Prädikatausdruck > ist "false", der Ereignis von der Sitzung vor der Verarbeitung von den Aktionen und Zielen für die Sitzung gelöscht wird. Die Länge von Prädikatausdrücken ist auf 3000 Zeichen beschränkt, wodurch die Länge von Zeichenfolgenargumenten eingeschränkt wird. 
  
 *event_field_name*  
 Ist der Name des Ereignisfelds, das die Prädikatquelle identifiziert.  
  
 [*Event_module_guid*]. *Event_package_name*. *predicate_source_name*  
 Ist der Name der globalen Prädikatquelle, wobei Folgendes gilt:  
  
-   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *Event_package_name* ist das Paket, das das prädikatobjekt enthält.  
  
-   *Predicate_source_name* wird in der dm_xe_objects-Sicht als Object_type 'Pred_source' definiert.  
  
 [*Event_module_guid*]. *Event_package_name*. *predicate_compare_name*  
 Der Name des Prädikatobjekts, das mit dem Ereignis verknüpft werden soll. Dabei gilt Folgendes:  
  
-   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *Event_package_name* ist das Paket, das das prädikatobjekt enthält.  
  
-   *Predicate_compare_name* ist eine globale Quelle, die in der dm_xe_objects-Sicht als Object_type 'Pred_compare' definiert.  
  
 *number*  
 Alle numerischen Typen umfassen **decimal**. Einschränkungen stellen der verfügbare physische Speicher oder eine Zahl dar, die zu groß ist, um als 64-Bit-Ganzzahl dargestellt werden zu können.  
  
 "*Zeichenfolge*"  
 Entweder eine ANSI- oder Unicode-Zeichenfolge, die vom Prädikatvergleich verlangt wird. Für die Prädikatvergleichsfunktionen wird keine implizite Zeichenfolgentypkonvertierung ausgeführt. Die Übergabe des falschen Typs führt zu einem Fehler.  
  
 ADD TARGET [*Event_module_guid*]. *Event_package_name*. *Zielname*  
 Ist das Ziel, das mit der Ereignissitzung zu verknüpfen ist. Dabei gilt:  
  
-   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.  
  
-   *Event_package_name* ist das Paket, das das Aktionsobjekt enthält.  
  
-   *Target_name* ist das Ziel. Ziele werden in der sys.dm_xe_objects-Sicht als object_type 'target' angezeigt.  
  
 Legen Sie { *Target_parameter_name*= \<Wert > [,... *n*] }  
 Legt einen Zielparameter fest. Zielparameter werden in der dm_xe_object_columns-Sicht mit Column_type 'customizable' und Object_name = *Target_name*.  
  
> [!IMPORTANT]  
>  Wenn Sie ein Ringpufferziel verwenden, sollten Sie den max_memory-Zielparameter auf 2048 Kilobytes (KB) festlegen, um ein mögliches Abschneiden der Daten in der XML-Ausgabe zu vermeiden. Weitere Informationen zu die unterschiedlichen Zieltypen verwenden, finden Sie unter [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
 MIT ( \<Ereignissitzungsoptionen > [,...  *n* ]) Gibt Optionen an, mit der ereignissitzung zu verwenden.  
  
 MAX_MEMORY =*Größe* [KB | **MB** ]  
 Gibt an, wieviel Arbeitsspeicher der Sitzung für die Ereignispufferung maximal zugeordnet werden soll. Der Standardwert ist 4 MB. *Größe* ist eine ganze Zahl und Kilobyte (KB) oder Megabyte (MB) angegeben werden können.  
  
 EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS}  
 Gibt den Ereignisbeibehaltungsmodus an, der zum Behandeln von Ereignisverlusten verwendet werden soll.  
  
 **ALLOW_SINGLE_EVENT_LOSS**  
 Ein Ereignis der Sitzung darf verloren gehen. Ein einzelnes Ereignis wird nur gelöscht, wenn alle Ereignispuffer gefüllt sind. Wenn bei gefüllten Ereignispuffern nur ein Ereignis verloren geht, sind akzeptable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Leistungsmerkmale möglich, während Datenverluste im verarbeiteten Ereignisdatenstrom minimiert werden.  
  
 ALLOW_MULTIPLE_EVENT_LOSS  
 Volle Ereignispuffer, die mehrere Ereignisse enthalten, dürfen in der Sitzung verloren gehen. Die Anzahl verloren gegangener Ereignisse ist hängt von der Größe des Speichers, der Partitionierung des Speichers und der Größe der Ereignisse im Puffer der Sitzung zugeordnet Die Option minimiert die Leistungseinbußen auf dem Server, wenn Ereignispuffer schnell gefüllt werden, jedoch große Mengen von Ereignissen in der Sitzung verloren gehen können.  
  
 NO_EVENT_LOSS  
 Verluste von Ereignissen sind nicht zulässig. Diese Option wird sichergestellt, dass alle ausgelösten Ereignisse beibehalten werden. Diese Option verwendet wird, müssen alle Aufgaben, die Ereignisse auslösen, warten Sie, bis in einem Ereignispuffer Platz verfügbar wird. Dies kann spürbare Leistungsprobleme verursachen, während die Ereignissitzung aktiv ist. Möglicherweise werden Benutzerverbindungen blockiert, während auf das Leeren von Ereignissen aus dem Puffer gewartet wird.  
  
 MAX_DISPATCH_LATENCY = { *Sekunden* Sekunden | **UNENDLICHE** }  
 Gibt an, wie lange Ereignisse zwischengespeichert werden, bevor sie an Ereignissitzungsziele gesendet werden. Standardmäßig ist dieser Wert auf 30 Sekunden festgelegt.  
  
 *Sekunden* Sekunden  
 Die Wartezeit in Sekunden, bevor die Puffer geleert werden und ihr Inhalt an die Ziele gesendet wird. *Sekunden* ist eine ganze Zahl. Der Latenzzeitwert muss mindestens 1 Sekunde betragen. Mit dem Wert 0 kann jedoch eine INFINITE-Latenzzeit angegeben werden.  
  
 **UNBEGRENZTE**  
 Die Puffer werden nur dann geleert und ihr Inhalt an die Ziele gesendet, wenn die Puffer voll sind oder wenn die Ereignissitzung geschlossen wird.  
  
> [!NOTE]  
>  MAX_DISPATCH_LATENCY = 0 SECONDS entspricht MAX_DISPATCH_LATENCY = INFINITE.  
  
 MAX_EVENT_SIZE =*Größe* [KB | **MB** ]  
 Gibt die maximal zulässige Größe für Ereignisse an. MAX_EVENT_SIZE sollte so festgelegt werden, dass nur einzelne Ereignisse zugelassen werden, deren Wert den von MAX_MEMORY überschreitet. Ist der festgelegte Wert kleiner als der von MAX_MEMORY, wird ein Fehler ausgelöst. *Größe* ist eine ganze Zahl und Kilobyte (KB) oder Megabyte (MB) angegeben werden können. Wenn *Größe* in Kilobyte angegeben wird, die zulässige Mindestgröße beträgt 64 KB. Wenn MAX_EVENT_SIZE festgelegt ist, zwei Puffer der *Größe* werden zusätzlich zu MAX_MEMORY erstellt. Dies bedeutet, dass der gesamte für die Ereignispufferung verwendete Arbeitsspeicher dem Wert von MAX_MEMORY + 2 * MAX_EVENT_SIZE entspricht.  
  
 MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU}  
 Gibt den Speicherort an, an dem Ereignispuffer erstellt werden.  
  
 **NONE**  
 Innerhalb der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz wird ein einzelner Satz von Puffern erstellt.  
  
 PER_NODE  
 Ein Satz von Puffern wird für jeden NUMA-Knoten erstellt.  
  
 PER_CPU  
 Ein Satz von Puffern wird für jede CPU erstellt.  
  
 TRACK_CAUSALITY = {ON | **OFF** }  
 Gibt an, ob Kausalität verfolgt wird. Wenn das Verfolgen der Kausalität aktiviert ist, können ähnliche Ereignisse auf anderen Serververbindungen korreliert werden.  
  
 STARTUP_STATE = {ON | **OFF** }  
 Gibt an, ob diese Ereignissitzung beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch gestartet werden soll.  
  
> [!NOTE]  
>  Wenn STARTUP_STATE = ON, beginnt die Ereignissitzung erst, wenn SQL Server beendet und anschließend neu gestartet wird.  
  
 ON  
 Die Ereignissitzung wird beim Start gestartet.  
  
 **OFF**  
 Die Ereignissitzung wird nicht beim Start gestartet.  
  
## <a name="remarks"></a>Hinweise  
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
  
## <a name="see-also"></a>Siehe auch  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Sys. server_event_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [dm_xe_objects &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  


