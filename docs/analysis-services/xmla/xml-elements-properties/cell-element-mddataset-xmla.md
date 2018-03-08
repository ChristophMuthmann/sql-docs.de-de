---
title: Cell-Element (MDDataSet) (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Cell Element (MDDataSet)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords: Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d6c59b1833e211e43c9429e6bf4aeb265325d76d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="cell-element-mddataset-xmla"></a>Cell-Element (MDDataSet) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Enthält Informationen über eine einzelne Zelle, die von einer übergeordneten enthaltenen [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<CellData>  
   <Cell CellOrdinal="unsignedInt">  
      <!-- Zero or more cell property values -->  
      <!-- or -->  
      <Error>...</Error>  
   </Cell>  
</CellData>  
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
|Übergeordnete Elemente|[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)|  
|Untergeordnete Elemente|NULL oder mehr zelleigenschaftswerte oder [Fehler](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)|  
  
## <a name="attributes"></a>Attribute  
  
|attribute|Description|  
|---------------|-----------------|  
|CellOrdinal|Erforderliche **UnsignedInt** Attribut. Die Ordnungsposition der Zelle innerhalb des mehrdimensionalen Datasets.|  
  
## <a name="remarks"></a>Remarks  
 In der übergeordneten Tabelle **Stamm** Element, das **Achsen** Element ist, gefolgt vom der **CellData** -Element, das eine Auflistung von **Zelle** Elementen mit die Eigenschaftswerte für jede Zelle in dem multidimensionalen Datensatz zurückgegeben. Die **Zelle** Element enthält die **CellOrdinal** -Attribut, das die nullbasierte Ordnungsposition der Zelle innerhalb des mehrdimensionalen Datensatzes, und ein Element für jeden zelleneigenschaftswert angibt. der Zelle zugeordnet ist. Jeder zelleneigenschaftswert in der **Zelle** -Element wird durch ein separates XML-Element definiert. Der Wert der Zelleneigenschaft ist das XML-Element und der Name der Zelleneigenschaft, enthaltenen Daten gemäß der **CellInfo** Element des übergeordneten "Root"-Element entspricht dem Namen des XML-Elements.  
  
 Die folgende Syntax beschreibt einen Zelleneigenschaftswert:  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 Der Datentyp eines Zelleneigenschaftswerts wird nur für die VALUE-Zelleneigenschaft angegeben. Die Datentypen anderer Zelleneigenschaften werden durch die zelleneigenschaftsdefinition im bestimmt die **CellInfo** Element. Ein zelleneigenschaftswert kann ausgeschlossen werden, wenn ein Standardwert angegeben wurde (durch Einschließen einer **Standard** -Element für die Definition einer Zelleneigenschaft in enthaltenen der **CellInfo** Element) für eine Zelleneigenschaft oder wenn kein Standardwert angegeben wurde und der Wert der Zelleneigenschaft null ist.  
  
## <a name="cell-property-errors"></a>Zelleneigenschaftsfehler  
 Wenn eine Zelleneigenschaft aufgrund eines Fehlers zurückgegeben werden kann, die für die Instanz von stattfindet [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], z. B. ein Berechnungsfehler, der verhindert, dass den Wert, der für eine bestimmte Zelle zurückgegeben wird ein **Fehler** Element ersetzt den Inhalt der fraglichen Zelleneigenschaft. Das folgende XML-Beispiel beschreibt einen Zelleneigenschaftsfehler:  
  
```  
<Cell CellOrdinal="0">  
   <Value xsi:type="xsd:double">  
      <Error>  
         <ErrorCode>2148497527</ErrorCode>  
         <Description>Unknown error</Description>  
      </Error>  
   </Value>  
</Cell>  
```  
  
## <a name="calculating-cell-ordinal-values"></a>Berechnen der Ordinalwerte der Zelle  
 Der achsenverweis für eine Zelle berechnet werden kann, basierend auf einer **CellOrdinal** Attributwert. Grundsätzlich werden Zellen in einem Dataset nummeriert, als wäre das Dataset eine *p*-dimensionales Array, in dem *p* ist die Anzahl der Achsen. Die Zellen werden in zeilengerichteter Reihenfolge adressiert.  
  
 Hier wird angenommen, dass eine Anforderung vier Measures auf den Spalten und einen Crossjoin mit zwei Status mit vier Quartalen auf den Zeilen anfordert. Im folgenden Dataset-Ergebnis der **CellOrdinal** Eigenschaft für den Anteil der Dataset-Ergebnis, das in fett formatiertem Text ist der Satz {9, 10, 11, 13, 14, 15, 17, 18, 19}. Dies ist der Satz, da die Zellen in zeilengerichteter Reihenfolge nummeriert sind beginnend mit einem **CellOrdinal** 0 für die obere linke Zelle.  
  
|Status|Quarter|Unit Sales|Store-Cost|Store-Sales|Sales-Count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||Q2|18052|15332.02|38396.75|5915|  
||F3|18370|**15672.83**|**39394.05**|**6014**|  
||Q4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||Q2|15079|12678.96|31772.88|4799|  
||F3|16940|14273.78|35880.46|5432|  
||Q4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||Q2|29479|24953.25|62496.64|9654|  
||F3|30538|25958.26|64997.38|10007|  
||Q4|34235|29172.72|73016.34|11217|  
  
 Wenn die in der Abbildung gezeigte Formel angewendet wird, hat die Achse k = 0 Uk = 4 Elemente und die Achse k = 1 Uk = 8 Tupel. P = 2 ist die Gesamtzahl der Achsen in der Abfrage. Wenn man die Zelle mit dem Inhalt {Kalifornien, Q3, Speicherkosten} als S0 nimmt, ist die ursprüngliche Summe i = 0 bis 1. Für i = 0 ist die Tupelordinalzahl auf Achse 0 auf {Speicherkosten} 1. Für i = 1 ist die Tupelordinalzahl von {CA, Q3} 2.  
  
 Für i = 0 Ei = 1, dies der Fall ist für ich = 0 die Summe entspricht 1 * 1 = 1 und für ich = 1, die Summe ist 2 (tupelordinalzahl) Mal 4 (der Wert von Ei berechnet als 1 \* 4), oder 8. Die Summe von 1 + 8 ist dann 9, die Zellenordinalzahl für diese Zelle.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht die Struktur der **Zelle** -Element, einschließlich der Wert, FORMATTED_VALUE und FORMAT_STRING-Zelleneigenschaftswerte für jede Zelle.  
  
```  
<CellData>  
   <Cell CellOrdinal="0">  
      <Value xsi:type="xsd:double">16890</Value>  
      <FmtValue>16,890.00</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="1">  
      <Value xsi:type="xsd:int">50</Value>  
      <FmtValue>50</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="2">  
      <Value xsi:type="xsd:double">36175.2</Value>  
      <FmtValue>$36,175.20</FmtValue>  
      <FormatString>Currency</FormatString>  
   </Cell>  
</CellData>  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [MDDataSet-Datentyp &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
