---
title: "Unterstützte Kombinationen von SharePoint- und Reporting Services-Servern | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 0446c7b50f78074e44258aa973f6cf970cb9f50a
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>Unterstützte Kombinationen von SharePoint- und Reporting Services-Servern

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Ein SQL Server Reporting Services-Berichtsserver, der im SharePoint-Modus installiert ist, benötigt eine Version von SharePoint und das SQL Server Reporting Services-Add-In (rsSharePoint.msi) für SharePoint-Produkte, das Sie auf den SharePoint-Servern installieren. In diesem Thema werden die unterstützten Kombinationen zusammengefasst.

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Unterstützte Kombinationen von SharePoint- und Reporting Services-Komponenten

 In der folgenden Tabelle werden die unterstützten Kombinationen von Berichtsserver, dem Reporting Services-Add-In für SharePoint-Produkte und SharePoint-Produkten zusammengefasst. Nicht in der folgenden Tabelle aufgeführte Kombinationen werden nicht unterstützt.

### <a name="supported-combinations"></a>Unterstützte Kombinationen

||Berichtsserver|Add-In|SharePoint-Version|
|-|-------------------|-------------|------------------------|
|1|SQL Server 2016|SQL Server 2016|SharePoint 2016|
|2|SQL Server 2016|SQL Server 2016|SharePoint 2013|
|3|SQLServer 2014|SQLServer 2014|SharePoint 2013|
|4|SQLServer 2014|SQLServer 2014|SharePoint 2010|
|5|SQL Server 2012 SP3|SQL Server 2014 und SQL Server 2012 SP3|SharePoint 2013|
|6|SQL Server 2012 SP2|SQL Server 2014 und SQL Server 2012 SP2|SharePoint 2013|
|7|SQL Server 2012 SP1|SQL Server 2014 und SQL Server 2012 SP1|SharePoint 2013|
|8|SQL Server 2012 und SQL Server 2012 SP1*|SQLServer 2014|SharePoint 2010|
|9|SQL Server 2012|SQL Server 2012|SharePoint 2010|
|10|SQL Server 2008 R2|SQLServer 2014|SharePoint 2010|
|11|SQL Server 2008 R2|SQL Server 2012 und SQL Server 2012 SP1 oder höher|SharePoint 2010|
|12|SQL Server 2008 R2|SQL Server 2008 R2|SharePoint 2010|
|13|SQL Server 2008 R2|SQL Server 2008 SP2|SharePoint 2007|
|14|SQL Server 2008 SP2|SQL Server 2008 R2|SharePoint 2010|
|15|SQL Server 2008 SP2|SQL Server 2008 und SQL Server 2008 SP2|SharePoint 2007|

 *Ausnahme: Power View-Integration wird nicht unterstützt.

 Links zu den Add-In-Downloadseiten finden Sie unter [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  

 **Weitere Überlegungen**:

- Stellen Sie sicher, dass alle SharePoint-Server innerhalb der Farm aktualisiert sind. Dazu gehören auch die App- und Web-Front-End-Server.

- Die Unterstützung von SharePoint 2016, einschließlich der Power View-Integration, erfordert den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver und die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In-Version von SQL Server 2016 oder höher.

- Die Unterstützung von SharePoint 2013, einschließlich der Power View-Integration, erfordert den [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver und die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In-Version von SQL Server 2012 SP1 oder höher.

- Power View wurde in SQL Server 2012 eingeführt. Daher erfordert die Power View-Integration in SharePoint 2010 die SQL Server 2012-Version des Add-Ins oder eine höhere Version.

- Das SQL Server 2008 R2-Add-In wird von Berichtsservern von SQL Server 2012 (oder höher) nicht unterstützt. Das SQL Server 2008 R2-Add-In wird vom SharePoint 2010-Installationsprogramm für erforderliche Komponenten automatisch installiert. Vor der Installation einer neueren Add-In-Version muss das Add-In deinstalliert werden. Direkte Upgrades des Add-Ins werden nicht unterstützt.

- **Upgrade** : SharePoint 2010 mit installiertem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Add-In kann nicht direkt auf SharePoint 2013 aktualisiert werden. SharePoint 2013 erfordert SQL Server 2012 SP1 oder eine höhere Version des [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Add-Ins und -Berichtsservers. Weitere Informationen zum Upgrade finden Sie unter [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

## <a name="next-steps"></a>Nächste Schritte

 [Verfügbarkeit des Reporting Services-Add-Ins für SharePoint-Produkte](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
