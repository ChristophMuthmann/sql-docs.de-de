---
title: Skripterstellung und PowerShell mit Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/14/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 0702fd257a20656ba61ebced29f17a971ee06f45
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Skripterstellung und PowerShell mit Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt eine Vielzahl von Entwicklungs- und Verwaltungsszenarien über Skripts, beispielsweise das Befehlszeilenprogramm RS.exe, PowerShell-Cmdlets für Berichtsserver im SharePoint-Modus und die Nutzung des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Objektmodells in PowerShell für den einheitlichen und den SharePoint-Modus.  
  
-   Administratoren können Skripts in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] erstellen, um das Bereitstellen und Verwalten einer Berichtsserverinstallation zu automatisieren. Zudem können Administratoren [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts generieren und ausführen, mit denen eine Berichtsserver-Datenbank erstellt, konfiguriert und aktualisiert werden kann. Administratoren können auch die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] verfügbaren Funktionen zum Aufzeichnen und Wiedergeben von Skripts verwenden, um routinemäßige Wartungsaufgaben zu automatisieren.  
  
-   Entwickler können benutzerdefinierte Anwendungen erstellen, die Skripts enthalten. Sie können Skripts ausführen, mit denen den Report Server-Webdienst aufgerufen wird. Fast jeder Vorgang, den Sie in verwaltetem Code schreiben können, kann auch als Skript geschrieben werden.  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unterstützt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET-Skript als Skriptsprache, die vom Hilfsprogramm RS.exe, einem auf dem Berichtsserver ausgeführten Skripthost, verarbeitet werden kann.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>PowerShell-Cmdlets für Reporting Services im SharePoint-Modus und Beispiele  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus umfasst [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Cmdlets für die Verwaltung des Berichtsservers.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md) enthält die folgenden Beispiele:  
  
    -   Erstellen einer Dienstanwendung und eines Proxys  
  
    -   Überprüfen und Aktualisieren einer Übermittlungserweiterung  
  
    -   Abrufen und Festlegen von Eigenschaften der Reporting Services-Anwendungsdatenbank, z. B. Timeout der Datenbank  
  
    -   Datenerweiterungen auflisten  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Reporting Services-Objektmodell und Powershell-Beispiele  
 ![PowerShell-Inhalt](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content")  
  
 PowerShell-Aufruf des Kern-Objektmodells und zum größten Teil gültig für SharePoint- und einheitlichen Modus, z. B. die Migrationsarbeit, Abonnementarbeit und weitere Beispiele für Abonnementarbeit in SQL15.  
  
-   [Verwenden von PowerShell, um Reporting Services-Abonnenten zu ändern und aufzulisten sowie ein Abonnement auszuführen](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [Verwenden von PowerShell zum Erstellen einer Azure-VM mit einem Berichtsserver im einheitlichen Modus](http://msdn.microsoft.com/library/azure/dn449661.aspx).  
  
-   Weitere Informationen finden Sie im Abschnitt „Zugriff auf die WMI-Klassen mit PowerShell“ in [Access the Reporting Services WMI Provider](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  

## <a name="rsexe-scripting-samples"></a>Skriptbeispiele für RS.exe  
  
-   [Reporting Services-Beispielskript für "rs.exe" zum Migrieren von Inhalten zwischen Berichtsservern](../../reporting-services/tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
-   Zusätzliche Skripts, Anwendungs- und Erweiterungsbeispiele finden Sie unter [SQL Server Reporting Services-Produktbeispiele](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hilfsprogramm RS.exe &#40;SSRS&#41;](../../reporting-services/tools/rs-exe-utility-ssrs.md)   
 [Skripts für Bereitstellungs- und Verwaltungsaufgaben](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
 [Script with the rs.exe Utility and the Web Service (Skripterstellung mit dem Hilfsprogramm rs.exe und dem Webdienst)](../../reporting-services/tools/script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
