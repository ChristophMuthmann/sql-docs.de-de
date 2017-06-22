---
title: Verwenden von benutzerdefinierten Assemblys mit starkem Namen | Microsoft Docs
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
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 3c024efb9f8531ed9b87b0e2b7d7b22489a76dcf
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="using-strong-named-custom-assemblies"></a>Verwenden von benutzerdefinierten Assemblys mit starken Namen
  Ein starker Name identifiziert eine Assembly und enthält den Textnamen der Assembly, die vierteilige Versionsnummer, Kulturinformationen (falls verfügbar), einen öffentlichen Schlüssel und eine digitale Signatur, die im Manifest der Assembly gespeichert werden. Ein starker Name identifiziert eine Assembly eindeutig für die Common Language Runtime (CLR) und stellt die binäre Integrität sicher.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>Verwenden von AllowPartiallyTrustedCallersAttribute  
 Um Assemblys mit starkem Namen mit Berichten verwenden zu können, müssen Sie Ihre Assembly mit starkem Namen von teilweise vertrauenswürdigem Code unter Verwendung der Assembly aufgerufen werden zulassen **AllowPartiallyTrustedCallers** Attribut. Sie können **AllowPartiallyTrustedCallersAttribute** Assemblys mit starkem Namen vom Berichts-Designer oder dem Berichtsserver in Berichtsausdrücken aufgerufen werden können. Damit Assemblys mit starkem Namen von teilweise vertrauenswürdigem Code aufgerufen werden dürfen, müssen Sie folgendes Attribut auf Assemblyebene zu Ihrer Assemblyattributdatei hinzufügen.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** gilt nur, wenn von einer Assembly mit starkem Namen auf Assemblyebene angewendet. Weitere Informationen zum Anwenden von Attributen auf Assemblyebene finden Sie unter "Anwenden von Attributen" in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
> [!CAUTION]  
>  Wenn **AllowPartiallyTrustedCallersAttribute** vorhanden ist, ist die Standardeinstellung **FullTrustLinkDemand** sicherheitsüberprüfungen verhindert, sodass auf die Assembly aufgerufen werden kann von einer anderen teilweise vertrauenswürdigen Assembly. Alle Sicherheitsprüfungen, einschließlich der Attribute für die deklarative Sicherheit auf Klassen- oder Methodenebene, müssen explizit angegeben werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von benutzerdefinierten Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
