---
title: Sichern und Wiederherstellen
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Beschreibt, wie die Daten sichern und Wiederherstellen von Works für SQL Server Parallel Data Warehouse (PDW)."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: d4669957-270a-4e50-baf3-14324ca63049
caps.latest.revision: 
ms.openlocfilehash: 06863b600ed62d795db82aa5aa3ae5c88578833a
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="backup-and-restore"></a>Sichern und Wiederherstellen
Beschreibt, wie die Daten sichern und Wiederherstellen von Works für SQL Server Parallel Data Warehouse (PDW). Sicherungs-und Wiederherstellungsvorgänge sind für die Wiederherstellung im Notfall verwendet werden. Sicherung und Wiederherstellung können auch zum Kopieren einer Datenbank auf einem Gerät in einer anderen Anwendung verwendet werden.  
    
## <a name="BackupRestoreBasics"></a>Grundlagen der Sicherung und Wiederherstellung  
Eine PDW *datenbanksicherung* ist eine Kopie einer Anwendungsdatenbank, in einem Format gespeichert, sodass er zum Wiederherstellen der ursprünglichen Datenbank in einer Anwendung verwendet werden kann.  
  
Eine PDW Sicherung wird erstellt, mit der [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md) t-Sql-Anweisung und formatierte für die Verwendung mit der [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) Anweisung; es für andere Zwecke nicht verwendbar ist. Die Sicherung kann nur in einer Anwendung mit der gleichen Anzahl oder eine größere Anzahl von Serverknoten wiederhergestellt werden.  
  
<!-- MISSING LINKS

The [master database](master-database.md) is a SMP SQL Server database. It is backed up with the BACKUP DATABASE statement. To restore master, use the [Restore the Master Database](configuration-manager-restore-master-database.md) page of the Configuration Manager tool.  

-->
  
PDW verwendet SQL Server backup-Technologie, um Appliance-Datenbanken sichern und wiederherstellen. Optionen zur Sicherung der SQL Server sind vorkonfiguriert, um die Komprimierung von Sicherungen verwenden. Sie können keine Sicherungsoptionen z. B. Komprimierung, Checksum-Blockgröße und Puffergröße festlegen.  
  
Datenbanksicherungen werden auf eine oder mehrere Sicherungsserver gespeichert, die in Ihrem eigenen Kundennetzwerk vorhanden sein.  PDW schreibt eine Benutzerdatenbank-Sicherung direkt von den Computeknoten parallel auf einem Sicherungsserver und eine Benutzerdatenbank-Sicherung parallel direkt aus dem backup-Server an den Computeknoten wiederhergestellt.  
  
Sicherungen werden auf dem backup-Server als ein Satz von Dateien in das Windows-Dateisystem gespeichert. Eine Sicherung der PDW-Datenbank kann nur mit PDW wiederhergestellt werden. Allerdings können Sie datenbanksicherungen vom backup-Server auf einen anderen Speicherort mithilfe von Standardprozessen für die Sicherung von Windows-Datei archivieren. Weitere Informationen zu backup-Server, finden Sie unter [abrufen und konfigurieren einen Sicherungsserver](acquire-and-configure-backup-server.md).  
  
## <a name="BackupTypes"></a>Datenbank-Sicherungstypen  
Es gibt zwei Arten von Daten, die eine Sicherung erfordern: Benutzerdatenbanken und Systemdatenbanken (z. B. der master-Datenbank). PDW das Transaktionsprotokoll nicht gesichert.  
  
Eine vollständige Sicherung ist eine Sicherung einer gesamten PDW-Datenbank. Dies ist der Standard-Sicherungstyp aus. Eine vollständige Sicherung einer Benutzerdatenbank enthält Datenbankbenutzer und Datenbankrollen. Eine Sicherung der Master-Datenbank umfasst Anmeldungen.  
  
Eine differenzielle Sicherung enthält alle Änderungen seit der letzten vollständigen Sicherung. Eine differenzielle Sicherung normalerweise weniger Zeit als eine vollständige Sicherung und häufiger ausgeführt werden kann. Wenn mehrere differenzielle Sicherungen auf der gleichen vollständigen Sicherung basieren, enthält jeder differenziellen Sicherung aller Änderungen in der vorherigen differenziellen an.  
  
Sie konnten z. B. eine vollständige Sicherung wöchentlich und täglich eine differenzielle Sicherung erstellen. Zum Wiederherstellen der Datenbank, die vollständige Sicherung sowie der letzten muss (falls vorhanden) differenziellen wiederhergestellt werden.  
  
Eine differenzielle Sicherung ist nur für Benutzerdatenbanken unterstützt. Eine Sicherung der Master-Datenbank ist immer eine vollständige Sicherung.  
  
Um die gesamte Anwendung sichern, müssen Sie eine Sicherung aller Benutzerdatenbanken und eine Sicherung der master-Datenbank ausführen.  
  
## <a name="BackupProc"></a>Sicherungsvorgang der Datenbank  
Das folgende Diagramm zeigt den Fluss der Daten während einer datenbanksicherung.  
  
![PDW-Sicherungsverfahren](media/backup-process.png "PDW-Sicherungsverfahren")  
  
Im Rahmen des Sicherungsvorgangs funktioniert wie folgt:  
  
1.  Benutzer übermittelt eine BACKUP DATABASE-t-SQL-Anweisung mit dem Steuerungsknoten.  
  
    -   Die Sicherung ist eine vollständige oder differenzielle Sicherung.  
  
2.  Für die Benutzerdatenbanken erstellt der Knoten "Zugriffssteuerung" (MPP Engine) eine verteilte Abfrage eine parallele datenbanksicherung ausführen möchten.  
  
3.  Jeder Knoten die Sicherungskopien der Sicherungsdatei auf dem backup-Server mit SQL Server die Sicherungsfunktion beteiligt ist.  
  
    -   Jeder Knoten beteiligt Kopien einer Sicherungsdatei auf dem backup-Server.  
  
    -   Die Benutzerdatenbank-Sicherung (vollständigen oder differenziellen) umfasst eine Sicherung des Bereichs der Datenbank gespeichert, die auf jeder Serverknoten, und eine Sicherung der Datenbankbenutzer und Datenbankrollen.  
  
4.  Das Gerät führt die Sicherung parallel mit dem InfiniBand-Netzwerk.  
  
    -   PDW führt jede vollständige und differenzielle Sicherung parallel aus. Mehrere datenbanksicherungen werden jedoch nicht gleichzeitig ausgeführt. Jede Anforderung für die Sicherung muss zuvor gesendeten Sicherungen abgeschlossen warten.  
  
    -   Eine Sicherung der master-Datenbank sichert nur aus dem Knoten "Zugriffssteuerung". Dieser Sicherungstyp wird seriell ausgeführt.  
  
5.  Eine PDW Sicherung ist eine Gruppe von Dateien in einem Verzeichnis, das aus dem Gerät befindet. Der Verzeichnisname ist als Netzwerknamen Pfad und das Verzeichnis angegeben. Das Verzeichnis darf kein lokaler Pfad sein, und es dürfen sich nicht auf dem Gerät.  
  
6.  Nachdem die Sicherung abgeschlossen ist, können das Windows-Dateisystem Sie das Sicherungsverzeichnis an einen anderen Speicherort kopieren bei Bedarf.  
  
    -   Eine Sicherung kann nur in einer PDW-Anwendung wiederhergestellt werden, die ein gleich großer oder größerer Anteil an Serverknoten.  
  
    -   Der Name der Sicherung kann nicht geändert werden, vor dem Ausführen einer Wiederherstellung. Der Name für das Sicherungsverzeichnis muss den Namen des ursprünglichen Namen des Sicherungssatzes übereinstimmen. Der ursprüngliche Name der Sicherung befindet sich in der Datei "Backup.xml" in das Sicherungsverzeichnis. Zum Wiederherstellen einer Datenbank auf einen anderen Namen können Sie den neuen Namen in der Restore-Befehl angeben. Beispiel: `RESTORE DATABASE MyDB1 FROM DISK = ꞌ\\10.192.10.10\backups\MyDB2ꞌ`  
  
## <a name="RestoreModes"></a>Datenbank wiederherstellen-Modi  
Eine vollständige datenbankwiederherstellung erstellt die PDW-Datenbank mithilfe der Daten in der datenbanksicherung neu. Die Wiederherstellung der Datenbank erfolgt über zuerst eine vollständige Sicherung wiederhergestellt, und klicken Sie dann optional eine differenzielle Sicherung wiederherstellen. Die Wiederherstellung der Datenbank enthält die Datenbankbenutzer und Datenbankrollen.  
  
Eine einzige Header-Wiederherstellung gibt die Headerinformationen für eine Datenbank zurück. Es werden die Daten nicht in der Anwendung wiederhergestellt.  
  
Eine Wiederherstellung der Anwendung ist eine Wiederherstellung der gesamten Anwendung. Dies schließt alle Benutzerdatenbanken und der master-Datenbank wiederherstellen.  
  
## <a name="RestoreProc"></a>Wiederherstellungsvorgang  
Das folgende Diagramm zeigt den Fluss der Daten während einer Wiederherstellung der Datenbank.  
  
![Wiederherstellungsprozess](media/restore-process.png "Wiederherstellungsprozess")  
  
## <a name="restoring-to-an-appliance-with-the-same-number-of-compute-nodes"></a>Wiederherstellen bis zu eine Einheit mit derselben Anzahl von Compute-Knoten **  
  
Beim Wiederherstellen von Daten erkennt die Appliance die Anzahl der Serverknoten auf die Einheit für die Quelle und Ziel-Einheit. Wenn beide Einheiten eine gleiche Anzahl von Serverknoten haben, funktioniert der Wiederherstellungsprozess wie folgt:  
  
1.  Die datenbanksicherung wiederhergestellt werden, ist in einer Windows-Dateifreigabe auf einem nicht-Appliance-Sicherungsserver verfügbar. Für optimale Leistung wird dieser Server in der Regel mit dem Gerät InfiniBand-Netzwerk verbunden.  
  
2.  Benutzer übermittelt eine [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md) Tsql-Anweisung mit dem Steuerungsknoten.  
  
    -   Die Wiederherstellung ist eine vollständige Wiederherstellung oder eine Wiederherstellung des Headers. Die vollständige Wiederherstellung eine vollständige Sicherung wiederhergestellt, und klicken Sie dann optional eine differenzielle Sicherung wiederhergestellt.  
  
3.  Der Knoten "Zugriffssteuerung" (MPP Engine) erstellt einen verteilte Abfrageplan eine parallele Wiederherstellung ausführen.  
  
    -   SQL-ServerPDW führt die Wiederherstellung einer Benutzerdatenbank parallel. Allerdings sind mehrere datenbanksicherungen und Wiederherstellungen nicht gleichzeitig ausgeführt werden. Das Modul MPP Fügt jeder Restore-Anweisung in eine Warteschlange; Sie müssen warten zuvor übermittelten Sicherung und Wiederherstellen von Anforderungen, um den Vorgang abzuschließen.  
  
    -   Eine Wiederherstellung der master-Datenbank wird nur die Daten mit dem Steuerungsknoten wiederhergestellt. die Wiederherstellung wird seriell ausgeführt.  
  
    -   Eine Wiederherstellung der Headerinformationen erfolgt schnell und alle Daten auf die Knoten Compute oder Steuerelement nicht wiederhergestellt. Der Knoten "Zugriffssteuerung" wird stattdessen die Ergebnisse als Ausgabe einer Abfrage zurückgegeben.  
  
4.  Die Sicherungsdateien Abrufen über die Appliance InfiniBand-Netzwerk in der Regel auf die richtige Serverknoten parallel kopiert.  
  
5.  Jeder Serverknoten stellt seine Teil der Datenbank wieder her. Wenn keines der Wiederherstellung nicht erfolgreich abgeschlossen, werden alle Datenbanken entfernt, und die Wiederherstellung abgeschlossen werden konnte.  
  
## <a name="restoring-to-an-appliance-with-a-larger-number-of-compute-nodes"></a>Wiederherstellen in einer Anwendung mit einer größeren Anzahl von Serverknoten  
  
Wiederherstellen einer Sicherung in einer Anwendung mit einer größeren Anzahl von Serverknoten, wächst die Größe der belegten Datenbank relativ zur Anzahl von Compute-Knoten.  
  
Erstellt z. B. bei der Wiederherstellung einer 60-GB-Datenbank von einer 2-Knoten-Einheit (30 GB pro Knoten) in einer Anwendung 6 Knoten SQL Server PDW eine 180 GB-Datenbank (6 Knoten mit 30 GB pro Knoten) auf dem Gerät 6 Knoten. SQL Server PDW stellt anfänglich 2 Knoten entsprechend die Quellkonfiguration der Datenbank wieder her, und klicken Sie dann die Daten für alle 6 Knoten neu verteilt.  
  
Nach der Weitergabe enthält jeder Serverknoten weniger tatsächlichen Daten und mehr freien Speicher als jeder Compute-Knoten auf der kleinere Source-Anwendung. Verwenden Sie den zusätzlichen Speicherplatz, um die Datenbank weitere Daten hinzuzufügen. Wenn die wiederhergestellte Datenbank größer ist, als Sie benötigen, können Sie [ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md) zum Verkleinern der Datenbank-Dateigrößen.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Sicherung und Wiederherstellung|Description|  
|---------------------------|---------------|  
|Bereiten Sie einen Server als Sicherungsserver.|[Erwerben und Konfigurieren eines backup-Servers ](acquire-and-configure-backup-server.md)|  
|Sichern einer Datenbank an.|[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)|  
|Stellen Sie eine Datenbank wieder her.|[STELLEN SIE DIE DATENBANK WIEDER HER.](../t-sql/statements/restore-database-parallel-data-warehouse.md)|    
<!-- MISSING LINKS
|Create a disaster recovery plan.|[Create a Disaster Recovery Plan](create-disaster-recovery-plan.md)|
|Restore the master database.|To restore the master database, use the [Restore the master database](configuration-manager-restore-master-database.md) page in the Configuration Manager tool.| 
|Copy a database from one appliance to another appliance.|[Copy a PDW database to another appliance](copy-pdw-database-to-another-appliance.md).|  
|Monitor backups and restores.|[Monitor backups and restores](monitor-backup-and-restore.md)|  
-->
