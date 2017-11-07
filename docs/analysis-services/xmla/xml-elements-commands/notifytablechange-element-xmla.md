---
title: NotifyTableChange-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NotifyTableChange Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 45e156076d7d97164fcb43674e3975daf6944e1e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange-Element (XMLA)
  Benachrichtigt eine Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , die mit Tabellen in einer bestimmten Datenquelle ist eine Änderung aufgetreten.  
  
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
  
  

