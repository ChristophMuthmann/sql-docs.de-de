---
title: Sperren-Element (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Lock Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98e5087dc10ae495dec711c35fa807cb9fd68e02
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="lock-element-xmla"></a>Lock-Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Sperrt ein bestimmtes Objekt auf eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|Datentyp und -länge|InclusionThresholdSetting|  
|Standardwert|InclusionThresholdSetting|  
|Cardinality|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md), [Modus](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md), [Objekt](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Der **Lock** -Befehl sperrt die gemeinsame oder exklusive Nutzung eines Objekts im Rahmen der derzeit aktiven Transaktion. Nur Datenbankadministratoren oder Serveradministratoren können explizit einen **Lock** -Befehl ausgeben. Eine Sperre in einem Objekt verhindert, dass ein Commit für Transaktionen ausgeführt wird, bevor die Sperre entfernt wurde. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] unterstützt zwei Arten von Sperren: gemeinsame Sperren und exklusive Sperren. Weitere Informationen zu den von unterstützten Typen von Sperren [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], finden Sie unter [Mode-Element &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ermöglicht nur die Sperrung von Datenbanken. Die **Objekt** Element muss einen Objektverweis auf enthalten eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank. Wenn das **Object** -Element nicht angegeben ist oder wenn das **Object** -Element auf ein Objekt verweist, bei dem es sich nicht um eine Datenbank handelt, tritt ein Fehler auf.  
  
 Andere Befehle geben implizit eine **Sperre** Befehl eine [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank. Jeder Vorgang, der Daten oder Metadaten aus einer Datenbank einliest (z. B. jede **Discover** -Methode oder eine **Execute** -Methode, die einen **Statement** -Befehl ausführt), gibt implizit eine gemeinsame Sperre der Datenbank aus. Jede Transaktion, die Änderungen an Daten oder Metadaten zu einem Objekt auf ein Commit ausgeführt wird ein [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Datenbank, z. B. ein **Execute** externen ausgeführte Methode ein **Alter** Befehl, gibt implizit eine exklusive Sperre für die die Datenbank.  
  
 Alle Sperren werden im Kontext der aktuellen Transaktion abgehalten. Wenn die aktuelle Transaktion ausgeführt oder für diese ein Rollback durchgeführt wird, werden alle Sperren, die innerhalb der Transaktion definiert sind, automatisch aufgehoben.  
  
## <a name="see-also"></a>Siehe auch  
 [Unlock-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
