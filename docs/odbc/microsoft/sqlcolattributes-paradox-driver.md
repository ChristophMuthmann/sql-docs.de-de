---
title: SQLColAttributes (Paradox-Treiber) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 414ad2afeb627b413ecfc3ee166f694813e2676a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes (Paradox-Treiber)
> [!NOTE]  
>  Dieses Thema enthält Paradox treiberspezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attribut|Kommentare|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Für "LONGVARBINARY"-Daten ist SQL_COLUMN_DISPLAY_SIZE die maximale Länge der Spalte, nicht die maximale Länge der Spalte multipliziert 2.|  
|SQL_OWNER_NAME|Eine leere Zeichenfolge ("") wird in dieser Spalte zurückgegeben, weil der Name des Besitzers nicht unterstützt wird.|  
|SQL_QUALIFIER_NAME|Der Pfad zu einem Verzeichnis zurückgegeben wird.|  
|SQL_COLUMN_SEARCHABLE|"LONGVARBINARY" und LONGVARCHAR Spalten werden als SQL_UNSEARCHABLE gemeldet.<br /><br /> Fester und variabler Länge, Binär und Unicodezeichen-Datentypen werden durchsucht werden, obwohl "LONGVARBINARY" und LONGVARCHAR nicht.|  
  
> [!NOTE]  
>  Oben ist keine vollständige Liste der Attribute zurückgegebenes **SQLColAttributes**.

