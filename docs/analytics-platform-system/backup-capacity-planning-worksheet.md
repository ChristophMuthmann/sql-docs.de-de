---
title: Sicherungsserver Kapazitätsplanung Arbeitsblatt (SQLServer PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Mit diesem Arbeitsblatt Kapazität unterstützt Sie beim Bestimmen der Anforderungen für die backup-Server zum Ausführen von SQL Server PDW Sicherung und Wiederherstellung.
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 36294bf6-6dde-481f-a190-d4382b04c030
caps.latest.revision: 6
ms.openlocfilehash: 1548d284f78043e5f878bafe9922480fe762dbfe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="backup-server-capacity-planning-worksheet"></a>Sicherungsserver Capacity planning Arbeitsblatt
Mit diesem Arbeitsblatt Kapazität unterstützt Sie beim Bestimmen der Anforderungen für die backup-Server zum Ausführen von SQL Server PDW Sicherung und Wiederherstellung. Hiermit können Sie Ihren Plan für Kaufverhalten neue oder Bereitstellung vorhandene Sicherungsserver erstellen.  
  
Dieses Arbeitsblatt ist eine Ergänzung zu den Anweisungen in [erwerben und Konfigurieren eines Servers für die Sicherung](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Arbeitsblatt für Kapazität Planung für Backup-Server  

### <a name="notes"></a>Hinweise  
  
1.  Dieses Arbeitsblatt gilt für Server, die Sicherung und Wiederherstellung Vorgänge für PDW-Datenbanken ausgeführt werden.  
  
2.  Die einzige Möglichkeit, PDW-Datenbanken sichern und Wiederherstellen wird die Datenbank sichern und Wiederherstellen der Datenbank-SQL-Befehle verwendet. Sobald die Sicherungsdaten auf dem backup-Server ist, existiert jedoch als eine Reihe von Windows-Dateien. Sie können die von Ihrem Server an einem anderen Speicherort archivieren der Sicherungsdateien mithilfe der herkömmliche Windows dateibasierte Sicherungsmethoden.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Symbol "Zwischenablage"](media/clipboard-icon.png "zwischenablagesymbol") Kapazität Planungsarbeitsblatt 
  
Drucken Sie dieses Arbeitsblatt, und füllen Sie es mit Ihren eigenen Anforderungen.  
  
|Komponente|Anforderung|Füllen Sie diese Spalte mit Ihren eigenen Anforderungen|Empfehlungen|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Speicherung|Maximale Anzahl Bytes, die Sie auf dem backup-Server auf einen bestimmten Zeitraum speichern möchten.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Herausfinden Sie, um die speicheranforderungen zu bestimmen, wie viele Daten auf dem backup-Server in einen angegebenen Zeitraum gespeichert werden sollen.<br /><br />Die Sicherungsdaten werden auf dem backup-Server in einem komprimierten Format gespeichert. Komprimierungsraten Daten hängen von den Eigenschaften der Daten ab.<br /><br />Zum Beispiel: als eine grobe Schätzung der schätzen ein Komprimierungsverhältnis von 7:1 relativ zur Größe der nicht komprimierten Daten empfohlen. Dies setzt voraus, dass mindestens 80 % der Daten in gruppierte columnstore-Indizes gespeichert werden. Beispielsweise konnte Wenn 700 GB von nicht komprimierten Daten in einer Datenbank und sich in gruppierte columnstore-Indizes befindet, dann Sie schätzen, dass die datenbanksicherung ungefähr 100 GB benötigen.<br /><br />Wenn Sie mehrere Kopien von datenbanksicherungen auf dem backup-Server verwenden möchten, müssen Sie dafür zu berücksichtigen.<br /><br />Zum Beispiel: Wenn Sie beabsichtigen, 10 Datenbanken sichern, die jeweils 5 TB nicht komprimierte Daten enthalten, die Datenbanken eine Gesamtgröße von 50 TB aufweisen. Wenn Sie planen, diese 10 Datenbanken täglich 5 Tage lang in einer Zeile zu sichern, ist die Gesamtgröße des nicht komprimierte 250 TB. Ein Komprimierungsverhältnis von 7:1 datenbankwiederherstellungszeit, benötigen Sie 250 / 7 = 35,7 TB Speicher auf dem backup-Server. Empfohlen wird konservative und abrufen zu 30 % zusätzliche Kapazität Varianzen berücksichtigen und vergrößert.  In diesem Beispiel wäre eine bessere 46,6 TB.|  
|Netzwerk|Netzwerk-Verbindungstyp.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Bestimmen Sie den besten Netzwerkverbindungstyp, der Ihre lastanforderungen-Rate erfüllen kann.<br /><br />Zum Beispiel: InfiniBand oder 10 Gbit-Ethernet-die optimale gebe laden Tarife. 1Gbit Ethernet wird die Last Raten auf 360 GB pro Stunde oder weniger beschränkt.|  
|E/A|Bytes pro Stunde für Schreibvorgänge.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Für das Schreiben von Sicherungen auf Datenträger, 4 TB pro Stunde schreibgeschwindigkeit optimal sind.<br /><br />Zum Beispiel: für die Laufwerke, die 50 MB/s, schreiben können, sollten Sie mindestens 24 Laufwerke sowie mehrere für Spiegelung oder Parität.<br /><br />E/a-Kapazität indexvereinigungen berücksichtigt alle der e/a-Vorgänge auf den Server laden. Verfügt der Server das Laden anderer e/a-Datenverkehr neben riesige Datenmengen, wie z. B. das Empfangen von Datendateien von einem ETL-Server werden die e/a-Anforderungen zu erhöhen.|  
|CPU|Anzahl von Sockets.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Empfangen und Speichern von Sicherungsdateien ist keine CPU-Intensive Anwendung.  Es wird empfohlen, als eine Mindestanforderung unter Verwendung eines 2-Socket-Servers vor kurzem hergestellt.|  
|RAM|GB Arbeitsspeicher, der zum Zwischenspeichern von Dateien während der Windows ermöglicht lädt.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Empfangen und Speichern von Sicherungsdateien erfordert nur wenig Arbeitsspeicher auf dem Server geladen.<br /><br />Um die RAM-Anforderungen zu ermitteln, finden Sie in Ihrer Installation von Windows Server und alle 3rd Party anwendungsanforderungen. Wir empfehlen mindestens 32 GB, wenn Sie nicht den Anforderungen aus anderen Quellen verfügen.|  
  
Wenn Sie bestimmen die kapazitätsanforderungen fertig sind, an zurück, der [erwerben und Konfigurieren eines Servers geladen](acquire-and-configure-loading-server.md) Thema, um Ihre Bestellung zu planen.  
  
## <a name="see-also"></a>Siehe auch  
[Sicherung und Laden von hardware](backup-and-loading-hardware.md)  
  
