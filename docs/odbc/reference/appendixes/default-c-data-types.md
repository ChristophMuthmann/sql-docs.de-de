---
title: Standard-C-Datentypen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83040ffdab8b9715fc8caeb024bec6a9fc05d4d4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="default-c-data-types"></a>Standard-C-Datentypen
Wenn eine Anwendung in SQL_C_DEFAULT gibt **SQLBindCol**, **SQLGetData**, oder **SQLBindParameter**, der Treiber wird davon ausgegangen, dass der C-der Ausgabe oder Eingabepuffer Datentyp entspricht dem SQL-Datentyp der Spalte oder des Parameters, der der Puffer gebunden ist.  
  
> [!IMPORTANT]  
>  Interoperable Anwendungen ausführen können, sollten nicht SQL_C_DEFAULT verwenden. Stattdessen sollten sie immer die C-Typ des Puffers angeben, die sie verwenden. Da Treiber den Standard-C-Typ aus den folgenden Gründen nicht immer ordnungsgemäß bestimmen können sieht folgendermaßen aus:  
  
-   Wenn das DBMS einen SQL-Datentyp einer Spalte oder Parameter heraufstuft, kann nicht vom Treiber nicht den ursprünglichen SQL-Datentyp einer Spalte oder Parameter ermittelt. Aus diesem Grund kann nicht die entsprechenden Standard-C-Datentyp geprüft.  
  
-   Wenn der Treiber, ob eine bestimmte Spalte oder Parameter signiert ist, nicht ermitteln kann, wie häufig der Fall ist, wenn der Vorgang wurde sollte vom DBMS, verarbeitet der Treiber kann nicht bestimmt werden, ob der entsprechende Standard C-Datentyp mit oder ohne Vorzeichen sein.  
  
     SQL_C_DEFAULT nur als eine Vereinfachung der Programmierung bereitgestellt wird, wird die Anwendung keine Funktionalität verloren, wenn die tatsächliche C-Datentyp angegeben.  
  
 Eine Tabelle mit den Standard-C-Datentyp für jeden SQL-Datentyp dient in [Konvertieren von Daten aus SQL in C-Datentypen](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)weiter unten in diesem Anhang.
