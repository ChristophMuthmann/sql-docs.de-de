---
title: Verwenden von benutzerdefinierten Assemblys mit Berichten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0931134ffb0a1511a02a1919d0e68acc55d5f34b
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="using-custom-assemblies-with-reports"></a>Verwenden benutzerdefinierter Assemblys mit Berichten
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] können Sie benutzerdefinierten Code für Werte, Formate und Formatierungen von Berichtselementen schreiben. Beispielsweise können Sie mit benutzerdefiniertem Code Währungen entsprechend einem Gebietsschema formatieren, bestimmte Werte mit speziellen Formatierungen belegen oder andere Geschäftsregeln anwenden, die in Ihrem Unternehmen praktiziert werden. Eine Möglichkeit, diesen Code in Berichte einzufügen ist die Erstellung eine benutzerdefinierten Codeassembly unter Verwendung der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , die Sie die in Ihren Berichtsdefinitionsdateien aus verweisen können. Der Server ruft die Funktionen in Ihren benutzerdefinierten Assemblys auf, wenn ein Bericht ausgeführt wird. Mithilfe von benutzerdefinierten Assemblys können spezielle Funktionen abgerufen werden, die Sie in den Berichten verwenden möchten.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Verweisen auf Assemblys in einer RDL-Datei](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 Beschreibt, wie in einer Sprachdatei der Berichtsdefinition auf die benutzerdefinierten Assemblys verwiesen wird.  
  
 [Bereitstellen einer benutzerdefinierten Assembly](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 Beschreibt den Einsatz einer benutzerdefinierten Assembly im Berichtsserver und im Berichts-Manager.  
  
 [Verwenden von benutzerdefinierten Assemblys mit starkem Namen](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 Beschreibt die Verwendung benutzerdefinierter Assemblys zusammen mit starken Namen.  
  
 [Berechtigungserteilung in benutzerdefinierten Assemblys](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 Beschreibt, wie benutzerdefinierte Assemblys mit beschränkten und speziellen Berechtigungen eingesetzt werden und wie diese Berechtigungen im Code erteilt werden.  
  
 [Zugreifen auf benutzerdefinierte Assemblys über Ausdrücke](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 Beschreibt, wie benutzerdefinierte Assemblymethoden als Berichtsausdrücke in den Berichtsdefinitionen aufgerufen werden.  
  
 [Initialisieren von Objekten benutzerdefinierter Assemblys](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 Beschreibt, wie Werte für benutzerdefinierte Assemblyobjekte initialisiert werden, die von einem Bericht aufgerufen werden.  
  
 [Vorgehensweise: Debuggen von benutzerdefinierten Assemblys](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 Beschreibt das Debuggen von benutzerdefiniertem Assemblycode.  
  
## <a name="see-also"></a>Siehe auch  
 [Report Definition Language &#40; SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
