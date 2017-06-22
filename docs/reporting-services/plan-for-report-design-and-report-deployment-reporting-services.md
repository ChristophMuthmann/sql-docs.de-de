---
title: Planen von Berichtsentwurf und-Bereitstellung | Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 09/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
caps.latest.revision: 19
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 69c0ea4110b678e9bffa959992d48f2c28df5897
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="plan-for-report-design-and-report-deployment--reporting-services"></a>Planen von Berichtsentwurf und -bereitstellung | Reporting Services
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] bietet eine Reihe von Ansätzen zum Erstellen und Bereitstellen von paginierten Berichten. Erhalten Sie Informationen, wie Sie eine Umgebung für die Berichterstellung und einen Berichtsserver planen, die reibungslos zusammenarbeiten.

Dieses Thema bietet eine Übersicht über die Unterstützung der Berichtsdefinition durch [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Komponenten. Eine Berichtsdefinition ist eine XML-Datei, die in der Berichtsdefinitionssprache (Report Definition Language, RDL) oder in der Berichtsdefinitionssprache für Clients (Report Definition Language for Clients, RDLC) geschrieben ist. Jede Berichtsdefinition entspricht einer bestimmten Schemaversion, die am Anfang der Datei aufgelistet ist.  
  
 RDL-Dateien werden im Berichts-Designer in [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] -Projekten erstellt, sowie im Berichts-Generator. RDLC-Dateien werden mit den ReportViewer-Steuerelementen erstellt, die in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]enthalten sind.
  
##  <a name="bkmk_rdl_schema_versions"></a> RDL-Schemaversionen  
 In der folgenden Tabelle sind alle verfügbaren Schemaversionen und die in diesem Thema verwendeten Abkürzungen der Schemaversionen aufgeführt:  
  
|Abkürzung|Schemaversion|  
|------------------|--------------------|  
|2016 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2016/01/reportdefinition`|
|2010 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition`|  
|2008 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition`|  
|2005 RDL<br /><br /> 2005 RDLC|`http://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition`|  
|2000 RDL|`http://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition`|  
  
 Weitere Informationen zu RDL und RDL-Schemas finden Sie in den folgenden Themen:  
  
-   [Microsoft SQL Server XML-Schemas](http://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [Spezifikationen der Berichtsdefinitionssprache](http://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [Berichtsdefinitionssprache (Report Definition Language, RDL) &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
 Weitere Informationen zu ReportViewer-Steuerelementen finden Sie unter [ReportViewer-Steuerelemente (Visual Studio)](http://msdn.microsoft.com/library/ms251671.aspx).  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a> Unterstützung von Berichtsservern und RDL-Schemas  
 Eine Berichtsdefinitionsdatei kann wie folgt auf einem [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] -Berichtsserver bereitgestellt werden:  
  
-   **Berichts-Designer:** Stellen Sie einen Bericht im Berichts-Designer in [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]bereit.  
  
-   **Report-Generator:** Speichern Sie einen Bericht aus dem Berichts-Generator auf dem Berichtsserver.  
  
-   **Webportal:** Laden Sie einen Bericht aus dem [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]auf einen Berichtsserver im einheitlichen Modus hoch.  
  
-   **SharePoint:** Laden Sie einen Bericht auf eine SharePoint-Website hoch, die mit einem Berichtsserver im SharePoint-Modus konfiguriert wurde.  
  
-   **Programmgesteuert:** Veröffentlichen Sie einen Bericht programmgesteuert mithilfe der SOAP-API-Schnittstellen auf einem Berichtsserver. Weitere Informationen finden Sie unter [Report Server Web Service](../reporting-services/report-server-web-service/report-server-web-service.md).  
  
 In der folgenden Tabelle werden die unterstützten RDL-Schemaversionen nach Versionen des Berichtsservers aufgelistet.  
  
|Berichtsserverversion|RDL-Schemaversion|  
|---------------------------|------------------------|  
|SQL Server 2016|2016 RDL<br /><br />2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> oder<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> oder<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|2010 RDL<br /><br /> 2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|2008 RDL<br /><br /> 2005 RDL<br /><br /> 2000 RDL|  
  
 Wenn Sie eine Berichtsdefinition auf den Berichtsserver hochladen oder ein Upgrade eines Berichtsservers ausführen, auf dem Berichte vorhanden sind, wird auf dem Berichtsserver die Berichtsdefinition im ursprünglichen Format beibehalten. **Bei der ersten Verwendung**aktualisiert der Berichtsserver den Bericht in der Berichtsserver-Datenbank auf ein binäres Format, das für nachfolgende Sichten beibehalten wird. Die Berichtsdefinition (.rdl) selbst wird nicht aktualisiert.  
  
 Sie können vom Berichtsserver eine schreibgeschützte Kopie der Berichtsdefinitionsdatei (.rdl) extrahieren. Navigieren Sie auf einem Berichtsserver im einheitlichen Modus zum [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], wählen Sie den Bericht aus, und klicken auf **Herunterladen**. Wechseln Sie in einer Bereitstellung im SharePoint-Modus zur Dokumentbibliothek, wählen Sie den Bericht aus, und klicken Sie auf **Kopie herunterladen**.  
  
 Um die Berichtsdefinition zu aktualisieren, müssen Sie den Bericht in einer Berichterstellungsumgebung wie SQL Server Data Tools oder Berichts-Generator öffnen und speichern.  
  
 Weitere Informationen über Berichtsupgrades und die unterstützten Schemaversionen finden Sie unter [Aktualisieren von Berichten](../reporting-services/install-windows/upgrade-reports.md).  
  
##  <a name="bkmk_report_authoring_and_deployment"></a> Unterstützung von Berichterstellung und -bereitstellung  
 Berichterstellungsumgebungen sind der Berichts-Designer in [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] -Projekten sowie der Berichts-Generator. Berichterstellungsumgebungen bieten viele Arten der Unterstützung für Berichtsupgrades, den Berichtsentwurf, die Berichtsvorschau im lokalen Modus, die Berichtsvorschau auf dem Berichtsserver sowie die Berichtsbereitstellung.  
  
 In der folgenden Tabelle wird die Unterstützung für das Erstellen und Bereitstellen von Berichtsdefinitionen für unterschiedliche Schemaversionen zusammengefasst:  
  
|Berichterstellungsumgebung|Erstellte RDL-Version|Bereitstellen der RDL-Version|Bereitstellen für Berichtsserverversionen|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|SQL Server 2016-Berichts-Generator|Erstellt 2016 RDL<br /><br /> Führt für ältere Versionen von RDL ein Upgrade auf 2016 RDL aus.|2016 RDL|SQL Server 2016|
|Berichts-Designer in SQL Server 2016 Data Tools – Business Intelligence für Microsoft Visual Studio 2015|Erstellt 2016 RDL<br /><br /> Führt für ältere Versionen von RDL ein Upgrade auf 2016 RDL aus.|2016 RDL|SQL Server 2016|
|Berichts-Designer in SQL Server 2014 Data Tools – Business Intelligence für Microsoft Visual Studio 2012<br /><br /> oder<br /><br /> Berichts-Designer in SQL Server 2012 Data Tools – Business Intelligence für Microsoft Visual Studio 2012<br /><br /> oder<br /><br /> Berichts-Designer in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Data Tools, enthalten in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].|Erstellt 2010 RDL<br /><br /> Führt für ältere Versionen von RDL ein Upgrade auf 2010 RDL aus.|2010 RDL|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Berichts-Designer in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio|Erstellt 2010 RDL<br /><br /> Führt für ältere Versionen von RDL ein Upgrade auf 2010 RDL aus.|2010 RDL|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Berichts-Designer in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio|Autoren 2008 RDL<br /><br /> Führt für ältere Versionen von RDL ein Upgrade auf 2008 RDL aus.|2008 RDL|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|
  
 Weitere Informationen zu SQL Server Data Tools (SSDT) finden Sie in den folgenden Themen:  
  
-   [Bereitstellung und Versionsunterstützung in SQL Server Data Tools &#40;SSRS&#41;](../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [SQL Server Data Tools für Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx)  
  
##  <a name="bkmk_reportviewer"></a> ReportViewer-Steuerelemente  
 Ein [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ReportViewer-Steuerelement kann einen RDLC-Bericht im lokalen Vorschaumodus oder im Remotemodus anzeigen; das Steuerelement kann eine RDL-Datei anzeigen, die auf einem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -Berichtsserver gehostet wird. In der folgenden Tabelle sind die RDL-Versionen aufgelistet, die von den ReportViewer-Steuerelementen für die lokale Verarbeitung (.rdlc) unterstützt werden. Informationen zur serverseitigen RDL-Unterstützung finden Sie im Abschnitt [Unterstützung von Berichtsservern und RDL-Schemas](#bkmk_report_server_rdl_schema_support).  
  
|ReportViewer-Steuerelement im Produkt|RDL-Version für lokale Vorschau|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2015 <br/><br/>oder<br/><br/>[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> oder<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> oder<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|2008 RDL|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> oder<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|2005 RDL|  
  
 Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [Konvertieren von RDLC-Dateien in RDL-Dateien](http://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [ReportViewer-Steuerelemente (Visual Studio)](http://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [Hinzufügen und Konfigurieren der ReportViewer-Steuerelemente](http://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>Siehe auch  
 [Berichte, Berichtsteile und Berichtsdefinitionen &#40;Berichts-Generator und SSRS&#41;](../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Reporting Services-Tools](../reporting-services/tools/reporting-services-tools.md)   
 [Berichtsdefinitionssprache (Report Definition Language, RDL) &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  

