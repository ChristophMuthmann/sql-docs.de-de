---
title: SQLColAttributes (Excel-Treiber) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Excel Driver
ms.assetid: 7c4833e3-ff0c-4313-9ab8-21379ceab656
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 776fac64a8e0da05964013dced69bc1d4d5e8aae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolattributes-excel-driver"></a>SQLColAttributes (Excel-Treiber)
> [!NOTE]  
>  Dieses Thema enthält die Excel-Treiber-spezifische Informationen. Allgemeine Informationen zu dieser Funktion finden Sie unter den entsprechenden Themen unter [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Attribut|Kommentare|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|Für "LONGVARBINARY"-Daten ist SQL_COLUMN_DISPLAY_SIZE die maximale Länge der Spalte, nicht die maximale Länge der Spalte multipliziert 2.|  
|SQL_OWNER_NAME|Eine leere Zeichenfolge ("") wird in dieser Spalte zurückgegeben, weil der Name des Besitzers nicht unterstützt wird.|  
|SQL_QUALIFIER_NAME|Der Pfad zu einem Verzeichnis zurückgegeben wird.|  
|SQL_COLUMN_SEARCHABLE|"LONGVARBINARY" und LONGVARCHAR Spalten werden als SQL_UNSEARCHABLE gemeldet.<br /><br /> Fester und variabler Länge, Binär und Unicodezeichen-Datentypen werden durchsucht werden, obwohl "LONGVARBINARY" und LONGVARCHAR nicht.|  
  
> [!NOTE]  
>  Oben ist keine vollständige Liste der Attribute zurückgegebenes **SQLColAttributes**.
