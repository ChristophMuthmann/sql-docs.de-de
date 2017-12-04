---
title: Verweisen auf Assemblys in einer RDL-Datei | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: "36"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fb34fd3f73b8b7451d52c9794697e4a6c3f8b82e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>Verweisen auf Assemblys in einer RDL-Datei
  Um die Verwendung von Assemblys mit benutzerdefiniertem Code in Berichtsdefinitionsdateien zu unterstützen, sind zwei RDL-Elemente (Report Definition Language) in der RDL-Spezifikation enthalten: das **CodeModules** und das **Classes**-Element.  
  
 Mithilfe des **CodeModules**-Elements kann in Berichtsausdrücken auf Assemblys mit verwaltetem Code verwiesen werden. **CodeModules** ist ein Element auf oberster Ebene, das den Verweis auf die Assembly enthält, mit der in Ihren Berichtsdefinitionsdateien spezialisierte Funktionen aufgerufen werden. Ein Eintrag in einer Berichtsdefinition, der die Verwendung einer benutzerdefinierten Assembly unterstützt, kann folgendermaßen aussehen:  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 Statt <xref:System.Reflection.Assembly.Load%2A> aus benutzerdefiniertem Code aufzurufen, registrieren Sie die benutzerdefinierten Assemblys entweder, indem Sie der RDL-Datei die **CodeModule**-Elemente manuell hinzufügen, oder mithilfe der Registerkarte **Verweise** im Dialogfeld **Berichtseigenschaften**. Weitere Informationen finden Sie unter [Benutzerdefinierter Code und Assemblyverweise in Ausdrücken in Berichts-Designer &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)-Ausdruck dar.  
  
 Das **Classes**-Element unterstützt die Verwendung von Instanzelementen in einer Berichtsdefinition. **Classes** ist ein Element der obersten Ebene, das einen Verweis auf den Klassen- und einen Instanznamen enthält. Ein Eintrag in einer Berichtsdefinition, der die Verwendung von Instanzelementen unterstützt, kann folgendermaßen aussehen:  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 Weitere Informationen finden Sie unter [Zugriff auf benutzerdefinierte Assemblys über Ausdrücke](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden benutzerdefinierter Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
