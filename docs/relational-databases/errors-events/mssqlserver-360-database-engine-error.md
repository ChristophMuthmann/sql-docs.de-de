---
title: MSSQLSERVER_360 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 360 (Database Engine error)
ms.assetid: e2b7c1b2-3679-4206-9b25-6bd55ef96a2c
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 6c7ea84073c7326a510402e66bdbcf126f77e87b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver360"></a>MSSQLSERVER_360
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|360|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DML_UPDATE_SPARSE_AND_COLSET|  
|Meldungstext|Die Zielspaltenliste einer INSERT-, UPDATE- oder MERGE-Anweisung kann nicht sowohl eine Sparsespalte als auch den Spaltensatz enthalten, in dem sich die Sparsespalte befindet. Schreiben Sie die Anweisung um, sodass entweder nur die Sparsespalte oder nur der Spaltensatz enthalten ist.|  
  
## <a name="explanation"></a>Erklärung  
Ein Spaltensatz ist eine nicht typisierte XML-Darstellung, in der einige Spalten einer Tabelle zu einer strukturierten Ausgabe zusammengefasst werden. Es wurde versucht, sowohl den Spaltensatz als auch eine Spalte aus dem Spaltensatz zu ändern, sodass zwei Verweise auf die gleiche Spalte entstanden.  
  
## <a name="user-action"></a>Benutzeraktion  
Schreiben Sie die Anweisung um, sodass Verweise auf entweder die Spalte mit geringer Dichte oder auf den Spaltensatz enthalten sind. Schließen Sie jedoch keinesfalls beide in die Anweisung ein.  
  
