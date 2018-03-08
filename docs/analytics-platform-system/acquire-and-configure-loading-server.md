---
title: Erwerben und Konfigurieren eines Servers geladen (SQLServer PDW)
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
description: "Abrufen und einen laden-Server als nicht-Appliance WindowsSystem für die Einreichung von riesige Datenmengen mit SQL Server Parallel Data Warehouse konfigurieren."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: a434b174-a818-4f73-b218-264619bab664
caps.latest.revision: "19"
ms.openlocfilehash: d4a91dc3216945b3f473e1b5b131333ad8d210d3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="acquire-and-configure-a-loading-server"></a>Erwerben und Konfigurieren eines Servers geladen
In diesem Thema wird beschrieben, wie erwerben und Konfigurieren als nicht-Appliance WindowsSystem für die Einreichung von riesige Datenmengen zu SQL Server Parallel Data Warehouse (PDW) eines Servers geladen wird.  
  
## <a name="Basics"></a>Grundlagen  
Der Server laden:  
  
-   Muss sich nicht in einem einzelnen Server sein. Sie können gleichzeitig mit mehreren Servern für das Laden laden.  
  
-   Bereitgestellt und von Ihr IT-Team verwaltet wird. Möglicherweise verfügen Sie bereits einen Server oder Server, die zum Laden von Daten in PDW verwendet werden können.  
  
-   Befindet sich in Ihrem eigenen nicht-Appliance Gestell und kann nicht in das Analytics Platform System-Gerät platziert werden.  
  
-   Ist mit dem Gerät über die Appliance InfiniBand-Netzwerk oder über Ethernet verbunden. Es wird empfohlen, für die Leistung mit InfiniBand.  
  
-   Befindet sich in Ihren eigenen Kundendomäne nicht der Domäne der Anwendung. Es ist keine Vertrauensstellung zwischen Ihrer Kunden und der Appliance-Domäne ein.  
  
## <a name="Step1"></a>Schritt 1: Ermitteln der kapazitätsanforderungen  
Das System laden kann als eine oder mehrere beim Laden von Servern entworfen werden, das gleichzeitige laden auszuführen. Jeder Server laden muss nicht in nur für das Laden, zugewiesen werden, solange sie die Leistung und Speicher die Anforderungen Ihrer arbeitsauslastung behandelt.  
  
Die Systemanforderungen für einen Server laden hängt der eigenen arbeitsauslastung, fast vollständig. Verwenden der [laden Server Kapazität Planungsarbeitsblatt](loading-server-capacity-planning-worksheet.md) feststellen, dass die kapazitätsanforderungen.  
  
## <a name="Step2"></a>Schritt 2: Abrufen der sServer  
Nun, dass Sie die kapazitätsanforderungen besser verstehen, können Sie planen, die Server und Netzwerkkomponenten, die Sie zum Erwerb oder bereitstellen müssen. Integrieren Sie, die folgende Liste von Anforderungen für Ihren Einkauf Plan und erwerben Sie den Server zu oder Bereitstellen Sie einen vorhandenen Server.  
  
### <a name="R"></a>Softwareanforderungen  
Unterstützte Betriebssysteme:  
  
-   WindowsServer 2012 oder Windows Server 2012 R2. Diese Betriebssysteme benötigen die FDR-Netzwerkadapter.  
  
-   Windows Server 2008 R2. Dieses Betriebssystem wird der DDR-Netzwerkadapter benötigt.  
  
Der Server muss das Gebietsschema EN-US verwenden, um das Dwloader laden Command-Line-Tool verwenden. Dwloader unterstützt keine anderen Gebietsschemas.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Netzwerkanforderungen für WindowsServer 2012 und Windows Server 2012 R2  
Obwohl für das Laden von nicht erforderlich ist, ist InfiniBand der empfohlenen Verbindungstyp zum Laden von Servern. Verwenden Sie für optimale Leistung Windows Server 2012 oder Windows Server 2012 R2 und der FDR InfiniBand-Netzwerkadapter auf um den Server Laden mit dem Gerät InfiniBand-Netzwerk zu verbinden.  
  
Zur Vorbereitung einer Verbindungs mit Windows Server 2012 oder Windows Server 2012 R2 InfiniBand:  
  
1.  Planen den Server im rack aus, um das Gerät, damit Sie das Gerät hergestellt werden können InfiniBand-switches zu schließen. Weitere Informationen über Mellanox-Technologien InfiniBand, finden Sie im Whitepaper [Einführung in InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Erwerben Sie einen Netzwerkadapter für Mellanox ConnectX-3 FDR InfiniBand und duale Port. Es wird empfohlen, erwerben den Netzwerkadapter mit zwei Ports für die Fehlertoleranz während der Datenübertragung. Ein Netzwerkadapter zwei Port ist für hohe Verfügbarkeit erforderlich.  
  
3.  Erwerben Sie 2 FDR InfiniBand-Kabel für eine dual-Port-Karte oder 1 FDR InfiniBand-Kabel für einen einzelnen Port-Karte. Die FDR InfiniBand-Kabel verbindet den Server Laden mit dem Gerät InfiniBand-Netzwerk. Die Länge der Kabel hängt von den Abstand zwischen dem Server geladen und die Einheiten InfiniBand-Switches, entsprechend Ihrer Umgebung ab.  
  
## <a name="Step3"></a>Schritt 3: Verbinden Sie den Server mit InfiniBand-Netzwerke  
Gehen Sie folgendermaßen vor, um den Server Laden mit dem InfiniBand-Netzwerk zu verbinden. Wenn der Server das InfiniBand-Netzwerk nicht verwendet wird, überspringen Sie diesen Schritt.  
  
1.  Rack Server schließen genug, um das Gerät, damit Sie die Appliance InfiniBand-Netzwerk hergestellt werden können.  
  
2.  Installieren Sie den InfiniBand Mellanox ConnectX-3 FDR InfiniBand-Netzwerkadapter in den Server geladen.  
  
3.  Verwenden Sie die FDR-Kabel, um InfiniBand-Netzwerkadapter mit einer der zwei InfiniBand-Schalter in der ersten Appliance Rack herstellen.  
  
4.  Installieren Sie und konfigurieren Sie den entsprechenden Windows-Treiber für den InfiniBand-Netzwerkadapter.  
  
    -   InfiniBand-Treiber für Windows sind von der OpenFabrics Alliance, einer Branche Consortium InfiniBand-Hersteller entwickelt.  Der richtige Treiber möglicherweise mit dem InfiniBand-Netzwerkadapter verteilt wurden. Wenn dies nicht der Fall ist, wird der Treiber kann von www.openfabrics.org heruntergeladen werden.  
  
5.  Konfigurieren Sie InfiniBand und DNS-Einstellungen für die Netzwerkadapter. Anweisungen zur Konfiguration finden Sie unter [konfigurieren InfiniBand-Netzwerkadapter](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Schritt 4: Installieren der Tools laden  
Die Clienttools stammen aus dem Microsoft Download Center herunterladen. 

Um Dwloader zu installieren, führen Sie die Installation Dwloader aus den Clienttools aus.
  
Wenn Sie die Integrationsdienste für das Laden verwenden möchten, müssen Sie Integration Services und Integration Services-Zieladapter installieren. Die Adapter werden in den Clienttools verfügbar.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Schritt 5: Starten Sie laden  
Sie sind jetzt bereit, um das Laden von Daten zu starten. Weitere Informationen finden Sie in den folgenden Themen:  
  
1.  [Dwloader laden-Befehlszeilentool](dwloader.md)  
  
2.  [– Übersicht](load-overview.md)  
  
## <a name="performance"></a>Leistung  
Optimale ladeleistung unter Windows Server 2012 und darüber hinaus aktivieren Sie Dateiinitialisierung, damit bei Daten überschrieben werden, das Betriebssystem keine vorhandene Daten mit Nullen überschrieben werden. Ist dies ein Sicherheitsrisiko, da Daten auf den Datenträgern noch vorhanden ist, werden Sie sicher, dass die sofortige Dateiinitialisierung zu deaktivieren.  
  
## <a name="Security"></a>Sicherheit-Hinweise  
Da die zu ladenden Daten nicht auf dem Gerät gespeichert werden, ist Ihr IT-Team zuständig für das Verwalten aller Aspekte der Sicherheit für Ihre Daten zu laden. Beispielsweise schließt dies die Verwaltung der Sicherheit der Daten zu laden, die Sicherheit des Servers verwendet, um Lasten zu speichern und die Sicherheit der Netzwerkinfrastruktur, die der Laden in der SQL Server PDW-Anwendung eine Verbindung herstellt.  
  
> [!IMPORTANT]  
> Es ist besonders wichtig, jeden Server laden zu sichern, die Dwloader laden Command-Line-Tool verwenden. Wenn Dwloader Daten geladen wird, authentifiziert es zuerst mit dem Steuerungsknoten verschoben, und klicken Sie dann nach der erfolgreichen Authentifizierung Daten vom Server laden direkt an den Computeknoten über Datenkanäle. Die Überprüfung des Zertifikats erfolgt nicht während der Hand-Shake zwischen jedem Laden von Server und jeder Serverknoten. Dadurch verbleibt die Serverknoten für Man-in-the-Middle-Angriffe auf jeden Datenkanal während des Ladens verfügbar gemacht. Diese Angriffe können manipulierte und/oder Offenlegung von Informationen führen.  
  
Um Sicherheitsrisiken mit Ihren Daten zu reduzieren, empfehlen wir Folgendes:  
  
-   Legen Sie ein Windows-Konto, das ausschließlich zum Zweck der Laden von Daten in PDW verwendet wird. Ermöglichen Sie diesem Konto Berechtigungen für den Load-Speicherort und an keiner anderen Stelle verfügen.  
  
-   Legen Sie einen PDW-Benutzer, die über Berechtigungen zum Laden von Daten verfügt. Abhängig von Ihren sicherheitsanforderungen könnten Sie einen bestimmten Benutzer pro Datenbank verfügen.  
  
-   Vorgänge auf dem Server laden, können einen UNC-Pfad von dem Pull-Daten von außerhalb des vertrauenswürdigen internen Netzwerks akzeptieren. Und ein Angreifer im Netzwerk oder mit der Möglichkeit, die namensauflösung beeinflussen kann abfangen oder Ändern von Daten in der SQL Server-PDW gesendet. Dies stellt ein Risiko der Offenlegung von Manipulationen und Informationen. Manipulationen sollten Sie minimieren, indem Sie ohne Signaturen für die Verbindung. Um dieses Risiko zu verringern, legen Sie die folgende Gruppe Richtlinienoption **Security-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\sicherheitsoptionen** auf dem Server laden: **Microsoft-Netzwerkclient: Kommunikation digital signieren (immer): Aktiviert**  
  
-   Deaktivieren Sie sofortige Dateiinitialisierung unter Windows Server 2012 und höher. Dies ist ein Kompromiss zwischen Leistung und Sicherheit, wie im Abschnitt Leistung aufgeführt. Sie müssen entscheiden, was am besten gemäß Ihren sicherheitsanforderungen ist.  
  
## <a name="see-also"></a>Siehe auch  
[Sicherung und Wiederherstellung (Übersicht)](backup-and-restore-overview.md)  
  
