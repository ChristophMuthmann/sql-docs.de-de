---
title: "Wichtige Änderungen in SQL Server Reporting Services in SQL Server 2016 | Microsoft Docs"
ms.date: 07/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 6348d05b8dbe6c8ab1a682388b4e69ce438e6a12
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---

# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>Aktuelle Änderungen in SQL Server Reporting Services in SQL Server 2016

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

In diesem Thema werden wichtige Änderungen in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]beschrieben. Diese Änderungen können u. U. zur Funktionsunfähigkeit von Anwendungen, Skripts oder Funktionen führen, die auf früheren Versionen von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]basieren. Diese Probleme können nach einem Upgrade oder in benutzerdefinierten Skripts oder Berichten auftreten.

## <a name="security-extensions"></a>Sicherheitserweiterungen

Benutzerdefinierte Sicherheitserweiterungen erfordern einige Änderungen, damit sie mit dem neuen [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]funktionieren. Sicherheitserweiterungen müssen die IAuthenticationExtension2-Schnittstelle verwenden.

## <a name="wmi-provider"></a>WMI-Anbieter

Der Name der [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] -Anwendung ändert sich von „ReportManager“ in „ReportServerWebApp“.

## <a name="next-steps"></a>Nächste Schritte

[Verändertes Programmverhalten in SQL Server Reporting Services in SQL Server 2016](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Neuigkeiten in Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[Als veraltet markierte Funktionen in SQL Server Reporting Services in SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[Nicht mehr unterstützte Features in SQL Server Reporting Services in SQL Server 2016](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
