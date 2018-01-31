---
title: ROUND (SSIS-Ausdruck) | Microsoft-Dokumentation
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
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc531db140527e9ec2bfd73adffb2a81f2bcfcf4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="round-ssis-expression"></a>ROUND (SSIS-Ausdruck)
  Gibt einen numerischen Ausdruck zurück, der auf die angegebene Länge oder Genauigkeit gerundet wurde. Der length-Parameter muss zu einer ganzen Zahl ausgewertet werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>Argumente  
 *numeric_expression*  
 Ein Ausdruck eines gültigen numerischen Datentyps. Weitere Informationen finden Sie unter [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *length*  
 Ein ganzzahliger Ausdruck. Dies ist die Genauigkeit, auf die *numeric_expression* gerundet wird.  
  
## <a name="result-types"></a>Ergebnistypen  
 Der Typ entspricht dem Typ von *numeric*_*expression*.  
  
## <a name="remarks"></a>Remarks  
 Das *length* -Argument muss zu einer positiven ganzen Zahl oder 0 (null) ausgewertet werden.  
  
 ROUND gibt ein NULL-Ergebnis zurück, wenn das Argument NULL ist.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Diese Beispiele runden numerische Literale auf eine Länge von drei. Als erstes Ergebnis wird 137.1570 zurückgegeben und als zweites Ergebnis 137.1580.  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Funktionen &#40;SSIS-Ausdruck&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
