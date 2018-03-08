---
title: Erstellen Sie die ARBEITSAUSLASTUNGSGRUPPE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
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
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
ms.assetid: d949e540-9517-4bca-8117-ad8358848baa
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cec1360259d78679fab31a45a074d5fbbf3779b5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Arbeitsauslastungsgruppe unter Ressourcenkontrolle und verknüpft die Arbeitsauslastungsgruppe mit einem Ressourcenpool der Ressourcenkontrolle. Die Ressourcenkontrolle ist nicht verfügbar in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE WORKLOAD GROUP group_name  
[ WITH  
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING {   
    [ pool_name | "default" ]    
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]   
    } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *group_name*  
 Der benutzerdefinierte Name für die Arbeitsauslastungsgruppe. *Gruppenname* ist alphanumerisch, kann bis zu 128 Zeichen sein, muss innerhalb einer Instanz eindeutig sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und Sie müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 WICHTIGKEIT = {NIEDRIG | **MITTEL** | HOHE}  
 Gibt die relative Wichtigkeit einer Anforderung in der Arbeitsauslastungsgruppe an. Wichtigkeit kann einen der folgenden, wobei MEDIUM die Standardeinstellung:  
  
-   LOW  
-   MEDIUM (Standard)    
-   HIGH  
  
> [!NOTE]  
> Intern wird jede Wichtigkeitseinstellung als Zahl gespeichert, die für Berechnungen verwendet wird.  
  
 IMPORTANCE hat einen lokalen Bezug zum Ressourcenpool; Arbeitsauslastungsgruppen mit verschiedener Wichtigkeit innerhalb desselben Ressourcenpools beeinflussen sich gegenseitig, haben jedoch keine Auswirkungen auf Arbeitsauslastungsgruppen in anderen Ressourcenpools.  
  
 REQUEST_MAX_MEMORY_GRANT_PERCENT =*Wert*  
 Gibt die Höchstmenge an Arbeitsspeicher an, die eine einzelne Anforderung vom Pool in Anspruch nehmen kann. Dieser Prozentwert ist relativ zur Ressourcenpoolgröße, die von MAX_MEMORY_PERCENT festgelegt wird.  
  
> [!NOTE]  
> Die angegebene Menge bezieht sich nur auf den für die Abfrageausführung gewährten Arbeitsspeicher.  
  
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
  
 REQUEST_MAX_CPU_TIME_SEC =*value*  
 Gibt die maximale CPU-Zeit in Sekunden an, die eine Anforderung beanspruchen kann. *Wert* muss 0 oder eine positive ganze Zahl sein. Die Standardeinstellung für *Wert* ist 0 (null) bedeutet unbeschränkt.  
  
> [!NOTE]  
> Standardmäßig wird Ressourcenkontrolle nicht verhindern, dass eine Anforderung fortgesetzt, wenn die maximale Zeit überschritten wird. Es wird jedoch ein Ereignis generiert. Weitere Informationen finden Sie unter [CPU Threshold Exceeded-Ereignisklasse](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md).  

> [!IMPORTANT]
> Beginnend mit [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3, und Verwenden von [Ablaufverfolgungsflag 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md), Ressourcenkontrolle wird eine Anforderung abgebrochen, wenn die maximale Zeit überschritten wird. 
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*value*  
 Gibt die maximale Zeit in Sekunden an, die eine arbeitsspeicherzuweisung (Arbeitsspeicherpuffer) auf das Freiwerden eine Abfrage wartet.  
  
> [!NOTE]  
>  Eine Abfrage schlägt nicht grundsätzlich fehl, wenn das Timeout der Arbeitsspeicherzuweisung erreicht wird. Eine Abfrage schlägt nur fehl, wenn zu viele Abfragen gleichzeitig ausgeführt werden. Andernfalls könnte die Abfrage nur die minimale Arbeitsspeicherzuweisung nutzen, was zu reduzierter Abfrageleistung führen kann.  
  
 *Wert* muss 0 oder eine positive ganze Zahl sein. Die Standardeinstellung für *Wert*, 0, verwendet eine interne Berechnung basierend auf den Abfragekosten, um die maximale Zeit festlegen.  
  
 MAX_DOP =*value*  
 Gibt den maximalen Grad der Parallelität (DOP) für parallele Anforderungen an. *Wert* muss 0 oder eine positive ganze Zahl sein. Der zulässige Bereich für *Wert* liegt zwischen 0 und 64. Die Standardeinstellung für *Wert*, 0, verwendet die globale Einstellung. MAX_DOP wird wie folgt behandelt:  
  
-   MAX_DOP als Abfragehinweis wird so lange verwendet, wie die Arbeitsauslastungsgruppe MAX_DOP nicht überschritten wird. Wenn der Wert des MAXDOP-Abfragehinweises den mit der Ressourcenkontrolle konfigurierten Wert überschreitet, verwendet das Datenbankmodul den MAXDOP-Wert der Ressourcenkontrolle.  
  
-   ###MAX_DOP als Abfragehinweis überschreibt immer sp_configure 'max. Grad an Parallelität'.  
  
-   Die Arbeitsauslastungsgruppe MAX_DOP überschreibt sp_configure 'Max. Grad an Parallelität'.  
  
-   Wenn die Abfrage zur Kompilierzeit als seriell (MAX_DOP = 1 ) markiert ist, kann sie zur Laufzeit nicht wieder in parallel geändert werden, und zwar unabhängig von der Arbeitsauslastungsgruppe oder der sp_configure-Einstellung.  
  
-   Nach der Konfiguration kann DOP nur bei Arbeitsspeicher-Engpässen verringert werden. Die Neukonfiguration der Arbeitsauslastungsgruppe ist während des Wartens in der Speicherzuweisungs-Warteschlange nicht sichtbar.  
  
 GROUP_MAX_REQUESTS =*value*  
 Gibt die maximale Anzahl gleichzeitiger Anforderungen an, die in der Arbeitsauslastungsgruppe ausgeführt werden können. *Wert* muss 0 oder eine positive ganze Zahl sein. Die Standardeinstellung für *Wert*0 lässt unbegrenzte Anforderungen. Wenn die maximale Anzahl gleichzeitiger Anforderungen erreicht wird, kann sich ein Benutzer dieser Gruppe zwar anmelden, wird jedoch in den Wartezustand versetzt, bis die Anzahl gleichzeitiger Anforderungen unter den angegebenen Wert gefallen ist.  
  
 Mithilfe von { *Pool_name* | **"Default"** }  
 Verknüpft die Arbeitsauslastungsgruppe mit dem benutzerdefinierten Ressourcenpool identifizierten *Pool_name*. Hierdurch wird die Arbeitsauslastungsgruppe im Endeffekt im Ressourcenpool platziert. Wenn *Pool_name* nicht angegeben wird, oder wenn das USING-Argument nicht verwendet wird, wird die Arbeitsauslastungsgruppe in den vordefinierten Standardpool der Ressourcenkontrolle eingefügt.  
  
 "default" ist ein reserviertes Wort und muss bei der Verwendung mit USING in Anführungszeichen ("") oder Klammern ([]) eingeschlossen werden.  
  
> [!NOTE]  
>  Für vordefinierte Arbeitsauslastungsgruppen und Ressourcenpools werden ausschließlich kleingeschriebene Namen verwendet, z. B. "default". Dies sollte bei Servern beachtet werden, die bei der Sortierung zwischen Groß-/Kleinschreibung unterscheiden. Server, die bei der Sortierung keine Groß- und Kleinschreibung unterscheiden, z. B. SQL_Latin1_General_CP1_CI_AS, behandeln "default" und "Default" gleich.  
  
 EXTERNE External_pool_name | "Default"  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 Arbeitsauslastungsgruppe kann einen externen Ressourcenpool angeben. Sie können eine Arbeitsauslastungsgruppe zu definieren und zuordnen 2 Pools:  
  
-   Einen Ressourcenpool für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Arbeitslasten und Abfragen  
  
-   Einen externen Ressourcenpool für externe Prozesse. Weitere Informationen finden Sie unter [Sp_execute_external_script &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 REQUEST_MEMORY_GRANT_PERCENT: Die Indexerstellung kann verwendet werden, um mehr Arbeitsbereichsspeicher als ursprünglich zugewiesen zu verwenden, damit eine bessere Leistung erzielt wird. Diese besondere Behandlung wird von der Ressourcenkontrolle in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützt. Die Zuweisung anfänglichen und zusätzlichen Arbeitsspeichers wird jedoch durch den Ressourcenpool und die Einstellungen der Arbeitsauslastungsgruppe begrenzt.  
  
 **Erstellung eines Indexes für eine partitionierte Tabelle**  
  
 Der durch die Indexerstellung für nicht ausgerichtete partitionierte Tabellen belegte Arbeitsspeicher ist proportional zur Anzahl der beteiligten Partitionen. Wenn der insgesamt erforderliche Arbeitsspeicher die Grenze übersteigt, die pro Abfrage von der unter Ressourcenkontrolle stehenden Arbeitsauslastungsgruppe festgelegt wurde (REQUEST_MAX_MEMORY_GRANT_PERCENT), kann die Indexerstellung möglicherweise nicht erfolgreich ausgeführt werden. Da die Arbeitsauslastungsgruppe "default" Abfragen zulässt, die die pro Abfrage festgelegte Grenze für mindestens erforderlichen Arbeitsspeicher übersteigen, können Benutzer dieselbe Indexerstellung in Arbeitsauslastungsgruppen des Typs "default" ausführen. Voraussetzung ist, dass der Standardressourcenpool über ausreichend Gesamtarbeitsspeicher verfügt, um eine solche Abfrage ausführen zu können.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt, wie eine Arbeitsauslastungsgruppe mit dem Namen `newReports` erstellt wird. Sie verwendet die Standardeinstellungen der Ressourcenkontrolle und befindet sich in deren Standardpool. Im Beispiel wird der `default`-Pool angegeben, wobei dies jedoch nicht erforderlich ist.  
  
```  
CREATE WORKLOAD GROUP newReports  
    USING "default" ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  

