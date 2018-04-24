---
title: ALTER WORKLOAD GROUP (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
caps.latest.revision: 56
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4bdc49a57b8b864284fa4411ddb0b970bed1c704
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert eine vorhandene Konfiguration einer Resource-Governor-Arbeitsauslastungsgruppe und weist sie optional einem Resource-Governor-Ressourcenpool zu.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
ALTER WORKLOAD GROUP { group_name | "default" }  
[ WITH  
    ([ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING { pool_name | "default" } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *group_name* | "**default**"  
 Der Name einer vorhandenen benutzerdefinierten Arbeitsauslastungsgruppe oder der standardmäßigen Ressourcenkontrollen-Arbeitsauslastungsgruppe.  
  
> [!NOTE]  
> Die Ressourcenkontrolle erstellt den "Standard" und interne Gruppen, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.  
  
 Die "default"-Option muss in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden, wenn sie mit ALTER WORKLOAD GROUP verwendet wird, um einen Konflikt mit dem vom System reservierten Wort DEFAULT zu vermeiden. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
> Für vordefinierte Arbeitsauslastungsgruppen und Ressourcenpools werden ausschließlich kleingeschriebene Namen verwendet, z.B. "default". Dies sollte bei Servern beachtet werden, die bei der Sortierung zwischen Groß-/Kleinschreibung unterscheiden. Server, die bei der Sortierung keine Groß- und Kleinschreibung unterscheiden, z. B. SQL_Latin1_General_CP1_CI_AS, behandeln "default" und "Default" gleich.  
  
 IMPORTANCE = { LOW | MEDIUM | HIGH }  
 Gibt die relative Wichtigkeit einer Anforderung in der Arbeitsauslastungsgruppe an. Die Wichtigkeit kann einen der folgenden Werte aufweisen:  
  
-   LOW  
-   MEDIUM (Standard)  
-   HIGH  
  
> [!NOTE]  
> Intern wird jede Wichtigkeitseinstellung als Zahl gespeichert, die für Berechnungen verwendet wird.  
  
 IMPORTANCE hat einen lokalen Bezug zum Ressourcenpool; Arbeitsauslastungsgruppen mit verschiedener Wichtigkeit innerhalb desselben Ressourcenpools beeinflussen sich gegenseitig, haben jedoch keine Auswirkungen auf Arbeitsauslastungsgruppen in anderen Ressourcenpools.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*value*  
 Gibt die Höchstmenge an Arbeitsspeicher an, die eine einzelne Anforderung vom Pool in Anspruch nehmen kann. Dieser Prozentwert ist relativ zur Ressourcenpoolgröße, die von MAX_MEMORY_PERCENT festgelegt wird.  
  
> [!NOTE]  
> Die angegebene Menge bezieht sich nur auf den für die Abfrageausführung gewährten Arbeitsspeicher.  
  
 *value* muss 0 (null) oder ein positiver Integer sein. Der zulässige Bereich für *value* liegt zwischen 0 und 100. Die Standardeinstellung für *value* ist 25.  
  
 Beachten Sie Folgendes:  
  
-   Das Festlegen von *value* auf 0 (null) verhindert, dass Abfragen mit SORT- und HASH JOIN-Vorgängen in benutzerdefinierten Arbeitsauslastungsgruppen ausgeführt werden.  
  
-   Es wird davon abgeraten, *value* auf einen höheren Wert als 70 festzulegen, da der Server möglicherweise nicht genug freien Arbeitsspeicher reservieren kann, wenn andere gleichzeitige Abfragen ausgeführt werden. Dadurch tritt möglicherweise der Timeoutfehler 8645 auf.  
  
> [!NOTE]  
>  Wenn die Arbeitsspeicheranforderungen der Abfrage den Grenzwert überschreiten, der von diesem Parameter angegeben wird, führt der Server folgende Vorgänge aus:  
>   
>  Bei benutzerdefinierten Arbeitsauslastungsgruppen versucht der Server, den Grad der Parallelität für diese Abfrage zu reduzieren, bis die Arbeitsspeicheranforderung den Grenzwert unterschreitet oder bis der Grad der Parallelität dem Wert 1 entspricht. Wenn die Arbeitsspeicheranforderung der Abfrage den Grenzwert immer noch überschreitet, tritt Fehler 8657 auf.  
>   
>  Bei internen und Standard-Arbeitsauslastungsgruppen lässt der Server zu, dass der Abfrage der erforderliche Arbeitsspeicher zugewiesen wird.  
>   
>  Beachten Sie, dass in beiden Fällen der Timeoutfehler 8645 auftreten kann, wenn der Server nicht über ausreichend physischen Arbeitsspeicher verfügt.  
  
 REQUEST_MAX_CPU_TIME_SEC =*value*  
 Gibt die maximale CPU-Zeit in Sekunden an, die eine Anforderung beanspruchen kann. *value* muss 0 (null) oder ein positiver Integer sein. Die Standardeinstellung für *value* ist 0 (null), also unbegrenzt.  
  
> [!NOTE]  
> Resource Governor verhindert nicht, dass eine Anforderung bei Erreichung des maximalen Zeitlimits fortgesetzt wird. Es wird jedoch ein Ereignis generiert. Weitere Informationen finden Sie unter [CPU Threshold Exceeded (Ereignisklasse)](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md). 

> [!IMPORTANT]
> Ab [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 bricht Resource Governor mit [Ablaufverfolgungsflag 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) eine Anforderung ab, wenn die maximale Zeit überschritten wird.
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*value*  
 Gibt die maximale Zeit in Sekunden an, die eine Abfrage auf das Freiwerden einer Arbeitspeicherzuweisung (Arbeitsspeicherpuffer) wartet.  
  
> [!NOTE]  
>  Eine Abfrage schlägt nicht grundsätzlich fehl, wenn das Timeout der Arbeitsspeicherzuweisung erreicht wird. Eine Abfrage schlägt nur fehl, wenn zu viele Abfragen gleichzeitig ausgeführt werden. Andernfalls könnte die Abfrage nur die minimale Arbeitsspeicherzuweisung nutzen, was zu reduzierter Abfrageleistung führen kann.  
  
 *value* muss eine positive ganze Zahl sein. Die Standardeinstellung für *value* ist 0 (null); hierbei wird eine interne Berechnung basierend auf den Abfragekosten verwendet, um die maximale Zeit zu ermitteln.  
  
 MAX_DOP =*value*  
 Gibt den maximalen Grad der Parallelität (DOP) für parallele Anforderungen an. *value* muss 0 (null) oder eine positive Ganzzahl zwischen 1 und 255 sein. Wenn *value* 0 ist, wählt der Server den maximalen Grad an Parallelismus aus. Dies ist die Standardeinstellung und die empfohlene Einstellung.  
  
> [!NOTE]  
>  Der Istwert, den der [!INCLUDE[ssDE](../../includes/ssde-md.md)] für MAX_DOP festlegt, ist möglicherweise kleiner als der angegebene Wert. Der endgültige Wert wird von Formel min(255, *number of CPUs)* bestimmt.  
  
> [!CAUTION]  
>  Das Ändern von MAX_DOP kann die Leistung des Servers beeinträchtigen. Wenn Sie MAX_DOP ändern müssen, wird empfohlen, diesen auf einen Wert festzulegen, der kleiner oder gleich der maximalen Anzahl der Hardware- Zeitplanungsmodule ist, die in einem einzelnen NUMA-Knoten vorhanden sind. Es wird empfohlen, MAX_DOP nicht auf einen höheren Wert als 8 festzulegen.  
  
 MAX_DOP wird wie folgt behandelt:  
  
-   MAX_DOP als Abfragehinweis wird so lange berücksichtigt, wie die Arbeitsauslastungsgruppe MAX_DOP nicht überschritten wird.  
  
-   ###MAX_DOP als Abfragehinweis überschreibt immer sp_configure 'max. Grad an Parallelität'.  
  
-   Die Arbeitsauslastungsgruppe MAX_DOP überschreibt sp_configure 'Max. Grad an Parallelität'.  
  
-   Wenn die Abfrage zur Kompilierzeit als seriell (MAX_DOP = 1 ) markiert ist, kann sie zur Laufzeit nicht wieder in parallel geändert werden, und zwar unabhängig von der Arbeitsauslastungsgruppe oder der sp_configure-Einstellung.  
  
 Nach der Konfiguration kann DOP nur bei Arbeitsspeicher-Engpässen verringert werden. Die Neukonfiguration der Arbeitsauslastungsgruppe ist während des Wartens in der Speicherzuweisungs-Warteschlange nicht sichtbar.  
  
 GROUP_MAX_REQUESTS =*value*  
 Gibt die maximale Anzahl gleichzeitiger Anforderungen an, die in der Arbeitsauslastungsgruppe ausgeführt werden können. *value* muss 0 (null) oder ein positiver Integer sein. Die Standardeinstellung für *value*, 0, lässt unbegrenzte Anforderungen zu. Wenn die maximale Anzahl gleichzeitiger Anforderungen erreicht wird, kann sich ein Benutzer dieser Gruppe zwar anmelden, wird jedoch in den Wartezustand versetzt, bis die Anzahl gleichzeitiger Anforderungen unter den angegebenen Wert gefallen ist.  
  
 USING { *pool_name* | "**default**" }  
 Verknüpft die Arbeitsauslastungsgruppe mit dem benutzerdefinierten Ressourcenpool, der durch *pool_name* angegeben wird, wodurch die Arbeitsauslastungsgruppe in den Ressourcenpool eingefügt wird. Wenn *pool_name* nicht bereitgestellt wird oder wenn das USING-Argument nicht verwendet wird, wird die Arbeitsauslastungsgruppe in den vordefinierten Standardpool von Resource Governor eingefügt.  
  
 Die "default"-Option muss in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden, wenn sie mit ALTER WORKLOAD GROUP verwendet wird, um einen Konflikt mit dem vom System reservierten Wort DEFAULT zu vermeiden. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Bei der "default"-Option wird die Groß-/Kleinschreibung beachtet.  
  
## <a name="remarks"></a>Remarks  
 ALTER WORKLOAD GROUP ist für die Standardgruppe zulässig.  
  
 Änderungen an der Konfiguration der Arbeitsauslastungsgruppe werden erst wirksam, nachdem ALTER RESOURCE GOVERNOR RECONFIGURE ausgeführt wurde. Wenn Sie eine Einstellung mit Auswirkung auf den Plan ändern, wird die neue Einstellung nur in zuvor zwischengespeicherten Plänen nach dem Ausführen von DBCC FREEPROCCACHE (*pool_name*) wirksam, wobei *pool_name* der Name eines Ressourcenpools von Resource Governor ist, dem die Arbeitsauslastungsgruppe zugeordnet ist.  
  
-   Wenn Sie MAX_DOP in 1 ändern möchten, muss DBCC FREEPROCCACHE nicht ausgeführt werden, da parallele Pläne im seriellen Modus ausgeführt werden können. Möglicherweise ist dies jedoch nicht so effizient wie ein als serieller Plan kompilierter Plan.  
  
-   Wenn Sie MAX_DOP von 1 in 0 oder in einen Wert größer als 1 ändern, muss DBCC FREEPROCCACHE nicht ausgeführt werden. Serielle Pläne können jedoch nicht parallel ausgeführt werden. Das Löschen des entsprechenden Cache ermöglicht daher neuen Plänen, mit Parallelität kompiliert zu werden.  
  
> [!CAUTION]  
>  Das Löschen zwischengespeicherter Pläne aus einem Ressourcenpool, der mehreren Arbeitsauslastungsgruppen zugeordnet ist, wirkt sich auf alle Arbeitsauslastungsgruppen mit dem benutzerdefinierten Ressourcenpool aus, der durch *pool_name* ausgewiesen wird.  
  
 Sie sollten bei der Ausführung von DDL-Anweisungen mit dem Status der Ressourcenkontrolle vertraut sein. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 REQUEST_MEMORY_GRANT_PERCENT: In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] kann bei der Indexerstellung mehr Arbeitsbereichsspeicher verwendet werden, als ursprünglich zugewiesen, um eine bessere Leistung zu erzielen. Die Ressourcenkontrolle in höheren Versionen unterstützt diese besondere Behandlung, die ursprüngliche und alle weiteren Speicherzuweisungen werden jedoch durch den Ressourcenpool und die Einstellungen für Arbeitsauslastungsgruppe begrenzt.  
  
 **Indexerstellung für eine partitionierte Tabelle**  
  
 Der durch die Indexerstellung für nicht ausgerichtete partitionierte Tabellen belegte Arbeitsspeicher ist proportional zur Anzahl der beteiligten Partitionen.  Wenn der insgesamt erforderliche Arbeitsspeicher die Grenze übersteigt, die pro Abfrage von der unter Ressourcenkontrolle stehenden Arbeitsauslastungsgruppe festgelegt wurde (REQUEST_MAX_MEMORY_GRANT_PERCENT), kann die Indexerstellung möglicherweise nicht erfolgreich ausgeführt werden. Da die Arbeitsauslastungsgruppe "default" Abfragen zulässt, die die pro Abfrage festgelegte Grenze mit dem mindestens für eine [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-Kompatibilität erforderlichen Arbeitsspeicher übersteigen, können Benutzer dieselbe Indexerstellung in Arbeitsauslastungsgruppen des Typs "default" ausführen. Voraussetzung ist, dass der Standard-Ressourcenpool über ausreichend Gesamtarbeitsspeicher verfügt, um eine solche Abfrage ausführen zu können.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel veranschaulicht, wie die Wichtigkeit von Anforderungen in der Standardgruppe von `MEDIUM` in `LOW` geändert werden kann.  
  
```  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 Das folgende Beispiel veranschaulicht, wie eine Arbeitsauslastungsgruppe aus dem Pool, in dem sie sich befindet, in den Standardpool verschoben wird.  
  
```  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
