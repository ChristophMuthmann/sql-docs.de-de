---
title: XML-Datentypen (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 57e14656a089736a8b7ce9566362c9d7c8888a5d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="xml-data-types-xmla"></a>XML-Datentypen (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Zusätzlich zu den standardmäßigen Grundtypen und abgeleiteten Typen definiert, die von der XML 1.0-Empfehlung definiert die XML for Analysis (XMLA) 1.1-Spezifikation zusätzliche Datentypen, um die Darstellung von mehrdimensionalen und tabellarischen Daten zu unterstützen.  
  
 XMLA verwendet die in der folgenden Tabelle aufgelisteten Datentypen.  
  
|Datentypen|Description|  
|----------------|-----------------|  
|Boolean|Der **boolean** -XML-Standarddatentyp.|  
|Decimal|Der **decimal** -XML-Standarddatentyp.|  
|[EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|Ein Namespace auf dem **root** -Element. Dieser Namespace wird zurückgegeben, wenn ein XMLA-Befehl kein Ergebnis zurückgibt, weil der XMLA-Befehl nicht normalerweise kein Ergebnis zurückgibt, oder aufgrund eines Fehlers auf das [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz beim Ausführen des XMLA-Befehls.|  
|[EnumString](../../../analysis-services/xmla/xml-data-types/enumstring-data-type-xmla.md)|Ein Satz genannter Zeichenfolgenkonstanten für einen gegebenen Enumerator.|  
|Integer|Der **int** -XML-Standarddatentyp.|  
|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)|Mehrdimensionale Daten, die zurückgegeben werden, indem Sie die *Ergebnis* Parameter von der [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Methode.|  
|[Resultset](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|Ein selbstbeschreibendes XML-Resultset, das von der **Execute** -Methode zurückgegeben wird.|  
|[Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|Zurückgegebene Zeilen aus einer Datenquelle, die von einem eingebetteten XML-Schema strukturiert wurden die [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) Methode.|  
|Zeichenfolge|Der **string** -XML-Standarddatentyp.|  
|UnsignedInt|Der **unsignedInt** -XML-Schematyp.|  
  
 Vollständige Beschreibungen der XML-Standarddatentypen finden Sie in den Kandidatenempfehlungen des World Wide Web Consortium (WC3).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Elemente &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML for Analysis &#40; XMLA &#41; Referenz](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
