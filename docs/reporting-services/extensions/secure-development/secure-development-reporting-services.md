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
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- development security [Reporting Services]
- security [Reporting Services], development
- security [Reporting Services], strategies
ms.assetid: 12161a6c-b93b-4312-9d27-0c922561eb9b
caps.latest.revision: "15"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5a82e0223882d98db52cd9837ea8f9cb1ae832de
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
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
  
  
