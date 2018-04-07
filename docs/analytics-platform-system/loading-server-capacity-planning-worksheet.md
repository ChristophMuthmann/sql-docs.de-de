---
title: Laden die Server-Arbeitsblatt für Kapazität Planung (SQLServer PDW)
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
description: Mit diesem Arbeitsblatt Kapazität können Sie die Anforderungen für einen Server laden zum Laden von Daten in SQL Server PDW zu bestimmen.
ms.date: 01/05/2017
ms.topic: article
ms.assetid: df2155be-a624-40ba-9a85-58af708f7ce7
caps.latest.revision: 9
ms.openlocfilehash: 73f4b55c82f0b2b5e3c7cb73222a546d3dfc4af6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="loading-server-capacity-planning-worksheet"></a>Laden die Planung Arbeitsblatt für die Server-Kapazität
Mit diesem Arbeitsblatt Kapazität können Sie die Anforderungen für einen Server laden zum Laden von Daten in SQL Server PDW zu bestimmen. Hiermit können Sie Ihren Plan für den Kauf bzw. Bereitstellung vorhandene Server laden erstellen.  
  
## <a name="worksheet-notes"></a>Arbeitsblatt-Hinweise
  
1.  Dieses Arbeitsblatt gilt, für Server, das Laden von Daten mit der **Dwloader** laden-Befehlszeilentool.  
  
2.  Zum Laden von Daten mit Integration Services oder eine dritte Partei laden-Tool aus, können die Anforderungen hängen davon ab Unterschiede in den Ladevorgang.  
  
3.  Die meisten Anforderungen gelten für laden entweder Datendateien komprimierte und nicht komprimierten. Alle Unterschiede hinsichtlich sind fett aufgeführt.  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![Zwischenablage](media/clipboard-icon.png "Zwischenablage") Arbeitsblatt Kapazitätsplanung  
  
Drucken Sie dieses Arbeitsblatt, und füllen Sie es mit Ihren eigenen Anforderungen.  
  
|Komponente|Anforderung|Füllen Sie diese Spalte mit Ihren eigenen Anforderungen|Empfehlungen|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Speicherung|Maximale Anzahl Bytes, die Sie auf dem Server Laden an einen bestimmten Zeitraum speichern möchten.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Herausfinden Sie, um die speicheranforderungen zu bestimmen, wie viele Daten auf dem Server Laden in einen angegebenen Zeitraum gespeichert werden sollen.  Die kapazitätsanforderungen sind Laden nur für Dateien. das Betriebssystem und das Laden Sie Dateien sollten auf anderen Datenträgerarrays befinden.<br /><br />Zum Beispiel: Wenn Sie planen, Laden von 100 GB an Daten vom Datenträger 3 Mal pro Tag, aber löschen die Datendateien nicht bis zum Ende der Woche, benötigen Sie eine minimale 2,1 TB der Datendateien gespeichert. Empfohlen wird konservative und abrufen zu 30 % mehr Speicher Varianzen und Wachstum berücksichtigt.  In diesem Beispiel wäre eine bessere 2,73 TB Speicherplatz.|  
|Load-Rate|Maximale Anzahl Bytes pro Stunde, der in PDW geladen.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Dies ist eine Schätzung. Wenn Sie diese Anforderung zu berechnen, wird davon ausgegangen Sie, dass die Dateien bereits auf dem Server geladen sind und andere Bedingungen verwenden, laden so gut wie möglich sind.<br /><br />Zum Beispiel: nicht erforderlich, da Dwloader nicht komprimierte Daten immer mit den PDW sendet Komprimierbarkeit der Daten zu berücksichtigen. Keine Notwendigkeit, datentypkonvertierungen und die Größe der Zieltabelle zu berücksichtigen.|  
|Netzwerk|Netzwerk-Verbindungstyp.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Bestimmen Sie den besten Netzwerkverbindungstyp für Ihre lastanforderungen-Rate.<br /><br />Zum Beispiel: InfiniBand 10 Gbit-Ethernet-erhalten oder die optimale laden Sätze. 1 Gbit-Ethernet wird die Last Raten auf 360 GB pro Stunde oder weniger beschränkt.|  
|E/A|Bytes pro Stunde für Lese- und Schreibvorgänge.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Um Daten zu laden, muss Dwloader aller Daten vom Datenträger gelesen vor dem Senden mit PDW.<br /><br />Jeder Server Laden von kann nicht Daten geladen schneller als die Appliance Daten aus allen laden Quellen empfangen kann. Um Geld sparen, Planen Sie die e/a, lesen die Kapazität für das Laden, damit der Auslastungskapazität des Geräts nicht überschritten wird.<br /><br />Beispiel:<br />PDW empfängt und lädt Daten in einem 1-Rack-Appliance an eine maximale Rate von 1,8 TB pro Stunde. Für eine Einheit mit 2 oder mehr Racks beträgt die maximale Auslastung Rate 3,6 TB pro Stunde.<br /><br />Wenn Sie beabsichtigen, die gleichzeitig von mehreren Servern für das Laden zu laden, werden die e/a-Anforderungen für jeden Server laden kleiner sein als bei einem Server alle Laden Aktionen ist.<br /><br />Zum Beispiel: eine laden-Server kann maximal 1,8 TB pro Stunde für einen 1-Rack-Appliance laden. Zwei beim Laden der Server konnte jeder gleichzeitig 900 GB pro Stunde in einem 1-Gestell eingebaut geladen werden. Höheres Maß an Parallelität können Effizienz und den maximalen Durchsatz reduzieren.<br /><br />E/a-Kapazität indexvereinigungen berücksichtigt alle der e/a-Vorgänge auf den Server laden. Verfügt der Server das Laden anderer e/a-Datenverkehr neben riesige Datenmengen, wie z. B. das Empfangen von Datendateien von einem ETL-Server werden die e/a-Anforderungen zu erhöhen.<br /><br />Für komprimierte Daten hängen die Komprimierung Datenrate die e/a-Anforderungen. Dwloader liest die komprimierten Daten, und Dekomprimieren es vor dem Senden mit PDW. Je höher die Komprimierungsrate, desto weniger Daten der Server laden müssen vom Datenträger gelesen.<br /><br />Zum Beispiel: Wenn die erforderliche Rate 1,8 TB pro Stunde, und die Daten auf dem Server Laden mit 2:1-Komprimierung gespeichert ist, dann Laden der Server nur 900 GB pro Stunde vom Datenträger anstelle von 1,8 TB zu lesen muss. Ein Komprimierungsverhältnis von 3:1 bedeutet, dass der Server laden muss 600 GB pro Stunde vom Datenträger gelesen.|  
|CPU|Anzahl von Sockets.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Zum Laden von nicht komprimierten Daten, ist Dwloader keine CPU-Intensive Anwendung.  Es wird empfohlen, als eine Mindestanforderung unter Verwendung eines 2-Socket-Servers vor kurzem hergestellt.<br /><br />Zum Laden von komprimierten Daten, benötigen Sie genügend CPU-Leistung auf die Daten vor dem Senden in PDW nicht dekomprimieren. Dwloader kann 10 aktiven Threads gleichzeitig ausführen. Wenn Sie beabsichtigen, 10 komprimierte Dateien gleichzeitig zu laden, wird empfohlen, dass der Server über mindestens eine 10-Core-CPU oder zwei CPUs mit 6 Kernen verfügt.|  
|RAM|GB Arbeitsspeicher, der zum Zwischenspeichern von Dateien während der Windows ermöglicht lädt.|![Stiftsymbol](media/pencil-icon.png "Stiftsymbol")|Dwloader verwendet nur wenig Arbeitsspeicher auf dem Server geladen. Für die Leistung zu erzielen verwendet Windows Arbeitsspeicher zum Laden von Dateien zwischenspeichern, nach der sie vom Datenträger gelesen werden.<br /><br />Um die RAM-Anforderungen zu ermitteln, finden Sie in Ihrer Installation von Windows Server und alle 3rd Party anwendungsanforderungen. Wir empfehlen mindestens 32 GB, wenn Sie nicht den Anforderungen aus anderen Quellen verfügen.<br /><br />Für komprimierte Daten ist ein schneller RAM nützlich, da es die dekomprimierung beschleunigt wird.|  
  
## <a name="see-also"></a>Siehe auch  
[Erwerben und Konfigurieren eines ladenden Servers](acquire-and-configure-loading-server.md)  
[Dwloader Command-Line-Ladeprogramm](dwloader.md)  
  
