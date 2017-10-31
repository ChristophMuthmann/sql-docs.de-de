---
title: ALTER EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EVENT SESSION
- ALTER_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- extended events [SQL Server], Transact-SQL
- ALTER EVENT SESSION statement
ms.assetid: da006ac9-f914-4995-a2fb-25b5d971cd90
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b6fd062bf55bb2630c436d452d2bab05a2f2d53d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-event-session-transact-sql"></a>ALTER EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Startet oder beendet eine Ereignissitzung oder ändert die Konfiguration einer Ereignissitzung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER EVENT SESSION event_session_name  
ON SERVER  
{  
    [ [ {  <add_drop_event> [ ,...n] }     
       | { <add_drop_event_target> [ ,...n ] } ]   
    [ WITH ( <event_session_options> [ ,...n ] ) ]  
    ]  
    | [ STATE = { START | STOP } ]  
}  
  
<add_drop_event>::=  
{  
    [ ADD EVENT <event_specifier>   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n ] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n ] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
   ]   
   | DROP EVENT <event_specifier> }  
  
<event_specifier> ::=  
{  
[event_module_guid].event_package_name.event_name  
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
  
<add_drop_event_target>::=  
{  
    ADD TARGET <event_target_specifier>  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
    | DROP TARGET <event_target_specifier>  
}  
  
<event_target_specifier>::=  
{  
    [event_module_guid].event_package_name.target_name  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>Argumente  
  
|||  
|-|-|  
|Begriff|Definition|  
|*event_session_name*|Ist der Name einer vorhandenen Ereignissitzung.|  
|STATUS = START &#124; BEENDEN|Startet oder beendet die Ereignissitzung. Dieses Argument ist nur gültig, wenn ALTER EVENT SESSION auf ein Ereignissitzungsobjekt angewendet wird.|  
|ADD EVENT \<Ereignisbezeichner >|Ordnet das identifizierte \<Event_specifier > mit der ereignissitzung.|
|[*Event_module_guid*]*. event_package_name.event_name*|Ist der Name eines Ereignisses in einem Ereignispaket, wobei Folgendes gilt:<br /><br /> -   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.<br />-   *Event_package_name* ist das Paket, das das Aktionsobjekt enthält.<br />-   *Ereignisname* ist das Ereignisobjekt.<br /><br /> Ereignisse werden in der sys.dm_xe_objects-Sicht als object_type 'event' angezeigt.|  
|Legen Sie { *Event_customizable_attribute*= \<Wert > [,... *n*] }|Gibt anpassbare Attribute für das Ereignis an. Anpassbare Attribute werden in der dm_xe_object_columns-Sicht mit Column_type 'customizable' und Object_name = *Event_name*.|  
|Aktion ({[*Event_module_guid*]*. event_package_name.action_name* [ **,**... *n*] } )|Die Aktion, die mit der Ereignissitzung verknüpft werden soll. Dabei gilt:<br /><br /> -   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.<br />-   *Event_package_name* ist das Paket, das das Aktionsobjekt enthält.<br />-   *Aktionsname* ist das Aktionsobjekt.<br /><br /> Aktionen werden in der sys.dm_xe_objects-Sicht als object_type 'action' angezeigt.|  
|WOBEI \<Prädikatausdruck >|Gibt den Prädikatausdruck verwendet, um zu bestimmen, ob ein Ereignis verarbeitet werden sollen. Wenn \<Prädikatausdruck > ist "true", wird das Ereignis verarbeitet, indem Sie die Aktionen und Zielen für die Sitzung. Wenn \<Prädikatausdruck > ist "false", der Ereignis von der Sitzung vor der Verarbeitung von den Aktionen und Zielen für die Sitzung gelöscht wird. Die Länge von Prädikatausdrücken ist auf 3000 Zeichen beschränkt, wodurch die Länge von Zeichenfolgenargumenten eingeschränkt wird.|
|*event_field_name*|Ist der Name des Ereignisfelds, das die Prädikatquelle identifiziert.|  
|[event_module_guid].event_package_name.predicate_source_name|Ist der Name der globalen Prädikatquelle, wobei Folgendes gilt:<br /><br /> -   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.<br />-   *Event_package_name* ist das Paket, das das prädikatobjekt enthält.<br />-   *Predicate_source_name* wird in der dm_xe_objects-Sicht als Object_type 'Pred_source' definiert.|  
|[*Event_module_guid*]. *Event_package_name*. *predicate_compare_name*|Der Name des Prädikatobjekts, das mit dem Ereignis verknüpft werden soll. Dabei gilt Folgendes:<br /><br /> -   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.<br />-   *Event_package_name* ist das Paket, das das prädikatobjekt enthält.<br />-   *Predicate_compare_name* ist eine globale Quelle, die in der dm_xe_objects-Sicht als Object_type 'Pred_compare' definiert.|  
|DROP EVENT \<Ereignisbezeichner >|Löscht das identifizierte Ereignis  *\<Event_specifier >*. \<Event_specifier > muss in der ereignissitzung gültig sein.|  
|ADD TARGET \<ereigniszielbezeichner >|Ordnet das Ziel identifizierten \<ereigniszielbezeichner > mit der ereignissitzung.|
|[*Event_module_guid*]. *Event_package_name*. *Zielname*|Der Name eines Ziels in der Ereignissitzung, wobei Folgendes gilt:<br /><br /> -   *Event_module_guid* ist die GUID für das Modul, das das Ereignis enthält.<br />-   *Event_package_name* ist das Paket, das das Aktionsobjekt enthält.<br />-   *Target_name* ist die Aktion. Aktionen werden in der sys.dm_xe_objects-Sicht als object_type 'target' angezeigt.|  
|Legen Sie { *Target_parameter_name*= \<Wert > [,... *n*] }|Legt einen Zielparameter fest. Zielparameter werden in der dm_xe_object_columns-Sicht mit Column_type 'customizable' und Object_name = *Target_name*.<br /><br /> **HINWEIS!** Wenn Sie ein Ringpufferziel verwenden, sollten Sie den max_memory-Zielparameter auf 2048 Kilobytes (KB) festlegen, um ein mögliches Abschneiden der Daten in der XML-Ausgabe zu vermeiden. Weitere Informationen zu die unterschiedlichen Zieltypen verwenden, finden Sie unter [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).|  
|DROP TARGET \<ereigniszielbezeichner >|Löscht das durch \<ereigniszielbezeichner >. \<ereigniszielbezeichner > muss in der ereignissitzung gültig sein.|  
|EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** &#124; ALLOW_MULTIPLE_EVENT_LOSS &#124; NO_EVENT_LOSS}|Gibt den Ereignisbeibehaltungsmodus an, der zum Behandeln von Ereignisverlusten verwendet werden soll.<br /><br /> **ALLOW_SINGLE_EVENT_LOSS**<br /> Ein Ereignis der Sitzung darf verloren gehen. Ein einzelnes Ereignis wird nur gelöscht, wenn alle Ereignispuffer gefüllt sind. Wenn bei gefüllten Ereignispuffern nur ein Ereignis verloren geht, sind akzeptable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Leistungsmerkmale möglich, während Datenverluste im verarbeiteten Ereignisdatenstrom minimiert werden.<br /><br /> ALLOW_MULTIPLE_EVENT_LOSS<br /> Volle Ereignispuffer, die mehrere Ereignisse enthalten, dürfen in der Sitzung verloren gehen. Die Anzahl verloren gegangener Ereignisse ist abhängig von der Größe des Speichers, der Partitionierung des Speichers und der Größe der Ereignisse im Puffer der Sitzung zugeordnet. Die Option minimiert die Leistungseinbußen auf dem Server, wenn Ereignispuffer schnell gefüllt werden, jedoch große Mengen von Ereignissen in der Sitzung verloren gehen können.<br /><br /> NO_EVENT_LOSS<br /> Verluste von Ereignissen sind nicht zulässig. Diese Option wird sichergestellt, dass alle ausgelösten Ereignisse beibehalten werden. Diese Option verwendet wird, müssen alle Aufgaben, die Ereignisse auslösen, warten Sie, bis in einem Ereignispuffer Platz verfügbar wird. Dies kann spürbare Leistungsprobleme verursachen, während die Ereignissitzung aktiv ist. Möglicherweise werden Benutzerverbindungen blockiert, während auf das Leeren von Ereignissen aus dem Puffer gewartet wird.|  
|MAX_DISPATCH_LATENCY = { *Sekunden* Sekunden &#124; **UNENDLICHE** }|Gibt die Zeitspanne, die Ereignisse gepuffert werden im Arbeitsspeicher, bevor Sie an ereignissitzungsziele gesendet wird. Der Latenzzeitwert muss mindestens 1 Sekunde betragen. Mit dem Wert 0 kann jedoch eine INFINITE-Latenzzeit angegeben werden. Standardmäßig ist dieser Wert auf 30 Sekunden festgelegt.<br /><br /> *Sekunden* Sekunden<br /> Die Wartezeit in Sekunden, bevor die Puffer geleert werden und ihr Inhalt an die Ziele gesendet wird. *Sekunden* ist eine ganze Zahl.<br /><br /> **UNBEGRENZTE**<br /> Die Puffer werden nur dann geleert und ihr Inhalt an die Ziele gesendet, wenn die Puffer voll sind oder wenn die Ereignissitzung geschlossen wird.<br /><br /> **HINWEIS!** MAX_DISPATCH_LATENCY = 0 SECONDS entspricht MAX_DISPATCH_LATENCY = INFINITE.|  
|MAX_EVENT_SIZE =*Größe* [KB &#124; **MB** ]|Gibt die maximal zulässige Größe für Ereignisse an. MAX_EVENT_SIZE sollte so festgelegt werden, dass nur einzelne Ereignisse zugelassen werden, deren Wert den von MAX_MEMORY überschreitet. Ist der festgelegte Wert kleiner als der von MAX_MEMORY, wird ein Fehler ausgelöst. *Größe* ist eine ganze Zahl und Kilobyte (KB) oder Megabyte (MB) angegeben werden können. Wenn *Größe* in Kilobyte angegeben wird, die zulässige Mindestgröße beträgt 64 KB. Wenn MAX_EVENT_SIZE festgelegt ist, zwei Puffer der *Größe* werden zusätzlich zu MAX_MEMORY erstellt. Dies bedeutet, dass der gesamte für die Ereignispufferung verwendete Arbeitsspeicher dem Wert von MAX_MEMORY + 2 * MAX_EVENT_SIZE entspricht.|  
|MEMORY_PARTITION_MODE = { **NONE** &#124; PER_NODE &#124; PER_CPU}|Gibt den Speicherort an, an dem Ereignispuffer erstellt werden.<br /><br /> **NONE**<br /> Ein einzelner Satz von Puffern wird erstellt, in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.<br /><br /> PRO Knoten - ist ein Satz von Puffern für jeden NUMA-Knoten erstellt.<br /><br /> PRO CPU - ist ein Satz von Puffern für jede CPU erstellt.|  
|TRACK_CAUSALITY = {ON &#124; **OFF** }|Gibt an, ob Kausalität verfolgt wird. Wenn das Verfolgen der Kausalität aktiviert ist, können ähnliche Ereignisse auf anderen Serververbindungen korreliert werden.|  
|STARTUP_STATE = {ON &#124; **OFF** }|Gibt an, ob diese Ereignissitzung beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch gestartet werden soll.<br /><br /> Wenn STARTUP_STATE = ON ereignissitzung beginnt erst, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beendet und neu gestartet wird.<br /><br /> FÜR = Ereignis, die Sitzung beim Start gestartet wird.<br /><br /> **DEAKTIVIERT** = Ereignis Sitzung wurde beim Systemstart nicht gestartet.|  
  
## <a name="remarks"></a>Hinweise  
 Die Argumente ADD und DROP können nicht in der gleichen Anweisung verwendet werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY EVENT SESSION-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird eine Ereignissitzung gestartet, es werden einige Statistiken zur Livesitzung ermittelt, und anschließend werden der vorhandenen Sitzung zwei Ereignisse hinzugefügt.  
  
```  
-- Start the event session  
ALTER EVENT SESSION test_session  
ON SERVER  
STATE = start;  
GO  
-- Obtain live session statistics   
SELECT * FROM sys.dm_xe_sessions;  
SELECT * FROM sys.dm_xe_session_events;  
GO  
  
-- Add new events to the session  
ALTER EVENT SESSION test_session ON SERVER  
ADD EVENT sqlserver.database_transaction_begin,  
ADD EVENT sqlserver.database_transaction_end;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Ziele für erweiterte Ereignisse von SQL Server](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)   
 [Sys. server_event_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [dm_xe_objects &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  

