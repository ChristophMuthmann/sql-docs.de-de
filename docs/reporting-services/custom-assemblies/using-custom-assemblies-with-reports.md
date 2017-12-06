---
title: Verwenden benutzerdefinierter Assemblys mit Berichten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: custom-assemblies
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: "32"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a69e1ddb566cdadf9f1baafa436337ceffd3f322
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="using-custom-assemblies-with-reports"></a>Verwenden benutzerdefinierter Assemblys mit Berichten
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können Sie benutzerdefinierten Code für Werte, Formate und Formatierungen von Berichtselementen schreiben. Beispielsweise können Sie mit benutzerdefiniertem Code Währungen entsprechend einem Gebietsschema formatieren, bestimmte Werte mit speziellen Formatierungen belegen oder andere Geschäftsregeln anwenden, die in Ihrem Unternehmen praktiziert werden. Eine Möglichkeit, diesen Code in Berichte einzufügen, besteht in der Erstellung einer benutzerdefinierten Codeassembly unter Verwendung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], auf die Ihre Berichtsdefinitionsdateien verweisen können. Der Server ruft die Funktionen in Ihren benutzerdefinierten Assemblys auf, wenn ein Bericht ausgeführt wird. Mithilfe von benutzerdefinierten Assemblys können spezielle Funktionen abgerufen werden, die Sie in den Berichten verwenden möchten.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Referencing Assemblies in an RDL File (Verweisen auf Assemblys in einer RDL-Datei)](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 Beschreibt, wie in einer Sprachdatei der Berichtsdefinition auf die benutzerdefinierten Assemblys verwiesen wird.  
  
 [Bereitstellen einer benutzerdefinierten Assembly](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 Beschreibt den Einsatz einer benutzerdefinierten Assembly im Berichtsserver und im Berichts-Manager.  
  
 [Using Strong-Named Custom Assemblies (Verwenden von benutzerdefinierten Assemblys mit starken Namen)](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 Beschreibt die Verwendung benutzerdefinierter Assemblys zusammen mit starken Namen.  
  
 [Asserting Permissions in Custom Assemblies (Berechtigungserteilung in benutzerdefinierten Assemblys)](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 Beschreibt, wie benutzerdefinierte Assemblys mit beschränkten und speziellen Berechtigungen eingesetzt werden und wie diese Berechtigungen im Code erteilt werden.  
  
 [Accessing Custom Assemblies Through Expressions (Zugriff auf benutzerdefinierte Assemblys über Ausdrücke)](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 Beschreibt, wie benutzerdefinierte Assemblymethoden als Berichtsausdrücke in den Berichtsdefinitionen aufgerufen werden.  
  
 [Initializing Custom Assembly Objects (Initialisieren von Objekten benutzerdefinierter Assemblys)](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 Beschreibt, wie Werte für benutzerdefinierte Assemblyobjekte initialisiert werden, die von einem Bericht aufgerufen werden.  
  
 [How to: Debug Custom Assemblies (Vorgehensweise: Debuggen von benutzerdefinierten Assemblys)](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 Beschreibt das Debuggen von benutzerdefiniertem Assemblycode.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsdefinitionssprache (SSRS)](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
