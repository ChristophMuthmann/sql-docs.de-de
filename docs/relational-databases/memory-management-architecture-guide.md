---
title: "Handbuch zur Architektur der Speicherverwaltung | Microsoft Docs"
ms.custom: ""
ms.date: "10/21/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Handbuch, Architektur der Speicherverwaltung"
  - "Handbuch zur Architektur der Speicherverwaltung"
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
caps.latest.revision: 6
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 6
---
# Handbuch zur Architektur der Speicherverwaltung
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

## <a name="memory-architecture"></a>Arbeitsspeicherarchitektur

In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird Arbeitsspeicher nach Bedarf dynamisch reserviert und freigegeben. Die Angabe des Arbeitsspeicherumfangs durch den Administrator, der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zugeordnet werden soll, ist in der Regel nicht erforderlich, obwohl die Möglichkeit weiterhin besteht und in einigen Umgebungen erforderlich ist.

Eines der vorrangigen Ziele beim Entwurf jeder Datenbanksoftware ist die Minimierung der Datenträger-E/A, da Lese- und Schreibvorgänge auf dem Datenträger zu den ressourcenintensivsten Vorgängen zählen. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erstellt einen Pufferpool im Arbeitsspeicher, um Seiten aufzunehmen, die aus der Datenbank gelesen werden. Ein großer Teil des Codes in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dient dazu, die Anzahl von physischen Lese- und Schreibvorgängen zwischen dem Datenträger und dem Pufferpool zu minimieren. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] versucht, ein Gleichgewicht zwischen den beiden folgenden Zielen herzustellen:

* Verhindern, dass der Pufferpool so groß wird, dass im gesamten System nicht genügend Arbeitsspeicher verfügbar ist.
* Minimieren physischer E/A-Vorgänge in den Datenbankdateien durch Maximieren der Größe des Pufferpools.


> [!NOTE]
> Bei einem stark ausgelasteten System können umfangreiche Abfragen, die zum Ausführen sehr viel Arbeitsspeicher erfordern, nicht immer die Mindestmenge des angeforderten Arbeitsspeichers erhalten. Während auf die Arbeitsspeicherressourcen gewartet wird, wird deshalb ein Timeoutfehler erzeugt. Zur Behebung dieses Problems sollten Sie den Wert für die Option [Abfragewartezeit](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md) erhöhen. Für eine parallele Abfrage können Sie den Wert für die Option [Max. Grad an Parallelität](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) reduzieren.
 
> [!NOTE]
> Bei einem stark ausgelasteten System mit ungenügendem Arbeitsspeicher können Abfragen mit Zusammenführungsjoin, Sortierung und Bitmap im Abfrageplan zum Löschen der Bitmap führen, wenn für die Abfragen nicht der für die Bitmap erforderliche minimale Arbeitsspeicher verfügbar ist. Dies kann die Abfrageleistung beeinträchtigen. Wenn zudem der Sortierprozess nicht genügend Arbeitsspeicher erhält, kann dies zu einer erhöhten Verwendung von Arbeitstabellen in der tempdb-Datenbank führen, was ein Anwachsen der tempdb-Datenbank bewirkt. Um dieses Problem zu lösen, müssen Sie physischen Arbeitsspeicher hinzufügen oder die Abfragen so optimieren, dass Sie einen anderen und schnelleren Abfrageplan verwenden.
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversiontokenssnoversionmdmd"></a>Bereitstellen der maximalen Menge von Arbeitsspeicher für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Mithilfe von AWE und der Berechtigung „Locked Pages in Memory“ können Sie für das [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbankmodul die folgenden Mengen von Arbeitsspeicher bereitstellen. (Die folgende Tabelle enthält eine Spalte für 32-Bit-Versionen, die nicht mehr verfügbar sind.)

| |32-Bit <sup>1</sup> |64-Bit
|-------|-------|-------| 
|Konventioneller Arbeitsspeicher |Alle Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Bis zu der für den virtuellen Prozessadressraum geltenden Beschränkung: <br>– 2 GB<br>– 3 GB mit Startparameter „/3gb“ <sup>2</sup> <br>– 4 GB unter WOW64 <sup>3</sup> |Alle Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Bis zu der für den virtuellen Prozessadressraum geltenden Beschränkung: <br>– 7 TB mit IA64-Architektur (IA64 wird in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] und höher nicht unterstützt)<br>– Maximum des Betriebssystems mit X64 Architektur <sup>4</sup>
|AWE-Mechanismus (Ermöglicht [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], auf 32-Bit-Plattformen über die Beschränkung für den virtuellen Prozessadressraum hinauszugehen.) |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard, Enterprise und Developer Edition: Pufferpool kann auf bis zu 64 GB Arbeitsspeicher zugreifen.|Nicht zutreffend <sup>5</sup> |
|Betriebssystemberechtigung „Lock Pages in Memory“ (Ermöglicht das Sperren des physischen Speichers, sodass das Betriebssystem keine Seiten des gesperrten Arbeitsspeichers auslagern kann.) <sup>6</sup> |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard, Enterprise und Developer Edition: Erforderlich, damit der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Prozess den AWE-Mechanismus verwenden kann. Über den AWE-Mechanismus zugeordneter Speicher kann nicht ausgelagert werden. <br> Wird dieses Privileg erteilt, ohne dass AWE aktiviert ist, hat dies keine Auswirkungen auf den Server. |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition und Developer Edition: Empfohlen, um Seitenauslagerungen durch das Betriebssystem zu vermeiden. Kann je nach Arbeitsauslastung einen Leistungsvorteil ergeben. Die Menge des Arbeitsspeichers, auf den zugegriffen werden kann, ist vergleichbar mit dem konventionellen Arbeitsspeicher. |

<sup>1</sup> Ab [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] sind 32-Bit-Versionen nicht verfügbar.  
<sup>2</sup> „/3gb“ ist ein Startparameter des Betriebssystems. Weitere Informationen finden Sie in der MSDN Library.  
<sup>3</sup> WOW64 (Windows on Windows 64) ist ein Modus, in dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (32-Bit) unter einem 64-Bit-Betriebssystem ausgeführt wird.  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition unterstützt bis zu 128 GB. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition unterstützt das Maximum des Betriebssystems.  
<sup>5</sup> Beachten Sie, dass die Option „sp_configure awe enabled“ in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (64-Bit) vorhanden ist, jedoch ignoriert wird.    
<sup>6</sup> Wenn die Berechtigung „Lock Pages in Memory (LPIM)“ erteilt wird (entweder für 32-Bit zur Unterstützung von AWE oder für 64-Bit als eigenständige Option), wird empfohlen, auch die Option „Max. Serverarbeitsspeicher“ festzulegen.

> [!NOTE]
> Ältere Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] können unter einem 32-Bit-Betriebssystem ausgeführt. Für den Zugriff auf mehr als 4 GB Arbeitsspeicher auf einem 32-Bit-Betriebssystem ist Address Windowing Extensions (AWE) erforderlich, um den Speicher zu verwalten. Dies ist nicht erforderlich, wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] unter 64-Bit-Betriebssystemen ausgeführt wird. Weitere Informationen zu AWE finden Sie unter [Prozessadressraum](https://msdn.microsoft.com/library/ms189334) und [Verwalten von Arbeitsspeicher für große Datenbanken](https://msdn.microsoft.com/library/ms191481) in der Dokumentation zu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2008.   


## <a name="dynamic-memory-management"></a>Dynamische Arbeitsspeicherverwaltung

Die Arbeitsspeicherverwaltung des Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbankmoduls ruft standardmäßig so viel Arbeitsspeicher wie nötig ab, ohne dass es dabei zu einem Speicherengpass im System kommt. Das Datenbankmodul verwendet dazu die für Arbeitsspeicherbenachrichtigungen verfügbaren APIs in Microsoft Windows.

Der virtuelle Adressraum von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann in zwei verschiedene Bereiche unterteilt werden: den von Pufferpool verwendeten Bereich und den Rest. Wenn der AWE-Mechanismus aktiviert ist, kann der Pufferpool in dem AWE zugeordneten Arbeitsspeicherbereich liegen. Auf diese Weise steht zusätzlicher Arbeitsspeicher für Datenbankseiten zur Verfügung. 

Der Pufferpool ist eine primäre Speicherbelegungsquelle von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Externe Komponenten im [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Prozess, z. B. COM-Objekte, die nicht die Möglichkeiten der Arbeitsspeicherverwaltung von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nutzen, verwenden Arbeitsspeicher außerhalb des vom Pufferpool reservierten virtuellen Adressraum.

Beim Starten berechnet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Größe des virtuellen Adressraumes für den Pufferpool auf Grundlage verschiedener Parameter, z. B. der Größe des physischen Arbeitsspeichers des Systems, der Anzahl der Serverthreads und verschiedener Startparameter. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserviert die berechnete Größe des virtuellen Adressraumes für den Pufferpool, verwendet jedoch nur die für die aktuelle Last erforderliche Größe an physischem Arbeitsspeicher.

Die Instanz greift dann je nach Arbeitsauslastung auf weiteren Arbeitsspeicher zu. Wenn weitere Benutzer eine Verbindung herstellen und Abfragen ausführen, ruft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dem Bedarf entsprechend zusätzlichen physischen Arbeitsspeicher ab. Eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz ordnet so lange zusätzlichen physischen Arbeitsspeicher zu, bis entweder die Zielvorgabe „Max. Serverarbeitsspeicher“ erreicht ist oder Windows anzeigt, dass kein weiterer freier Arbeitsspeicher zur Verfügung steht. Die Instanz gibt Arbeitsspeicher frei, wenn die Einstellung für „Min. Serverarbeitsspeicher“ überschritten wird oder Windows anzeigt, dass zu wenig freier Arbeitsspeicher vorhanden ist.

Sobald weitere Anwendungen auf einem Computer gestartet werden, auf dem eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ausgeführt wird, benötigen sie Arbeitsspeicher, sodass der Umfang des freien physischen Arbeitsspeichers auf einen Wert unter dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Ziel fällt. Die Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] passt ihren Arbeitsspeicherverbrauch an. Wenn eine andere Anwendung beendet wird und mehr Arbeitsspeicher verfügbar wird, vergrößert die Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Speicherbelegung. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann mehrere MB Arbeitsspeicher pro Sekunde freigeben und reservieren, um schnell auf Änderungen der Speicherbelegung zu reagieren.


## <a name="effects-of-min-and-max-server-memory"></a>Auswirkungen der Konfigurationsoptionen Min. Serverarbeitsspeicher und Max. Serverarbeitsspeicher

Durch die Konfigurationsoptionen „Min. Serverarbeitsspeicher“ und „Max. Serverarbeitsspeicher“ werden die obere und untere Grenze für den Umfang des Speichers festgelegt, der vom Pufferpool des Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbankmoduls verwendet wird. Der Pufferpool reserviert nicht sofort die Menge an Speicher, die durch „Min. Serverarbeitsspeicher“ angegeben wurde. Der Pufferpool reserviert zuerst nur so viel Speicher, wie für die Initialisierung erforderlich ist. Mit ansteigender Arbeitsauslastung des Datenbankmoduls wird weiterer Speicher reserviert, um die Arbeitsauslastung zu unterstützen. Der Pufferpool gibt erst dann einen Teil des reservierten Speichers wieder frei, wenn der unter „Min. Serverarbeitsspeicher“ angegebene Wert erreicht wurde. Sobald „Min. Serverarbeitsspeicher“ erreicht ist, verwendet der Pufferpool den Standardalgorithmus, um Speicher nach Bedarf zu reservieren und freizugeben. Der einzige Unterschied besteht darin, dass der Pufferpool bei der Speicherbelegung nie unter die Ebene absinkt, die durch „Min. Serverarbeitsspeicher“ angegeben ist, und nie mehr Speicher reserviert, als durch die unter „Max. Serverarbeitsspeicher“ angegebene Ebene angegeben ist.

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserviert als Prozess mehr Speicher als durch die Option „Max. Serverarbeitsspeicher“ angegeben wird. Sowohl interne als auch externe Komponenten können Speicher außerhalb des Pufferpools belegen; dies führt zur Beanspruchung zusätzlicher Speicherkapazitäten, der dem Pufferpool zugeordnete Speicher stellt jedoch normalerweise den größten Teil des von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] belegten Speichers dar.


Der Umfang des vom Datenbankmodul reservierten Speichers hängt ausschließlich von der Arbeitsauslastung der jeweiligen Instanz ab. Eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz, die nur wenige Anforderungen verarbeitet, wird den Wert von „Min. Serverarbeitsspeicher“ möglicherweise nie erreichen.

Wenn für „Min. Serverarbeitsspeicher“ und „Max. Serverarbeitsspeicher“ derselbe Wert angegeben wurde, beendet das Datenbankmodul die dynamische Freigabe und Zuordnung von Speicher für den Pufferpool, sobald der dem Datenbankmodul zugeordnete Speicher diesen Wert erreicht hat.

Wenn eine Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf einem Computer ausgeführt wird, auf dem häufig andere Anwendungen gestartet oder beendet werden, kann das Starten anderer Anwendungen durch die Belegung und Freigabe von Speicher, die durch die Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vorgenommen wird, verlangsamt werden. Wenn [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eine von mehreren Serveranwendungen ist, die auf einem einzelnen Computer ausgeführt werden, kann es darüber hinaus erforderlich sein, dass der Umfang des [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zugeordneten Speichers von Systemadministratoren gesteuert wird. In solchen Fällen können Sie mithilfe der Optionen „Min. Serverarbeitsspeicher“ und „Max. Serverarbeitsspeicher“ steuern, wie viel Speicher von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet werden kann. Weitere Informationen finden Sie unter [Konfigurationsoptionen für den Serverarbeitsspeicher](../database-engine/configure-windows/server-memory-server-configuration-options.md).

Die Optionen „Min. Serverarbeitsspeicher“ und „Max. Serverarbeitsspeicher“ werden in Megabytes angegeben.

## <a name="memory-used-by-includessnoversiontokenssnoversionmdmd-objects-specifications"></a>Spezifikationen für den von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Objekten verwendeten Arbeitsspeicher

In der folgenden Liste werden die Richtwerte für den Arbeitsspeicher beschrieben, den die einzelnen Objekte in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] belegen. Die aufgeführten Angaben sind Schätzwerte und können je nach Umgebung und Erstellung der Objekte variieren.

* Sperre: 64 Bytes + 32 Bytes pro Besitzer   
* Benutzerverbindung: Etwa (3* *Netzwerkpaketgröße + 94 KB)    

Die Netzwerkpaketgröße entspricht der Größe der TDS-Pakete (Tabular Data Stream), die für die Kommunikation zwischen Anwendungen und dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbankmodul verwendet werden. Die Standardpaketgröße beträgt 4 KB und wird durch die Konfigurationsoption Netzwerkpaketgröße gesteuert.

Wenn mehrere aktive Resultsets (Multiple Active Result Sets, MARS) aktiviert sind, benötigt die Benutzerverbindung ca. (3 + 3 * numerische_logische_Verbindungen) * Netzwerkpaketgröße + 94 KB.

## <a name="buffer-management"></a>Pufferverwaltung

Der Hauptzweck einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Datenbank ist das Speichern und Abrufen von Daten. Daher stellt eine hohe Ein-/Ausgabe auf dem Datenträger ein Hauptmerkmal des Datenbankmoduls dar. Datenträger-E/A-Vorgänge beanspruchen viele Ressourcen und benötigen relativ viel Zeit für die Ausführung. Daher ist [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] so konzipiert, dass E/A-Vorgänge möglichst effizient gestaltet werden. Die Pufferverwaltung ist eine zentrale Komponente zum Erreichen dieser Effizienz. Die Pufferverwaltungskomponente weist zwei Mechanismen auf: den Puffer-Manager, mit dem auf Datenbankseiten zugegriffen wird und mit dem sie aktualisiert werden, und den Puffercache (auch als Pufferpool bezeichnet), mit dem Datenbankdatei-E/A-Vorgänge reduziert werden. 

### <a name="how-buffer-management-works"></a>Funktionsweise der Pufferverwaltung

Ein Puffer ist eine 8-KB-Seite im Arbeitsspeicher. Dies entspricht der Größe einer Datenseite oder Indexseite. Der Puffercache ist ebenfalls in Seiten von je 8 KB unterteilt. Mit dem Puffer-Manager werden die Funktionen verwaltet, mit denen Daten- oder Indexseiten aus Datenbankdatenträgerdateien in den Puffercache geladen und geänderte Seiten zurück auf den Datenträger geschrieben werden. Eine Seite verbleibt im Puffercache, bis der Pufferbereich vom Puffer-Manager zum Laden weiterer Daten benötigt wird. Daten werden nur dann zurück auf den Datenträger geschrieben, wenn sie geändert wurden. Daten im Puffercache können mehrfach geändert werden, bevor sie zurück auf den Datenträger geschrieben werden. Weitere Informationen finden Sie unter [Lesen von Seiten](../relational-databases/reading-pages.md) und [Schreiben von Seiten](../relational-databases/writing-pages.md).

Beim Starten berechnet [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die Größe des virtuellen Adressraums für den Puffercache auf Grundlage verschiedener Parameter, z.B. der Größe des physischen Arbeitsspeichers des Systems, der konfigurierten Anzahl maximaler Serverthreads und verschiedener Startparameter. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserviert die berechnete Größe des virtuellen Adressraums (das Arbeitsspeicherziel) für den Puffercache, verwendet jedoch nur die für die aktuelle Last erforderliche Größe an physischem Arbeitsspeicher. Sie können die Spalten **bpool_commit_target** und **bpool_committed** in der Katalogsicht [der sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) abfragen, um die Anzahl der als Arbeitsspeicherziel reservierten Seiten bzw. die Anzahl der Seiten zurückzugeben, für die im Puffercache ein Commit ausgeführt wird.

Das Intervall zwischen dem Start von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und dem Zeitpunkt, wenn der Puffercache sein Arbeitsspeicherziel erreicht hat, wird als Anlaufprozess bezeichnet. In dieser Zeit wird der Puffer mit den erforderlichen Leseanforderungen gefüllt. Durch eine Leseanforderung für eine einzelne Seite wird beispielsweise eine einzelne Pufferseite gefüllt. Dies bedeutet, dass der Anlaufprozess von der Anzahl und der Art der Clientanforderungen abhängt. Dieser Prozess wird beschleunigt, indem Leseanforderungen für einzelne Seiten in ausgerichtete 8-Seiten-Anforderungen transformiert werden. Dadurch kann der Anlaufprozess sehr viel schneller erfolgen, insbesondere auf Maschinen mit großem Arbeitsspeicher.

Ein Großteil seines Arbeitsspeichers verwendet der Puffer-Manager im [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Vorgang. Daher erfolgt eine Zusammenarbeit zwischen Puffer-Manager und Speicher-Manager, damit auch andere Komponenten die Puffer verwenden können. Der Puffer-Manager interagiert vorrangig mit den folgenden Komponenten:

* Ressourcen-Manager zur Steuerung der gesamten Speicherauslastung, und für 32-Bit-Plattformen zur Steuerung der Adressraumverwendung.  
* Datenbank-Manager und dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Betriebssystem (SQLOS) für Datei-E/A-Vorgänge auf niedriger Ebene.  
* Protokoll-Manager für Write-Ahead-Protokollierung.  

### <a name="supported-features"></a>Unterstützte Funktionen

Der Puffer-Manager unterstützt die folgenden Funktionen:

* Der Puffer-Manager ist NUMA-fähig (Non-Uniform Memory Access). Außerdem werden Puffercacheseiten auf NUMA-Hardwareknoten verteilt, sodass ein Thread auf eine Pufferseite zugreifen kann, die dem lokalen NUMA-Knoten zugewiesen ist, statt den Zugriff über einen fremden Speicher vorzunehmen. 
* Der Puffer-Manager unterstützt das Hinzufügen von Arbeitsspeicher im laufenden Systembetrieb (Hot Add Memory), das dem Benutzer ermöglicht, physischen Arbeitsspeicher hinzuzufügen, ohne den Server neu starten zu müssen. 
* Es werden auch große Seiten auf 64-Bit-Plattformen vom Puffer-Manager unterstützt. Die Seitengröße ist spezifisch für die Version von Windows. 
* Es werden vom Puffer-Manager zusätzliche Diagnosen bereitgestellt, durch die dynamische Verwaltungssichten offengelegt werden. Mithilfe dieser Sichten können Sie verschiedene für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] spezifische Betriebssystemressourcen überwachen. Beispielsweise können Sie mithilfe der Sicht „sys.dm_os_buffer_descriptors“ die Seiten im Puffercache überwachen.   

### <a name="disk-io"></a>Datenträger-E/A
Mit dem Puffer-Manager werden nur Lese- und Schreibvorgänge für die Datenbank ausgeführt. Sonstige Datei- und Datenbankvorgänge, z. B. öffnen, schließen, erweitern und verkleinern) werden von den Datei- und Datenbank-Manager-Komponenten ausgeführt. 

Datenträger-E/A-Vorgänge des Puffer-Managers weisen die folgenden Merkmale auf:

* Alle E/A-Vorgänge werden asynchron ausgeführt, sodass der aufrufende Thread die Verarbeitung fortsetzen kann, während der E/A-Vorgang im Hintergrund ausgeführt wird.
* Alle E/A-Vorgänge werden an die aufrufenden Threads ausgegeben, sofern nicht die Option „affinity I/O“ verwendet wird. Durch die Option Affinity I/O Mask wird die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenträger-E/A an eine bestimmte Teilmenge der CPUs gebunden. In High-End-OLTP-Umgebungen (Online Transactional Processing, Onlinetransaktionsverarbeitung) für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann diese Erweiterung die Leistung von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Threads, die E/A verursachen, verbessern.
* Mehrfachseiten-E/A wird durch Scatter-Gather-E/A erreicht; dadurch wird ermöglicht, dass Daten in nicht zusammenhängende Bereiche des Arbeitsspeichers oder aus diesen übertragen werden können. Damit kann der Puffercache von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] problemlos gefüllt oder gelöscht werden; zugleich werden mehrere physische E/A-Anforderungen verhindert. 

#### <a name="long-io-requests"></a>Lange E/A-Anforderungen  
Vom Puffer-Manager werden alle seit mindestens 15 Sekunden ausstehenden E/A-Anforderungen gemeldet. Damit kann der Systemadministrator einfacher zwischen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Problemen und Problemen im E/A-Subsystem unterscheiden. Es wird die Fehlermeldung 833 angegeben. Im [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Fehlerprotokoll wird sie wie folgt angezeigt:

`` 
SQL Server has encountered %d occurrence(s) of I/O requests taking longer than %d seconds to complete on file [%ls] in database [%ls] (%d). The OS file handle is 0x%p. The offset of the latest long I/O is: %#016I64x.
`` 

Eine lange E/A kann entweder ein Lese- oder ein Schreibvorgang sein; in der Meldung wird dies nicht angegeben. Bei Meldungen zu langen E/A-Vorgängen handelt es sich um Warnungen, nicht um Fehlermeldungen. Probleme mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] werden nicht angegeben. Die Meldungen werden ausgegeben, damit der Systemadministrator die Ursache der langen Antwortzeiten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] leichter ermitteln kann und um Probleme, die nicht durch [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verursacht werden, abgrenzen zu können. Die Meldungen erfordern keine bestimmte Vorgehensweise; der Systemadministrator sollte jedoch untersuchen, weshalb die E/A-Anforderung so viel Zeit beansprucht, oder ob die benötigte Zeit gerechtfertigt ist.

#### <a name="causes-of-long-io-requests"></a>Ursachen für lange E/A-Anforderungen  
Eine Meldungen zu langen E/A-Vorgängen kann darauf hinweisen, dass ein E/A-Vorgang dauerhaft blockiert ist und nicht beendet werden kann (dies wird auch als „verlorener E/A-Vorgang“ bezeichnet) oder dass der E/A-Vorgang noch nicht beendet wurde. Es kann anhand der Meldung nicht ermittelt werden, welches Szenario hier zutrifft. Eine verlorene E/A führt jedoch häufig zu einem Latchtimeout.

Lange Wartezeiten bei der E/A sind häufig ein Hinweis auf eine zu hohe Arbeitsauslastung für das Datenträgersubsystem in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ein unzureichendes Datenträgersubsystem wird in folgenden Fällen angezeigt:

* Es werden mehrere lange E/A-Meldungen im Fehlerprotokoll angezeigt bei starker [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Arbeitsauslastung.
* Leistungsindikatoren weisen auf eine lange Datenträgerwartezeit, lange Datenträgerwarteschlangen und eine fehlende Datenträger-Leerlaufzeit hin.  

Lange E/A-Vorgänge können auch durch eine Komponente im E/A-Pfad verursacht werden (z. B. durch einen Treiber, einen Controller oder durch Firmware), bei der das Bedienen einer alten E/A-Anforderung kontinuierlich verschoben wird, anstatt neuere Anforderungen zu bedienen, die näher an der aktuellen Position des Lesekopfs liegen. Das häufig verwendete Verfahren, dass sich die Priorität in Bezug auf die Bearbeitung von Anforderungen danach richtet, welche Anforderungen näher an der aktuellen Position des Lese-/Schreibkopfes liegen, wird auch als "Fahrstuhlsuche" bezeichnet. Es ist möglicherweise schwierig, dies mithilfe des Systemmonitors von Windows (PERFMON.EXE) zu prüfen, da die meisten E/A-Vorgänge direkt bedient werden. Lange E/A-Anforderungen werden durch Arbeitsauslastungen erschwert, bei denen viele sequenzielle E/A-Anforderungen (z. B. Sichern und Wiederherstellen, Prüfen von Tabellen, Sortieren, Erstellen von Indizes, Massenladen und Dateien auf Null setzen) ausgeführt werden.

Isolierte lange E/A-Anforderungen, die nicht mit einer der vorherigen Bedingungen verknüft sind, können durch einen Hardware- oder Treiberfehler verursacht werden. Das Systemereignisprotokoll enthält möglicherweise ein ähnliches Ereignis, mit dem eine Problemdiagnose vorgenommen werden kann.

#### <a name="error-detection"></a>Fehlererkennung  
Von Datenbankseiten kann einer von zwei möglichen optionalen Mechanismen verwendet werden, mit dem die Integrität der Seite ab dem Zeitpunkt sichergestellt werden kann, an dem die Datei auf den Datenträger geschrieben wird, bis zu dem Zeitpunkt, wenn sie erneut gelesen wird: Schutz vor zerrissenen Seiten und Prüfsummenschutz. Anhand dieser Mechanismen kann die richtige Funktionsweise des Datenspeichers, der Hardwarekomponenten (Controller, Treiber, Kabel) und des Betriebssystems unabhängig geprüft werden. Der Schutz wird der Seite hinzugefügt, bevor sie auf den Datenträger geschrieben wird, und überprüft, wenn die Seite vom Datenträger gelesen wird.

#### <a name="torn-page-protection"></a>Schutz vor zerrissenen Seiten  
Der Schutz vor zerrissenen Seiten, der in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 eingeführt wurde, stellt in erster Linie eine Methode zum Erkennen von Seitenbeschädigungen dar, die auf Stromausfälle zurückzuführen sind. Beispielsweise kann der Fall eintreten, dass durch einen unerwarteten Stromausfall nur ein Teil einer Seite auf den Datenträger geschrieben wird. Bei Verwenden des Schutzes vor zerrissenen Seiten wird eine 2-Bit-Signatur am Ende jedes 512-Byte-Sektors in der Seite eingefügt (nachdem die ursprünglichen zwei Bit in den Seitenkopf kopiert wurden). Die Signatur wechselt bei jedem Schreibvorgang zwischen den Binärzuständen 01 und 10. Damit kann jederzeit ermittelt werden, ob nur ein Teil der Sektoren auf den Datenträger geschrieben wird: Wenn ein Bit beim späteren Lesen der Seite den falschen Zustand aufweist, wurde die Seite nicht richtig auf den Datenträger geschrieben, d.h., es wird eine zerrissene Seite ermittelt. Für die Erkennung von zerrissenen Seiten sind nur minimale Ressourcen erforderlich. Es werden jedoch keine Fehler erkannt, die durch Hardwarefehler des Datenträgers verursacht werden.

#### <a name="checksum-protection"></a>Prüfsummenschutz  
Der Prüfsummenschutz, der in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 eingeführt wird, ermöglicht eine verbesserte Datenintegritätsprüfung. Eine Prüfsumme wird für die Daten berechnet, die in den einzelnen Seiten geschrieben werden, und im Seitenkopf gespeichert. Wenn eine Seite, deren Prüfsumme gespeichert wird, vom Datenträger gelesen wird, wird vom Datenbankmodul die Prüfsumme für die Daten in der Seite neu berechnet. Wenn die neue Prüfsumme von der gespeicherten Prüfsumme abweicht, wird der Fehler 824 ausgegeben. Mithilfe des Prüfsummenschutzes können mehr Fehler ermittelt werden als mithilfe des Schutzes vor zerrissenen Seiten, da sich jedes in der Seite enthaltene Byte auf dieses Verfahren auswirkt. Der Prüfsummenschutz ist jedoch relativ ressourcenintensiv. Wenn die Prüfsumme aktiviert ist, werden durch Stromausfälle oder fehlerhafte Hard- oder Firmware verursachte Fehler erkannt, sobald die Seite vom Puffer-Manager vom Datenträger gelesen wird.

Die Art des verwendeten Seitenschutzes stellt ein Attribut der Datenbank dar, in der die Seite enthalten ist. Der Prüfsummenschutz stellt den Standardschutz für Datenbanken dar, die in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 und höheren Versionen erstellt wurden. Der Seitenschutzmechanismus wird beim Erstellen der Datenbank angegeben; er kann mithilfe von ALTER DATABASE modifiziert werden. Sie können den aktuellen Seitenschutz bestimmen, indem Sie eine Abfrage an die Spalte „page_verify_option“ in der Katalogsicht [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) oder die „IsTornPageDetectionEnabled“-Eigenschaft der [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md)-Funktion senden. Bei einer Änderung der Seitenschutzeinstellungen haben die neuen Einstellungen nicht unmittelbar Auswirkungen auf die gesamte Datenbank. Stattdessen wird von Seiten die aktuelle Schutzebene der Datenbank übernommen, wenn der nächste Schreibvorgang für die Seite erfolgt. Dies bedeutet, dass in der Datenbank Seiten mit unterschiedlichem Schutz enthalten sein können. 

## <a name="understanding-non-uniform-memory-access"></a>Grundlegendes zu NUMA (Non-Uniform Memory Access)

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ist NUMA-fähig (Non-Uniform Memory Access) und liefert hervorragende Leistungen auf NUMA-Hardware, ohne dass eine besondere Konfiguration notwendig wäre. Mit immer schnelleren Prozessoren und einer wachsenden Anzahl von Prozessoren wird es zunehmend schwieriger, die Speicherlatenzzeit zu verringern, die für die Verwendung dieser zusätzlichen Verarbeitungsleistung erforderlich ist. Für die Umgehung dieser Schwierigkeit stellen Hardwarehersteller große L3-Caches bereit; dies ist jedoch nur eine eingeschränkte Lösung. Die NUMA-Architektur bietet eine skalierbare Lösung für dieses Problem. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] kann die Vorteile NUMA-basierter Computer nutzen, ohne dass Anwendungsänderungen erforderlich sind. Weitere Informationen finden Sie unter [Vorgehensweise: Konfigurieren von SQL Server für die Verwendung von Soft-NUMA](../database-engine/configure-windows/soft-numa-sql-server.md).

## <a name="see-also"></a>Siehe auch
[Lesen von Seiten](../relational-databases/reading-pages.md)   
 [Schreiben von Seiten](../relational-databases/writing-pages.md)
