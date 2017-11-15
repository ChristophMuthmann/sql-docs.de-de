---
title: Anmerkungen zur Version von SQL Server 2012 SP4 | Microsoft-Dokumentation
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: "0"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b09784b129109f907c19a56a2a6fadcba119e73d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-2012-sp4-release-notes"></a>Anmerkungen zur Version von SQL Server 2012 SP4
Im Folgenden werden die Verbesserungen zusammengefasst, die in der Version SQL Server 2012 P4 enthalten sind. Außerdem werden Probleme beschrieben, die Sie prüfen sollten, bevor Sie SP4 installieren oder Probleme bei der Installation beheben. Versionsanmerkungen sind nur online verfügbar, nicht auf dem Installationsmedium. Diese Seite wird regelmäßig aktualisiert, wenn neue Probleme auftreten. Eine detaillierte Auflistung der Problembehebungen für SP4 finden Sie unter [SQL Server 2012 SP4 Release](https://go.microsoft.com/fwlink/?linkid=846937).  

> Das Service Pack 4 enthält alle kumulativen Updates der Version SQL Server 2012 SP3.
  
##<a name="download-pages"></a>Downloadseiten
Unter den folgenden Links finden Sie die Hauptdownloadpakete für SQL Server 2012 SP3. Downloadseiten enthalten Systemanforderungen und grundlegende Installationsanweisungen.
- [SQL Server 2012 SP4 Patchinstallation](https://go.microsoft.com/fwlink/?linkid=846829)
- [SQL Server 2012 SP4 Express](https://go.microsoft.com/fwlink/?linkid=846905)
- [Microsoft SQL Server 2012 SP4 Feature Pack](https://go.microsoft.com/fwlink/?linkid=846907)

##  <a name="sp4-performance-and-scale-improvements"></a>Verbesserungen hinsichtlich der Leistung und Skalierung von SP4

- **Verbesserte Prozedur zum Cleanup des Verteilungs-Agents:** Aufgrund einer zu großen Verteilungsdatenbank kam es zu Blockierungen und Deadlocks. Im Rahmen einer verbesserten Cleanup-Prozedur sollen einige davon beseitigt werden. 
- **Dynamische Skalierung des Speicherobjekts:** Partitionieren Sie Speicherobjekte dynamisch auf der Grundlage der Anzahl von Knoten und Kernen, um sie auf moderner Hardware zu skalieren. Mithilfe der dynamischen Promotion sollen potentielle Engpässe vermieden und threadsichere Speicherobjekte automatisch partitioniert werden. Unpartitionierte Speicherobjekte können dynamisch höher gestuft werden, um anhand der Knoten partitioniert zu werden. Die Anzahl der Partitionen entspricht der Anzahl der NUMA-Knoten. Speicherobjekte, die anhand der Knoten partitioniert werden, können noch höher gestuft werden, um anhand der CPU partitioniert zu werden. Dabei entspricht die Anzahl der Partitionen der Anzahl der CPU.
- **Aktivieren Sie > 8TB for Buffer Pool (> 8TB für Pufferpool):** Aktivieren Sie 128-TB virtuellen Adressraum für die Verwendung des Pufferpools.
- **Cleanup der Änderungsnachverfolgung**: Verbesserte Leistung und Effizienz des Cleanup der Änderungsnachverfolgung für Nebentabellen bei der Änderungsnachverfolgung. 

## <a name="sp4-supportability-and-diagnostics-improvements"></a>Verbesserungen hinsichtlich der Unterstützung und Diagnose von SP4

- **Unterstützung von vollständigen Speicherabbildungen für Replikations-Agents:** Wenn Replikations-Agents derzeit auf Ausnahmefehler stoßen, erstellen sie standardmäßig ein Miniabbild der Ausnahmesymptome. Standardmäßig sind bei Ausnahmefehlern komplexe Problembehandlungsvorgänge erforderlich. Mit SP4 wird ein neuer Registrierungsschlüssel eingeführt, der die Erstellung eines vollständigen Speicherabbilds für Replikations-Agents unterstützt.
- **Erweiterte Diagnose in Showplan XML:** Showplan XML wurde dahingehend erweitert, dass nun Informationen über aktivierte Ablaufverfolgungsflags, Teile des Arbeitsspeichers zur Optimierung des Joins geschachtelter Schleifen sowie über die CPU-Zeit und die verstrichene Zeit zur Verfügung stehen. 
- **Verbesserte Korrelation zwischen XE- und DMV-Diagnosen:** Query_hash- und query_plan_hash-Felder werden verwendet, um Abfragen eindeutig zu identifizieren. Sie werden von der DMV als varbinary(8) und von XEvent als UINT64 definiert. Da der SQL Server nicht über „unsignierten bigint“ verfügt, können Umwandlungen nicht immer erfolgreich vorgenommen werden. Mit dieser Verbesserung werden neue Aktions- bzw. Filterspalten für XEvent eingeführt, die query_hash und query_plan_hash weitestgehend entsprechen, es sei denn, sie werden als INT64 definiert, wodurch Abfragen zwischen XE und DMV besser korreliert werden können. 
- **Bessere Diagnose der Speicherzuweisung und -auslastung:** Neuer query_memory_grant_usage XEvent (Backport von Server 2016 SP1)
- **Hinzufügen einer Protokollnachverfolgung zu Schritten der SSL-Aushandlung:** Fügen Sie bitweise Ablaufverfolgungsinformationen für erfolgreiche bzw. fehlgeschlagene Aushandlungen, einschließlich Protokolle, hinzu. Dies kann bei der Problembehandlung von Konnektivitätsszenarios hilfreich sein, wenn beispielsweise TLS 1.2 bereitgestellt wird.
- **Festlegen eines angemessenen Kompatibilitätsgrads für die Verteilungsdatenbank :** Nach der Installation des Service Packs ändert sich der Kompatibilitätsgrad der Verteilungsdatenbank auf 90. Die Änderung des Kompatibilitätsgrads ist auf ein Problem bei der gespeicherten Prozedur sp_vupgrade_replication zurückzuführen. Das Service Pack wurde nun dahingehend geändert, dass es nun einen angemessenen Kompatibilitätsgrad für die Verteilungsdatenbank bestimmt. 
- **Neuer Datenbankkonsolenbefehl (DBCC) zum Klonen einer Datenbank:** „Clone database“ (Datenbank klonen) ist ein neuer DBCC-Befehl, mit dem es Hauptbenutzern wie CSS ermöglicht wird, Probleme mit bestehenden Produktionsdatenbanken zu behandeln, indem Schemata und Metadaten ohne die Daten geklont werden. Der Aufruf wird mit der DBCC-Klondatenbank (‘source_database_name’, ‘clone_database_name’) ausgeführt. Geklonte Datenbanken dürfen nicht in Produktionsumgebungen verwendet werden. Verwenden Sie den folgenden Befehl, wenn Sie überprüfen möchten, ob eine Datenbank nach dem Aufruf zum Klonen generiert wurde: Wählen Sie DATABASEPROPERTYEX('clonedb', 'isClone') (DATABASEPROPERTYEX('clonedb', 'isClone')) aus. Der Rückgabewert 1 bedeutet TRUE und 0 FALSE. 
- **Informationen zur TempDB-Datei und Dateigröße im SQL-Fehlerprotokoll:** Drucken Sie die Anzahl der Dateien aus, und lösen Sie eine Warnung aus, wenn sich die Größe und die automatische Vergrößerung von TempDB-Dateien beim Starten unterscheiden.
- **IFI-Supportnachrichten im SQL Server-Fehlerprotokoll:** Geben Sie im Fehlerprotokoll an, dass die schnelle Datenbankdateiinitialisierung aktiviert bzw. deaktiviert ist.
- **Neue DMF zum Ersetzen des DBCC INPUTBUFFER:** Eine neue dynamische Verwaltungsfunktion, sys.dm_input_buffer, die session_id als Parameter verwendet, wird eingeführt, um den DBCC INPUTBUFFER zu ersetzen.
- **Erweiterung für XEvents zum Lesen von Routingfehlern für eine Verfügbarkeitsgruppe:** Derzeit wird read_only_rout_fail XEvent nur ausgelöst, wenn zwar eine Routingliste besteht, jedoch zu keinem der Server auf dieser Liste eine Verbindung hergestellt werden kann. Diese Verbesserung beinhaltet zusätzliche Informationen zur Unterstützung bei der Problembehandlung und Erweiterungen zu den Codepunkten, bei denen XEvent ausgelöst wird. 
- **Verbesserte Handhabung von Service Broker mit Failover einer Verfügbarkeitsgruppe:** Wenn Service Broker für Datenbanken der Verfügbarkeitsgruppe derzeit aktiviert ist, bleiben bei einem Failover der Verfügbarkeitsgruppe alle Service Broker-Verbindungen, die dem primären Replikat entstammen, geöffnet. Mit dieser Verbesserung werden all diese offenen Verbindungen während eines Failover der Verfügbarkeitsgruppe geschlossen.
- **[Partitionierung mit der automatischen soft-NUMA:](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx)** Mit der Version SQL 2014 SP2 wird die automatische soft-NUMA eingeführt, wenn das Ablaufverfolgungsflag 8079 auf Serverebene aktiviert ist. Wenn das Ablaufverfolgungsflag 8079 beim Starten aktiviert ist, fragt SQL Server 2014 SP2 das Hardwarelayout ab und konfiguriert soft-NUMA automatisch auf Systemen, die mindestens acht CPU pro NUMA-Knoten vermelden. Die automatische soft-NUMA ist Hyperthread-fähig (HT/logischer Prozessor). Durch die Partitionierung und Erstellung von weiteren Knoten wird die Hintergrundverarbeitung skaliert, indem die Anzahl von Listenern, Skalierungen sowie Netzwerk- und Verschlüsselungsfunktionen erhöht wird. Wir empfehlen Ihnen, die Leistung der Arbeitsauslastung mit der automatischen soft-NUMA vor der Aktivierung im Rahmen der Produktion zunächst zu testen.

## <a name="see-also"></a>Siehe auch
- [Installieren von SQL Server 2012-Wartungsupdates](https://msdn.microsoft.com/library/hh479746(v=sql.110).aspx)
- [So identifizieren Sie die SQL Server-Version und -Edition](https://support.microsoft.com/en-us/help/321185)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
