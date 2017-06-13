---
title: "Unterstützte Kombinationen von SharePoint- und Reporting Services-Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 2e66cac836de44e8d2a9f23d88a600daaa26c0d1
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>Unterstützte Kombinationen von SharePoint- und Reporting Services-Server
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  Ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver, der im SharePoint-Modus installiert ist, benötigt eine Version von SharePoint und das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In (rsSharePoint.msi) für SharePoint-Produkte, das Sie auf den SharePoint-Servern installieren.  In diesem Thema werden die unterstützten Kombinationen zusammengefasst.  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Unterstützte Kombinationen von SharePoint- und Reporting Services-Komponenten  
 In der folgenden Tabelle werden die unterstützten Kombinationen von Berichtsserver, dem Reporting Services-Add-In für SharePoint-Produkte und SharePoint-Produkten zusammengefasst. Nicht in der folgenden Tabelle aufgeführte Kombinationen werden nicht unterstützt.  
  
### <a name="supported-combinations"></a>Unterstützte Kombinationen  
  
||Berichtsserver|Add-In|SharePoint-Version|  
|-|-------------------|-------------|------------------------|  
|1|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2016|  
|2|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|SharePoint 2013|  
|3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|  
|4|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|5|SQL Server 2012 SP3|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und SQL Server 2012 SP3|SharePoint 2013|  
|6|SQL Server 2012 SP2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und SQL Server 2012 SP2|SharePoint 2013|  
|7|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|  
|8|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]*|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|9|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|  
|10|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|  
|11|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] und [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|  
|12|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|  
|13|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
|14|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|  
|15|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|  
  
 *Ausnahme: Power View-Integration wird nicht unterstützt.  
  
 Links zu den Add-In-Downloadseiten finden Sie unter [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
 **Weitere Hinweise:**  

- Stellen Sie sicher, dass alle SharePoint-Server innerhalb der Farm aktualisiert sind. Dazu gehören auch die App- und Web-Front-End-Server.

-   Die Unterstützung von SharePoint 2016, einschließlich der Power View-Integration, erfordert den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver und die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In-Version von SQL Server 2016 oder höher.  

-   Die Unterstützung von SharePoint 2013, einschließlich der Power View-Integration, erfordert den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver und die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In-Version von SQL Server 2012 SP1 oder höher.  
  
-   Power View wurde in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]eingeführt. Daher erfordert die Power View-Integration in SharePoint 2010 die [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] -Version des Add-Ins oder eine höhere Version.  
  
-   Das SQL Server 2008 R2-Add-In wird von Berichtsservern von SQL Server 2012 (oder höher) nicht unterstützt. Das SQL Server 2008 R2-Add-In wird vom SharePoint 2010-Installationsprogramm für erforderliche Komponenten automatisch installiert. Vor der Installation einer neueren Add-In-Version muss das Add-In deinstalliert werden. Direkte Upgrades des Add-Ins werden nicht unterstützt.  
  
-   **Upgrade** : SharePoint 2010 mit installiertem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In kann nicht direkt auf SharePoint 2013 aktualisiert werden. SharePoint 2013 erfordert [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] oder eine höhere Version des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-Ins und -Berichtsservers. Weitere Informationen zum Upgrade finden Sie unter [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
  


