---
title: Verwenden von Variablen und Parametern (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c34ab14400aa2f40495b9931422751c43c6260e9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-variables-and-parameters-mdx"></a>Verwenden von Variablen und Parametern (MDX)
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]können Sie eine MDX-Anweisung (Multidimensional Expressions) parametrisieren. Eine parametrisierte Anweisung ermöglicht Ihnen das Erstellen von allgemeinen Anweisungen, die während der Laufzeit angepasst werden können.  
  
 Beim Erstellen einer parametrisierten Anweisung kennzeichnen Sie den Parameternamen, indem Sie dem Namen das @-Zeichen voranstellen. Beispielsweise @Year wäre ein gültiger Parametername  
  
 MDX unterstützt Parameter nur für Literal- oder skalare Werte. Zum Erstellen eines Parameters, der auf ein Element, eine Menge oder ein Tupel verweist, müssen Sie eine Funktion verwenden (z. B. [StrToMember](../../../mdx/strtomember-mdx.md) oder [StrToSet](../../../mdx/strtoset-mdx.md)).  
  
 In der folgenden XML for Analysis (XMLA) beispielsweise die @CountryName Parameter enthält das Land, für welche Kunden Daten abgerufen:  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 Wenn Sie diese Funktionalität mit OLE DB verwenden möchten, verwenden Sie die **ICommandWithParameters** -Schnittstelle. Wenn Sie diese Funktionalität mit ADOMD.Net verwenden möchten, verwenden Sie die **AdomdCommand.Parameters** -Auflistung.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
