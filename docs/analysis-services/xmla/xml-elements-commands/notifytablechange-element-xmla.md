---
title: NotifyTableChange-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: NotifyTableChange Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords: NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 66d277cd3bff3c0dfbb8ea95d0ac6ca76be20f78
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Benachrichtigt eine Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , die mit Tabellen in einer bestimmten Datenquelle ist eine Änderung aufgetreten.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <NotifyTableChange>  
      <Object>...</Object>  
      <TableNotifications>...</TableNotifications>  
   </NotifyTableChange>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Die **NotifyTableChange** Befehl ermöglicht einer Clientanwendung explizit benachrichtigen ein [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz fest, dass eine oder mehrere Tabelle(n) in einer Datenquelle geändert wurden. Beim proaktiven Caching zeigt diese Benachrichtigung an, dass relationale OLAP-Objekte (ROLAP), die auf diesen Tabellen basieren, überprüft und aktualisiert werden sollten.  
  
 Diese Benachrichtigungsmethode wird am besten für ROLAP-Objekte verwendet, die auf Sichten oder benannten Abfragen basieren, die in einer Datenquellensicht definiert sind, deren Änderungen schwer zu erkennen sind.  
  
 Die **Objekt** -Element muss auf eine Datenquelle in verweisen die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank. Wenn das **Object** -Element auf ein Objekt verweist, bei dem es sich nicht um eine Datenquelle handelt, tritt ein Fehler auf.  
  
 Weitere Informationen zum proaktiven Zwischenspeichern finden Sie unter [Proaktives Zwischenspeichern &#40;Partitionen&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
