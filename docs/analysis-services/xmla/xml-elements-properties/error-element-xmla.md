---
title: Error-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
apiname: Error Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords: Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8071fdade167282df64330bce680c44b73a2c533
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="error-element-xmla"></a>Error-Element (XMLA)
  Enthält Informationen zu einem Fehler zurückgegeben, die von einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Message>  
   <Error   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
<!-- or -->  
<Cell><!-- or row -->  
   <!-- A child element -->  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception"  
         < ErrorCode>...</ErrorCode>  
         < Description>...</Description>  
         < Source>...</Source>  
         < HelpFile>...</HelpFile>  
      </Error>  
   <!-- /A child element -- >  
</Cell>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-1: Optionales Element, das nur einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[MessageBox](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Untergeordnete Elemente|Finden Sie in der folgenden Tabelle aus.|  
  
|Ancestor|Untergeordnete Elemente|  
|--------------|--------------------|  
|[MessageBox](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|Keine|  
|[Zelle](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [Zeile](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Beschreibung](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [Quelle](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|ErrorCode|Erforderliche **UnsignedInt** Attribut (nur wenn **Nachricht** ist das übergeordnete Element.) Enthält den numerischen Rückgabecode des Fehlers.|  
|Severity|Optionale **Zeichenfolge** Attribut (nur wenn **Nachricht** ist das übergeordnete Element.) Enthält das Ausmaß des Fehlers.|  
|Description|Optionale **Zeichenfolge** Attribut (nur wenn **Nachricht** ist das übergeordnete Element.) Enthält den beschreibenden Text des Fehlers.|  
|Quelle|Optionale **Zeichenfolge** Attribut (nur wenn **Nachricht** ist das übergeordnete Element.) Enthält den Namen der Komponente, die den Fehler generiert hat.|  
|HelpFile|Optionale **Zeichenfolge** Attribut (nur wenn **Nachricht** ist das übergeordnete Element.) Enthält den Pfad oder die URL zur Hilfedatei oder dem Thema, das den Fehler beschreibt.|  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="see-also"></a>Siehe auch  
 [Warning-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
