---
title: Überwachung mit Admin-Konsole – Analytics Platform System | Microsoft Docs
description: Für Analytics Platform System stellt die Verwaltungskonsole für eine Webanwendung, die die Appliance Zustand, Integrität und Leistung Informationen bereitstellt. Benutzer eine Verbindung herstellen, um die Verwaltungskonsole über einen Internet-Browser.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5f7c6ef68a8f91121a63def8e2153a5c38873aa3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>Überwachen Sie die Einheit mit der Verwaltungskonsole - Analyseplattformsystem
Die Verwaltungskonsole ist eine SQL Server PDW-Webanwendung, die die Appliance Zustand, Integrität und Leistung Informationen bereitstellt. Benutzer eine Verbindung herstellen, um die Verwaltungskonsole über Internet Explorer.  
  
## <a name="About"></a>Informationen zur Verwaltungskonsole  
![Anwendungskonsole, Home](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Appliance**  
Home  
Bietet eine kurze Zusammenfassung des Status Appliance.  
  
Integrität  
Zeigt die Anwendungstopologie mit Indikatoren zeigt die Integrität der einzelnen überwachten Komponenten innerhalb eines jeden Knotens. Können Sie den aktuellen Status der einzelnen Knoten und Eigenschaften der Komponenten Knoten anzuzeigen.  
  
Werden Warnungen von Hardware und Software angezeigt.  
  
Systemmonitor  
Zeigt Diagramme für die Performance Monitor an.  
  
**Parallel Data Warehouse**  
Home  
Enthält eine kurze Zusammenfassung des PDW-Status.  
  
Sitzungen  
Zeigt aktive Sitzungen von PDW-Benutzer. Dies kann helfen, für die Überwachung Ressourcenkonflikte.  
  
Abfragen  
Zeigt eine Liste der ausgeführten Abfragen und zuletzt abgeschlossenen Abfragen. Verwandte Fehler werden angezeigt, sofern vorhanden. Außerdem bietet die Möglichkeit zum Anzeigen von Details der Ausführungsinformationen für die Abfrage Ausführung planen und Knoten.  
  
Lädt  
Zeigt geladen werden Pläne, die den aktuellen Status der Laden von PDW sowie verwandte Fehler, sofern vorhanden.  
  
Sicherungen/Wiederherstellungen  
Zeigt ein Protokoll von PDW sicherungs- und Wiederherstellungsvorgänge.  
  
Integrität  
Zeigt die PDW-Topologie mit Indikatoren zeigt die Integrität der einzelnen überwachten Komponenten innerhalb eines jeden Knotens. Können Sie den aktuellen Status der einzelnen Knoten und Eigenschaften der Komponenten Knoten anzuzeigen.  
  
Werden Warnungen von Hardware und Software angezeigt.  
  
Ressourcen  
Zeigt eine Liste der PDW-Ressourcensperren und ihren aktuellen Status.  
  
Speicherung  
Enthält eine Zusammenfassung der PDW-speicherauslastung.  
  
Systemmonitor  
Zeigt Diagramme für die PDW Performance Monitor an.  
  
**HDInsight**  
Home  
Enthält eine kurze Zusammenfassung des HDInsight-Status.  
  
HDFS  
Fasst die speicherplatzausnutzung HDInsight, und listet die Top 10 Speicherplatz Consumer.  
  
Zuordnen/reduzieren  
Fasst den Status der MapReduce-Aufträge an.  
  
Integrität  
Zeigt die HDInsight-Topologie mit Indikatoren zeigt die Integrität der einzelnen überwachten Komponenten innerhalb eines jeden Knotens. Können Sie den aktuellen Status der einzelnen Knoten und Eigenschaften der Komponenten Knoten anzuzeigen.  
  
Werden Warnungen von Hardware und Software angezeigt.  
  
Speicherung  
Enthält eine Zusammenfassung der HDInsight-speicherauslastung.  
  
Systemmonitor  
Zeigt Diagramme für die Performance Monitor an.  
  
> [!NOTE]  
> Die-Verwaltungskonsole verfügt über eine Auflösung von 1024 x 768. Die Administratorkonsole zeigt am besten mit einer Bildschirmauflösung von 1280 X 1024 oder höher.  
  
## <a name="Connect"></a>Herstellen einer Verbindung mit der Verwaltungskonsole  
Verbindung mit der Verwaltungskonsole erfordert:  
  
-   AT Internet Explorer Version 10.  
  
-   Berechtigungen für die Verwaltungskonsole zugreifen. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Die IP-Adresse des Clusters mit Knoten Steuerelement.  Rufen Sie dies von den SQL Server PDW-Administrator.  
  
Verwenden Sie zur Verbindung mit der Verwaltungskonsole Internet Explorer- und Https, um die IP-Adresse des Clusters mit Knoten Steuerelement zu suchen. Wenn die IP-Adresse des Clusters mit Knoten Steuerelement ist beispielsweise `10.192.63.102`, geben Sie `https://10.192.63.102` in der Adressleiste des Browsers. Der erste Bildschirm fordert Ihre **Anmeldung** und **Kennwort**. Geben Sie entweder eine Anmeldung für SQL Server-Authentifizierung und ein Kennwort oder eine Windows-authentifizierte Anmeldung und Windows-Kennwort ein. Wenn Sie einen Anmeldenamen für Windows-Authentifizierung verwenden, wird der Verwaltungskonsole Identitätswechsel verwendet werden.  
  
## <a name="RelatedTasks"></a>Admin-Konsolentasks  
Die Admin-Konsole bietet die Möglichkeit zur Überwachung der folgenden:  
  
|||  
|-|-|  
|**Informationstyp**|**Vorgehensweise beim Zugriff in der Verwaltungskonsole**|  
|Gesamtstatus des Geräts|Klicken Sie auf **Anwendungszustand** im oberen Menü oder **Home**.|  
|Warnungen|Klicken Sie auf **Warnungen**. Weitere Informationen finden Sie unter [Grundlegendes zu Admin-Konsole Warnungen &#40;Analyseplattformsystem&#41;](understanding-admin-console-alerts.md).|  
|Appliance-Komponenten und deren status|Klicken Sie auf **Anwendungszustand** im oberen Menü oder **Home**.|  
|Monitor-Anforderungen (einschließlich Abfragen, lädt, Sicherungen und Wiederherstellungen)|Klicken Sie auf **Sitzungen** , die derzeit aktive oder aktuelle Sitzungen finden Sie unter.<br /><br />Klicken Sie auf **Abfragen** , die derzeit aktive oder aktuelle Abfragen finden Sie unter. Die für Abfragen angezeigten Informationen gehören lädt, Sicherungen und Wiederherstellungen.<br /><br />Klicken Sie auf **Sperren** zu aktiven Sperren finden Sie unter.|  
|Zusätzliche Informationen für lädt, Sicherungen und Wiederherstellungen zu überwachen.|Klicken Sie auf **lädt** oder **Sicherungen/Wiederherstellungen**.|  
|Leistungsinformationen|Klicken Sie auf **Systemmonitor**.|  
  
## <a name="see-also"></a>Siehe auch  
[Überwachen der Appliance &#40;Analyseplattformsystem&#41;](appliance-monitoring.md)  
  
