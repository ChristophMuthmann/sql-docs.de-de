---
title: "Beheben von OOM-Problemen (nicht genügend Arbeitsspeicher) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 838f604df21a87912db8d48f815a73c6af27c8f2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="resolve-out-of-memory-issues"></a>Beheben von OOM-Problemen (nicht genügend Arbeitsspeicher)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] verwendet mehr Arbeitsspeicher und nutzt diesen auf andere Weise als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es kann vorkommen, dass der installierte, [!INCLUDE[hek_2](../../includes/hek-2-md.md)] zugeordnete Arbeitsspeicher Ihren wachsenden Anforderungen nicht mehr gerecht wird, sodass kein ausreichender Arbeitsspeicher zur Verfügung steht. In diesem Thema erfahren Sie, wie Sie OOM-Situationen (Out of Memory, nicht genügend Arbeitsspeicher) beheben. Weitere Hinweise zur Vermeidung von Situationen mit unzureichendem Arbeitsspeicher finden Sie auch unter dem Thema [Überwachung und Problembehebung bei der Arbeitsspeichernutzung](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) .  
  
## <a name="covered-in-this-topic"></a>In diesem Thema  
  
|Thema|Übersicht|  
|-----------|--------------|  
|[Beheben von Fehlern aufgrund von OOM-Bedingungen bei der Datenbankwiederherstellung](#bkmk_resolveRecoveryFailures)|Erläutert, wie Sie bei der Fehlermeldung „Fehler beim Wiederherstellungsvorgang für Datenbank „*\<Datenbankname>*“ aufgrund von unzureichendem Arbeitsspeicher im Ressourcenpool „*\<Ressourcenpoolname>*““ vorgehen.|  
|[Beheben von Beeinträchtigungen der Arbeitsauslastung durch wenig oder unzureichenden Arbeitsspeicher](#bkmk_recoverFromOOM)|Erläutert, wie Sie vorgehen, wenn die Leistung durch unzureichenden Arbeitsspeicher beeinträchtigt wird.|  
|[Beheben von Seitenzuordnungsfehlern aufgrund von unzureichendem Arbeitsspeicher, obwohl ausreichend Arbeitsspeicher verfügbar ist](#bkmk_PageAllocFailure)|Erläutert, wie Sie bei der Fehlermeldung „Seitenbelegungen für die Datenbank „*\<Datenbankname>*“ sind aufgrund unzureichenden Arbeitsspeichers im Ressourcenpool „*\<Ressourcenpoolname>*“ nicht zulässig“ vorgehen. … nicht zugelassen" vorgehen, wenn ausreichend Arbeitsspeicher für den Vorgang verfügbar ist.|
|[Bewährte Methoden zum Verwenden von In-Memory OLTP in einer Umgebung mit virtuellen Computern](#bkmk_VMs)|Zu berücksichtigende Punkte beim Verwenden von In-Memory-OLTP in einer virtualisierten Umgebung.|
  
##  <a name="bkmk_resolveRecoveryFailures"></a> Beheben von Fehlern aufgrund von OOM-Bedingungen bei der Datenbankwiederherstellung  
 Wenn Sie versuchen, eine Datenbank wiederherzustellen, erhalten Sie möglicherweise folgende Fehlermeldung: „Fehler beim Wiederherstellungsvorgang für Datenbank „*\<Datenbankname>*“ aufgrund von unzureichendem Arbeitsspeicher im Ressourcenpool „*\<Ressourcenpoolname>*““. Dies gibt an, dass der Server nicht genügend verfügbaren Arbeitsspeicher zum Wiederherstellen der Datenbank hat.
   
Der Server, auf dem Sie eine Datenbank wiederherstellen, muss genügend verfügbaren Arbeitsspeicher für die speicheroptimierten Tabellen in der Datenbanksicherung haben, denn andernfalls wird die Datenbank nicht online geschaltet.  
  
Hat der Server genügend physischen Arbeitsspeicher, aber dieser Fehler tritt weiterhin auf, könnte es sein, dass andere Prozesse zu viel Arbeitsspeicher beanspruchen oder ein Konfigurationsproblem dazu führt, dass nicht genügend Arbeitsspeicher für die Wiederherstellung verfügbar ist. Liegt ein Problem dieser Art vor, können Sie die folgenden Maßnahmen ergreifen, um mehr Arbeitsspeicher für die Wiederherstellung verfügbar zu machen: 
  
-   Schließen Sie ausgeführte Anwendungen vorübergehend.   
    Indem Sie eine oder mehrere aktive Anwendungen schließen oder Dienste, die derzeit nicht benötigt werden, beenden, machen Sie den Arbeitsspeicher, der von den Anwendungen oder Diensten verwendet wurde, für den Wiederherstellungsvorgang verfügbar. Nach der erfolgreichen Wiederherstellung können Sie sie wieder starten.  
  
-   Erhöhen Sie den Wert von MAX_MEMORY_PERCENT.   
    Ist die Datenbank [an einen Ressourcenpool gebunden](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)(dies ist die bewährte Methode), wird der für einen Wiederherstellungsvorgang verfügbare Arbeitsspeicher durch MAX_MEMORY_PERCENT gesteuert. Ist der Wert zu niedrig, schlägt ein Wiederherstellen fehl. In diesem Codeausschnitt wird MAX_MEMORY_PERCENT für den PoolHk-Ressourcenpool in 70 % des installierten Arbeitsspeichers geändert.  
  
    > [!IMPORTANT]  
    > Wenn der Server auf einem virtuellen Computer ausgeführt wird und nicht dediziert ist, legen Sie den Wert von MIN_MEMORY_PERCENT auf denselben Wert wie MAX_MEMORY_PERCENT fest.   
    > Weitere Informationen finden Sie im Thema [Verwenden von In-Memory-OLTP in einer Umgebung mit virtuellen Computern](#bkmk_VMs).  
  
    ```tsql  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     Weitere Informationen zu maximalen Werten für MAX_MEMORY_PERCENT finden Sie im Themenabschnitt [Prozentsatz des für speicheroptimierte Tabellen und Indizes verfügbaren Arbeitsspeichers](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
-   Erhöhen Sie **Max. Serverarbeitsspeicher**.  
    Informationen zum Konfigurieren von **Max. Serverarbeitsspeicher** finden Sie unter dem Thema [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
##  <a name="bkmk_recoverFromOOM"></a> Beheben von Beeinträchtigungen der Arbeitsauslastung durch wenig oder unzureichenden Arbeitsspeicher  
 Grundsätzlich sind Situationen mit wenig oder unzureichendem Arbeitsspeicher zu vermeiden. Häufig lassen sich OOM-Situationen durch eine durchdachte Planung und Überwachung vermeiden. Aber auch die beste Planung schützt nicht vor unvorhersehbaren Ereignissen, die zu knappem oder unzureichendem Arbeitsspeicher führen können. Eine OOM-Bedingung kann in zwei Schritten behoben werden:  
  
1.  [Öffnen einer DAC (dedizierte Administratorverbindung)](#bkmk_openDAC)  
  
2.  [Korrekturmaßnahme](#bkmk_takeCorrectiveAction)  
  
###  <a name="bkmk_openDAC"></a> Öffnen einer DAC (dedizierte Administratorverbindung)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt eine dedizierte Administratorverbindung (Dedicated Administrator Connection, DAC) zur Verfügung. Mit der DAC können Administratoren auf eine ausgeführte Instanz des SQL Server-Datenbankmoduls zugreifen, um Probleme auf dem Server zu beheben, selbst wenn der Server auf andere Clientverbindungen nicht reagiert. Die DAC wird mithilfe des Hilfsprogramms `sqlcmd` und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aufgerufen.  
  
 Hilfe zum Verwenden von DAC mithilfe von SSMS oder `sqlcmd` finden Sie unter [Diagnoseverbindung für Datenbankadministratoren](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
###  <a name="bkmk_takeCorrectiveAction"></a> Korrekturmaßnahme  
 Um die OOM-Bedingung zu beheben, müssen Sie entweder vorhandenen Arbeitsspeicher freigeben, indem Sie die Arbeitsspeichernutzung reduzieren, oder den Tabellen im Arbeitsspeicher mehr Arbeitsspeicherkapazität zur Verfügung stellen.  
  
#### <a name="free-up-existing-memory"></a>Freigeben von vorhandenem Arbeitsspeicher  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>Löschen unwichtiger Zeilen aus speicheroptimierten Tabellen und Abwarten der Garbage Collection  
 Sie können unbedeutende Zeilen aus einer speicheroptimierten Tabelle entfernen. Der Garbage Collector gibt den von diesen Zeilen belegten Speicher wieder an den verfügbaren Arbeitsspeicher zurück. Garbage-Zeilen werden vom In-Memory OLTP-Modul auf aggressive Weise gesammelt. Allerdings kann die Garbage Collection durch eine Transaktion mit langer Ausführungszeit verhindert werden. Beispiel: Bei einer Transaktion, die fünf Minuten ausgeführt wird, kann für Zeilenversionen, die aufgrund von Update-/Löschvorgängen erstellt wurden, während die Transaktion aktiv war, keine Garbage Collection ausgeführt werden.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>Verschieben einer oder mehrerer Zeilen in eine datenträgerbasierte Tabelle  
 In den folgenden TechNet-Artikeln finden Sie Richtlinien zum Verschieben von Zeilen aus einer speicheroptimierten Tabelle in eine datenträgerbasierte Tabelle.  
  
-   [Partitionierung auf Anwendungsebene](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [Anwendungsmuster zur Partitionierung von speicheroptimierten Tabellen](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>Erhöhen der verfügbaren Arbeitsspeicherkapazität  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>Erhöhen des MAX_MEMORY_PERCENT-Werts für den Ressourcenpool  
 Wenn Sie keinen benannten Ressourcenpool für die Tabellen im Arbeitsspeicher erstellt haben, sollten Sie dies nachholen und die [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Datenbanken daran binden. Im Thema [Binden einer Datenbank mit speicheroptimierten Tabellen an einen Ressourcenpool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) finden Sie eine Anleitung zum Erstellen und Binden Ihrer [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Datenbanken an einen Ressourcenpool.  
  
 Wenn die [!INCLUDE[hek_2](../../includes/hek-2-md.md)] -Datenbank an einen Ressourcenpool gebunden ist, können Sie den Arbeitsspeicheranteil, auf den der Pool zugreifen kann, erhöhen. Im Unterabschnitt [Ändern von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT für einen vorhandenen Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) finden Sie entsprechende Anleitungen zum Ändern.  
  
 Erhöhen Sie den Wert von MAX_MEMORY_PERCENT.   
In diesem Codeausschnitt wird MAX_MEMORY_PERCENT für den PoolHk-Ressourcenpool in 70 % des installierten Arbeitsspeichers geändert.  
  
> [!IMPORTANT]  
>  Wenn der Server auf einem virtuellen Computer ausgeführt wird und nicht dediziert ist, legen Sie den Wert von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT auf denselben Wert fest.   
> Weitere Informationen finden Sie im Thema [Verwenden von In-Memory-OLTP in einer Umgebung mit virtuellen Computern](#bkmk_VMs).  
  
```tsql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 Weitere Informationen zu maximalen Werten für MAX_MEMORY_PERCENT finden Sie im Themenabschnitt [Prozentsatz des für speicheroptimierte Tabellen und Indizes verfügbaren Arbeitsspeichers](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable).  
  
##### <a name="install-additional-memory"></a>Installieren zusätzlichen Arbeitsspeichers  
 Die beste Lösung besteht letztendlich darin, falls möglich, zusätzlichen physischen Arbeitsspeicher zu installieren. In diesem Fall sollten Sie bedenken, dass Sie möglicherweise auch den Wert von MAX_MEMORY_PERCENT erhöhen können (siehe Unterabschnitt [Ändern von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT für einen vorhandenen Pool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)), da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wahrscheinlich nicht mehr Arbeitsspeicher benötigen wird, und Sie einen großen bzw. den gesamten Teil des neu installierten Arbeitsspeichers dem Ressourcenpool zur Verfügung stellen können.  
  
> [!IMPORTANT]  
>  Wenn der Server auf einem virtuellen Computer ausgeführt wird und nicht dediziert ist, legen Sie den Wert von MIN_MEMORY_PERCENT und MAX_MEMORY_PERCENT auf denselben Wert fest.   
> Weitere Informationen finden Sie im Thema [Verwenden von In-Memory-OLTP in einer Umgebung mit virtuellen Computern](#bkmk_VMs).  
  
##  <a name="bkmk_PageAllocFailure"></a> Beheben von Seitenzuordnungsfehlern aufgrund von unzureichendem Arbeitsspeicher, obwohl ausreichend Arbeitsspeicher verfügbar ist  
 Wenn Sie die Fehlermeldung `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'http://go.microsoft.com/fwlink/?LinkId=330673' for more information.` im Fehlerprotokoll erhalten, obwohl der verfügbare physische Arbeitsspeicher zum Zuordnen der Seite ausreichend ist, kann dies daran liegen, dass die Ressourcenkontrolle deaktiviert ist. Wenn die Ressourcenkontrolle deaktiviert ist, führt MEMORYBROKER_FOR_RESERVE zu einem künstlichen Mangel an Arbeitsspeicher.  
  
 Um dieses Problem zu beheben, müssen Sie die Ressourcenkontrolle aktivieren.  
  
 Weitere Informationen zu Einschränkungen sowie Anweisungen zum Aktivieren des Resource Governors mit dem Objekt-Explorer, über Eigenschaften des Resource Governors oder mit Transact-SQL finden Sie unter [Aktivieren des Resource Governors](../../relational-databases/resource-governor/enable-resource-governor.md) .  
 
## <a name="bkmk_VMs"></a> Verwenden von In-Memory-OLTP in einer Umgebung mit virtuellen Computern
Servervirtualisierung kann durch eine verbesserte Anwendungsbereitstellung, Wartung, Verfügbarkeit sowie Sicherungs- und Wiederherstellungsprozesse das IT-Kapital und die Betriebskosten Ihres Unternehmens senken und die IT-Effizienz steigern. Dank der neuesten technologischen Entwicklungen können komplexe Datenbankarbeitslasten mithilfe der Virtualisierung leichter konsolidiert werden. Dieses Thema enthält bewährte Methoden zur Verwendung von SQL Server In-Memory-OLTP in einer virtualisierten Umgebung.

### <a name="memory-pre-allocation"></a>Vorabbelegung von Arbeitsspeicher
Für den Arbeitsspeicher in einer virtualisierten Umgebung sind bessere Leistung und erweiterte Unterstützung zentrale Faktoren. Sie müssen sowohl in der Lage sein, virtuellen Computern auf Basis der jeweiligen Anforderungen (Last zu Spitzenzeiten und außerhalb von Spitzenzeiten) schnell Arbeitsspeicher zuzuordnen als auch sicherzustellen, dass dieser Arbeitsspeicher nicht verschwendet wird. Der dynamischer Arbeitsspeicher von Hyper-V erhöht die Flexibilität bei der Zuweisung und Verwaltung von Arbeitsspeicher zwischen virtuellen Computern, die auf einem Host ausgeführt werden.

Einige bewährte Methoden für die Virtualisierung und Verwaltung von SQL Server müssen geändert werden, wenn eine Datenbank mit speicheroptimierten Tabellen virtualisiert wird. Ohne speicheroptimierte Tabellen lauten zwei bewährte Methoden wie folgt:
-  Bei Verwendung von „Min. Serverarbeitsspeicher“ sollte nur die tatsächlich erforderliche Speichermenge zugewiesen werden, sodass ausreichend Speicher für andere Prozesse verbleibt (und Auslagerungen vermieden werden).
-  Legen Sie den Wert für die Vorabbelegung von Arbeitsspeicher nicht zu hoch fest. Andernfalls erhalten andere Prozesse u. U. nicht ausreichend Speicher, wenn sie ihn brauchen. Dies kann zu Speicherauslagerungen führen.

Wenn Sie für eine Datenbank mit speicheroptimierten Tabellen die oben genannten Methoden verwenden, kann der Versuch, die Datenbank wiederherzustellen, dazu führen, dass die Datenbank im Status "Wiederherstellung steht aus" hängen bleibt, obwohl genügend Arbeitsspeicher zum Wiederherstellen der Datenbank verfügbar ist. Die Ursache hierfür ist, dass In-Memory-OLTP die Daten beim Starten aggressiver in den Speicher lädt, als die dynamische Speicherbelegung den Arbeitsspeicher der Datenbank zuweist.

### <a name="resolution"></a>Lösung
Um dieses Risiko abzuschwächen, ordnen Sie der Datenbank vorab genügend Arbeitsspeicher zu, um die Datenbank wiederherzustellen oder neu zu starten. Verwenden Sie hierfür nicht den Minimalwert auf Basis des dynamischen Speichers, um den zusätzlichen Arbeitsspeicher bei Bedarf bereitzustellen.
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten des Arbeitsspeichers für In-Memory OLTP](http://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [Überwachung und Problembehebung bei der Arbeitsspeichernutzung](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [Binden einer Datenbank mit speicheroptimierten Tabellen an einen Ressourcenpool](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Handbuch zur Architektur der Speicherverwaltung](../../relational-databases/memory-management-architecture-guide.md)  
 [Serverkonfigurationsoptionen für den Serverarbeitsspeicher](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
