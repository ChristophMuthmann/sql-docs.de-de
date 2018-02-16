---
title: Verwalten von Caches (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1b9c03bfa8c320eac3a3eb81b705f295122c337e
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="managing-caches-xmla"></a>Verwalten von Caches (XMLA)
  Sie können die [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) -Befehl in XML for Analysis (XMLA) auf den Cache einer angegebenen Dimension oder Partition zu löschen. Das Löschen des Cache zwingt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den Cache für dieses Objekt neu erstellen.  
  
## <a name="specifying-objects"></a>Angeben von Objekten  
 Die [Objekt](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) Eigenschaft von der **ClearCache** Befehl einen Objektverweis nur für eines der folgenden Objekte enthalten kann. Bei einem Objektverweis, der sich nicht auf eines der folgenden Objekte bezieht, tritt ein Fehler auf:  
  
 Datenbank  
 Löscht den Cache für alle Dimensionen und Partitionen, die in der Datenbank enthalten sind.  
  
 Dimension  
 Löscht den Cache für die angegebene Dimension.  
  
 Cube  
 Löscht den Cache für alle Partitionen, die in den Measuregruppen für den Cube enthalten sind.  
  
 Measuregruppe  
 Löscht den Cache für alle Partitionen, die in der Measuregruppe enthalten sind.  
  
 Partition  
 Löscht den Cache für die angegebene Partition.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
