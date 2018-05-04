---
title: Power Pivot-Serververwaltung und-Konfiguration in der Zentraladministration | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e14e6068bc5d6538eab1ec13c3a3cc37ed34fb61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-server-administration-and-configuration-in-central-administration"></a>PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Die -Serververwaltung und -Konfiguration wird mithilfe der SharePoint-Zentraladministration von SharePoint Service-Anwendungsadministratoren ausgeführt.  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint muss konfiguriert werden, bevor es verwendet werden kann. Nachdem Sie [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint mithilfe des SQL Server-Setups installiert haben, können Sie es wie folgt konfigurieren:  
  
-   [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Konfigurationstool oder [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint 2013-Konfigurationstool  
  
-   SharePoint-Zentraladministration  
  
-   PowerShell-Cmdlets  
  
 Alle drei Ansätze sorgen für einen vollständig konfigurierten Server.  
  
 Dieser Abschnitt umfasst Tasks zum Konfigurieren der Software mit Zentraladministration. Sie müssen sämtliche drei der erforderlichen unten in der Liste aufgeführten Konfigurationstasks ausführen.  
  
> [!IMPORTANT]  
>  Für SharePoint 2010 muss SharePoint 2010 Service Pack 1 (SP1) installiert sein, bevor Sie [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint oder eine SharePoint-Farm konfigurieren können, die einen [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Datenbankserver verwendet. Wenn Sie das Service Pack noch nicht installiert haben, holen Sie dies jetzt nach, bevor Sie mit der Serverkonfiguration beginnen.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-central-administration"></a>Vorteile einer Konfiguration von PowerPivot für SharePoint mithilfe der Zentraladministration  
 SharePoint-Zentraladministration ist die Administratoranwendung einer SharePoint-Farm. Wenn Sie Farmadministrator sind, ziehen Sie es beim Hinzufügen einer [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint-Instanz zur Farm eventuell vor, ein vertrautes Tool zu verwenden.  
  
 Im Gegensatz zu [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Konfigurationstools oder PowerShell-Cmdlets, bietet die Zentraladministration Seiten, über die beim Konfigurieren einer Anwendung oder eines Servers alle Optionen angegeben werden, die Sie festlegen können. Andere Ansätze komprimieren entweder den Konfigurationsworkflow in eine geringere Anzahl von Schritten oder erfordern vorheriges Wissen darüber, wie ein SharePoint-Server mit PowerShell konfiguriert wird.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [PowerPivot-Konfiguration mit Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [Power Pivot-Konfigurationstools](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Link|Typ|Taskbeschreibung|  
|----------|----------|----------------------|  
|[Bereitstellen von Power Pivot-Lösungen in SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)|Erforderlich|Bei diesem Schritt werden die Projektmappendateien installiert, über die der Farm und den Websitesammlungen Programmdateien und Anwendungsseiten hinzugefügt werden.|  
|[Erstellen und Konfigurieren einer PowerPivot-Dienstanwendung in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)|Erforderlich|Mit diesem Schritt wird der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Systemdienst bereitgestellt.|  
|[Aktivieren der PowerPivot-Funktionsintegration für Websitesammlungen in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|Erforderlich|Mit diesem Schritt werden [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Funktionen auf Websitesammlungsebene aktiviert.|  
|[Hinzufügen von MSOLAP.5 als vertrauenswürdigen Datenanbieter in Excel Services](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|Required|Mit diesem Schritt wird der OLE DB-Anbieter für Analysis Services als vertrauenswürdiger Anbieter in Excel Services hinzugefügt.|  
|[PowerPivot-Datenaktualisierung mit SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)|Empfohlen|Eine Datenaktualisierung ist optional, wird aber empfohlen. Dies ermöglicht es Ihnen, unbeaufsichtigte Updates der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Daten in veröffentlichten Excel-Arbeitsmappen zu planen.|  
|[Konfigurieren des PowerPivot-Kontos für die unbeaufsichtigte Datenaktualisierung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)|Empfohlen|Mit diesem Schritt wird ein zweckgebundenes Konto bereitgestellt. Dieses kann dazu verwendet werden, um Datenaktualisierungsaufträge auf dem Server auszuführen.|  
|[Konfigurieren der Sammlung von Verwendungsdaten für Power Pivot für SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|Optional|Die Verwendung der Datensammlung wird standardmäßig konfiguriert. Sie können die Standardeinstellungen mithilfe dieser Schritte ändern.|  
|[Konfigurieren der dedizierten Datenaktualisierung oder reinen Abfrageverarbeitung (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/5e027605-1086-4941-bb01-f315df8f829b)|Optional|Eine [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Instanz kann ausschließlich Datenaktualisierungsaufträgen oder Abfragen zugeordnet sein. Außerdem können Sie Standardeinstellungen zu parallelen Datenaktualisierungsaufträgen ändern.|  
|[Konfigurieren von Power Pivot-Dienstkonten](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)|Optional|Hier wird erläutert, wie Kennwörter oder Änderungsdienstkonten aktualisiert werden.|  
|[Verbinden einer PowerPivot-Dienstanwendung mit einer SharePoint-Webanwendung in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|Optional|Hier wird erläutert, wie Dienstzuordnungen geändert werden.|  
|[Erstellen eines vertrauenswürdigen Speicherorts für Power Pivot-Websites in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|Optional|Hier wird erläutert, wie der [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Katalog als vertrauenswürdiger Speicherort hinzugefügt wird.|  
|[Konfigurieren und Anzeigen der SharePoint-Protokolldateien und -Diagnoseprotokollierung &#40;PowerPivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)|Optional|Die Ereignisprotokollierung wird standardmäßig konfiguriert. Sie können die Standardeinstellungen mithilfe dieser Schritte ändern.|  
|[Konfigurieren von Power Pivot-Integritätsregeln](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)|Optional|Serverintegritätsregeln werden standardmäßig konfiguriert. Sie können mithilfe dieser Schritte einige der Standardeinstellungen ändern.|  
|[Erstellen und Anpassen von PowerPivot-Katalogen](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)|Optional|Hinsichtlich der Installationen, die Sie manuell konfigurieren, wird über diese Prozedur erläutert, wie eine [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Katalogbibliothek erstellt wird, die Bildminiaturansichten der in ihr enthaltenen [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappen anzeigt.|  
|[Hinzufügen eines BI-Semantikmodell-Verbindungs-Inhaltstyps zu einer Bibliothek &#40;PowerPivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)|Optional|Hier wird erläutert, wie eine Dokumentbibliothek erweitert wird, um die Erstellung von Verbindungsdateien des BI-Semantikmodells zu unterstützen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Installation von PowerPivot für SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [Konfigurationseinstellungsverweis &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Notfallwiederherstellung für PowerPivot für SharePoint](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
