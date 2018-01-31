---
title: GETDATE (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 290899a8b4b1bca1fb20bd18f7703d63c7bb8f51
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="getdate-ssis-expression"></a>GETDATE (SSIS-Ausdruck)
  Gibt das aktuelle Datum des Systems in einem DT_DBTIMESTAMP-Format zurück. Die GETDATE-Funktion weist keine Argumente auf.  
  
> [!NOTE]  
>  Die Länge des von der GETDATE-Funktion zurückgegebenen Ergebnisses beträgt 29 Zeichen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>Argumente  
 InclusionThresholdSetting  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 In diesem Beispiel wird das Jahr des aktuellen Datums zurückgegeben.  
  
```  
DATEPART("year",GETDATE())  
```  
  
 In diesem Beispiel wird die Anzahl von Tagen zwischen einem Datum in der **ModifiedDate** -Spalte und dem aktuellen Datum zurückgegeben.  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 In diesem Beispiel werden dem aktuellen Datum drei Monate hinzugefügt.  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GETUTCDATE &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
