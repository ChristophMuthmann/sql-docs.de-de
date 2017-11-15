---
title: Ordner- und Dateiberechtigungen (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Master Data Services], file and folder
- folders [Master Data Services]
- files [Master Data Services]
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 641155bf64d2389bc6e3cf2e297d12fc808602bc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="folder-and-file-permissions-master-data-services"></a>Ordner- und Dateiberechtigungen (Master Data Services)
  Bei der Installation von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]werden Ordner und Dateien im Dateisystem in dem Installationspfad installiert, der für freigegebenen Funktionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] festgelegt wurde. Wenn Sie den Standardinstallationspfad für freigegebene Funktionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwenden, lautet der Installationspfad für [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] wie folgt: *Laufwerk*:\Programme\Microsoft SQL Server\130\Master Data Services. Sie können den Installationspfad für freigegebene Funktionen ändern; achten Sie dabei jedoch auf Berechtigungen, die vom übergeordneten Ordner geerbt werden, und auf explizit für [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]festgelegte Berechtigungen.  
  
## <a name="inherited-permissions"></a>Geerbte Berechtigungen  
 Der Order **Microsoft SQL Server** , der Ordner **Master Data Services** und die meisten Unterordner und Dateien erben Berechtigungen vom übergeordneten Ordner, der bei der Installation von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] angegeben wurde. Bei Auswahl des Standardinstallationspfads lautet der übergeordnete Ordner, von dem Berechtigungen geerbt werden, *Laufwerk*:\Programme. In der folgenden Tabelle werden die Standardberechtigungen für den Ordner **Programme**beschrieben.  
  
> [!NOTE]  
>  Wenn Sie die Standardberechtigungen für den Ordner **Programme**ändern oder einen anderen Installationspfad auswählen, erben die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Ordner und -Dateien Berechtigungen von dem jeweils übergeordneten Ordner, d.h. die Berechtigungen können sich von denen in der nachfolgenden Tabelle unterscheiden.  
  
###### <a name="program-files-default-permissions"></a>Standardberechtigungen im Ordner Programme  
  
|Gruppen- oder Kontoname|Berechtigungen|  
|---------------------------|-----------------|  
|CREATOR OWNER|Spezielle Berechtigungen|  
|SYSTEM|Spezielle Berechtigungen|  
|Administratoren|Spezielle Berechtigungen|  
|Benutzer|Lesen & Ausführen, Ordnerinhalt auflisten, Lesen|  
|TrustedInstaller|Ordnerinhalt auflisten, Spezielle Berechtigungen|  
  
## <a name="explicit-permissions"></a>Explizite Berechtigungen  
 Der Ordner **MDSTempDir** und die Datei Web.config von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (im Ordner **WebApplication** ) erben keine Berechtigungen. Sie verfügen über Berechtigungen, die bei der Installation von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]explizit festgelegt werden und vom ausgewählten Installationspfad unabhängig sind. Ändern Sie diese Berechtigungen nicht.  
  
###### <a name="mdstempdir-permissions"></a>Berechtigungen im Ordner "MDSTempDir"  
  
|Gruppen- oder Kontoname|Berechtigungen|  
|---------------------------|-----------------|  
|SYSTEM|Ändern, Lesen & Ausführen, Ordnerinhalt auflisten, Lesen, Schreiben|  
|Administratoren|Ändern, Lesen & Ausführen, Ordnerinhalt auflisten, Lesen, Schreiben|  
|MDS_ServiceAccounts|Ändern, Lesen & Ausführen, Ordnerinhalt auflisten, Lesen, Schreiben|  
  
###### <a name="webconfig-permissions"></a>Berechtigungen in der Datei "Web.config"  
  
|Gruppen- oder Kontoname|Berechtigungen|  
|---------------------------|-----------------|  
|SYSTEM|Vollzugriff, Ändern, Lesen & Ausführen, Lesen, Schreiben|  
|Administratoren|Vollzugriff, Ändern, Lesen & Ausführen, Lesen, Schreiben|  
|MDS_ServiceAccounts|Lesen & Ausführen, Lesen|  
  
 Weitere Informationen zu den Inhalten der Web.config-Datei von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] finden Sie unter [Webkonfigurationsreferenz &#40;Master Data Services&#41;](../master-data-services/web-configuration-reference-master-data-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von Master Data Services](../master-data-services/install-windows/install-master-data-services.md)  
  
  
