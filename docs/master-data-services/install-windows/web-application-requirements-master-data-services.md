---
title: "Anforderungen f&#252;r die Webanwendung (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "Master Data Services"
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
caps.latest.revision: 40
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 38
---
# Anforderungen f&#252;r die Webanwendung (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ist eine Webanwendung, die von den Internetinformationsdiensten (IIS) gehostet wird. [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] funktioniert nur in Internet Explorer 9 oder höher. Internet Explorer 8 und frühere Versionen, Microsoft Edge und Chrome werden nicht unterstützt.  
  
 Verwenden Sie [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] zum Erstellen und Konfigurieren der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung. [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] konfiguriert IIS auf dem lokalen Computer und eignet sich deshalb besonders für Aufgaben in Verbindung mit der anfänglichen Webkonfiguration. Konfigurieren Sie z.B. eine [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Umgebung mit einer einzelnen [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webanwendung, oder konfigurieren Sie die erste Webanwendung in einer [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Bereitstellung für horizontales Skalieren. Verwenden Sie IIS-Tools, um komplexere Aufgaben, z. B. das Konfigurieren mehrerer Webserver in einer Bereitstellung für horizontales Skalieren, auszuführen.  
  
> [!NOTE]  
>  Jeder Computer, auf dem Sie Komponenten von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] installieren, muss lizenziert werden. Weitere Informationen finden Sie im Endbenutzerlizenzvertrag (End User License Agreement, EULA).  
  
## Anforderungen  
  
### Betriebssystem  
 Überprüfen Sie vor der Installation von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] folgende Voraussetzungen:    
    
-   [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)    
  
### Microsoft Silverlight  
 Um in der [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung zu arbeiten, muss Silverlight 5 auf dem Clientcomputer installiert sein. Falls Sie nicht über die erforderliche Version von Silverlight verfügen, werden Sie aufgefordert, diese zu installieren, wenn Sie zu einem Bereich der Webanwendung navigieren, in dem sie erforderlich ist. Sie können Silverlight 5 von [hier](http://go.microsoft.com/fwlink/?LinkId=243096)installieren.  
  
### Rolle und Rollendienste  
 Unter Windows Server 2012 oder Windows Server 2012 R2 können Sie den **Server-Manager** in der Microsoft Management Console (MMC) verwenden, um die Rolle **Webserver (IIS)** und die erforderlichen Rollendienste zu installieren.  
 
 
> [!IMPORTANT]  
>Die **Komprimierung dynamischer Inhalte** ist standardmäßig aktiviert. Dadurch wird die Größe der XML-Antwort erheblich verringert und die Netzwerk-E/A reduziert, obwohl die CPU-Auslastung erhöht wird.  Weitere Informationen finden Sie unter **[CTP 2.0] Verbesserte Leistung** in [Neuigkeiten (Master Data Services) &#40;MDS&#41;](../../master-data-services/what-s-new-in-master-data-services-mds.md).  
  
||  
|-|  
|Internetinformationsdienste (IIS)<br /><br /> Webverwaltungstools<br /><br /> IIS-Verwaltungskonsole<br /><br /> WWW (World Wide Web)-Dienste<br /><br /> Anwendungsentwicklung<br /><br /> .NET-Erweiterbarkeit 3.5<br /><br /> .NET-Erweiterbarkeit 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> ISAPI-Erweiterungen<br /><br /> ISAPI-Filter<br /><br /> Allgemeine HTTP-Funktionen<br /><br /> Standarddokument<br /><br /> Verzeichnissuche<br /><br /> HTTP-Fehler<br /><br /> Statischer Inhalt<br /><br /> [Hinweis: Installieren Sie nicht die WebDAV-Veröffentlichung]<br /><br /> Integrität und Diagnose<br /><br /> HTTP-Protokollierung<br /><br /> Anforderungsüberwachung<br /><br /> Leistung<br /><br /> Komprimierung statischer Inhalte<br /><br /> Sicherheit<br /><br /> Anforderungsfilterung<br /><br /> Windows-Authentifizierung|  
  
### Funktionen 
 Unter Windows Server 2012 und Windows Server 2012 R2 können Sie den **Server-Manager** verwenden, um die folgenden erforderlichen Funktionen zu installieren.  
  
||  
|-|  
|.NET Framework 3.5 (einschließlich .NET 2.0 und 3.0)<br /><br /> .NET Framework 4.5 Advanced Services<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> HTTP-Aktivierung [Hinweis: Dies ist erforderlich.]<br /><br /> TCP-Portfreigabe<br /><br /> Aktivierungsdienst für Windows-Prozesse<br /><br /> Prozessmodell<br /><br /> .NET-Umgebung<br /><br /> Konfiguration-APIs|  
  
 Nachfolgend finden Sie ein PowerShell-Beispielskript zum Hinzufügen von erforderlichen Serverrollen und -funktionen. Die erforderlichen Serverrollen und -funktionen variieren je nach Umgebung.  
  
```powershell  
Install-WindowsFeature Web-Mgmt-Console, AS-NET-Framework, Web-Asp-Net, Web-Asp-Net45, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Http-Logging, Web-Request-Monitor, Web-Stat-Compression, Web-Filtering, Web-Windows-Auth, NET-Framework-Core, WAS-Process-Model, WAS-NET-Environment, WAS-Config-APIs  
  
Install-WindowsFeature Web-App-Dev, NET-Framework-45-Features -IncludeAllSubFeature –Restart  
```  
  
 Weitere Informationen zu PowerShell-Befehlen finden Sie unter [Install-WindowsFeature](https://technet.microsoft.com/library/jj205467).  
  
### Konten und Berechtigungen  
  
|Typ|Beschreibung|  
|----------|-----------------|  
|Windows-Konto|Sie müssen sich am Webservercomputer mit einem Windows-Konto anmelden, das über die Berechtigung zum Konfigurieren von Windows-Rollen, Rollendiensten und Funktionen sowie zum Erstellen und Verwalten von Anwendungspools, Websites und Webanwendungen in IIS auf dem lokalen Computer verfügt.|  
|Dienstkonto|Wenn Sie die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung in [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]erstellen, müssen Sie eine Identität für den Anwendungspool angeben, in dem die Anwendung ausgeführt wird. Dieses Konto kann sich von dem Konto unterscheiden, das beim Erstellen der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank als Dienstkonto angegeben wurde.<br /><br /> Die ID muss einem Domänenbenutzerkonto entsprechen und wird für den Datenbankzugriff zur Datenbankrolle mds_exec in der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank hinzugefügt. Weitere Informationen finden Sie unter [Datenbankanmeldenamen, -benutzer und -rollen &#40;Master Data Services&#41;](../../master-data-services/database-logins-users-and-roles-master-data-services.md). Darüber hinaus wird dieses Konto einer [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Windows-Gruppe hinzugefügt, z.B. **MDS_ServiceAccounts**, der Berechtigungen für das temporäre Kompilierungsverzeichnis **MDSTempDir** im Dateisystem erteilt wurden. Weitere Informationen finden Sie unter [Ordner- und Dateiberechtigungen &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md).|  
  
## Siehe auch  
 [Installieren von Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)   
 [Installieren von Master Data Services und IIS-Rollen und -Funktionen](../../sql-server/media/master-data-services.png)       
 [Erstellen einer Master Data Manager-Webanwendung &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [Webkonfiguration &#40;Seite im Konfigurations-Manager für Master Data Services&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  