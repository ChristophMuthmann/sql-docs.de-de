---
title: "Lesen von Seiten | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Seiten"
ms.assetid: f8da760e-aacb-4661-9f3a-2578d8c11e4e
caps.latest.revision: 3
author: "pmasl"
ms.author: "pelopes"
manager: "jhubbard"
caps.handback.revision: 3
---
# Lesen von Seiten
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

Die E/A-Aktivitäten einer Instanz von SQL Server [!INCLUDE[ssDE](../includes/ssde-md.md)] schließen logische und physische Lesevorgänge ein. Ein logischer Lesevorgang erfolgt immer dann, wenn das [!INCLUDE[ssDE](../includes/ssde-md.md)] eine Seite aus dem [Puffercache](../relational-databases/memory-management-architecture-guide.md) anfordert. Wenn sich die Seite derzeit nicht im Puffercache befindet, wird ein physischer Lesevorgang durchgeführt, um die Seite vom Datenträger in den Puffercache zu kopieren.

Die von einer Instanz des [!INCLUDE[ssDE](../includes/ssde-md.md)]s generierten Leseanforderungen werden vom relationalen Modul gesteuert und vom Speichermodul weiter optimiert. Das relationale Modul ermittelt die effizienteste Zugriffsmethode (Tabellenscan, Indexscan oder schlüsselgesteuerter Lesevorgang); die Zugriffsmethoden und Puffer-Manager-Komponenten des Speichermoduls bestimmen das allgemeine Muster der durchzuführenden Lesevorgänge und optimieren die Lesevorgänge, die für die Implementierung der Zugriffsmethode erforderlich sind. Der Thread, der den Batch ausführt, plant die Ausführung der Lesevorgänge.

## <a name="read-ahead"></a>Vorauslesen (Read-Ahead)
Das [!INCLUDE[ssDE](../includes/ssde-md.md)] unterstützt einen Leistungsoptimierungsmechanismus, der als Read-Ahead oder Vorauslesen bekannt ist. Dieser Mechanismus antizipiert die für die Erfüllung eines Abfrageausführungsplans erforderlichen Daten und Indexseiten und platziert diese Seiten in den Puffercache, noch bevor sie von der Abfrage benötigt werden. Dies ermöglicht eine Überlappung von Berechnungs- und E/A-Aktivitäten, sodass sowohl die CPU- als auch die Datenträgerressourcen voll ausgenutzt werden können. 

Mithilfe des Read-Ahead-Mechanismus kann das [!INCLUDE[ssDE](../includes/ssde-md.md)] bis zu 64 aufeinanderfolgende Seiten (512 KB) aus einer Datei lesen. Der Lesevorgang wird als einzelner Scatter-Gather-Vorgang durchgeführt, und die entsprechende Anzahl (wahrscheinlich nicht aufeinanderfolgender) Puffer wird in den Puffercache eingelesen. Falls bestimmte Seiten aus dem Seitenbereich bereits im Puffercache vorhanden sind, wird die entsprechende Seite nach Abschluss des Lesevorgangs aus den einzulesenden Seiten entfernt. Der Seitenbereich kann auch von einem der beiden Enden aus "gekürzt" werden, wenn sich die entsprechenden Seiten bereits im Cache befinden.

Für Datenseiten und Indexseiten ist je ein unterschiedlicher Read-Ahead-Mechanismus verfügbar.

### <a name="reading-data-pages"></a>Lesen von Datenseiten
Tabellenscans, die zum Lesen von Datenseiten verwendet werden, sind in [!INCLUDE[ssDE](../includes/ssde-md.md)] sehr effizient. Die IAM-Seiten (Index Allocation Map) in einer SQL Server-Datenbank listen die von einer Tabelle oder einem Index verwendeten Datenblöcke auf. Das Speichermodul kann die IAM lesen, um eine geordnete Liste der Datenträgeradressen zu erstellen, die gelesen werden müssen. Hierdurch wird dem Speichermodul ermöglicht, E/A-Operationen in Form von langen, sequenziellen Lesevorgängen zu optimieren, die abhängig von ihrem Speicherort auf dem Datenträger nacheinander ausgeführt werden. Weitere Informationen zu IAM-Seiten finden Sie unter [Verwalten des von Objekten verwendeten Speicherplatzes](../relational-databases/pages-and-extents-architecture-guide.md).

### <a name="reading-index-pages"></a>Lesen von Indexseiten
Im Speichermodul werden Indexseiten nacheinander in der Reihenfolge der Schlüssel gelesen. Diese Abbildung zeigt z. B. eine vereinfachte Darstellung eines Satzes von Blattseiten, die einen Satz von Schlüsseln enthalten, und den Zwischenindexknoten, der eine Zuordnung der Blattseiten vornimmt. Weitere Informationen zur Struktur von Seiten in einem Index finden Sie unter [Gruppierte Indexstrukturen](../relational-databases/pages-and-extents-architecture-guide.md).

![Reading_Pages](../relational-databases/media/reading-pages.gif)

Das Speichermodul verwendet die Informationen der Zwischenindexseite oberhalb der Blattebene, um serielle Read-Ahead-Operationen für die Seiten zu planen, die die Schlüssel enthalten. Wenn eine Anforderung für alle Schlüssel von ABC bis DEF erfolgt, liest das Speichermodul zunächst die Indexseite oberhalb der Blattseite. Es wird jedoch nicht einfach ein Lesevorgang in der Reihenfolge von Seite 504 bis Seite 556, der letzten Seite mit Schlüsseln im gewünschten Bereich, durchgeführt. Stattdessen scannt das Speichermodul die Zwischenindexseite und erstellt eine Liste der Blattseiten, die gelesen werden müssen. Anschließend plant das Speichermodul alle Lesevorgänge, geordnet nach Schlüsseln. Das Speichermodul erkennt ebenfalls, dass es sich bei den Seiten 504/505 und 527/528 um zusammenhängende Seiten handelt, und führt einen einzelnen Scatter-Lesevorgang aus, um angrenzende Seiten in einem einzigen Vorgang abzurufen. Wenn viele Seiten in einem seriellen Vorgang abgerufen werden sollen, plant das Speichermodul einen Block von Lesevorgängen zur selben Zeit. Wenn eine Teilmenge dieser Lesevorgänge abgeschlossen ist, plant das Speichermodul dieselbe Anzahl neuer Lesevorgänge, bis alle erforderlichen Lesevorgänge geplant sind.

Das Speichermodul verwendet Vorababrufvorgänge, um Basistabellen-Nachschlagevorgänge in nicht gruppierten Indizes zu beschleunigen. Die Blattzeilen eines nicht gruppierten Indexes enthalten Zeiger auf die Datenzeilen, die die jeweiligen Schlüsselwerte enthalten. Während das Speichermodul die Blattseiten des nicht gruppierten Indexes liest, beginnt es mit der Planung asynchroner Lesevorgänge für die Datenzeilen, deren Zeiger bereits abgerufen wurden. Auf diese Weise kann das Speichermodul Datenzeilen aus der zugrunde liegenden Tabelle abrufen, bevor der Scan des nicht gruppierten Indexes abgeschlossen ist. Dieses Verfahren wird unabhängig davon eingesetzt, ob die Tabelle über einen gruppierten Index verfügt. SQL Server Enterprise verwendet Vorababrufvorgänge häufiger als andere Editionen von SQL Server, wodurch mehr Seiten im Read-Ahead-Modus gelesen werden können. Der Grad der Vorababrufvorgänge kann in keiner Edition konfiguriert werden. Weitere Informationen zu nicht gruppierten Indizes finden Sie unter [Strukturen nicht gruppierter Indizes](../relational-databases/pages-and-extents-architecture-guide.md).

## <a name="advanced-scanning"></a>Erweitertes Scannen
Die erweiterte Scanfunktion von SQL Server Enterprise ermöglicht es, dass vollständige Tabellenscans für mehrere Tasks freigegeben werden. Wenn für einen Ausführungsplan einer Transact-SQL-Anweisung ein Scan der Datenseiten in einer Tabelle erforderlich ist und das [!INCLUDE[ssDE](../includes/ssde-md.md)] erkennt, dass die Tabelle bereits für einen anderen Ausführungsplan gescannt wurde, verknüpft [!INCLUDE[ssDE](../includes/ssde-md.md)] den zweiten Scan mit dem ersten Scan, und zwar an der aktuellen Position des zweiten Scans. [!INCLUDE[ssDE](../includes/ssde-md.md)] liest jede Seite einmal und übergibt die Zeilen jeder Seite an beide Ausführungspläne. Dieser Vorgang wird fortgesetzt, bis das Ende der Tabelle erreicht ist. 

Zu diesem Zeitpunkt verfügt der erste Ausführungsplan über das vollständige Ergebnis eines Scans, der zweite Ausführungsplan muss jedoch noch die Datenseiten abrufen, die gelesen wurden, bevor der Join mit dem laufenden Scan erfolgt ist. Der Scan für den zweiten Ausführungsplan kehrt zur ersten Datenseite der Tabelle zurück und scannt die folgenden Seiten, bis die Seite erreicht ist, an der der Join mit dem ersten Scan erfolgt ist. Auf diese Weise können beliebig viele Scans kombiniert werden. [!INCLUDE[ssDE](../includes/ssde-md.md)] durchläuft die Datenseiten so lange, bis sämtliche Scans abgeschlossen sind. Dieser Mechanismus wird auch als "Karussellscan" (Merry-Go-Round Scanning) bezeichnet und zeigt, warum die Reihenfolge der Ergebnisse einer SELECT-Anweisung ohne ORDER BY-Klausel nicht sichergestellt werden kann. 

Nehmen Sie z. B. an, Sie verfügen über eine Tabelle mit 500.000 Seiten. UserA führt eine Transact-SQL-Anweisung aus, für die ein Scan der Tabelle erforderlich ist. Wenn dieser Scan 100.000 Seiten verarbeitet hat, führt UserB eine weitere Transact-SQL-Anweisung aus, die dieselbe Tabelle scannt. Das [!INCLUDE[ssDE](../includes/ssde-md.md)] plant einen Satz mit Leseanforderungen für die Seiten nach Seite 100.001 und gibt die Zeilen für jede Seite an beide Scans zurück. Wenn der Scan Seite 200.000 erreicht, führt UserC eine weitere Transact-SQL-Anweisung aus, die dieselbe Tabelle scannt. Beginnend mit Seite 200.001 gibt [!INCLUDE[ssDE](../includes/ssde-md.md)] die Zeilen jeder gelesenen Seite an alle drei Scans zurück. Nachdem die Zeile 500.000 gelesen wurde, ist der Scan für UserA abgeschlossen. Die Scans für UserB und UserC kehren an den Anfang zurück und beginnen mit dem Lesen von Seite 1. Wenn [!INCLUDE[ssDE](../includes/ssde-md.md)] Seite 100.000 erreicht, ist der Scan für UserB abgeschlossen. Der Scan für UserC wird allein fortgesetzt, bis Seite 200.000 erreicht ist. An diesem Punkt sind alle Scans abgeschlossen. 

Ohne die erweiterten Scanfunktionen müssten sich die einzelnen Benutzer den Pufferspeicher teilen, was Konflikte in der Speicherverteilung verursachen würde. Dieselben Seiten würden dann einmal für jeden Benutzer gelesen werden, anstatt einmal gelesen und dann für mehrere Benutzer freigegeben zu werden. Dies würde die Leistung beeinträchtigen und Ressourcen unnötig beanspruchen.

## <a name="see-also"></a>Siehe auch
[Handbuch zur Architektur von Seiten und Blöcken](../relational-databases/pages-and-extents-architecture-guide.md)   
 [Schreiben von Seiten](../relational-databases/writing-pages.md)