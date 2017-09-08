---
title: ALTER WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e5a5d5650311115edc52866abdd167700438cc1f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Konfiguration einer vorhandenen Resource Governor Workload und weist sie optional einen an einen Ressourcenpool der Ressourcenkontrolle.  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
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
 *Gruppenname* | "**Standard**"  
 Der Name einer vorhandenen benutzerdefinierten Arbeitsauslastungsgruppe oder der standardmäßigen Ressourcenkontrollen-Arbeitsauslastungsgruppe.  
  
> [!NOTE]  
>  Die Ressourcenkontrolle erstellt den "Standard" und interne Gruppen, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist.  
  
 Die "default"-Option muss in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden, wenn sie mit ALTER WORKLOAD GROUP verwendet wird, um einen Konflikt mit dem vom System reservierten Wort DEFAULT zu vermeiden. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Verwenden vordefinierte Arbeitsauslastungsgruppen und Ressourcenpools werden ausschließlich Kleinbuchstabe Namen, z. B. "Default". Dies sollte bei Servern beachtet werden, die bei der Sortierung zwischen Groß-/Kleinschreibung unterscheiden. Server, die bei der Sortierung keine Groß- und Kleinschreibung unterscheiden, z. B. SQL_Latin1_General_CP1_CI_AS, behandeln "default" und "Default" gleich.  
  
 IMPORTANCE = { LOW | MEDIUM | HIGH }  
 Gibt die relative Wichtigkeit einer Anforderung in der Arbeitsauslastungsgruppe an. Die Wichtigkeit kann einen der folgenden Werte aufweisen:  
  
-   LOW  
  
-   MEDIUM (Standard)  
  
-   HIGH  
  
> [!NOTE]  
>  Intern wird jede Wichtigkeitseinstellung als Zahl gespeichert, die für Berechnungen verwendet wird.  
  
 IMPORTANCE hat einen lokalen Bezug zum Ressourcenpool; Arbeitsauslastungsgruppen mit verschiedener Wichtigkeit innerhalb desselben Ressourcenpools beeinflussen sich gegenseitig, haben jedoch keine Auswirkungen auf Arbeitsauslastungsgruppen in anderen Ressourcenpools.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*Wert*  
 Gibt die Höchstmenge an Arbeitsspeicher an, die eine einzelne Anforderung vom Pool in Anspruch nehmen kann. Dieser Prozentwert ist relativ zur Ressourcenpoolgröße, die von MAX_MEMORY_PERCENT festgelegt wird.  
  
> [!NOTE]  
>  Die angegebene Menge bezieht sich nur auf den für die Abfrageausführung gewährten Arbeitsspeicher.  
  
 *Wert* muss 0 oder eine positive ganze Zahl sein. Der zulässige Bereich für *Wert* liegt zwischen 0 und 100. Die Standardeinstellung für *Wert* ist 25.  
  
 Beachten Sie Folgendes:  
  
-   Festlegen von *Wert* auf 0 verhindert, dass Abfragen mit Sort- und HASH JOIN-Vorgängen in benutzerdefinierten Arbeitsauslastungsgruppen ausgeführt wird.  
  
-   Wir empfehlen nicht die Einstellung *Wert* größer als 70, da der Server möglicherweise nicht genug freien Arbeitsspeicher reservieren festgelegt, wenn andere gleichzeitige Abfragen ausgeführt werden. Dadurch tritt möglicherweise der Timeoutfehler 8645 auf.  
  
> [!NOTE]  
>  Wenn die Arbeitsspeicheranforderungen der Abfrage den Grenzwert überschreiten, der von diesem Parameter angegeben wird, führt der Server folgende Vorgänge aus:  
>   
>  Bei benutzerdefinierten Arbeitsauslastungsgruppen versucht der Server, den Grad der Parallelität für diese Abfrage zu reduzieren, bis die Arbeitsspeicheranforderung den Grenzwert unterschreitet oder bis der Grad der Parallelität dem Wert 1 entspricht. Wenn die Arbeitsspeicheranforderung der Abfrage den Grenzwert immer noch überschreitet, tritt Fehler 8657 auf.  
>   
>  Bei internen und Standard-Arbeitsauslastungsgruppen lässt der Server zu, dass der Abfrage der erforderliche Arbeitsspeicher zugewiesen wird.  
>   
>  Beachten Sie, dass in beiden Fällen der Timeoutfehler 8645 auftreten kann, wenn der Server nicht über ausreichend physischen Arbeitsspeicher verfügt.  
  
 REQUEST_MAX_CPU_TIME_SEC =*Wert*  
 Gibt die maximale CPU-Zeit in Sekunden an, die eine Anforderung beanspruchen kann. *Wert* muss 0 oder eine positive ganze Zahl sein. Die Standardeinstellung für *Wert* ist 0 (null) bedeutet unbeschränkt.  
  
> [!NOTE]  
>  Die Ressourcenkontrolle verhindert nicht, dass eine Anforderung bei Erreichung des maximalen Zeitlimits fortgesetzt wird. Es wird jedoch ein Ereignis generiert. Weitere Informationen finden Sie unter [CPU Threshold Exceeded-Ereignisklasse](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).  
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*Wert*  
 Gibt die maximale Zeit in Sekunden an, die eine Abfrage auf das Freiwerden einer Arbeitspeicherzuweisung (Arbeitsspeicherpuffer) wartet.  
  
> [!NOTE]  
>  Eine Abfrage schlägt nicht grundsätzlich fehl, wenn das Timeout der Arbeitsspeicherzuweisung erreicht wird. Eine Abfrage schlägt nur fehl, wenn zu viele Abfragen gleichzeitig ausgeführt werden. Andernfalls könnte die Abfrage nur die minimale Arbeitsspeicherzuweisung nutzen, was zu reduzierter Abfrageleistung führen kann.  
  
 *Wert* muss eine positive ganze Zahl sein. Die Standardeinstellung für *Wert*, 0, verwendet eine interne Berechnung basierend auf den Abfragekosten, um die maximale Zeit festlegen.  
  
 MAX_DOP =*Wert*  
 Gibt den maximalen Grad der Parallelität (DOP) für parallele Anforderungen an. *Wert* muss 0 oder eine positive ganze Zahl, 1 und 255. Wenn *Wert* gleich 0 ist, wählt der Server die Max. Grad an Parallelität. Dies ist die Standardeinstellung und die empfohlene Einstellung.  
  
> [!NOTE]  
>  Der Istwert, den der [!INCLUDE[ssDE](../../includes/ssde-md.md)] für MAX_DOP festlegt, ist möglicherweise kleiner als der angegebene Wert. Der endgültige Wert richtet sich nach der Formel min (255, *Anzahl von CPUs)*.  
  
> [!CAUTION]  
>  Das Ändern von MAX_DOP kann die Leistung des Servers beeinträchtigen. Wenn Sie MAX_DOP ändern müssen, wird empfohlen, diesen auf einen Wert festzulegen, der kleiner oder gleich der maximalen Anzahl der Hardware- Zeitplanungsmodule ist, die in einem einzelnen NUMA-Knoten vorhanden sind. Es wird empfohlen, MAX_DOP nicht auf einen höheren Wert als 8 festzulegen.  
  
 MAX_DOP wird wie folgt behandelt:  
  
-   MAX_DOP als Abfragehinweis wird so lange berücksichtigt, wie die Arbeitsauslastungsgruppe MAX_DOP nicht überschritten wird.  
  
-   ###MAX_DOP als Abfragehinweis überschreibt immer sp_configure 'max. Grad an Parallelität'.  
  
-   Die Arbeitsauslastungsgruppe MAX_DOP überschreibt sp_configure 'Max. Grad an Parallelität'.  
  
-   Wenn die Abfrage als seriell markiert ist (MAX_DOP = 1) zum Zeitpunkt der Kompilierung, es kann nicht wieder in Parallel geändert werden zur Laufzeit unabhängig von der arbeitsauslastung oder der Sp_configure-Einstellung.  
  
 Nach der Konfiguration kann DOP nur bei Arbeitsspeicher-Engpässen verringert werden. Die Neukonfiguration der Arbeitsauslastungsgruppe ist während des Wartens in der Speicherzuweisungs-Warteschlange nicht sichtbar.  
  
 GROUP_MAX_REQUESTS =*Wert*  
 Gibt die maximale Anzahl gleichzeitiger Anforderungen an, die in der Arbeitsauslastungsgruppe ausgeführt werden können. *Wert* muss 0 oder eine positive ganze Zahl sein. Die Standardeinstellung für *Wert*0 lässt unbegrenzte Anforderungen. Wenn die maximale Anzahl gleichzeitiger Anforderungen erreicht wird, kann sich ein Benutzer dieser Gruppe zwar anmelden, wird jedoch in den Wartezustand versetzt, bis die Anzahl gleichzeitiger Anforderungen unter den angegebenen Wert gefallen ist.  
  
 Mithilfe von { *Pool_name* | "**Standard**"}  
 Verknüpft die Arbeitsauslastungsgruppe mit dem benutzerdefinierten Ressourcenpool identifizierten *Pool_name*, die eingefügt der Arbeitsauslastungsgruppe im Ressourcenpool. Wenn *Pool_name* nicht angegeben ist oder wenn das USING-Argument nicht verwendet wird, wird die Arbeitsauslastungsgruppe in den vordefinierten Standardpool der Ressourcenkontrolle eingefügt.  
  
 Die "default"-Option muss in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden, wenn sie mit ALTER WORKLOAD GROUP verwendet wird, um einen Konflikt mit dem vom System reservierten Wort DEFAULT zu vermeiden. Weitere Informationen finden Sie unter [Datenbankbezeichner](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Bei der "default"-Option wird die Groß-/Kleinschreibung beachtet.  
  
## <a name="remarks"></a>Hinweise  
 ALTER WORKLOAD GROUP ist für die Standardgruppe zulässig.  
  
 Änderungen an der Konfiguration der Arbeitsauslastungsgruppe werden erst wirksam, nachdem ALTER RESOURCE GOVERNOR RECONFIGURE ausgeführt wurde. Wenn Sie eine Einstellung zur planauswirkung zu ändern, die neue Einstellung werden erst wirksam zuvor zwischengespeicherte Pläne nach dem Ausführen von DBCC FREEPROCCACHE (*Pool_name*), wobei *Pool_name* ist der Name einer Ressource Ressourcenpool der Ressourcenkontrolle auf dem die Arbeitsauslastungsgruppe zugeordnet ist.  
  
-   Wenn Sie MAX_DOP auf 1 ändern möchten, ist das Ausführen von DBCC FREEPROCCACHE nicht erforderlich, da parallele Pläne im seriellen Modus ausgeführt werden können. Allerdings so effizient wie einen Plan als ein serieller Plan kompiliert möglicherweise nicht.  
  
-   Wenn Sie MAX_DOP von 1 auf 0 ändern oder ein Wert größer als 1 ist, Ausführen von DBCC FREEPROCCACHE nicht erforderlich ist. Serielle Pläne jedoch kann nicht parallel ausgeführt werden, damit das Löschen des Zwischenspeichers jeweiligen auf neue Pläne aus, um potenziell die Möglichkeit wird mit der Parallelität kompiliert werden.  
  
> [!CAUTION]  
>  Löschen zwischengespeicherter Pläne aus einem Ressourcenpool, die mehr als eine Arbeitsauslastungsgruppe zugeordnet ist wirkt sich auf alle Arbeitsauslastungsgruppen mit dem benutzerdefinierten Ressourcenpool identifizierten *Pool_name*.  
  
 Sie sollten bei der Ausführung von DDL-Anweisungen mit dem Status der Ressourcenkontrolle vertraut sein. Weitere Informationen finden Sie unter [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 REQUEST_MEMORY_GRANT_PERCENT: In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] kann bei der Indexerstellung mehr Arbeitsbereichsspeicher verwendet werden, als ursprünglich zugewiesen, um eine bessere Leistung zu erzielen. Die Ressourcenkontrolle in höheren Versionen unterstützt diese besondere Behandlung, die ursprüngliche und alle weiteren Speicherzuweisungen werden jedoch durch den Ressourcenpool und die Einstellungen für Arbeitsauslastungsgruppe begrenzt.  
  
 **Erstellung eines Indexes für eine partitionierte Tabelle**  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

