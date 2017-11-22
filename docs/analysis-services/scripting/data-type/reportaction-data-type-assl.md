---
title: ReportAction-Datentyp (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ReportAction Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReportAction
helpviewer_keywords: ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2d88cfbf36d07dec984d38712b8e5ab893d811a5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="reportaction-data-type-assl"></a>ReportAction-Datentyp (ASSL)
  Definiert einen abgeleiteten Datentyp, der eine Aktion darstellt, generiert eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Bericht.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<ReportAction>  
   <!-- The following elements extend Action -->  
   <ReportServer>...</ReportServer>  
   <Path>...</Path>  
   <ReportParameters>...</ReportParameters>  
   <ReportFormatParameters>...</ReportFormatParameters>  
</ReportAction>  
```  
  
## <a name="data-type-characteristics"></a>Datentypmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Basisdatentypen|[Aktion](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|Abgeleitete Datentypen|Keine|  
  
## <a name="data-type-relationships"></a>Datentypbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|Keine|  
|Untergeordnete Elemente|[Pfad](../../../analysis-services/scripting/properties/path-element-assl.md), [ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md), [ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md), [ReportServer](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|  
|Abgeleitete Elemente|[Aktion](../../../analysis-services/scripting/objects/action-element-assl.md) ([Aktionen](../../../analysis-services/scripting/collections/actions-element-assl.md) Auflistung von [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) oder [Perspektive](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Hinweise  
 Der Berichtsserver antwortet auf URL-basierte Anforderungen nach Berichten. Die Berichtsaktion wird über einen Typen- *Report*definiert. Die Ressourcen und Parameter werden als Bestandteil der URL-Zeichenfolge an den Server gesendet, wenn die Aktion erstellt wird. Der Server macht die Aktion als Aktion des Typrowsets verfügbar.  
  
 Das entsprechende Element im Objektmodell von Analysis Management Objects (AMO) ist <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services Scripting Language-XML-Datentypen &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
