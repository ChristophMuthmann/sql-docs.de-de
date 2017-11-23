---
title: Methoden (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
f1_keywords: http://schemas.microsoft.com/analysisservices/2003/engine#
helpviewer_keywords:
- methods [XML for Analysis]
- XML for Analysis, methods
- XMLA, methods
ms.assetid: c6768dd4-ca06-4a85-93b7-5fd5700886ad
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7adec520de671a643eed87a5fcda9419b9f6bfa5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---methods"></a>XML-Elemente - Methoden
  Die XML for Analysis (XMLA)-Protokoll verwendet zwei Methoden, **Discover** und **Execute**, um ein gängiges Verfahren für Anwendungen, um den Zugriff auf Informationen in einer Instanz von bieten [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Da diese Methoden mit Simple Object Access-Protokoll (SOAP) aufgerufen werden, akzeptieren Sie Eingaben und übermitteln Ausgaben in XML. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementiert beide Methoden gemäß der XML for Analysis 1.1-Spezifikation.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den folgenden Themen werden die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementierten XMLA-Methoden beschrieben.  
  
|Methode|Description|  
|------------|-----------------|  
|[Discover-Methode &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Ruft Informationen wie die Liste der verfügbaren Datenbanken oder die Details zu einem bestimmten Objekt von einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ab. Die mit der **Discover** -Methode abgerufenen Daten hängen von den Werten der an sie übergebenen Parameter ab.|  
|[Execute-Methode &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Sendet XMLA-Befehle an eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dies schließt Anforderungen im Zusammenhang mit Datenübertragung ein, z. B. das Abrufen oder Aktualisieren von Daten auf dem Server.|  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Elemente &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML-Datentypen &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML-Elemente &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
