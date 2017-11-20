---
title: OPENQUERY (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENQUERY
dev_langs:
- DMX
helpviewer_keywords:
- OPENQUERY statement
ms.assetid: fe57f3a3-a8e6-402c-995e-bd2fe28a7a7c
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: edfae84521fae05a34448cf0f8ea3ace01e31ed4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt---openquery"></a>&lt;quelldatenabfrage&gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ersetzt die Quelldatenabfrage durch eine Abfrage an eine vorhandene Datenquelle. Die Anweisungen INSERT, SELECT FROM PREDICTION JOIN und SELECT FROM NATURAL PREDICTION JOIN unterstützen **OPENQUERY**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumente  
 *benannte datasource*  
 Eine Datenquelle, die auf die [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Datenbank.  
  
 *Abfragesyntax*  
 Eine Abfragesyntax, die ein Rowset zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 **OPENQUERY** bietet eine sicherere Möglichkeit für das Zugreifen auf externe Daten, weil es Datenquellenberechtigungen unterstützt. Da die Verbindungszeichenfolge direkt in der Datenquelle gespeichert wird, können Administratoren die Eigenschaften der Datenquelle dazu verwenden, den Zugriff auf die Daten zu verwalten. Weitere Informationen zu Datenquellen finden Sie unter [unterstützte Datenquellen &#40; SSAS – mehrdimensional &#41; ](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 Durch Abfragen des **MDSCHEMA_INPUT_DATASOURCES** -Schemarowsets können Sie eine Liste der Datenquellen abrufen, die auf einem Server verfügbar sind. Weitere Informationen zur Verwendung von **MDSCHEMA_INPUT_DATASOURCES**, finden Sie unter [MDSCHEMA_INPUT_DATASOURCES-Rowset](../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md).  
  
 Sie können auch eine Liste mit Datenquellen in der aktuellen Analysis Services-Datenbank zurückgeben, indem Sie folgende DMX-Abfrage verwenden:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die MyDS-Datenquelle, die bereits in definiert die [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Datenbank erstellen Sie eine Verbindung mit der [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] Datenbank und zum Abfragen der **vTargetMail** anzeigen.  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Siehe auch  
 [&#60; quelldatenabfrage &#62;](../dmx/source-data-query.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

