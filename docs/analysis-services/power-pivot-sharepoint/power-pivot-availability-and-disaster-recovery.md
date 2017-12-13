---
title: Power Pivot-Availability and Disaster Recovery | Microsoft Docs
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
ms.assetid: 4aaf008c-3bcb-4dbf-862c-65747d1a668c
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b2cfe66cc530881a848d7f3d8850c62c0af1486
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="power-pivot-availability-and-disaster-recovery"></a>Verfügbarkeit und Notfallwiederherstellung in PowerPivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Verfügbarkeit und notfallwiederherstellung für Pläne [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] in erster Linie abhängig vom Entwurf der SharePoint-Farm, die Menge des für verschiedene Komponenten akzeptablen Ausfallzeit und Tools und bewährte Methoden, die Sie zur Gewährleistung der Verfügbarkeit zu implementieren. In diesem Thema finden Sie eine Übersicht der Technologien und Beispiele für Topologiediagramme, die beim Planen der Verfügbarkeit und der Notfallwiederherstellung für eine Bereitstellung von [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] hilfreich sein können.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **In diesem Thema:**  
  
-   [SharePoint 2013-Beispieltopologie für Hochverfügbarkeit von Power Pivot](#bkmk_sharepoint2013)  
  
-   [SharePoint 2010-Beispieltopologie für Hochverfügbarkeit von PowerPivot](#bkmk_sharepoint2010)  
  
-   [PowerPivot Dienstanwendungsdatenbank und die Verfügbarkeits- und Wiederherstellungstechnologien in SQL Server](#bkmk_sql_server_technologies)  
  
-   [Links zu weiteren Informationen](#bkmk_more_resources)  
  
##  <a name="bkmk_sharepoint2013">
            </a> SharePoint 2013-Beispieltopologie für Hochverfügbarkeit von Power Pivot  
 Eine Bereitstellung von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 bietet mehr Flexibilität beim Planen der Verfügbarkeit für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . In SharePoint 2013 wird die im SharePoint-Modus bereitgestellte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz, die auch als [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Server bezeichnet wird, außerhalb der SharePoint-Farm ausgeführt und kann auf separaten Servern installiert werden. Jede Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im SharePoint-Modus wird in Excel Services registriert. Der gemeinsame [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienst und die Dienstanwendung werden auf SharePoint-Anwendungsservern ausgeführt.  
  
 Das folgende Diagramm zeigt ein Beispiel für eine Bereitstellung von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013. Dieses Bereitstellungsbeispiel bietet eine gute Verfügbarkeit der [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Dienste und setzt voraus, dass die Datenbanken regelmäßig gesichert werden.  
  
 ![PowerPivot-Verfügbarkeit in 2013](../../analysis-services/power-pivot-sharepoint/media/ssas-powerpivot-services-2013.png "Powerpivot-Verfügbarkeit in 2013")  
  
-   **(1)** Die Web-Front-End-Server. Verwenden Sie das [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013-Add-In, um die Datenanbieter auf jedem Server zu installieren. Weitere Informationen zur Installation finden Sie unter [Installieren oder Deinstallieren des PowerPivot für SharePoint-Add-Ins &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   **(2)** Der gemeinsame [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienst wird **auf jedem** Anwendungsserver ausgeführt, sodass die Dienstanwendung **auf mehreren** Anwendungsservern ausgeführt werden kann. Wenn ein einzelner Anwendungsserver offline geschaltet wird, bleibt die [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Anwendung weiterhin verfügbar.  
  
-   **(3)** Die Dienste für Excel-Berechnungen werden auf jedem Anwendungsserver ausgeführt, sodass die Dienstanwendung auf mehreren Anwendungsservern ausgeführt werden kann. Wenn ein einzelner Anwendungsserver offline geschaltet wird, bleiben die Dienste für Excel-Berechnungen weiterhin verfügbar.  
  
-   **(4)** und **(6)** Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] im SharePoint-Modus werden auf Servern außerhalb der SharePoint-Farm ausgeführt. Dies beinhaltet auch den Windows-Dienst **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])**. Jede dieser Instanzen ist in Excel Services **(3)** registriert. Excel Services verwaltet den Lastenausgleich der Anforderungen an die [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Server. Die [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013-Architektur ermöglicht es Ihnen, mehrere Server für [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] einzurichten, sodass Sie bei Bedarf problemlos weitere Instanzen hinzufügen können. Weitere Informationen finden Sie unter [Verwalten von Excel Services-Datenmodelleinstellungen (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\).aspx).  
  
-   **(5)** SQL Server-Datenbanken, die für Inhalts-, Konfigurations- und Anwendungsdatenbanken verwendet werden. Diese enthalten auch die Datenbank für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung. In Ihrem Plan für die Notfallwiederherstellung muss auch die Datenbankebene berücksichtigt werden. In diesem Entwurf werden die Datenbanken auf demselben Server wie **(4)** eine der [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Instanzen ausgeführt. **(4)** und **(5)** können sich aber auch auf unterschiedlichen Servern befinden.  
  
-   **(7)** Sicherung oder Redundanz für die SQL Server-Datenbank.  
  
##  <a name="bkmk_sharepoint2010">
            </a> SharePoint 2010-Beispieltopologie für Hochverfügbarkeit von PowerPivot  
 Die [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010-Architektur setzt voraus, dass alle [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Komponenten auf denselben SharePoint-Anwendungsservern ausgeführt werden. Dies umfasst auch die im SharePoint-Modus bereitgestellte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz sowie zwei gemeinsame Dienste, im Vergleich zu einem gemeinsamen Dienst in einer SharePoint 2013-Bereitstellung.  
  
 Das folgende Diagramm zeigt ein Beispiel für eine Bereitstellung von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010. Dieses Bereitstellungsbeispiel bietet eine gute Verfügbarkeit der [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Dienste und setzt voraus, dass die Datenbanken regelmäßig gesichert werden.  
  
 ![PowerPivot-Verfügbarkeit in Sharepoint 2010](../../analysis-services/power-pivot-sharepoint/media/ssas-powerpivot-services-2010.png "Powerpivot-Verfügbarkeit in Sharepoint 2010")  
  
-   **(1)** Die Web-Front-End-Server. Installieren Sie die Datenanbieter auf jedem Server. Weitere Informationen finden Sie unter [Installieren des OLE DB-Anbieters für Analysis Services auf SharePoint-Servern](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
-   **(2)** Die zwei gemeinsamen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Dienste und **(4)** der Windows-Dienst **SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])** werden auf den SharePoint-Anwendungsservern installiert.  
  
     Der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst wird **auf jedem** Anwendungsserver ausgeführt, sodass die Dienstanwendung **auf mehreren** Anwendungsservern ausgeführt werden kann. Wenn ein einzelner Anwendungsserver offline geschaltet wird, bleibt die [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Dienstanwendung weiterhin verfügbar.  
  
     Um die Kapazität von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in SharePoint 2010 zu erhöhen, stellen Sie mehr SharePoint-Anwendungsserver bereit, die den [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdienst ausführen.  
  
-   **(3)** Die Dienste für Excel-Berechnungen werden auf jedem Anwendungsserver ausgeführt, sodass die Dienstanwendung auf mehreren Anwendungsservern ausgeführt werden kann. Wenn ein einzelner Anwendungsserver offline geschaltet wird, bleiben die Dienste für Excel-Berechnungen weiterhin verfügbar.  
  
-   **(5)** SQL Server-Datenbanken, die für Inhalts-, Konfigurations- und Anwendungsdatenbanken verwendet werden. Diese enthalten auch die Datenbank für die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung. In Ihrem Plan für die Notfallwiederherstellung muss auch die Datenbankebene berücksichtigt werden.  
  
-   **(6)** Sicherung oder Redundanz für die SQL Server-Datenbank.  
  
##  <a name="bkmk_sql_server_technologies"></a> PowerPivot Dienstanwendungsdatenbank und die Verfügbarkeits- und Wiederherstellungstechnologien in SQL Server  
 Schließen Sie die [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Dienstanwendungsdatenbank in Ihre Hochverfügbarkeitsplanung von SharePoint ein. Der Standardname dieser Datenbank lautet `DefaultPowerPivotServiceApplicationDB-<GUID>`. Im Folgenden finden Sie eine Zusammenfassung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verfügbarkeitstechnologien und Empfehlungen, die Sie mit der [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] Datenbank einsetzen können. Weitere Informationen finden Sie unter [Unterstützte Hochverfügbarkeits- und Notfallwiederherstellungsoptionen für SharePoint-Datenbanken (SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx).  
  
||Kommentare|  
|-|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] und [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] synchrone Spiegelung in einer Farm für die Verfügbarkeit.|Unterstützt, aber nicht empfohlen. Es wird empfohlen, Always On im synchronen Commit-Modus zu verwenden.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] im synchronen Commit-Modus|Unterstützt und empfohlen.|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] asynchrone Spiegelung oder Protokollversand an eine andere Farm für die Notfallwiederherstellung.|Unterstützt.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] mit asynchronem Commit für die Notfallwiederherstellung|Supported|  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Protokollversand  
  
 Weitere Informationen zum Planen eines verzögerten Standbyszenarios für [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]finden Sie unter [PowerPivot-Notfallwiederherstellung](http://social.technet.microsoft.com/wiki/contents/articles/22137.sharepoint-powerpivot-disaster-recovery.aspx).  
  
## <a name="verification"></a>Überprüfung  
 Anweisungen und Skripts zur Überprüfung einer [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] -Bereitstellung vor und nach einer Notfallwiederherstellung finden Sie unter [Prüfliste: Überprüfen von PowerPivot für SharePoint mithilfe von PowerShell](../../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_more_resources"></a> Links zu weiteren Informationen  
  
-   [Unterstützte Hochverfügbarkeits- und Notfallwiederherstellungsoptionen für SharePoint-Datenbanken (SharePoint 2013)](http://technet.microsoft.com/library/jj841106.aspx)  
  
-   [Planen der Notfallwiederherstellung (SharePoint Server 2010)](http://technet.microsoft.com/library/ff628971\(v=office.14\).aspx)  
  
-   [Whitepaper zu Cloud-Sicherung und -Wiederherstellung](http://www.microsoft.com/server-cloud/solutions/cloud-backup-recovery.aspx?WT.srch=1&WT.mc_ID=SEM_BING_USEvergreenSearch_Unassigned&CR_CC=Unassigned#fbid=RjU2Nbzu2dT)  
  
-   [Microsoft® SQL Server Backup to Microsoft Windows® Azure®Tool](http://www.microsoft.com/download/details.aspx?id=40740)  
  
 **Community-Inhalt**  
  
-   [Verwalten von Dienstinstanzen unter SharePoint 2013](http://www.petri.co.il/manage-service-instances-sharepoint-2013.htm)  
  
