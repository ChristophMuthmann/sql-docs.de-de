---
title: REPLACENULL (SSIS-Ausdruck) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b99a726d050dc2235f653061295e5f0829e93150
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="replacenull-ssis-expression"></a>REPLACENULL (SSIS-Ausdruck)
  Gibt den Wert des zweiten Ausdrucksparameters zurück, wenn der erste Ausdrucksparameter NULL ist; andernfalls wird der Wert des ersten Ausdrucks zurückgegeben.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>Argumente  
 *expression 1*  
 Das Ergebnis dieses Ausdrucks wird mit NULL verglichen.  
  
 *expression 2*  
 Das Ergebnis dieses Ausdrucks wird zurückgegeben, wenn der erste Ausdruck NULL ergibt.  
  
## <a name="result-types"></a>Ergebnistypen  
 DT_WSTR  
  
## <a name="remarks"></a>Hinweise  
  
-   Die Länge von *expression 2* darf Null sein.  
  
-   REPLACENULL gibt ein NULL-Ergebnis zurück, wenn eines der Argumente NULL ist.  
  
-   BLOB-Spalten (DT_TEXT, DT_NTEXT, DT_IMAGE) werden von keimen der beiden Parameter unterstützt.  
  
-   Es wird davon ausgegangen, dass die zwei Ausdrücke den gleichen Rückgabetyp haben. Andernfalls versucht die Funktion, den 2. Ausdruck in den Rückgabetyp des 1. Ausdrucks umzuwandeln, was möglicherweise zu einem Fehler führt, wenn die Datentypen nicht kompatibel sind.  
  
## <a name="expression-examples"></a>Beispiele für Ausdrücke  
 Im folgenden Beispiel wird ein beliebiger NULL-Wert in einer Datenbankspalte durch eine Zeichenfolge (1900-01-01) ersetzt. Diese Funktion wird vor allem in häufigen Mustern für abgeleitete Spalten verwendet, in denen Sie NULL-Werte durch andere Werte ersetzen möchten.  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]  
>  Das folgende Beispiel zeigt, wie vorgegangen wurde [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] / [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)].  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? “1900-01-01” : MyColumn)   
```  
  
  

