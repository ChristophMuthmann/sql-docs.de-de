---
title: Standard-C-Datentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ff8e2e111db13f67c80189d225dad5084bfdb6e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="default-c-data-types"></a>Standard-C-Datentypen
Wenn eine Anwendung in SQL_C_DEFAULT gibt **SQLBindCol**, **SQLGetData**, oder **SQLBindParameter**, der Treiber wird davon ausgegangen, dass der C-der Ausgabe oder Eingabepuffer Datentyp entspricht dem SQL-Datentyp der Spalte oder des Parameters, der der Puffer gebunden ist.  
  
> [!IMPORTANT]  
>  Interoperable Anwendungen ausführen können, sollten nicht SQL_C_DEFAULT verwenden. Stattdessen sollten sie immer die C-Typ des Puffers angeben, die sie verwenden. Da Treiber den Standard-C-Typ aus den folgenden Gründen nicht immer ordnungsgemäß bestimmen können sieht folgendermaßen aus:  
  
-   Wenn das DBMS einen SQL-Datentyp einer Spalte oder Parameter heraufstuft, kann nicht vom Treiber nicht den ursprünglichen SQL-Datentyp einer Spalte oder Parameter ermittelt. Aus diesem Grund kann nicht die entsprechenden Standard-C-Datentyp geprüft.  
  
-   Wenn der Treiber, ob eine bestimmte Spalte oder Parameter signiert ist, nicht ermitteln kann, wie häufig der Fall ist, wenn der Vorgang wurde sollte vom DBMS, verarbeitet der Treiber kann nicht bestimmt werden, ob der entsprechende Standard C-Datentyp mit oder ohne Vorzeichen sein.  
  
     SQL_C_DEFAULT nur als eine Vereinfachung der Programmierung bereitgestellt wird, wird die Anwendung keine Funktionalität verloren, wenn die tatsächliche C-Datentyp angegeben.  
  
 Eine Tabelle mit den Standard-C-Datentyp für jeden SQL-Datentyp dient in [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)weiter unten in diesem Anhang.
