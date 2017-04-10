---
title: "Verbessern der Leistung der Mergereplikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Veröffentlichungen [SQL Server-Replikation], Entwurf und Leistung"
  - "Entwerfen von Datenbanken [SQL Server], Replikationsleistung"
  - "Merge-Agent, Leistung"
  - "Momentaufnahmen [SQL Server-Replikation], Leistungsaspekte"
  - "Mergereplikationsleistung [SQL Server-Replikation]"
  - "Abonnements [SQL Server-Replikation], Leistungsaspekte"
  - "Leistung [SQL Server-Replikation], Mergereplikation"
  - "Agents [SQL Server-Replikation], Leistung"
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# Verbessern der Leistung der Mergereplikation
  Nach Berücksichtigung der allgemeinen Leistungstipps beschrieben [Enhancing General Replication Performance](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), berücksichtigen Sie diese zusätzlichen Bereiche für die Mergereplikation.  
  
## Datenbankentwurf  
  
-   Indizieren Sie Spalten, die in Zeilenfiltern und Joinfiltern verwendet werden.  
  
     Erstellen Sie beim Verwenden eines Zeilenfilters für einen veröffentlichten Artikel einen Index für jede Spalte, die in der WHERE-Klausel des Filters verwendet wird. Ohne Index [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Lesen, jede Zeile in der Tabelle, um zu bestimmen, ob die Zeile in der Partition aufgenommen werden soll. Mit einem Index kann [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hingegen schnell ermitteln, welche Zeilen aufzunehmen sind. Am schnellsten geht die Verarbeitung, wenn die Replikation die WHERE-Klausel des Filters vollständig allein aus dem Index auflösen kann.  
  
     Außerdem sollten auch alle Spalten indiziert werden, die in Joinfiltern verwendet werden. Bei jeder Ausführung des Merge-Agents durchsucht dieser die Basistabelle, um festzustellen, welche Zeilen in einer übergeordneten Tabelle und welche Zeilen in verknüpften Tabellen in eine Partition aufzunehmen sind. Durch Erstellen eines Indexes für die verknüpften Spalten wird verhindert, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] jede Zeile in der Tabelle bei jeder Ausführung des Merge-Agents lesen muss.  
  
     Weitere Informationen zu Filtern finden Sie unter [veröffentlichten Daten filtern, für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Überlegen Sie, ob Sie Tabellen, die LOB-Datentypen (Large Object) enthalten, übernormalisieren sollten.  
  
     Bei der Synchronisierung muss der Merge-Agent möglicherweise die gesamte Datenzeile von einem Verleger oder Abonnenten lesen und übertragen. Falls die Zeile Spalten enthält, die LOBs verwenden, kann dieser Vorgang eine zusätzliche Speicherbelegung erfordern und die Leistung beeinträchtigen, auch wenn diese Spalten gar nicht aktualisiert wurden. Um die Wahrscheinlichkeit einer solchen Leistungsbeeinträchtigung zu verringern, sollten Sie LOB-Spalten in einer separaten Tabelle mit einer 1:1-Beziehung zu den restlichen Zeilendaten speichern. Die Datentypen **Text**, **Ntext**, und **Image** sind veraltet. Falls Sie LOBs einschließen, wir empfehlen die Verwendung von Datentypen **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, bzw..  
  
## Veröffentlichungsentwurf  
  
-   Verwenden Sie einen Veröffentlichungskompatibilitätsgrad von 90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version).  
  
     Wenn eine andere Version von, einen oder mehrere Abonnenten verwenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], angeben, dass nur die Veröffentlichung unterstützen muss [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version. Auf diese Weise kommt die Veröffentlichung in den Genuss der neuen Funktionen und Leistungsoptimierungen.  
  
-   Verwenden Sie geeignete Einstellungen für die Beibehaltungsdauer der Veröffentlichung.  
  
     Die Beibehaltungsdauer der Veröffentlichung (also die Zeit, nach deren Ablauf das Abonnement wieder synchronisiert werden muss) bestimmt, wie lange die Nachverfolgungsmetadaten gespeichert werden. Ein hoher Wert kann sich negativ auf die Speicher- und Verarbeitungsleistung auswirken. Weitere Informationen zum Festlegen der Beibehaltungsdauer der Veröffentlichung finden Sie unter [Abonnementablauf und-Deaktivierung](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Verwenden Sie herunterladbare Artikel lediglich in Tabellen, die ausschließlich auf dem Verleger geändert werden. Weitere Informationen finden Sie unter [Merge Replikationsleistung mit Download-Only Artikeln optimieren](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
### Filterentwurf und -verwendung  
  
-   Gestalten Sie Zeilenfilterklauseln nicht zu komplex.  
  
     Je weniger komplex die Filterkriterien sind, desto höher ist die Leistung des Merge-Agents beim Auswerten von Zeilenänderungen, die an Abonnenten gesendet werden sollen. Vermeiden Sie untergeordnete SELECT-Anweisungen innerhalb von Mergezeilenfilter-Klauseln. Verwenden Sie stattdessen Joinfilter, die im Allgemeinen effizienter sind, wenn Daten in einer Tabelle auf der Basis der Zeilenfilterklausel in einer anderen Tabelle partitioniert werden sollen. Weitere Informationen zum Filtern finden Sie unter [veröffentlichten Daten filtern, für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Verwenden Sie vorausberechnete Partitionen mit parametrisierten Filtern (diese Funktion wird standardmäßig verwendet). Weitere Informationen finden Sie unter [parametrisierte Filter Leistung mit Vorausberechnete Partitionen optimieren](../../../relational-databases/replication/merge/optimize-parameterized-filter-performance-with-precomputed-partitions.md).  
  
     Vorausberechnete Partitionen setzen dem Filterverhalten bestimmte Grenzen. Wenn Ihre Anwendung mit diesen Grenzen nicht, legen Sie die **Keep_partition_changes** option **True**, stellt einen Leistungsvorteil bieten. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Verwenden Sie bei Daten, die zwar gefiltert, nicht aber von mehreren Benutzer genutzt werden sollen, Partitionen, die sich nicht überlappen.  
  
     Die Replikation kann die Leistung bei Daten optimieren, die sich nicht in mehreren Partitionen befinden bzw. an mehrere Abonnements gesendet werden. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Erstellen Sie keine komplexen Joinfilterhierarchien.  
  
     Joinfilter mit fünf oder mehr Tabellen können die Leistung der Mergeverarbeitung deutlich beeinträchtigen. Sie sollten daher bei der Generierung von Joinfiltern mit fünf oder mehr Tabellen andere Lösungen in Betracht ziehen:  
  
    -   Vermeiden Sie das Filtern von Tabellen, bei denen es sich in erster Linie um Nachschlagetabellen, kleinere Tabellen und Tabellen handelt, die nicht geändert werden. Nehmen Sie diese Tabellen vollständig in die Veröffentlichung auf. Joinfilter sollten nur zwischen Tabellen verwendet werden, die zwischen Abonnenten partitioniert werden müssen. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
    -   Überlegen Sie, ob es nicht möglich ist, den Datenbankentwurf zu denormalisieren oder eine Zuordnungstabelle zu verwenden, wenn ein Join viele Tabellen enthält. Wenn ein Vertriebsmitarbeiter z. B. nur die Daten für seine eigenen Kunden benötigt, für die Zuordnung eines Kunden zu einem Vertriebsmitarbeiter aber sechs Joins notwendig sind, können Sie der Kundentabelle eine Spalte hinzufügen, aus der der jeweilige Vertriebsmitarbeiter hervorgeht. Die Angaben zum Vertriebsmitarbeiter sind zwar redundant, der Aufwand der Denormalisierung der Tabellen wird aber möglicherweise durch die Leistungssteigerungen bei der Replikationspartitionierung wieder wettgemacht.  
  
    -   Entwerfen Sie Ihre Anwendung mit Sorgfalt, um die Leistung vorausberechneter Partitionen zu verbessern, wenn in Batches vieles Datenänderungen enthalten sind. Stellen Sie sicher, dass die Änderungen an der übergeordneten Tabelle in einem Joinfilter vor den entsprechenden Änderungen in den untergeordneten Tabellen vorgenommen werden.  
  
-   Legen Sie die **Join_unique_key** option **1** Logik zulässt.  
  
     Wenn dieser Parameter auf **1** Gibt an, dass die Beziehung zwischen den untergeordneten und übergeordneten Tabellen in einem joinfilter 1: 1 oder 1: n ist. Legen Sie diesen Parameter nur auf **1** Wenn Sie eine Einschränkung für die verknüpfte Spalte in der untergeordneten Tabelle verfügen, die die Eindeutigkeit sicherstellt. Wenn der Parameter, um festgelegt ist **1** falsch, mangelnder Konvergenz der Daten auftreten kann. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Vermeiden Sie bei Verwendung vorausberechneter Partitionen das Ausführen von Batches mit vielen Änderungen.  
  
     Wenn der Merge-Agent ausgeführt wird, nachdem Sie einen Batch mit vielen Datenänderungen ausführen, wird der große Batch vom Agent in kleinere Batches unterteilt. Während dieser Zeit werden andere Merge-Agent-Prozesse möglicherweise blockiert. Reduzieren Sie die Anzahl der Änderungen in einem Batch, und führen Sie den Merge-Agent zwischen Batches aus. Wenn dies möglich ist, erhöhen Sie den Wert der **Generation_leveling_threshold** für die Veröffentlichung.  
  
## Überlegungen zu Abonnements  
  
-   Staffeln Sie die Zeitpläne für die Synchronisierung der Abonnements.  
  
     Wenn viele Abonnenten eine Synchronisierung mit einem Verleger ausführen, sollten Sie die Zeitpläne so staffeln, dass die Merge-Agents zu unterschiedlichen Zeiten ausgeführt werden. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## Merge-Agentparameter  
 Informationen zu den Merge-Agent und dessen Parametern finden Sie unter [Replikationsmerge-Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
-   Aktualisieren Sie alle Abonnenten für Pullabonnements für [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version.  
  
     Beim Aktualisieren des Abonnenten, [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version aktualisiert der Merge-Agent von den Abonnements auf diesem Abonnenten verwendet. Dieser Merge-Agent von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder einer höheren Version ist erforderlich, um die neuen Funktionen und Leistungsoptimierungsmöglichkeiten nutzen zu können.  
  
-   Wenn ein Abonnement über eine schnelle Verbindung synchronisiert wird und Änderungen vom Verleger und Abonnenten gesendet werden, verwenden die **– ParallelUploadDownload** -Parameter für den Merge-Agent.  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] einen neuen Parameter für den Merge-Agent eingeführt: **– ParallelUploadDownload**. Wenn Sie diesen Parameter verwenden, kann der Merge-Agent gleichzeitig sowohl die Änderungen, die auf den Verleger hochgeladen werden, als auch die Änderungen verarbeiten, die auf den Abonnenten heruntergeladen werden. Dieses Verhalten erweist sich in Umgebungen mit hohem Volumen als nützlich, die eine hohe Netzwerkbandbreite besitzen. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Replikations-Agent-Befehlszeilenparameter & #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Ausführbare Konzepte für die Programmierung von Replikations-Agents](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Erhöhen Sie den Wert der **- MakeGenerationInterval** -Parameters, insbesondere wenn Synchronisierung mehr Uploads von Abonnenten als Downloads an Abonnenten beinhaltet.  
  
-   Beim Synchronisieren von Datenzeilen mit einer umfangreichen Datenmenge, z. B. Zeilen mit LOB-Spalten, kann die Websynchronisierung eine zusätzliche Speicherbelegung erfordern und die Leistung beeinträchtigen. Diese Situation tritt ein, wenn der Merge-Agent eine XML-Nachricht generiert, die zu viele Datenzeilen mit großen Datenmengen enthält. Wenn der Merge-Agent zu viele Ressourcen während der Websynchronisierung verbraucht, verringern Sie die in einer einzelnen Nachricht gesendete Anzahl der Zeilen mithilfe einer der folgenden Möglichkeiten:  
  
    -   Verwenden Sie für den Merge-Agent das Agentprofil für langsame Links. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Verringern Sie die **- DownloadGenerationsPerBatch** und **- UploadGenerationsPerBatch** Parameter für den Merge-Agent auf einen Wert von 10 oder weniger. Der Standardwert für diese Parameter beträgt 50.  
  
## Überlegungen zu Momentaufnahmen  
  
-   Erstellen Sie in großen Tabellen eine ROWGUIDCOL-Spalte, bevor Sie die Anfangsmomentaufnahme generieren.  
  
     Bei der Mergereplikation benötigt jede veröffentlichte Tabelle eine ROWGUIDCOL-Spalte. Falls keine ROWGUIDCOL-Spalte in der Tabelle enthalten ist, bevor der Momentaufnahme-Agent die Anfangsmomentaufnahmedateien erstellt, muss der Agent zunächst die ROWGUIDCOL-Spalte hinzufügen und auffüllen. Im Sinne einer Leistungssteigerung bei der Generierung von Momentaufnahmen während der Mergereplikation sollten Sie daher vor dem Veröffentlichen für jede Tabelle eine ROWGUIDCOL-Spalte erstellen. Die Spalte kann einen beliebigen Namen aufweisen (**Rowguid** vom Snapshot-Agent wird standardmäßig verwendet), aber Sie müssen die folgenden Datentypmerkmale besitzen:  
  
    -   Der Datentyp muss UNIQUEIDENTIFIER sein.  
  
    -   Der Standardwert muss NEWSEQUENTIALID() oder NEWID() lauten. NEWSEQUENTIALID() ermöglicht eine höhere Leistung beim Ausführen und Nachverfolgen von Änderungen und wird daher empfohlen.  
  
    -   Die ROWGUIDCOL-Eigenschaft muss festgelegt werden.  
  
    -   Die Spalte muss über einen eindeutigen Index verfügen.  
  
-   Generieren Sie vorab Momentaufnahmen, und/oder ermöglichen Sie es den Abonnenten, beim ersten Synchronisieren die Momentaufnahmegenerierung und -anwendung anzufordern.  
  
     Verwenden Sie eine oder beide dieser Optionen, um Momentaufnahmen für Veröffentlichungen bereitzustellen, die parametrisierte Filter verwenden. Wenn Sie keine dieser beiden Optionen angeben, werden die Abonnements mit einer Reihe von SELECT- und INSERT-Anweisungen statt mit dem **bcp** -Hilfsprogramm initialisiert, wodurch sich der Prozess deutlich verlangsamt. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## Überlegungen zur Wartung und Überwachung  
  
-   Indizieren Sie die Systemtabellen für die Mergereplikation von Zeit zu Zeit neu.  
  
     Im Rahmen der Wartung für die Mergereplikation, überprüfen Sie gelegentlich die Vergrößerung der Systemtabellen Mergereplikation zugeordnet: **MSmerge_contents**, **MSmerge_genhistory**, und **MSmerge_tombstone**, **MSmerge_current_partition_mappings**, und **MSmerge_past_partition_mappings**. Führen Sie eine regelmäßige Neuindizierung dieser Tabellen durch. Weitere Informationen finden Sie unter [neu organisieren und Indizes neu erstellen](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Überwachen Sie Synchronisierung Leistung mit den **Synchronisierungsverlauf** Registerkarte im Replikationsmonitor.  
  
     Bei der Mergereplikation zeigt der Replikationsmonitor detaillierte Statistiken in der **Synchronisierungsverlauf** Registerkarte für jeden Artikel, die während der Synchronisierung, einschließlich der Zeit verarbeiteten in jeder Verarbeitungsphase (Hochladen von Änderungen, Herunterladen von Änderungen usw.) verbracht. Auf diese Weise können Sie besser die Tabellen identifizieren, die zu einer Verlangsamung führen, und Sie können hier auch hervorragend Leistungsprobleme im Zusammenhang mit Mergeabonnements diagnostizieren. Weitere Informationen zum Anzeigen detaillierter Statistiken finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
  