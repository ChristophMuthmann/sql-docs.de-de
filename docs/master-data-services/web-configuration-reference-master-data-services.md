---
title: Web Konfigurationsreferenz (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1be0e90d7d2ba9b2751677015957ca249d91119e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="web-configuration-reference-master-data-services"></a>Webkonfigurationsreferenz (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]wird eine Datei "Web.config" verwendet wird, um die Konfigurationseinstellungen enthält, die Internetinformationsdienste (Internet Information Services, IIS) auf dem Host ermöglichen die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Webanwendung und dem Webdienst. Diese Datei Web.config Datei befindet sich im Ordner WebApplication des [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Installationspfads. Weitere Informationen zu Pfaden und Berechtigungen finden Sie unter [Ordner- und Dateiberechtigungen &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Web.Config-Elemente  
 Die Datei "Web.config" enthält eine benutzerdefinierte [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Element  **\<MasterDataServices >**, zusätzlich zu den standardmäßigen IIS, .NET Framework, ASP.NET und Windows Communication Foundation (WCF)-Konfigurationselemente. Die folgende Tabelle beschreibt die Elemente mit den enthaltenen Web.config-Dateien.  
  
|Konfigurationselement|Description|  
|---------------------------|-----------------|  
|**masterDataServices**|Benutzerdefiniertes Element. Verbindet den [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Web-Service mit einer [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank.|  
|**connectionStrings**|ASP.NET-Element. Weitere Informationen finden Sie unter [connectionStrings-Element (ASP.NET-Einstellungsschema)](http://go.microsoft.com/fwlink/?LinkId=178347) in der MSDN Library.|  
|**system.web**|ASP.NET-Element. Weitere Informationen finden Sie unter [system.web-Element (ASP.NET-Einstellungsschema)](http://go.microsoft.com/fwlink/?LinkId=178348) in der MSDN Library.|  
|**startup**|.NET Framework-Element. Weitere Informationen finden Sie unter [ \<Startup >-Element](http://go.microsoft.com/fwlink/?LinkId=178349) in der MSDN Library.|  
|**Laufzeit**|.NET Framework-Element. Weitere Informationen finden Sie unter [ \<Runtime >-Element](http://go.microsoft.com/fwlink/?LinkId=178350) in der MSDN Library.|  
|**system.codedom**|.NET Framework-Element. Weitere Informationen finden Sie unter [ \<system.codedom > Element](http://go.microsoft.com/fwlink/?LinkId=178351) in der MSDN Library.|  
|**system.web.extensions**|ASP.NET-Element. Weitere Informationen finden Sie unter [system.web.extensions-Element (ASP.NET-Einstellungsschema)](http://go.microsoft.com/fwlink/?LinkId=178352) in der MSDN Library.|  
|**system.webServer**|Abschnittsgruppe, die IIS-Elemente enthält. Weitere Informationen finden Sie unter [system.webServer Section Group \[IIS 7 Settings Schema\]](http://go.microsoft.com/fwlink/?LinkId=178353) (Abschnittsgruppe „system.webServer“ [IIS 7-Einstellungsschema]) in der MSDN Library.|  
|**system.serviceModel**|WCF-Element. Weitere Informationen finden Sie unter [ \<system.serviceModel >](http://go.microsoft.com/fwlink/?LinkId=178354) in der MSDN Library.|  
|**system.diagnostics**|.NET Framework-Element. Weitere Informationen finden Sie unter [ \<system.diagnostics > Element](http://go.microsoft.com/fwlink/?LinkId=178355) in der MSDN Library.|  
|**appSettings**|ASP.NET-Element. Weitere Informationen finden Sie unter [appSettings-Element (allgemeines Einstellungsschema)](http://go.microsoft.com/fwlink/?LinkId=178356) in der MSDN Library.|  
  
## <a name="masterdataservices-element"></a>masterDataServices-Element  
 Die  **\<MasterDataServices >** Element ist ein benutzerdefiniertes Element, das verwendet wird, die Verbindung eine [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Webdiensts ein [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Datenbank.  
  
### <a name="syntax"></a>Syntax  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Elemente und Attribute  
  
|Element|Description|  
|----------|-----------------|  
|**Instanz**|Untergeordnetes Element. Enthält Attribute, die Informationen für den Webdienst und Datenbankverbindungszeichenfolge angeben.|  
|**virtualPath**|Attribute. Gibt den virtuellen Pfad der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]-Webanwendung und des entsprechenden Diensts an. Dies entspricht der **Pfad** Attribut des der  **\<Anwendung >** Element unter den  **\<Website >** Element in der IIS ApplicationHost.config-Datei.|  
|**siteName**|Attribute. Gibt den Namen der Website an, die die [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]-Webanwendung und den entsprechenden Dienst hostet. Dies entspricht der **Namen** Attribut des der  **\<Website >** Element unter  **\<Sites >** in der IIS ApplicationHost.config-Datei.|  
|**connectionName**|Attribute. Gibt den Namen der zu verwendeten Verbindung an. Dies entspricht der **Namen** Attribut des der  **\<hinzufügen >** Element unter den  **\<ConnectionStrings >** Element in der Datei "Web.config".|  
|**serviceName**|Attribute. Gibt den Namen des Web-Services an. Dies entspricht der **Namen** Attribut des der  **\<Service >** Element unter den  **\<Services >** Element in der Datei "Web.config".|  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird ein Dienst mit dem Namen MDS1 auf der Contoso-Website veranschaulicht und /MDs-Pfad, der eine von MDSDB angegebene Verbindungszeichenfolge verwendet.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
