---
title: "Von den SQL Server 2016-Editionen unterst&#252;tzte Reporting Services-Funktionen | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 39f03d2d-6e48-4b34-a9d3-07f86313b937
caps.latest.revision: 3
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 3
---
# Von den SQL Server 2016-Editionen unterst&#252;tzte Reporting Services-Funktionen
Dieses Thema bietet detaillierte Informationen zu den von verschiedenen [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Versionen unterstützten Funktionen.  
  
 SQL Server Evaluation Edition steht für einen Testzeitraum von 180 Tagen zur Verfügung.  
  
 Die neuesten Versionshinweise finden Sie unter [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md). Die letzten Informationen zu Neuigkeiten finden Sie unter [Neues bei Reporting Services (SSRS)](What's%20New%20in%20Reporting%20Services%20\(SSRS\).md).
    
 **SQL Server 2016 R2 ausprobieren!**    
    
 > [![Download aus dem Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) Laden Sie SQL Server 2016 aus dem **[Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)** herunter.    
    
> ![Virtueller Azure-Computer (klein)](../analysis-services/media/azure-virtual-machine-small.png) **[Starten eines virtuellen Computers, auf dem SQL Server 2016 bereits installiert ist](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

Informationen über Funktionen, die von den Evaluation- und Developer-Editionen unterstützt werden, finden Sie unter „SQL Server Enterprise Edition“.

Um zur Tabelle für eine SQL Server-Technologie zu navigieren, klicken Sie auf den zugehörigen Link:  

-   [Reporting Services](#SSRS)  
  
-   [Business Intelligence-Clients](#BIC)  

##  <a name="SSRS"></a> Reporting Services  
  
|Funktionsname|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Mobile Berichte und KPIs|ja||||||ja|  
|Unterstützte [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Edition für Katalogdatenbanken|Standard oder höher|Standard oder höher|Web|Express|||Standard oder höher|  
|Unterstützte [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Edition für Datenquellen|Alle   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Editionen|Alle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen|Web|Express|||Alle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen|  
|Berichtsserver|ja|Ja|Ja|Ja|||ja|  
|Berichts-Designer|ja|Ja|Ja|Ja|||ja|  
|Berichts-Designer-Webportal|ja|Ja|Ja|Ja|||ja|  
|Rollenbasierte Sicherheit|ja|Ja|Ja|Ja|||ja|  
|Export in Excel, PowerPoint, Word, PDF und Bilder|ja|Ja|Ja|Ja|||ja|  
|Verbesserte Messgeräte und Diagramme|ja|Ja|Ja|Ja|||ja|  
|Anheften von Berichtselementen an [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]Dashboards|ja|Ja|Ja|Ja|||ja|  
|Benutzerdefinierte Authentifizierung|ja|Ja|Ja|Ja|||ja|  
|Berichte als Datenfeeds|ja|Ja|Ja|Ja|||ja|  
|Modellunterstützung|ja|Ja|Ja||||Ja|  
|Erstellen von benutzerdefinierten Rollen für rollenbasierte Sicherheit|Ja|Ja|||||ja|  
|Modellelementsicherheit|ja|Ja|||||ja|  
|Uneingeschränktes Durchklicken|ja|Ja|||||ja|  
|Bibliothek freigegebener Komponenten|ja|Ja|||||ja|  
|Abonnements und Zeitplanung für E-Mail und Dateifreigabe|ja|Ja|||||ja|  
|Berichtsverlauf, Ausführungs-Momentaufnahmen und Zwischenspeichern|ja|Ja|||||ja|  
|SharePoint-Integration|ja|Ja|||||Ja|  
|Unterstützung von Remotedatenquellen und Nicht-SQL-Datenquellen<sup>1</sup>|Ja|Ja|||||ja|  
|RDCE-Erweiterbarkeit von Datenquellen, Übermittlung und Rendering|ja|Ja|||||ja|  
|Benutzerdefiniertes Branding|ja||||||ja|  
|Datengesteuerte Berichtsabonnements|ja||||||Ja|  
|Bereitstellung für horizontales Skalieren (Webfarmen)|Ja||||||ja|  
|Warnungen<sup>2</sup>|ja||||||ja|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] <sup>2</sup>|ja||||||Ja|  
  
 <sup>1</sup> Weitere Informationen zu unterstützten Datenquellen in SQL Server 2016 Reporting Services (SSRS) finden Sie unter [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
 <sup>2</sup> Erfordert Reporting Services im SharePoint-Modus. Weitere Informationen finden Sie unter [Installieren des SharePoint-Modus von Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
## Anforderungen für die Berichtsserver-Datenbankserver-Edition  
 Wenn Sie eine Berichtsserver-Datenbank erstellen, können nicht alle Editionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zum Hosten der Datenbank verwendet werden. Folgende Tabelle zeigt, welche Editionen von [!INCLUDE[ssDE](../includes/ssde-md.md)] Sie für spezielle Editionen von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]verwenden können.  
  
|Für diese Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Verwendung dieser Edition der Datenbankmodul-Instanz als Host für die Datenbank|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Enterprise oder Standard Editions (lokal oder remote)|  
|Standard|Enterprise oder Standard Editions (lokal oder remote)|  
|Web|Web Edition (nur lokal)|  
|Express mit Advanced Services|Express mit Advanced Services (nur lokal)|  
|Evaluation|Evaluation|  
  
##  <a name="BIC"></a> Business Intelligence-Clients  
 Die folgenden Softwareclientanwendungen sind im Microsoft Download Center verfügbar und bieten Unterstützung beim Erstellen von Business Intelligence-Dokumenten, die in einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz ausgeführt werden. Wenn Sie diese Dokumente in einer Serverumgebung hosten, verwenden Sie eine Edition von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], die diesen Dokumenttyp unterstützt. In der folgenden Tabelle wird dargestellt, welche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen die Serverfunktionen zum Hosten der in den Clientanwendungen erstellten Dokumente besitzen.  
  
|Name des Tools|Enterprise|Standard|Web|Express mit Advanced Services|Express mit Tools|Express|Entwickler|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] (RDL und RDS)|Ja|Ja|||||Ja|  
|[!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] (RSMOBILE)|Ja||||||Ja|  
|Power BI-Apps für mobile Geräte (iOS, Windows 10, Android) (RSMOBILE)|Ja||||||Ja|  
  
> [!NOTE]  
> 1.  In der oben aufgeführten Tabelle sind die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen angegeben, die zur Aktivierung dieser Clienttools erforderlich sind. Über diese Tools kann jedoch auf Daten zugegriffen werden, die von beliebigen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Editionen gehostet werden.  
> 2.  [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] ist der einzige Punkt für die Erstellung von mobilen Berichten. Stellen Sie eine Verbindung mit einem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Server her, um auf Datenquellen zuzugreifen und Berichte zu erstellen. Anschließend veröffentlichen Sie sie auf dem [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-Server für den Zugriff durch andere Benutzer in der Organisation auf dem Server oder auf mobilen Geräten. Sie können auch das eigenständige [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)] mit lokalen Datenquellen verwenden.  
> 3.  Unabhängig davon, ob Sie ein lokales [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] in der Cloud oder beides als Lösung für die Bereitstellung von Berichten verwenden, benötigen Sie nur eine mobile App für den Zugriff auf Dashboards und mobile Berichte auf mobilen Geräten. Die [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]-Apps stehen zum Download in den App-Stores für Windows, iOS oder Android bereit.  

## Siehe auch  
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [Produktspezifikationen für SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [Installation für SQLServer 2016](../database-engine/install-windows/installation-for-sql-server-2016.md) 