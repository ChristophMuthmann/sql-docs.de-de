---
title: Handbuch zur Thread- und Taskarchitektur | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/26/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 93be3a22ee517f90e65b8c8ba6dcaa8d90ed8515
ms.openlocfilehash: 3b835536b4f510021f0d966e3214cf1ec5f71f5c
ms.contentlocale: de-de
ms.lasthandoff: 06/07/2017

---
# <a name="thread-and-task-architecture-guide"></a>Handbuch zur Thread- und Taskarchitektur
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Threads sind eine Funktion des Betriebssystems, mit der Anwendungslogik auf mehrere gleichzeitige Ausführungspfade verteilt werden kann. Diese Funktion ist insbesondere dann hilfreich, wenn komplexe Anwendungen viele Tasks besitzen, die gleichzeitig ausgeführt werden können. 

Wenn ein Betriebssystem eine Instanz einer Anwendung ausführt, wird eine als Prozess bezeichnete Einheit erstellt, um die Instanz zu verwalten. Der Prozess besitzt einen so genannten Ausführungsthread. Dabei handelt es sich um eine Folge von Programmieranweisungen, die vom Anwendungscode ausgeführt werden. In einer einfachen Anwendung beispielsweise, mit einem einzigen Satz an Anweisungen, die seriell ausgeführt werden können, gibt es nur einen Ausführungspfad oder -thread durch die Anwendung. Komplexere Anwendungen können mehrere Tasks besitzen, die gleichzeitig anstatt seriell ausgeführt werden können. Dies erfolgt, indem die Anwendung einen eigenen Prozess für jeden Task startet. Das Starten eines Prozesses ist jedoch ein ressourcenintensiver Vorgang, der vermieden werden kann, indem die Anwendung anstelle von Prozessen separate Threads startet. Dieser Vorgang nimmt weniger Ressourcen in Anspruch. Außerdem kann das Ausführen der einzelnen Threads unabhängig von anderen Threads geplant werden, die einem Prozess zugeordnet sind.

Threads ermöglichen, dass komplexe Anwendungen CPUs effizienter verwenden; dies gilt auch für Computer mit nur einer CPU. Bei einer einzigen CPU kann zu einem bestimmten Zeitpunkt immer nur ein Thread ausgeführt werden. Wenn ein Thread einen umfangreiche Vorgang ausführt, für die die CPU nicht verwendet wird, z. B. beim Lesen oder Schreiben vom bzw. auf den Datenträger, kann so lange ein anderer Thread ausgeführt werden, bis der erste Vorgang beendet ist. Da es möglich ist, Threads auszuführen, während andere Threads auf das Abschließen eines Vorgangs warten, kann eine Anwendung die CPU optimal nutzen. Dies gilt insbesondere für Multibenutzeranwendungen mit umfangreichen E/A-Vorgängen, wie es bei einem Datenbankserver der Fall ist. Computer mit mehreren Mikroprozessoren oder CPUs können gleichzeitig nur einen Thread pro CPU ausführen. Wenn ein Computer beispielsweise über acht CPUs verfügt, können gleichzeitig acht Threads ausgeführt werden.

## <a name="sql-server-batch-or-task-scheduling"></a>Planen von Batches oder Tasks in SQL Server

### <a name="allocating-threads-to-a-cpu"></a>Reservieren von Threads für eine CPU

Standardmäßig startet jede Instanz von SQL Server jeden Thread. Wenn Affinität aktiviert wurde, weist das Betriebssystem jeden Thread einer bestimmten CPU zu. Das Betriebssystem verteilt Threads von SQL Server-Instanzen je nach Auslastung auf die Mikroprozessoren oder CPUs eines Computers. Manchmal kann das Betriebssystem einen Thread auch von einer stark beanspruchten CPU zu einer anderen CPU verlagern. Im Gegensatz dazu weist das SQL Server-Datenbankmodul Arbeitsthreads Zeitplanungsmodulen zu, die die Threads gleichmäßig auf die CPUs verteilen.

Die Affinitätsmaskenoption wird mit [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)festgelegt. Wenn die Affinitätsmaske nicht festgelegt wird, ordnet die SQL Server-Instanz den Zeitplanungsmodulen, die nicht durch die Maske ausgeschlossen werden, gleichmäßig Arbeitsthreads zu.

### <a name="using-the-lightweight-pooling-option"></a>Verwenden der Lightweightpooling-Option

Das Wechseln zwischen Threadkontexten stellt keinen sehr großen Aufwand dar. Für die meisten Instanzen von SQL Server stellt es keinen Leistungsunterschied dar, ob die Option für Lightweightpooling auf 0 oder 1 festgelegt ist. Die einzigen Instanzen von SQL Server, die möglicherweise von [Lightweightpooling](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) profitieren, sind diejenigen, die auf einem Computer mit folgenden Eigenschaften ausgeführt werden:    
* Ein großer Server mit mehreren CPUs.
* Alle CPUs werden mit nahezu maximaler Kapazität ausgeführt.
* Eine große Anzahl an Kontextwechseln findet statt.

Für diese Systeme kann eventuell eine geringe Leistungssteigerung erzielt werden, indem der Wert für Lightweightpooling auf 1 festgelegt wird.

Es wird empfohlen, die Fibermodusplanung nicht für Routinevorgänge zu verwenden, Der Grund hierfür liegt darin, dass es zu Leistungseinbußen führen kann, wenn die gängigen Vorteile des Kontextwechsels nicht genutzt werden können, und dass einige Komponenten von SQL Server im Fibermodus nicht ordnungsgemäß arbeiten können. Weitere Informationen finden Sie unter „Lightweightpooling“.

## <a name="thread-and-fiber-execution"></a>Thread- und Fiberausführung

Von Microsoft Windows wird ein numerisches Prioritätssystem verwendet, das von 1 bis 31 reicht, um die Ausführung von Threads zu planen. Null ist für die Verwendung durch das Betriebssystem reserviert. Wenn mehrere Threads auf die Ausführung warten, sendet Windows den Thread mit der höchsten Priorität.

Standardmäßig hat jede Instanz von SQL Server die Priorität 7, was als normale Priorität bezeichnet wird. Die Priorität von SQL Server-Threads ist somit hoch genug, um ausreichend CPU-Ressourcen zu erhalten, ohne jedoch im Gegenzug andere Anwendungen zu beeinträchtigen. 

Mithilfe der Konfigurationsoption [Prioritätserhöhung](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) kann die Priorität der Threads von einer Instanz von SQL Server auf 13 heraufgesetzt werden. Diese Einstellung wird als "hohe Priorität" bezeichnet. Durch diese Einstellung erhalten SQL Server-Threads eine höhere Priorität als die meisten anderen Anwendungen. SQL Server-Threads werden somit im Allgemeinen verteilt, sobald sie zur Ausführung bereit sind, und müssen nicht für Threads anderer Anwendungen zurücktreten. Auf diese Weise kann die Leistung gesteigert werden, wenn ein Server nur Instanzen von SQL Server und keine anderen Anwendungen ausführt. Wenn jedoch eine arbeitsspeicherintensive Operation in SQL Server durchgeführt wird, verfügen andere Anwendungen in der Regel nicht über eine ausreichend hohe Priorität, um Vorrang vor dem SQL Server-Thread zu besitzen. 

Falls Sie mehrere Instanzen von SQL Server auf einem Computer ausführen und die Prioritätserhöhung nur für einige Instanzen aktiviert ist, kann die Leistung von Instanzen, die mit normaler Priorität ausgeführt werden, beeinträchtigt werden. Auch kann die Leistung anderer Anwendungen und Komponenten auf dem Server beeinträchtigt werden, wenn die Prioritätserhöhung aktiviert ist. Diese Option sollte somit nur in genau kontrollierten Situationen verwendet werden.


## <a name="hot-add-cpu"></a>Hinzufügen von CPUs im laufenden Systembetrieb

Hinzufügen von CPUs im laufenden Systembetrieb bedeutet, dass Sie CPUs dynamisch hinzufügen können, während das System ausgeführt wird. CPUs können auf verschiedene Weise hinzugefügt werden: physisch durch neue Hardware, logisch durch eine Onlinepartitionierung der Hardware oder virtuell über eine Virtualisierungsschicht. Seit SQL Server 2008 unterstützt SQL Server das Hinzufügen von CPUs im laufenden Systembetrieb.

Voraussetzungen für das Hinzufügen von CPUs im laufenden Systembetrieb:  
* Die Hardware muss das Hinzufügen von CPUs zu einem laufenden System unterstützen.
* Sie müssen eines der folgenden Betriebssysteme verwenden: Windows Server 2008 Datacenter 64-Bit Edition oder Windows Server 2008 Enterprise Edition für Itanium-basierte Systeme
* SQL Server Enterprise.
* SQL Server kann nicht für die Verwendung von Soft-NUMA konfiguriert werden. Weitere Informationen zu Soft-NUMA finden Sie unter [Soft-NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md).

Neu hinzugefügte CPUs werden nicht automatisch von SQL Server verwendet. So wird verhindert, dass SQL Server CPUs verwendet, die aus einem anderen Grund hinzugefügt wurden. Führen Sie die [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) -Anweisung aus, nachdem Sie CPUs hinzugefügt haben, damit die neuen CPUs von SQL Server als verfügbare Ressourcen erkannt werden.

> [!NOTE]
> Falls Sie die Option [Affinity64 Mask](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) konfiguriert haben, muss diese Option so angepasst werden, dass die neuen CPUs verwendet werden.
 

## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>Bewährte Methoden zum Ausführen von SQL Server auf Computern mit mehr als 64 CPUs

### <a name="assigning-hardware-threads-with-cpus"></a>Zuweisen von Hardwarethreads zu CPUs

Verwenden Sie die Serverkonfigurationsoptionen „Affinity Mask“ und „Affinity64 Mask“ nicht, um Prozessoren an bestimmte Threads zu binden. Diese Optionen sind auf 64 CPUs beschränkt. Verwenden Sie stattdessen die SET PROCESS AFFINITY-Option von [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) .

### <a name="managing-the-transaction-log-file-size"></a>Verwalten der Größe der Transaktionsprotokolldatei

Verlassen Sie sich nicht auf automatische Vergrößerung, um die Transaktionsprotokolldatei zu vergrößern. Das Vergrößern des Transaktionsprotokolls muss ein serieller Prozess sein. Das Erweitern des Protokolls kann bis zum Abschließen der Protokollerweiterung verhindern, dass Transaktionsschreibvorgänge fortgeführt werden. Weisen Sie stattdessen allen Protokolldateien im Voraus Speicherplatz zu, indem Sie die Dateigröße auf einen Wert festlegen, der hoch genug ist, um der typischen Arbeitsauslastung in der Umgebung gerecht zu werden.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>Festlegen des maximalen Grads an Parallelität für Indexvorgänge

Die Leistung von Indexvorgängen, z. B. das Erstellen bzw. das erneute Erstellen von Indizes, kann auf Computern mit vielen CPUs verbessert werden, indem das Wiederherstellungsmodell der Datenbank vorübergehend entweder auf das massenprotokollierte oder auf das einfache Wiederherstellungsmodell festgelegt wird. Diese Indexvorgänge können eine bedeutende Protokollaktivität generieren, und Protokollkonflikte können sich auf den besten Grad an Parallelität (Degree of Parallelism, DOP) von SQL Server auswirken.

Darüber hinaus sollten Sie Anpassen der **Max. Grad an Parallelität (MAXDOP)** Serverkonfigurationsoption für diese Vorgänge. Die folgenden Richtlinien basieren auf internen Tests und sind allgemeine Empfehlungen. Testen Sie unterschiedliche MAXDOP-Einstellungen, um die optimale Einstellung für die Umgebung zu bestimmen.

* Beschränken Sie den Wert der Option „Max. Grad an Parallelität“ für das vollständige Wiederherstellungsmodell auf acht oder weniger.   
* Für das massenprotokollierte Modell oder das einfache Wiederherstellungsmodell sollten Sie den Wert der Option „Max. Grad an Parallelität“ auf einen Wert größer als acht festlegen.   
* Bei Servern, für die NUMA konfiguriert wurde, sollte der maximale Grad an Parallelität nicht die Anzahl von CPUs überschreiten, die den einzelnen NUMA-Knoten zugewiesen werden. Das liegt daran, dass die Abfrage mit größerer Wahrscheinlichkeit den lokalen Arbeitsspeicher von 1 NUMA-Knoten verwendet, sodass die Speicherzugriffzeit verbessert werden kann.  
* Für Server, auf denen hyper-threading aktiviert und wurden produzierten im Jahr 2009 oder früher (bevor Funktion Hyperthreading verbessert wurde), der MAXDOP-Wert sollte die Anzahl der physischen Prozessoren, anstatt von logischen Prozessoren nicht überschreiten.

Weitere Informationen zu der Max. Grad an Parallelität (Option), finden Sie unter [Konfigurieren der max Degree of Parallelism Server Configuration Option](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

### <a name="setting-the-maximum-number-of-worker-threads"></a>Festlegen der maximalen Anzahl von Arbeitsthreads

Legen Sie die maximale Anzahl von Arbeitsthreads immer auf einen höheren Wert als die Einstellung für den maximalen Grad an Parallelität fest. Die Anzahl der Arbeitsthreads muss immer auf einen Wert festgelegt werden, der mindestens das Siebenfache der Anzahl von CPUs beträgt, die auf dem Server vorhanden sind. Weitere Informationen finden Sie unter [Konfigurieren der Serverkonfigurationsoption „Maximale Anzahl von Arbeitsthreads“](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).

### <a name="using-sql-trace-and-sql-server-profiler"></a>Verwenden der SQL-Ablaufverfolgung und von SQL Server Profiler

 Es wird davon abgeraten, die SQL-Ablaufverfolgung und SQL Server Profiler in einer Produktionsumgebung zu verwenden. Der Aufwand zum Ausführen dieser Tools nimmt mit zunehmender Anzahl von CPUs zu. Wenn Sie die SQL-Ablaufverfolgung in einer Produktionsumgebung verwenden müssen, sollten Sie die Anzahl der Ablaufverfolgungsereignisse auf ein Minimum beschränken. Erstellen Sie für jedes Ablaufverfolgungsereignis ein Profil, und führen Sie einen Auslastungstest durch. Vermeiden Sie es, Ereignisse zu kombinieren, die die Leistung stark beeinträchtigen.

### <a name="setting-the-number-of-tempdb-data-files"></a>Festlegen der Anzahl der tempdb-Datendateien

In der Regel sollte die Anzahl der tempdb-Datendateien mit der Anzahl der CPUs übereinstimmen. Sie können den Aufwand für die Datenbankverwaltung jedoch reduzieren, indem Sie die Parallelitätsanforderungen von tempdb sorgfältig überdenken. Wenn ein System beispielsweise über 64 CPUs verfügt und tempdb in der Regel nur von 32 Abfragen verwendet wird, lässt sich keine Leistungsverbesserung erzielen, indem die Anzahl der tempdb-Dateien auf 64 erhöht wird.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>SQL Server-Komponenten, die mehr als 64 CPUs verwenden können

In der folgenden Tabelle sind SQL Server-Komponenten aufgeführt, und es wird angegeben, ob sie mehr als 64 CPUs verwenden können.

|Prozessname   |Ausführbares Programm |Verwenden von mehr als 64 CPUs |  
|----------|----------|----------|  
|SQL Server-Datenbankmodul |Sqlserver.exe  |Ja |  
|Reporting Services |Rs.exe |Nein |  
|Analysis Services  |As.exe |Nein |  
|Integration Services   |Is.exe |Nein |  
|Service Broker |Sb.exe |Nein |  
|Volltextsuche   |Fts.exe    |Nein |  
|SQL Server-Agent   |Sqlagent.exe   |Nein |  
|SQL Server Management Studio   |Ssms.exe   |Nein |  
|SQL Server-Setup   |Setup.exe  |Nein |  



