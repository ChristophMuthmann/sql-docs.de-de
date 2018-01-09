---
title: Measure-Element (CSDLBI) | Microsoft Docs
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
ms.assetid: bfbc9274-053a-421a-bb81-2095bba710be
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd9dfea18c7b201dfcf5838b43d59ae0f5b942a7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="measure-element-csdlbi"></a>Measure-Element (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Das Measure-Element ist ein komplexer Typ, der auf dem CSDL-Eigenschaftselement basiert. Die CSDLBI-Anmerkungen fügen Attribute hinzu, die die Definition von komplexen Formeln für Business Intelligence-Datenmodelle unterstützen.  
  
## <a name="elements-and-attributes"></a>Elemente und Attribute  
 In der nachfolgenden Tabelle werden die Elemente und Attribute aufgeführt, die das Measure-Element definieren; darüber hinaus werden alle Attribute für das Eigenschaftselement aufgeführt.  
  
|Name|Ist erforderlich|Description|  
|----------|-----------------|-----------------|  
|Kpi|nein|Erforderliches Element nur für Measures, die als KPI verwendet werden. Nicht alle Measures sind KPIs, aber alle KPIs müssen auf der Definition eines Measures basieren.<br /><br /> [KPI-Element &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)|  
|IsSimpleMeasure|nein|Ein true/false-Wert, der angibt, ob die Formel, die im Measure verwendet wird, eine einfache Aggregationen ist (SUM, COUNT, MIN, MAX, AVG, DistinctCount).<br /><br /> Der Standardwert ist true.|  
  
## <a name="example"></a>Beispiel  
 **Tabellarisch**  
  
 Das folgende Beispiel veranschaulicht zwei Measures aus dem tabellarischen AdventureWorks-Modellbeispiel in CSDLBI, Version 1.1. Das zweite Measure wurde durch das Hinzufügen von KPI-Elementen in einen KPI konvertiert.  
  
```  
  
<Property   
    Name="Order_Lines_Count"   
    Type="Int64">  
<bi:Measure   
    Caption="Order Lines Count"   
    ReferenceName="Order Lines Count"   
    Width="0"   
    IsSimpleMeasure="false" />  
</Property>  
  
<Property   
    Name="Total_Current_Quarter_Sales_Performance"   
    Type="Double">  
<bi:Measure   
    Caption="Total Current Quarter Sales Performance"   
    ReferenceName="Total Current Quarter Sales Performance"   
    Width="0"   
    IsSimpleMeasure="false">  
    <bi:Kpi   
    StatusGraphic="Three Signs Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Goal_" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Status_" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
```  
  
## <a name="example"></a>Beispiel  
 **Multidimensiona;**  
  
 Im folgenden Beispiel wird ein Measure aus dem Contoso-Vorgangscube in CSDLBI, Version 1.1, veranschaulicht, das als KPI verwendet wird.  
  
```  
  
<Property   
    Name="Sum_of_SalesAmount"   
    Type="Decimal" Precision="19" Scale="4">  
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
  
  
