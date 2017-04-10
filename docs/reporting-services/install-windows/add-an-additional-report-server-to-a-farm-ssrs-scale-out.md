---
title: "Hinzuf&#252;gen eines zus&#228;tzlichen Berichtsservers zu einer Farm (Horizontales Skalieren f&#252;r SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1a6b683-15cf-44ae-ac60-ceee63a60aaf
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 12
---
# Hinzuf&#252;gen eines zus&#228;tzlichen Berichtsservers zu einer Farm (Horizontales Skalieren f&#252;r SSRS)
  Wenn Sie einen zweiten oder weitere Berichtsserver im SharePoint-Modus zur SharePoint-Farm hinzufügen, können die Leistung und die Antwortzeit für die Verarbeitung des Berichtsservers verbessert werden. Wenn Sie beim Hinzufügen weiterer Benutzer, Berichte und anderer Anwendungen zum Berichtsserver feststellen, dass es zu Leistungseinbußen kommt, kann die Leistung durch das Hinzufügen weiterer Berichtsserver verbessert werden. Es wird außerdem empfohlen, einen zweiten Berichtsserver hinzuzufügen, um die Verfügbarkeit von Berichtsservern zu vergrößern, wenn es Probleme mit der Hardware gibt oder Sie allgemeine Wartungsarbeiten auf einzelnen Servern in der Umgebung durchführen. Ab Version [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] entsprechen die Schritte für horizontales Skalieren einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Umgebung im SharePoint-Modus der Standardbereitstellung von SharePoint-Farmen und nutzen die SharePoint-Lastenausgleichsfunktionen.  
  
> [!IMPORTANT]  
>  Das horizontales Skalieren von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wird nicht in allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt. Weitere Informationen finden Sie im Abschnitt zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
> [!TIP]  
>  Ab Version [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] verwenden Sie nicht mehr den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Konfigurations-Manager, um Server hinzuzufügen und Berichtsserver zu skalieren. SharePoint-Produkte verwalten das horizontale Skalieren von Berichtsdiensten, da SharePoint-Server mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienst der Farm hinzugefügt werden.  
  
 Informationen zum horizontalen Skalieren von Berichtsservern im einheitlichen Modus finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).  
  
##  <a name="bkmk_loadbalancing"></a> Lastenausgleich  
 Der Lastenausgleich von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienstanwendungen wird automatisch von SharePoint verwaltet, außer wenn die Umgebung eine benutzerdefinierte oder eine Drittanbieter-Lastenausgleichslösung hat. Das Standard-SharePoint-Lastenausgleichsverhalten ist, dass jede [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienstanwendung von allen Anwendungsservern ausgeglichen wird, wo Sie den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Dienst gestartet haben. Um zu überprüfen, ob der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienst installiert und gestartet ist, klicken Sie auf **Dienste auf dem Server verwalten** in der SharePoint-Zentraladministration.  
  
##  <a name="bkmk_prerequisites"></a> Voraussetzungen  
  
-   Sie müssen lokaler Administrator sein, um SQL Server-Setup auszuführen.  
  
-   Der Computer muss einer Domäne hinzugefügt werden.  
  
-   Sie müssen den Namen des vorhandenen Datenbankservers wissen, der die SharePoint-Konfiguration und Inhaltsdatenbanken hostet.  
  
-   Der Datenbankserver muss konfiguriert sein, um Remotedatenbankverbindungen zu berücksichtigen.  Wenn nicht, sind Sie nicht in der Lage, den neuen Server zur Farm hinzuzufügen, da der neue Server nicht in der Lage ist, eine Verbindung mit den SharePoint-Konfigurationsdatenbanken herzustellen.  
  
-   Auf dem neuen Server muss die gleiche Version von SharePoint installiert sein, die auf den aktuellen Farmservern ausgeführt wird. Wenn auf der Farm z.B. bereits SharePoint 2013 Service Pack 1 (SP1) installieren ist, müssen Sie SP1 auch auf dem neuen Server installieren, bevor er zur Farm hinzugefügt werden kann.  
  
##  <a name="bkmk_steps"></a> Schritte  
 Die Schritte in diesem Thema gehen davon aus, dass ein SharePoint-Farmadministrator den Server installiert und konfiguriert. Das Diagramm zeigt eine typische dreistufige Umgebung, und die nummerierten Elemente im Diagramm werden in der folgenden Liste beschrieben:  
  
-   (1) Mehrere Web-Front-End (WFE)-Server. Die WFE-Server erfordern das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-In für SharePoint 2016.  
  
-   (2) Ein Einzelanwendungsserver, der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und Websites ausführt, z. B. Zentraladministration. Mit den folgenden Schritte wird dieser Ebene ein zweiter Anwendungsserver hinzugefügt.  
  
-   (3) Zwei SQL Server-Datenbankserver.  
  
-   (4) Stellt eine Software oder eine Hardware-Netzwerklastenausgleichslösung (NLB) dar  
  
 ![Adding a Reporting Services application server](../../reporting-services/install-windows/media/rs-sharepointscale.gif "Adding a Reporting Services application server")  
  
 Die folgenden Schritte gehen davon aus, dass ein Administrator den Server installiert und konfiguriert. Der Server wird als neuer Anwendungsserver in der Farm eingerichtet und nicht als Web-Front-End (WFE) verwendet.  
  
|Schritt|Beschreibung und Link|  
|----------|--------------------------|  
|Fügen Sie einen SharePoint-Server zu einer Farm hinzu.|Sie müssen SharePoint installieren, um eine weitere Reporting Services-Anwendung bereitzustellen.<br/><br/>Für SharePoint 2013 finden Sie Informationen dazu unter [Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx).<br/><br/>Für SharePoint 2016 finden Sie Informationen dazu unter [Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx).|  
|Installieren und konfigurieren Sie Reporting Services im SharePoint-Modus.|Führen Sie die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Installation aus. Weitere Informationen zur Installation des SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [Installieren des ersten Berichtsservers im SharePoint-Modus](http://msdn.microsoft.com/de-de/b29d0f45-0068-4c84-bd7e-5b8a9cd1b538).<br /><br /> Wenn der Server nur als Anwendungsserver verwendet wird und der Server nicht als WFE verwendet wird, müssen Sie **Reporting Services-Add-In für SharePoint-Produkte** nicht auswählen.<br /><br /> 1) Wählen Sie auf der Seite **Setuprolle** die Option **SQL Server-Funktionsinstallation** aus.<br /><br /> 2) Wählen Sie auf der Seite **Funktionsauswahl** die Option **Reporting Services - SharePoint** aus.<br /><br /> 3) Überprüfen Sie auf der Seite **Reporting Services-Konfiguration**, ob die Option **Nur installieren** für **SharePoint-Modus von Reporting Services** aktiviert ist.|  
|Überprüfen Sie, ob der Reporting Services betriebsbereit ist.|1) Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Systemeinstellungen** auf **Server in dieser Farm verwalten**.<br /><br /> 2) Überprüfen Sie den **SQL Server Reporting Services-Dienst**.<br /><br />Weitere Informationen finden Sie unter [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).|  
  
##  <a name="bkmk_additional"></a> Zusätzliche Konfiguration  
 Sie können einzelne [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Server in einer horizontal skalierten Bereitstellung optimieren, um nur die Hintergrundverarbeitung auszuführen, damit sie bei der interaktiven Berichtsausführung keine zusätzlichen Ressourcen verbrauchen. Hintergrundverarbeitung schließt Zeitpläne, Abonnements und Datenwarnungen ein.  
  
 Legen Sie **\<IsWebServiceEnable>** in der Konfigurationsdatei **RSreportServer.config** auf FALSE fest, um das Verhalten einzelner Berichtsserver zu ändern.  
  
 Standardmäßig wird bei der Konfiguration von Berichtsservern der Wert \<IsWebServiceEnable> auf TRUE festgelegt. Wenn alle Server auf TRUE festgelegt werden, besteht bei der interaktiven und Hintergrundverarbeitung ein Lastenausgleich über alle Knoten hinweg in der Farm.  
  
 Wenn Sie bei der Konfiguration sämtlicher Berichtsserver den Wert \<IsWebServiceEnable> auf FALSE festlegen, wird eine Fehlermeldung angezeigt, die der Fehlermeldung ähnelt, die angezeigt wird, wenn Sie versuchen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Funktionen zu verwenden:  
  
      The Reporting Services Web Service is not enabled. Configure at least one instance of the Reporting Services SharePoint Service to have <IsWebServiceEnable> set to true. 
 
 Weitere Informationen finden Sie unter [Ändern einer Reporting Services-Konfigurationsdatei &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
## Siehe auch  
[Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2016](https://technet.microsoft.com/library/cc261752(v=office.16).aspx)  
[Hinzufügen eines SharePoint-Servers zu einer Farm in SharePoint Server 2013](https://technet.microsoft.com/library/cc261752(v=office.15).aspx)
  
  