---
title: SQLColAttributes Zuordnung | Microsoft Docs
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
- mapping deprecated functions [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], mapping
ms.assetid: 30e25719-176b-4c48-97d4-920766b22412
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b87311d3b913395fb0529392c7bc4ed9cc93024e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolattributes-mapping"></a>SQLColAttributes-Zuordnung
Wenn eine Anwendung ruft **SQLColAttributes** über einen ODBC 3.*.x* Treiber, den Aufruf von **SQLColAttributes** zugeordnet **SQLColAttribute** wie folgt:  
  
> [!NOTE]  
>  Das Präfix *FieldIdentifier* Werte in ODBC 3.*.x* wurde geändert, verwendet der 2 von ODBC. *X*. Das neue Präfix ist "SQL_DESC"; das alte Präfix wurde "SQL_COLUMN".  
  
1.  Wenn die Anwendung eine ODBC-2 ist. *x* Anwendung *fDescType* SQL_COLUMN_TYPE ist, und der zurückgegebene Typ ist präzise DATETIME-Typ, der Treiber-Manager-Zuordnungen, die das zurückgegebene für Datum, Uhrzeit und Timestamp-Codes Werte.  
  
2.  Wenn *fDescType* ist SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE oder SQL_COLUMN_COUNT der Treiber-Manager ruft **SQLColAttribute** in den Treiber mit der *FieldIdentifier* Argument SQL_DESC_NAME, SQL_DESC_NULLABLE oder SQL_DESC_COUNT, nach Bedarf zugeordnet *.* Alle anderen Werte des *fDescType* an den Treiber übergeben werden.  
  
 Eine ODBC 3.*.x* -Treiber muss die ODBC 3. unterstützen *.x* *FieldIdentifiers* für aufgeführten **SQLColAttribute**.  
  
 Eine ODBC 3.*.x* Treiber muss SQL_COLUMN_PRECISION und SQL_DESC_PRECISION, SQL_COLUMN_SCALE und SQL_DESC_SCALE, SQL_COLUMN_LENGTH und SQL_DESC_LENGTH unterstützen. Diese Werte unterscheiden, da mit einfacher Genauigkeit, Dezimalstellen und Länge in ODBC 3. unterschiedlich definiert sind *.x* als in ODBC 2. waren. *X*. Weitere Informationen finden Sie unter [Spaltengröße, Dezimalstellen, Oktettlänge übertragen und Anzeigegröße](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Anhang D:-Datentypen.
