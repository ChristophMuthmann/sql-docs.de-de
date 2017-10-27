---
title: "Sicherheitsüberlegungen für Erweiterungen | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], extensions
- extensions [Reporting Services], security
- permissions [Reporting Services], extensions
ms.assetid: 58cbdfeb-1105-4a7d-a3b8-b897ff95f367
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 1d7c7d5f46e1340de1fca0422ff91f64c910a32d
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="security-considerations-for-extensions"></a>Überlegungen zur Sicherheit von Erweiterungen
  Jede Anwendung für die Common Language Runtime (CLR) muss mit dem CLR-Sicherheitssystem interagieren. Bei der Ausführung einer solchen Anwendung wird diese automatisch ausgewertet, und sie erhält von der CLR einen Berechtigungssatz. Abhängig von den Berechtigungen, die die Anwendung erhält, wird sie entweder weiter ausgeführt, oder es wird eine Sicherheitsausnahme ausgelöst. Die lokalen Sicherheitseinstellungen und –richtlinien in den Dateien für die Sicherheitsrichtlinienkonfiguration eines bestimmten Berichtsservers definieren die Codeberechtigungen, die eine Assembly erhält.  
  
 Bevor Sie Berechtigungen anfordern, sollten Sie wissen, welche Ressourcen und geschützten Operationen Ihr Erweiterungscode verwenden soll. Außerdem sollten Sie wissen, von welchen Berechtigungen diese Ressourcen und Operationen geschützt werden. Darüber hinaus müssen Sie sämtliche Ressourcen verfolgen, auf die von Methoden der Klassenbibliotheken zugegriffen wird, die von den Erweiterungskomponenten aufgerufen werden. Weitere Informationen finden Sie unter "Anfordern von Berechtigungen" im [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Entwicklerhandbuch.  
  
 Erweiterungen, die auf einem Berichtsserver bereitgestellt ausführen müssen als vollständig vertrauenswürdig sein, was bedeutet, dass die Erweiterung muss Bestandteil einer Codegruppe sein, die gewährt wird die **FullTrust** Berechtigungssatz. Dies bedeutet auch, dass Ihre Erweiterung Zugriff auf bestimmte Serverressourcen und -vorgänge haben kann, die über CLR zur Verfügung stehen, abhängig vom Benutzer, der gerade für einen bestimmten Bericht authentifiziert wird. Weitere Informationen zu Codegruppen und Erweiterungen finden Sie unter [Codezugriffssicherheit in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] wendet die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Sicherheit für alle Erweiterungen an.  
  
 Die folgenden Bedingungen gelten für den Einsatz von Datenverarbeitungs-, Übermittlungs-, Rendering- und Sicherheitserweiterungen in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   Nur der lokale Administrator hat die Berechtigung, eine Erweiterung anzuwenden.  
  
-   Nur Benutzer mit der entsprechenden Lese-/Schreibberechtigung können die Konfigurationsdateien für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Komponente ändern, die gerade erweitert wird.  
  
-   Nur berechtigte Benutzer dürfen die Sicherheitsrichtliniendateien ändern und die Codezugriffssicherheit für eine Erweiterung aktivieren.  
  
 Weitere Informationen zur Codezugriffssicherheit in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], finden Sie unter [sichere Entwicklung &#40; Reporting Services &#41; ](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
 Weitere Informationen zur [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Sicherheit finden Sie in der .NET Framework-Sicherheit im [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Entwicklerhandbuch.  
  
## <a name="initialization-of-extension-assemblies"></a>Initialisierung von Erweiterungsassemblys  
 Wenn Erweiterungen zum ersten Mal vom Berichtsserver in den Speicher geladen werden, verwenden sie die Anmeldeinformationen für ein Dienstkonto. Denn einige Erweiterungsassemblys benötigen bestimmte Berechtigungen, um auf die Systemressourcen zugreifen, die Konfigurationsdateien lesen und andere abhängige Assemblys laden zu dürfen. Nachdem eine Assembly geladen und initialisiert wurde, verwenden alle nachfolgenden Aufrufe der Erweiterungsassemblys die Anmeldeinformationen vom Konto des Benutzers, der gerade angemeldet ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services-Erweiterungsbibliothek](../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

