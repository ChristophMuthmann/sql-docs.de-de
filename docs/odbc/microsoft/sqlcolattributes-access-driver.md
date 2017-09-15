---
title: SQLColAttributes (Access-Treiber) | Microsoft Docs
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
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2531bbc58e55c3c58452701f1dd66ac6702a535
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (Access-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Access-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attribut|Kommentare|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Für "LONGVARBINARY"-Daten ist SQL_COLUMN_DISPLAY_SIZE die maximale Länge der Spalte, nicht die maximale Länge der Spalte multipliziert 2.|  
|SQL_OWNER_NAME|Eine leere Zeichenfolge ("") wird in dieser Spalte zurückgegeben, weil der Name des Besitzers nicht unterstützt wird.|  
|SQL_QUALIFIER_NAME|Der Pfad zu einer Datenbankdatei wird zurückgegeben.|  
|SQL_COLUMN_SEARCHABLE|"LONGVARBINARY" und LONGVARCHAR Spalten werden als SQL_UNSEARCHABLE gemeldet.<br /><br /> Fester und variabler Länge, Binär und Unicodezeichen-Datentypen werden durchsucht werden, obwohl "LONGVARBINARY" und LONGVARCHAR nicht.|  
  
> [!NOTE]  
>  Oben ist keine vollständige Liste der Attribute zurückgegebenes **SQLColAttributes**.
