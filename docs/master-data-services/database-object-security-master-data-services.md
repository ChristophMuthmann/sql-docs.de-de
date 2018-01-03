---
title: Sicherheit von Datenbankobjekten (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database [Master Data Services], object security
- security [Master Data Services], database objects
ms.assetid: dd5ba503-7607-45d9-ad0d-909faaade179
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7058099b0da0b991327f6ab408e55fc7143f8d3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="database-object-security-master-data-services"></a>Sicherheit von Datenbankobjekten (Master Data Services)
  In der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank werden Daten in mehreren Datenbanktabellen gespeichert und in Sichten angezeigt. Daher können Informationen, die Sie in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung gesichert haben, für Benutzern mit Zugriff auf die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank sichtbar sein.  
  
 So kann das Mitarbeitermodell beispielsweise Informationen zu den Mitarbeitergehältern oder das Kontomodell Informationen zu den Unternehmensfinanzen enthalten. Sie können einem Benutzer in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Benutzeroberfläche den Zugriff auf diese Modelle verweigern, aber Benutzer mit Zugriff auf die Datenbank können diese Daten anzeigen.  
  
 Um den Benutzern nur spezifische Daten zur Verfügung zu stellen, können Sie Datenbankobjekten Berechtigungen zuweisen. Weitere Informationen über das Erteilen von Berechtigungen finden Sie unter [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../t-sql/statements/grant-object-permissions-transact-sql.md). Weitere Informationen zum Sichern von SQL Server finden Sie unter [Securing SQL Server](../relational-databases/security/securing-sql-server.md).  
  
 Die folgenden Tasks erfordern Zugriff auf die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank:  
  
-   [Bereitstellen von Daten](#Staging)  
  
-   [Überprüfen von Daten im Hinblick auf Geschäftsregeln](#rules)  
  
-   [Löschen von Versionen](#Versions)  
  
-   [Sofortiges Anwenden von Hierarchieelementberechtigungen](#Hierarchy)  
  
-   [Konfigurieren von Systemeinstellungen](#SysSettings)  
  
##  <a name="Staging"></a> Bereitstellen von Daten  
 In der folgenden Tabelle hat jedes sicherungsfähige Element "Name" als Teil des Namens. Dies gibt den Namen der Stagingtabelle an, die angegeben wird, wenn eine Entität erstellt wird. Weitere Informationen finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
|Aktion|Sicherungsfähige Elemente|Berechtigungen|  
|------------|----------------|-----------------|  
|Erstellen, aktualisieren und löschen Sie Blattelemente und ihre Attribute.|stg.name_Leaf|Erforderlich: INSERT<br /><br /> Optional: SELECT und UPDATE|  
|Laden Sie die Daten aus der Blattstagingtabelle in die entsprechenden MDS-Datenbanktabellen.|stg.udp_name_Leaf|Führen Sie|  
|Erstellen, aktualisieren und löschen Sie konsolidierte Elemente und ihre Attribute.|stg.name_Consolidated|Erforderlich: INSERT<br /><br /> Optional: SELECT und UPDATE|  
|Laden Sie die Daten aus der konsolidierten Stagingtabelle in die entsprechenden MDS-Datenbanktabellen.|stg.udp_name_Consolidated|Führen Sie|  
|Verschieben von Elementen in eine explizite Hierarchie|stg.name_Relationship|Erforderlich: INSERT<br /><br /> Optional: SELECT und UPDATE|  
|Laden Sie die Daten aus der Beziehungsstagingtabelle in die entsprechenden MDS-Tabellen.|stg.udp_name_Relationship|Führen Sie|  
|Zeigen Sie Fehler an, die aufgetreten sind, als Daten aus den Stagingtabellen in die MDS-Datenbanktabellen eingefügt wurden.|stg.udp_name_Relationship|SELECT|  
  
 Weitere Informationen finden Sie unter [Übersicht: Importieren von Daten aus Tabellen &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
##  <a name="rules"></a> Überprüfen von Daten im Hinblick auf Geschäftsregeln  
  
|Aktion|Sicherungsfähiges Element|Berechtigungen|  
|------------|---------------|-----------------|  
|Überprüfen einer Version der Daten anhand von Geschäftsregeln|mdm.udpValidateModel|Führen Sie|  
  
 Weitere Informationen finden Sie unter [Gespeicherte Überprüfungsprozedur &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
##  <a name="Versions"></a> Löschen von Versionen  
  
|Aktion|Sicherungsfähige Elemente|Berechtigungen|  
|------------|----------------|-----------------|  
|Bestimmen der ID der zu löschenden Version|mdm.viw_SYSTEM_SCHEMA_VERSION|SELECT|  
|Löschen einer Version eines Modells|mdm.udpVersionDelete|Führen Sie|  
  
 Weitere Informationen finden Sie unter [Löschen einer Version &#40;Master Data Services&#41;](../master-data-services/delete-a-version-master-data-services.md).  
  
##  <a name="Hierarchy"></a> Sofortiges Anwenden von Hierarchieelementberechtigungen  
  
|Aktion|Sicherungsfähige Elemente|Berechtigungen|  
|------------|----------------|-----------------|  
|Sofortiges Anwenden von Elementberechtigungen|mdm.udpSecurityMemberProcessRebuildModel|Führen Sie|  
  
 Weitere Informationen finden Sie unter [Sofortiges Anwenden von Elementberechtigungen &#40;Master Data Services&#41;](../master-data-services/immediately-apply-member-permissions-master-data-services.md).  
  
##  <a name="SysSettings"></a> Konfigurieren von Systemeinstellungen  
 Sie können bestimmte Systemeinstellungen konfigurieren, um das Verhalten in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]zu steuern. Sie können diese Einstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] oder, wenn Sie über die Zugriffsberechtigung UPDATE verfügen, direkt in die Datenbanktabelle mdm.tblSystemSetting anpassen. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherheit &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
