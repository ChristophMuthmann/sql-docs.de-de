---
title: Power Pivot-Verwendungsdatenerfassung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f443e4ecb0d6bb16eaf582c89b98af9eb35a25a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="power-pivot-usage-data-collection"></a>Sammlung von Power Pivot-Verwendungsdaten
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sammlung von Verwendungsdaten ist eine SharePoint-Funktion auf Farmebene. [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint verwendet und ergänzt dieses System, damit Berichte im [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard bereitgestellt werden, die die Verwendung von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Daten und -Diensten aufzeigen. Abhängig davon, wie SharePoint installiert wird, kann die Sammlung von Verwendungsdaten für die Farm deaktiviert sein. Ein Farmadministrator muss die Verwendungsprotokollierung aktivieren, damit die Verwendungsdaten für die Darstellung im [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard erstellt werden.  
  
 Informationen zu den Verwendungsdaten im [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard finden Sie unter [PowerPivot-Management-Dashboard und Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
  
##  <a name="usagearch"></a> Sammlung von Verwendungsdaten und Berichtsarchitektur  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]Verwendungsdaten werden gesammelt, Speicherung und Verwaltung mithilfe einer Kombination von Funktionen aus der SharePoint-Infrastruktur und die PowerPivot-Serverkomponenten. Die SharePoint-Infrastruktur umfasst einen zentralen Dienst für Verwendungsdaten und integrierte Zeitgeberaufträge. [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint fügt die längerfristige Speicherung der in der SharePoint-Zentraladministration angezeigten [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten und -berichte hinzu.  
  
 Ereignisinformationen gehen auf dem Anwendungsserver oder Web-Front-End in das System für die Sammlung von Verwendungsdaten ein. Die Verwendungsdaten durchlaufen das System in Reaktion auf Zeitgeberaufträge, durch die Daten aus temporären Datendateien auf dem physischen Server in den persistenten Speicher auf einem Datenbankserver verschoben werden. Das folgende Diagramm veranschaulicht, durch welche Komponenten und Prozesse Verwendungsdaten innerhalb des Datensammlungs- und Berichtssystems verschoben werden.  
  
 **Hinweis:** Vergewissern Sie sich, dass die Sammlung von Verwendungsdaten aktiviert ist. Wechseln Sie dazu in der SharePoint-Zentraladministration zu **Überwachung** . Weitere Informationen finden Sie unter [Konfigurieren der Sammlung von Verwendungsdaten für &#40;PowerPivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 ![Komponenten und Prozesse der verwendungsdatensammlung. ] (../../analysis-services/power-pivot-sharepoint/media/gmni-usagedata.gif "Komponenten und Prozesse der verwendungsdatensammlung.")  
  
|Phase|Description|  
|-----------|-----------------|  
|1|Die Sammlung von Verwendungsdaten wird durch Ereignisse ausgelöst, die von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Komponenten und [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] -Datenanbietern in SharePoint-Bereitstellungen generiert werden. Zu den konfigurierbaren Ereignissen, die aktiviert und deaktiviert werden können, gehören Verbindungsanforderungen, Anforderungen zum Laden und Entladen sowie Ereignisse zu Abfrageantwortzeiten, die vom [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst auf dem Anwendungsserver überwacht werden. Andere Ereignisse, die ausschließlich vom Server verwaltet werden und nicht deaktiviert werden können. Diese beinhalten Datenaktualisierungs- und Serverzustandsereignisse.<br /><br /> Zu Beginn werden Verwendungsdaten unter Verwendung der Datensammlungsfunktionen des SharePoint-Systems in lokalen Protokolldateien gesammelt und gespeichert. Die Dateien und ihr Speicherort sind Teil des Standardsystems zur Sammlung von Verwendungsdaten in SharePoint. Der Speicherort der Dateien ist auf allen Servern in der Farm identisch. Um den Speicherort des Protokollierungsverzeichnisses anzuzeigen oder zu ändern, wechseln Sie in der SharePoint-Zentraladministration zu **Überwachung** und klicken auf **Verwendungs- und Integritätsdatenerfassung konfigurieren**.|  
|2|Der Zeitgeberauftrag „Import der Microsoft SharePoint Foundation-Verwendungsdaten“ verschiebt Verwendungsdaten in geplanten Intervallen (standardmäßig einmal pro Stunde) aus den lokalen Dateien in die Datenbank der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung. Wenn eine Farm mehrere [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendungen enthält, weist jede eine eigene Datenbank auf. Ereignisse enthalten interne Informationen, durch die die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung angegeben wird, von der das Ereignis ausgelöst wurde. Mit den Anwendungsbezeichnern wird sichergestellt, dass Verwendungsdaten an die Anwendung gebunden werden, von der sie erstellt wurden.|  
|3|Die Daten werden in eine interne Berichtsdatenbank kopiert, die über die Zentraladministration für das [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard verfügbar ist.|  
|4|Die Datenquelle ist eine [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe, auf die Sie zum Erstellen benutzerdefinierter Berichte in Excel zugreifen können. Es gibt nur eine Quellarbeitsmappe. Alle lokalisierten Berichte basieren auf derselben Quellarbeitsmappe.|  
|5|Verwendungsdaten zu [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendungen werden Administratoren, die die Serverleistung und -verfügbarkeit verwalten, in Berichtsform zur Verfügung gestellt. Für die von SharePoint unterstützten Sprachen werden lokalisierte Arbeitsmappeninstanzen erstellt. Weitere Informationen finden Sie unter [Berichte zu Verwendungsdaten](#reporting) in diesem Thema.|  
  
##  <a name="sources"></a> Quellen von Verwendungsdaten  
 Wenn die Sammlung von Verwendungsdaten aktiviert ist, werden Daten für die folgenden Serverereignisse generiert.  
  
|Ereignis|Description|Konfigurierbar|  
|-----------|-----------------|------------------|  
|Verbindungen|Serververbindungen, die im Namen eines Benutzers hergestellt wurden, der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Daten in einer Excel-Arbeitsmappe abfragt. Verbindungsereignisse identifizieren den Benutzer, der eine Verbindung mit einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe geöffnet hat. In Berichten werden diese Informationen verwendet, um die häufigsten Benutzer, die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenquellen, auf die von den gleichen Benutzern zugegriffen wird, sowie Verbindungstrends im Zeitverlauf zu identifizieren.|Sie können das [Konfigurieren der Sammlung von Verwendungsdaten für &#40;PowerPivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Abfrageantwortzeiten|Abfrageantwortstatistiken, in denen Abfragen auf Grundlage ihrer Ausführungsdauer kategorisiert werden. Abfrageantwortstatistiken zeigen anhand von Mustern auf, wie viel Zeit der Server zur Beantwortung von Abfrageanforderungen benötigt.|Sie können das [Konfigurieren der Sammlung von Verwendungsdaten für &#40;PowerPivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Ladevorgänge für Daten|[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]-Ladevorgänge für Daten. Datenladeereignisse identifizieren, welche Datenquellen am häufigsten verwendet werden.|Sie können das [Konfigurieren der Sammlung von Verwendungsdaten für &#40;PowerPivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Entladevorgänge für Daten|Entladevorgänge für Daten von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendungen. Ein [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] entlädt inaktive [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Datenquellen, wenn sie nicht verwendet werden, der Server nicht über genügend Arbeitsspeicher verfügt oder zusätzlichen Arbeitsspeicher zum Ausführen von Datenaktualisierungsaufträgen benötigt.|Sie können das [Konfigurieren der Sammlung von Verwendungsdaten für &#40;PowerPivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Serverzustand|Servervorgänge, die den anhand der CPU- und Arbeitsspeicherauslastung ermittelten Serverzustand angeben. Hierbei handelt es sich um Verlaufsdaten. Sie enthalten keine Echtzeitinformationen zur aktuellen Verarbeitungslast des Servers.|Nein. Für dieses Ereignis werden immer Verwendungsdaten gesammelt.|  
|Datenaktualisierung|Durch den [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienst für geplante Datenaktualisierungen initiierte Datenaktualisierungsvorgänge. Der Verwendungsverlauf für Datenaktualisierungen wird auf Anwendungsebene für Betriebsberichte erfasst und auf der Seite Datenaktualisierung verwalten der jeweiligen Arbeitsmappe wiedergegeben.<br /><br /> **Hinweis:** Bei [!INCLUDE[ssSQL11SP1_md](../../includes/sssql11sp1-md.md)] - und SharePoint 2013-Bereitstellungen wird die Datenaktualisierung durch Excel Services und nicht durch den Analysis Services-Server verwaltet.|Nein. Verwendungsdaten für die Datenaktualisierung werden immer gesammelt, wenn Sie die Datenaktualisierung für die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung aktivieren.|  
  
##  <a name="servicesjobs"></a> Dienste und Zeitgeberaufträge  
 In der folgenden Tabelle werden die Dienste sowie Speicherorte für Datensammlungen im System für die Sammlung von Verwendungsdaten beschrieben. Anweisungen zum Überschreiben der zeitgeberauftragsplanung Erzwingen der datenaktualisierung für Integrität und die Verwendung in [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Management-Dashboard-Berichte, finden Sie unter [hier linkbeschreibung eingeben](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md). Sie können die Zeitgeberaufträge in der SharePoint-Zentraladministration einsehen. Wechseln Sie zu **Überwachung**, und klicken Sie auf **Auftragsstatus überprüfen**. Klicken Sie auf **Definitionen für Zeitgeberauftrag überprüfen**.  
  
|Komponente|Standardzeitplan|Description|  
|---------------|----------------------|-----------------|  
|SharePoint-Zeitgeberdienst (SPTimerV4)||Dieser Windows-Dienst wird lokal auf jedem Mitgliedscomputer in der Farm ausgeführt und verarbeitet alle auf Farmebene definierten Zeitgeberaufträge.|  
|Microsoft SharePoint Foundation für den Import von Verwendungsdaten|In SharePoint 2010 alle 30 Minuten. In SharePoint 2013 alle 5 Minuten.|Dieser Zeitgeberauftrag wird global auf Farmebene konfiguriert. Er verschiebt Verwendungsdaten aus lokalen Verwendungsprotokolldateien in die zentrale Datenbank für Verwendungsdaten. Sie können diesen Zeitgeberauftrag manuell ausführen, um einen Datenimportvorgang zu erzwingen.|  
|Microsoft SharePoint Foundation-Zeitgeberauftrag für die Verarbeitung von Verwendungsdaten|Täglich um 3:00 VORMITTAGS|Ab SQL Server 2012 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint wird dieser Zeitgeberauftrag für Upgrade- oder Migrationsszenarios unterstützt, falls noch ältere Verwendungsdaten in den SharePoint-Verwendungsdatenbanken enthalten sind. Ab SQL Server 2012 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint wird die SharePoint-Verwendungsdatenbank weder für die Sammlung von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten noch für den Workflow des Management-Dashboards verwendet. Der Zeitgeberauftrag kann manuell ausgeführt werden, um verbliebene [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -bezogene Daten in der SharePoint-Verwendungsdatenbank in die Datenbanken der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung zu verschieben.<br /><br /> Dieser Zeitgeberauftrag wird global auf Farmebene konfiguriert. Er überprüft die zentrale Datenbank für Verwendungsdaten auf abgelaufene Verwendungsdaten (d. h. auf Datensätze, die älter als 30 Tage sind). Für [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Server in der Farm führt dieser Zeitgeberauftrag eine zusätzliche Überprüfung auf [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten aus. Wenn [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten erkannt werden, verschiebt der Zeitgeberauftrag die Daten in die Datenbank einer Dienstanwendung und verwendet dabei den Anwendungsbezeichner, um die richtige Datenbank zu identifizieren.<br /><br /> Sie können diesen Zeitgeberauftrag manuell ausführen, um eine Überprüfung auf abgelaufene Daten oder einen Import von [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Verwendungsdaten in die Datenbank einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung zu erzwingen.|  
|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard – Zeitgeberauftrag für die Verarbeitung|Täglich um 3:00 VORMITTAGS|Dieser Zeitgeberauftrag aktualisiert die interne [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappe, die Verwaltungsdaten für das [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard enthält. Er ruft aktualisierte Informationen ab, die von SharePoint verwaltet werden, einschließlich Servernamen, Benutzernamen, Anwendungsnamen und Dateinamen, die in Dashboardberichten oder Webparts angezeigt werden.|  
  
##  <a name="reporting"></a> Berichte zu Verwendungsdaten  
 Sie können integrierte Berichte im [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Management-Dashboard anzeigen, um Verwendungsdaten zu [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Daten anzuzeigen. In den integrierten Berichten werden Verwendungsdaten konsolidiert, die aus Berichtsdatenstrukturen in der Datenbank der Dienstanwendung abgerufen werden. Da die zugrunde liegenden Berichtsdaten täglich aktualisiert werden, enthalten die integrierten Verwendungsberichte erst aktuelle Informationen, nachdem die Daten vom Microsoft SharePoint Foundation-Zeitgeberauftrag für die Verarbeitung von Verwendungsdaten in die Datenbank einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Dienstanwendung kopiert wurden. Standardmäßig geschieht dies einmal am Tag.  
  
 Weitere Informationen zum Anzeigen von Berichten finden Sie unter [PowerPivot-Management-Dashboard und Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Siehe auch  
 [PowerPivot-Management-Dashboard und Verwendungsdaten](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)   
 [Konfigurationseinstellungsverweis &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
