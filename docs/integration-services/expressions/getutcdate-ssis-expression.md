---
title: GETUTCDATE (SSIS-Ausdruck) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 07df1948bdd1a6d74ef3a858c1823838ab8e07a7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (SSIS-Ausdruck)
  Gibt das aktuelle Datum des Systems als UTC-Zeit (Universal Time Coordinate oder Greenwich Mean Time) in einem DT_DBTIMESTAMP-Format zurück. Die GETUTCDATE-Funktion weist keine Argumente auf.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>Argumente  
 InclusionThresholdSetting  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird das Jahr des aktuellen Datums als UTC-Zeit zurückgegeben.  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 In diesem Beispiel wird die Anzahl von Tagen zwischen einem Datum in der **ModifiedDate** -Spalte und dem aktuellen UTC-Datum zurückgegeben.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 In diesem Beispiel werden dem aktuellen UTC-Datum drei Monate hinzugefügt.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GETDATE &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
