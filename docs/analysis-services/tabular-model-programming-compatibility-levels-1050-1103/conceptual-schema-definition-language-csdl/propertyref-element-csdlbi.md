---
title: PropertyRef-Element (CSDLBI) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 8299efb9-e224-4a82-bdfc-a74ec92f8711
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9df2f9bfd77a854c90f08ed8b4314bfa212bf469
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="propertyref-element-csdlbi"></a>PropertyRef-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Das PropertyRef-Element ist ein einfacher Typ, der einen Verweis auf eine Spalte bereitstellt, das einen Wert, der von einer anderen Eigenschaft benötigt bereitstellt.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der folgenden Tabelle sind die Elemente und Attribute aufgeführt, die das PropertyRef-Element definieren.  
  
|Name|Ist erforderlich|Description|  
|----------|-----------------|-----------------|  
|Name|ja|Eine Zeichenfolge, die den Namen der Eigenschaft enthält, die Ziel des Verweises ist.|  
  
## <a name="propertyrefs-element"></a>PropertyRefs-Element  
 PropertyRefs ist ein komplexer Typ, der eine Auflistung von Eigenschaften definiert, wobei jede Eigenschaft in einem PropertyRef-Element enthalten ist.  
  
 In der folgenden Tabelle sind die Elemente und Attribute des PropertyRefs-Typs aufgeführt.  
  
|Name|Ist erforderlich|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|ja|Eine Zeichenfolge, die den Eigenschaftsverweis enthält.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Im folgenden Beispiel wird für das tabellarische AdventureWorks-Modellbeispiel in CSDLBI, Version 1.1, ein PropertyRef-Element veranschaulicht, das den Ursprung einer Formel angibt, die in einem Measure verwendet wird.  
  
```  
<bi:Measure Caption="Total Current Quarter Margin Performance" ReferenceName="Total Current Quarter Margin Performance" Width="0" IsSimpleMeasure="false">  
  <bi:Kpi StatusGraphic="Three Symbols UnCircled Colored">  
    <bi:KpiGoal>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Goal_" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Status_" />  
    </bi:KpiStatus>  
  </bi:Kpi>  
</bi:Measure>  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensional**  
  
 Im folgenden Beispiel wird in CSDLBI, Version 1.1, ein KPI aus dem Contoso-Vorgangscube veranschaulicht. Die PropertyRef-Elemente zeigen auf den Spalten, die die Formel oder die Werte enthalten, die verwendet werden, um das Ziel und den Status des KPI in Bezug auf das Ziel zu definieren.  
  
```  
<Property Name="Sum_of_SalesAmount" Type="Decimal" Precision="19" Scale="4">  
   <Documentation>  
     <Summary>KPI Description</Summary>  
   </Documentation>  
     <bi:Measure   
         Caption="Sum of SalesAmount"   
         ReferenceName="Sum of SalesAmount"   
         FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
     <bi:Kpi   
           StatusGraphic="Three Circles Colored">  
         <bi:KpiGoal>  
            <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
          </bi:KpiGoal>  
          <bi:KpiStatus>  
              <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
          </bi:KpiStatus>  
     </bi:Kpi>  
     </bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Technische Referenz für BI-Anmerkungen zu CSDL](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
