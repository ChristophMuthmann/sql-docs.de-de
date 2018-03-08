---
title: Sichere Entwicklung (Reporting Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- development security [Reporting Services]
- security [Reporting Services], development
- security [Reporting Services], strategies
ms.assetid: 12161a6c-b93b-4312-9d27-0c922561eb9b
caps.latest.revision: "15"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1e9152b933bbb6a021b232a7271d412c30169b5d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="secure-development-reporting-services"></a>Sichere Entwicklung (Reporting Services)
  Die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] bietet ein stabiles Sicherheitssystem, das Code in stark eingeschränkten, vom Administrator definierten Sicherheitskontexten ausführt. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verwendet das Sicherheitssystem von [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], das als Codezugriffssicherheit (oder beweisbasierte Sicherheit) bekannt ist. Wenn Codezugriffssicherheit vorliegt, ist der Benutzer vertrauenswürdig genug, um auf eine Ressource zuzugreifen; ist aber der Code, den der Benutzer ausführt, nicht vertrauenswürdig, wird der Zugriff auf diese Ressource verweigert.  
  
 Da die Sicherheit auf dem Code (und nicht auf bestimmten Benutzern) basiert, ist es möglich, Sicherheit für benutzerdefinierte Assemblys oder Daten, Übermittlungs-, Rendering- und Sicherheitserweiterungen, die Sie für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] entwickeln, auszudrücken. Ihr Erweiterungscode kann von beliebig vielen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Benutzern ausgeführt werden, die alle zum Zeitpunkt der Entwicklung unbekannt sind. Die benutzerdefinierten Assemblys oder die Erweiterungen, die Sie entwickeln, erfordern bestimmte Sicherheitsrichtlinien in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Diese Sicherheitsrichtlinien werden in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] als Typen dargestellt. Weitere Informationen über die Codezugriffssicherheit finden Sie unter "Codezugriffssicherheit" in der Dokumentation von [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Code Access Security in Reporting Services (Codezugriffssicherheit in Reporting Services)](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)  
 Gibt eine Einführung in Codezugriffssicherheit und Richtlinienkonfigurationen für benutzerdefinierte Assemblys und Erweiterungen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Understanding Security Policies (Grundlegendes zu Sicherheitsrichtlinien)](../../../reporting-services/extensions/secure-development/understanding-security-policies.md)  
 Beschreibt die verschiedenen Assemblytypen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] und die Auswirkungen der Codezugriffssicherheit auf die Codeberechtigungen.  
  
 [Using Reporting Services Security Policy Files (Verwenden von Reporting Services-Sicherheitsrichtliniendateien)](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)  
 Beschreibt die verschiedenen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Komponenten und die entsprechenden Richtlinienkonfigurationsdateien.  
  
  
