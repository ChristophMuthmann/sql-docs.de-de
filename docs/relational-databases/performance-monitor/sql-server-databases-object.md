---
title: SQL Server, Datenbanken-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
caps.latest.revision: "40"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c92dc55eedaf801ad283ecb18bb55a25ba49f4b1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-databases-object"></a>SQL Server, Datenbanken-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das **SQLServer:Datenbanken**-Objekt in SQL Server stellt Leistungsindikatoren bereit, mit denen Sie Massenkopiervorgänge, den Durchsatz von Sicherungs- und Wiederherstellungsvorgängen sowie Transaktionsprotokollaktivitäten überwachen können. Überwachen Sie Transaktionen und das Transaktionsprotokoll, um ermitteln zu können, wie viel Benutzeraktivität in der Datenbank auftritt und in welchem Umfang das Transaktionsprotokoll aufgefüllt wird. Durch den Umfang der Benutzeraktivität kann die Leistung der Datenbank bestimmt werden. Protokollgröße, Sperren und die Replikation können davon betroffen sein. Das Überwachen der Protokollaktivität auf niedriger Ebene zur Messung der Benutzeraktivität und der Ressourcennutzung kann Ihnen dabei helfen, Leistungsengpässe zu erkennen.  
  
 Es können mehrere Instanzen des **Datenbanken** -Objekts überwacht werden, von denen jede eine einzelne Datenbank darstellt.  
  
 In dieser Tabelle werden die **Datenbanken** -Leistungsindikatoren von SQL Server beschrieben.  
  
|Datenbanken-Leistungsindikatoren von SQL Server|Description|  
|-----------------------------------|-----------------|  
|**Aktive Transaktionen**|Anzahl von aktiven Transaktionen für die Datenbank.|  
|**Durchschn. Abstand von EOL/LP-Anforderung**|Durchschnittlicher Abstand in Byte vom Ende des Protokolls nach Protokollpoolanforderung für Anforderungen in der letzten VLF.| 
|**Sicherungs-/Wiederherstellungsdurchsatz/Sekunde**|Durchsatz von Lese-/Schreiboperationen bei Sicherungs- und Wiederherstellungsvorgängen für eine Datenbank pro Sekunde. So können Sie beispielsweise messen, wie sich die Leistung des Datenbank-Sicherungsvorgangs ändert, wenn mehr Sicherungsmedien parallel verwendet werden oder wenn schnellere Medien verwendet werden. Der Durchsatz eines Datenbank-Sicherungs- oder -Wiederherstellungsvorgangs ermöglicht es Ihnen, den Fortschritt und die Leistung der gesamten Sicherungs- und Wiederherstellungsvorgänge zu ermitteln.|  
|**Zeilen für Massenkopieren/Sekunde**|Anzahl von massenkopierten Zeilen pro Sekunde.|  
|**Durchsatz bei Massenkopieren/Sekunde**|Umfang der pro Sekunde massenkopierten Daten (in KB).|  
|**Commit-Tabelleneinträge**|Die Größe des speicherinternen Anteils der Commit-Tabelle für die Datenbanken. Weitere Informationen finden Sie unter [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md).|  
|**Größe der Datendatei(en) (KB)**|Die kumulierte Größe (in KB) aller Datendateien in der Datenbank, wobei auch jegliche automatische Vergrößerung berücksichtigt ist. Die Überwachung dieses Leistungsindikators ist z. B: nützlich, wenn die richtige Größe von **tempdb**ermittelt werden soll.|  
|**DBCC - Rate logischer Scans/Sekunde**|Anzahl an Bytes logischer Lesescans pro Sekunde für DBCC-Anweisungen (Database Console Commands, Datenbankkonsolenbefehle).|  
|**Commitzeit der Gruppe/s**|Die Verzögerungszeit der Gruppe (Mikrosekunden) pro Sekunde.|
|**Geleerte Protokollbytes/Sekunde**|Gesamtanzahl der geleerten Protokollbytes.|  
|**Protokollcache-Trefferquote**|Prozentsatz der Lesevorgänge im Protokollcache, die durch den Protokollcache aufgelöst werden konnten.|  
|**Basis für Protokoll-Cachetrefferquote**|Nur zur internen Verwendung.| 
|**Protokollcache-Lesevorgänge/Sekunde**|Lesevorgänge pro Sekunde, die über den Cache des Protokoll-Managers ausgeführt wurden.|  
|**Protokolldatei(en) Größe (KB)**|Die kumulierte Größe aller Protokolldateien in der Datenbank (in KB).|  
|**Von Protokolldatei(en) verwendete Größe (KB)**|Die kumulierte verwendete Größe aller Protokolldateien in der Datenbank.|  
|**Wartezeit für Protokollleerung**|Gesamte Wartezeit (in Millisekunden) bis zum Entleeren des Protokolls. Bei einer sekundären Always On-Datenbank gibt dieser Wert die Wartezeit für Protokolldatensätze an, die auf einem Datenträger festzuschreiben sind.|  
|**Ausstehende Protokollleerungen/Sekunde**|Anzahl von Commits pro Sekunde, die auf eine Protokollleerung warten.|  
|**Wartezeit für Protokollleerung (ms)**|Entspricht der Zeit in Millisekunden zum Ausführen von Schreibvorgängen für Protokollleerungen, die in der letzten Sekunde abgeschlossen wurden.|  
|**Protokollleerungen/Sekunde**|Anzahl an Protokollleerungen pro Sekunde.|  
|**Protokollvergrößerungen**|Gesamtanzahl von Vergrößerungen des Transaktionsprotokolls für diese Datenbank.|  
|**Protokollpool-Cachefehlversuche/Sekunde**|Anzahl an Anforderungen, für die der Protokollblock im Protokollpool nicht verfügbar war. Der *Protokollpool* ist ein arbeitsspeicherinterner Cache für das Transaktionsprotokoll. Dieser Cache wird verwendet, um das Lesen des Protokolls zur Wiederherstellung, Transaktionsreplikation, Rollback und [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]zu optimieren.|  
|**Protokollpool-Lesevorgänge auf dem Datenträger/Sekunde**|Anzahl an Lesevorgängen auf dem Datenträger, die vom Protokollpool zum Abrufen von Protokollblöcken ausgegeben wurden.|  
|**Protokollpool-Hashlöschungen/Sek.**|Die Rate der unformatierten Löschungen von Hasheinträgen aus dem Protokollpool.|
|**Protokollpool-Hasheinfügungen/Sek.**|Die Rate der unformatierten Einfügungen von Hasheinträgen in den Protokollpool.|
|**Protokollpool: ungültige Hasheinträge/Sek.**|Die Rate der fehlerhaften Hashsuchen wegen ungültiger Daten.|
|**Protokollpool: Protokollprüfungs-Schreibvorgänge/Sek.**|Die Rate der Protokoll-Blockschreibvorgänge für Protokollprüfungen, entweder von der Festplatte oder aus dem Arbeitsspeicher.|
|**Protokollpool: Protokollschreiber-Schreibvorgänge/Sek.**|Rate der Protokoll-Blockschreibvorgänge pro Protokoll-Schreibthread.|
|**Protokollpoolpush leerer FreierPool/s**|Rate der Protokollsperren-Pushfehler aufgrund eines leeren freien Pools.|
|**Protokollpoolpush bei unzureichendem Arbeitsspeicher/s**|Rate der Protokollsperren-Pushfehler aufgrund von unzureichendem Arbeitsspeicher.|
|**Protokollpoolpush kein freier Puffer/s**|Rate der Protokollsperren-Pushfehler aufgrund nicht verfügbarer leerer Puffer.|
|**Protokollpool erforderlich hinter Kürzungs-LSN/Sek.**|Protokollpool-Cachefehler, weil der angeforderte Block hinter der Kürzungs-LSN liegt.|
|**Basis für Protokollpoolanforderungen**|Nur zur internen Verwendung.| 
|**Protokollpoolanforderungen alte VLF/s**|Protokollpoolanforderungen, die nicht in der letzten VLF des Protokolls enthalten waren.|  
|**Protokollpoolanforderungen/Sekunde**|Die Anzahl an Protokollblockanforderungen, die vom Protokollpool verarbeitet wurden.|  
|**Protokollpool – Gesamtgröße des aktiven Protokolls**|Aktuelle Gesamtgröße des im freigegebenen Cachepuffer-Manager gespeicherten aktiven Protokolls in Byte.|
|**Protokollpool – Gesamtgröße des freigegebenen Pools**|Aktuelle gesamte Speicherauslastung des freigegebenen Cachepuffer-Managers in Byte.|
|**Protokollverkleinerungen**|Gesamtanzahl der Protokollverkleinerungen für diese Datenbank.|  
|**Protokollkürzungen**|Die Anzahl, wie oft das Transaktionsprotokoll verkleinert wurde.|  
|**Protokoll verwendet (Prozent)**|Der prozentuale Anteil des Speicherplatzes im Protokoll, der verwendet wird.|  
|**Replikations Replikationstransaktionen**|Anzahl von Transaktionen im Transaktionsprotokoll der Veröffentlichungsdatenbank, die für die Replikation gekennzeichnet sind, jedoch noch nicht an die Verteilungsdatenbank übermittelt wurden.|  
|**Replikations Trans. Zins**|Anzahl von Transaktionen, die pro Sekunde aus dem Transaktionsprotokoll der Veröffentlichungsdatenbank ausgelesen und an die Verteilungsdatenbank übermittelt wurden.|  
|**Verschiebung bei Datenverkleinerung Bytes/Sekunde**|Umfang an Daten, die bei der automatischen Verkleinerung oder der Ausführung von DBCC SHRINKDATABASE oder DBCC SHRINKFILE pro Sekunde verschoben wurden.|  
|**Nachverfolgte Transaktionen/Sekunde**|Anzahl an Transaktionen, für die ein Commit ausgeführt wurde und die in der Commit-Tabelle für die Datenbank erfasst wurden.|  
|**Transaktionen/Sekunde**|Anzahl an Transaktionen, die für die Datenbank pro Sekunde gestartet wurden.<br /><br /> **Transaktionen/Sekunde** zählt keine XTP-Transaktionen (d.h. Transaktionen, die durch eine nativ kompilierte gespeicherte Prozedur gestartet wurden).|  
|**Geschriebene Transaktionen/Sek**|Anzahl von Transaktionen, die in der letzten Sekunde Daten in die Datenbank geschrieben und einen Commit durchgeführt haben.|  
|**XTP-Controller-DLC-Latenzbasis**|Nur zur internen Verwendung.| 
|**XTP-Controller-DLC-Latenz/Abruf**|Durchschnittliche Latenz (in Mikrosekunden) zwischen Protokollblöcken, die in den Direct Log Consumer gelangen und vom XTP-Contoller pro Sekunde abgerufen werden.|
|**XTP-Controller-DLC-Spitzenlatenz**|Die größte aufgezeichnete Latenz (in Mikrosekunden) eines Abrufs vom Direct Log Consumer durch den XTP-Controller.|
|**Verarbeitete XTP-Controllerprotokolle/Sekunde**|Die Anzahl von Protokollbytes, die pro Sekunde vom XTP-Controllerthread verarbeitet werden.|
|**Verwendeter XTP-Speicher (KB)**|Die von XTP in der Datenbank verwendete Speichermenge.| 
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Datenbankreplikat](../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
  
