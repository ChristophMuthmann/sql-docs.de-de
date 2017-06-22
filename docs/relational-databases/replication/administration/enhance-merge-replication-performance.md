---
title: Verbessern der Leistung der Mergereplikation | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd62d43d9f77f0baf63487c15381e07814eea63d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="enhance-merge-replication-performance"></a>Verbessern der Leistung der Mergereplikation
  Im Anschluss an die in [Verbessern der allgemeinen Replikationsleistung](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)beschriebenen Überlegungen zur allgemeinen Leistung sollten Sie sich Gedanken über die im Folgenden beschriebenen zusätzlichen Aspekte im Zusammenhang mit einer Mergereplikation machen.  
  
## <a name="database-design"></a>Datenbankentwurf  
  
-   Indizieren Sie Spalten, die in Zeilenfiltern und Joinfiltern verwendet werden.  
  
     Erstellen Sie beim Verwenden eines Zeilenfilters für einen veröffentlichten Artikel einen Index für jede Spalte, die in der WHERE-Klausel des Filters verwendet wird. Ohne einen solchen Index muss [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] jede einzelne Zeile in der Tabelle lesen, um zu bestimmen, ob die Zeile in die Partition aufgenommen werden soll oder nicht. Mit einem Index kann [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hingegen schnell ermitteln, welche Zeilen aufzunehmen sind. Am schnellsten geht die Verarbeitung, wenn die Replikation die WHERE-Klausel des Filters vollständig allein aus dem Index auflösen kann.  
  
     Außerdem sollten auch alle Spalten indiziert werden, die in Joinfiltern verwendet werden. Bei jeder Ausführung des Merge-Agents durchsucht dieser die Basistabelle, um festzustellen, welche Zeilen in einer übergeordneten Tabelle und welche Zeilen in verknüpften Tabellen in eine Partition aufzunehmen sind. Durch Erstellen eines Indexes für die verknüpften Spalten wird verhindert, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] jede Zeile in der Tabelle bei jeder Ausführung des Merge-Agents lesen muss.  
  
     Weitere Informationen zur Filterung finden Sie unter [Filtern von veröffentlichten Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Überlegen Sie, ob Sie Tabellen, die LOB-Datentypen (Large Object) enthalten, übernormalisieren sollten.  
  
     Bei der Synchronisierung muss der Merge-Agent möglicherweise die gesamte Datenzeile von einem Verleger oder Abonnenten lesen und übertragen. Falls die Zeile Spalten enthält, die LOBs verwenden, kann dieser Vorgang eine zusätzliche Speicherbelegung erfordern und die Leistung beeinträchtigen, auch wenn diese Spalten gar nicht aktualisiert wurden. Um die Wahrscheinlichkeit einer solchen Leistungsbeeinträchtigung zu verringern, sollten Sie LOB-Spalten in einer separaten Tabelle mit einer 1:1-Beziehung zu den restlichen Zeilendaten speichern. Die Datentypen **text**, **ntext**und **image** sind als veraltet markiert. Wenn Sie LOBs verwenden, sollten Sie auf die Datentypen **varchar(max)**, **nvarchar(max)**und **varbinary(max)**zurückgreifen.  
  
## <a name="publication-design"></a>Veröffentlichungsentwurf  
  
-   Verwenden Sie einen Veröffentlichungskompatibilitätsgrad von 90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version).  
  
     Sofern nicht mindestens ein Abonnent eine andere Version als [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet, geben Sie an, dass die Veröffentlichung nur [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version unterstützen muss. Auf diese Weise kommt die Veröffentlichung in den Genuss der neuen Funktionen und Leistungsoptimierungen.  
  
-   Verwenden Sie geeignete Einstellungen für die Beibehaltungsdauer der Veröffentlichung.  
  
     Die Beibehaltungsdauer der Veröffentlichung (also die Zeit, nach deren Ablauf das Abonnement wieder synchronisiert werden muss) bestimmt, wie lange die Nachverfolgungsmetadaten gespeichert werden. Ein hoher Wert kann sich negativ auf die Speicher- und Verarbeitungsleistung auswirken. Weitere Informationen zum Festlegen der Beibehaltungsdauer der Veröffentlichung finden Sie unter [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Verwenden Sie herunterladbare Artikel lediglich in Tabellen, die ausschließlich auf dem Verleger geändert werden. Weitere Informationen finden Sie unter [Optimieren der Leistung der Mergereplikation durch nur herunterladbare Artikel](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
### <a name="filter-design-and-use"></a>Filterentwurf und -verwendung  
  
-   Gestalten Sie Zeilenfilterklauseln nicht zu komplex.  
  
     Je weniger komplex die Filterkriterien sind, desto höher ist die Leistung des Merge-Agents beim Auswerten von Zeilenänderungen, die an Abonnenten gesendet werden sollen. Vermeiden Sie untergeordnete SELECT-Anweisungen innerhalb von Mergezeilenfilter-Klauseln. Verwenden Sie stattdessen Joinfilter, die im Allgemeinen effizienter sind, wenn Daten in einer Tabelle auf der Basis der Zeilenfilterklausel in einer anderen Tabelle partitioniert werden sollen. Weitere Informationen zur Filterung finden Sie unter [Filtern von veröffentlichten Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Verwenden Sie vorausberechnete Partitionen mit parametrisierten Filtern (diese Funktion wird standardmäßig verwendet). Weitere Informationen finden Sie unter [Optimieren Parametrisierter Filter-Leistung mit Vorausberechneten Partitionen ](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
     Vorausberechnete Partitionen setzen dem Filterverhalten bestimmte Grenzen. Wenn Ihre Anwendung mit diesen Grenzen nicht zurecht kommt, legen Sie für die **keep_partition_changes** -Option **True**fest. Dies führt zu einer Leistungssteigerung. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Verwenden Sie bei Daten, die zwar gefiltert, nicht aber von mehreren Benutzer genutzt werden sollen, Partitionen, die sich nicht überlappen.  
  
     Die Replikation kann die Leistung bei Daten optimieren, die sich nicht in mehreren Partitionen befinden bzw. an mehrere Abonnements gesendet werden. Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Erstellen Sie keine komplexen Joinfilterhierarchien.  
  
     Joinfilter mit fünf oder mehr Tabellen können die Leistung der Mergeverarbeitung deutlich beeinträchtigen. Sie sollten daher bei der Generierung von Joinfiltern mit fünf oder mehr Tabellen andere Lösungen in Betracht ziehen:  
  
    -   Vermeiden Sie das Filtern von Tabellen, bei denen es sich in erster Linie um Nachschlagetabellen, kleinere Tabellen und Tabellen handelt, die nicht geändert werden. Nehmen Sie diese Tabellen vollständig in die Veröffentlichung auf. Joinfilter sollten nur zwischen Tabellen verwendet werden, die zwischen Abonnenten partitioniert werden müssen. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
    -   Überlegen Sie, ob es nicht möglich ist, den Datenbankentwurf zu denormalisieren oder eine Zuordnungstabelle zu verwenden, wenn ein Join viele Tabellen enthält. Wenn ein Vertriebsmitarbeiter z. B. nur die Daten für seine eigenen Kunden benötigt, für die Zuordnung eines Kunden zu einem Vertriebsmitarbeiter aber sechs Joins notwendig sind, können Sie der Kundentabelle eine Spalte hinzufügen, aus der der jeweilige Vertriebsmitarbeiter hervorgeht. Die Angaben zum Vertriebsmitarbeiter sind zwar redundant, der Aufwand der Denormalisierung der Tabellen wird aber möglicherweise durch die Leistungssteigerungen bei der Replikationspartitionierung wieder wettgemacht.  
  
    -   Entwerfen Sie Ihre Anwendung mit Sorgfalt, um die Leistung vorausberechneter Partitionen zu verbessern, wenn in Batches vieles Datenänderungen enthalten sind. Stellen Sie sicher, dass die Änderungen an der übergeordneten Tabelle in einem Joinfilter vor den entsprechenden Änderungen in den untergeordneten Tabellen vorgenommen werden.  
  
-   Legen Sie, wenn es die Logik zulässt, für die **join_unique_key** -Option **1** fest.  
  
     Mit dem Wert **1** geben Sie an, dass die Beziehung zwischen der untergeordneten und der übergeordneten Tabelle in einem Joinfilter 1:1 oder 1:n ist. Legen Sie für diesen Parameter aber nur dann **1** fest, wenn die verknüpfte Spalte in der untergeordneten Tabelle eine Einschränkung besitzt, die die Eindeutigkeit sicherstellt. Wenn für den Parameter fälschlicherweise **1** festgelegt wird, kann es zu einer Nichtkonvergenz der Daten kommen. Weitere Informationen finden Sie unter [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Vermeiden Sie bei Verwendung vorausberechneter Partitionen das Ausführen von Batches mit vielen Änderungen.  
  
     Wenn der Merge-Agent ausgeführt wird, nachdem Sie einen Batch mit vielen Datenänderungen ausführen, wird der große Batch vom Agent in kleinere Batches unterteilt. Während dieser Zeit werden andere Merge-Agent-Prozesse möglicherweise blockiert. Reduzieren Sie die Anzahl der Änderungen in einem Batch, und führen Sie den Merge-Agent zwischen Batches aus. Wenn dies nicht möglich ist, erhöhen Sie den Wert von **generation_leveling_threshold** für die Veröffentlichung.  
  
## <a name="subscription-considerations"></a>Überlegungen zu Abonnements  
  
-   Staffeln Sie die Zeitpläne für die Synchronisierung der Abonnements.  
  
     Wenn viele Abonnenten eine Synchronisierung mit einem Verleger ausführen, sollten Sie die Zeitpläne so staffeln, dass die Merge-Agents zu unterschiedlichen Zeiten ausgeführt werden. Weitere Informationen finden Sie unter [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## <a name="merge-agent-parameters"></a>Merge-Agentparameter  
 Informationen zum Merge-Agent und seinen Parametern finden Sie unter [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
-   Aktualisieren Sie alle Abonnenten für Pullabonnements auf [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version.  
  
     Beim Aktualisieren des Abonnenten auf [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder eine höhere Version wird auch der Merge-Agent aktualisiert, der von den Abonnements auf diesem Abonnenten verwendet wird. Dieser Merge-Agent von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder einer höheren Version ist erforderlich, um die neuen Funktionen und Leistungsoptimierungsmöglichkeiten nutzen zu können.  
  
-   Wenn ein Abonnement über eine schnelle Verbindung synchronisiert wird und vom Verleger und vom Abonnenten Änderungen gesendet werden, verwenden Sie für den Merge-Agent den **–ParallelUploadDownload** -Parameter.  
  
     In[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurde ein neuer Parameter für den Merge-Agent eingeführt: **–ParallelUploadDownload**. Wenn Sie diesen Parameter verwenden, kann der Merge-Agent gleichzeitig sowohl die Änderungen, die auf den Verleger hochgeladen werden, als auch die Änderungen verarbeiten, die auf den Abonnenten heruntergeladen werden. Dieses Verhalten erweist sich in Umgebungen mit hohem Volumen als nützlich, die eine hohe Netzwerkbandbreite besitzen. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Befehlszeilenparametern des Replikations-Agents &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Ausführbare Konzepte für die Programmierung von Replikations-Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Möglicherweise ist es ratsam, den Wert des **-MakeGenerationInterval** -Parameters zu erhöhen, insbesondere dann, wenn die Synchronisierung mehr Uploads von Abonnenten als Downloads an Abonnenten beinhaltet.  
  
-   Beim Synchronisieren von Datenzeilen mit einer umfangreichen Datenmenge, z. B. Zeilen mit LOB-Spalten, kann die Websynchronisierung eine zusätzliche Speicherbelegung erfordern und die Leistung beeinträchtigen. Diese Situation tritt ein, wenn der Merge-Agent eine XML-Nachricht generiert, die zu viele Datenzeilen mit großen Datenmengen enthält. Wenn der Merge-Agent zu viele Ressourcen während der Websynchronisierung verbraucht, verringern Sie die in einer einzelnen Nachricht gesendete Anzahl der Zeilen mithilfe einer der folgenden Möglichkeiten:  
  
    -   Verwenden Sie für den Merge-Agent das Agentprofil für langsame Links. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Verringern Sie die **- DownloadGenerationsPerBatch** - und **- UploadGenerationsPerBatch** -Parameter für den Merge-Agent auf einen Wert von 10 oder weniger. Der Standardwert für diese Parameter beträgt 50.  
  
## <a name="snapshot-considerations"></a>Überlegungen zu Momentaufnahmen  
  
-   Erstellen Sie in großen Tabellen eine ROWGUIDCOL-Spalte, bevor Sie die Anfangsmomentaufnahme generieren.  
  
     Bei der Mergereplikation benötigt jede veröffentlichte Tabelle eine ROWGUIDCOL-Spalte. Falls keine ROWGUIDCOL-Spalte in der Tabelle enthalten ist, bevor der Momentaufnahme-Agent die Anfangsmomentaufnahmedateien erstellt, muss der Agent zunächst die ROWGUIDCOL-Spalte hinzufügen und auffüllen. Im Sinne einer Leistungssteigerung bei der Generierung von Momentaufnahmen während der Mergereplikation sollten Sie daher vor dem Veröffentlichen für jede Tabelle eine ROWGUIDCOL-Spalte erstellen. Die Spalte kann einen beliebigen Namen aufweisen (der Momentaufnahme-Agent verwendet standardmäßig**rowguid** ), muss jedoch die folgenden Datentypmerkmale besitzen:  
  
    -   Der Datentyp muss UNIQUEIDENTIFIER sein.  
  
    -   Der Standardwert muss NEWSEQUENTIALID() oder NEWID() lauten. NEWSEQUENTIALID() ermöglicht eine höhere Leistung beim Ausführen und Nachverfolgen von Änderungen und wird daher empfohlen.  
  
    -   Die ROWGUIDCOL-Eigenschaft muss festgelegt werden.  
  
    -   Die Spalte muss über einen eindeutigen Index verfügen.  
  
-   Generieren Sie vorab Momentaufnahmen, und/oder ermöglichen Sie es den Abonnenten, beim ersten Synchronisieren die Momentaufnahmegenerierung und -anwendung anzufordern.  
  
     Verwenden Sie eine oder beide dieser Optionen, um Momentaufnahmen für Veröffentlichungen bereitzustellen, die parametrisierte Filter verwenden. Wenn Sie keine dieser beiden Optionen angeben, werden die Abonnements mit einer Reihe von SELECT- und INSERT-Anweisungen statt mit dem **bcp** -Hilfsprogramm initialisiert, wodurch sich der Prozess deutlich verlangsamt. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="maintenance-and-monitoring-considerations"></a>Überlegungen zur Wartung und Überwachung  
  
-   Indizieren Sie die Systemtabellen für die Mergereplikation von Zeit zu Zeit neu.  
  
     Als Teil der Wartung für die Mergereplikation überprüfen Sie gelegentlich die Vergrößerung der Systemtabellen, die mit der Mergereplikation verbunden sind: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings**und **MSmerge_past_partition_mappings**. Führen Sie eine regelmäßige Neuindizierung dieser Tabellen durch. Weitere Informationen finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Überwachen Sie mithilfe der Registerkarte **Synchronisierungsverlauf** im Replikationsmonitor die Synchronisierungsleistung.  
  
     Bei Mergereplikationen zeigt der Replikationsmonitor auf der Registerkarte **Synchronisierungsverlauf** detaillierte Statistiken für alle Artikel an, die während einer Synchronisierung verarbeitet werden. So lässt sich diesen Statistiken z. B. die Länge der einzelnen Verarbeitungsphasen (Hochladen von Änderungen, Herunterladen von Änderungen usw.) entnehmen. Auf diese Weise können Sie besser die Tabellen identifizieren, die zu einer Verlangsamung führen, und Sie können hier auch hervorragend Leistungsprobleme im Zusammenhang mit Mergeabonnements diagnostizieren. Weitere Informationen zum Anzeigen detaillierter Statistiken finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die einem Abonnement zugeordneten Agents &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
  
