---
title: "Übertragen Sie Oktettlänge | Microsoft Docs"
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
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 763f6fdd2790de695e1e2307cbcac4e0ed3018ae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="transfer-octet-length"></a>Oktettlänge übertragen
Die Übertragung Oktettlänge einer Spalte ist die maximale Anzahl von Bytes, die an die Anwendung zurückgegeben werden, wenn Daten, um die Standard-C-Datentyp übertragen werden. Bei Zeichendaten umfasst die Übertragung Oktettlänge nicht Speicherplatz für die Null-Abschlusszeichen. Die Übertragung Oktettlänge einer Spalte möglicherweise anders als die Anzahl der Bytes, die zum Speichern der Daten in der Datenquelle erforderlich sind.  
  
 Die Übertragung Oktettlänge definiert für jeden ODBC SQL-Datentyp wird in der folgenden Tabelle angezeigt.  
  
|SQL-Typ-ID|Länge|  
|-------------------------|------------|  
|Alle Typen mit Zeichen [a]|Die definiert oder die (für Variablentyp) maximale Länge der Spalte in Bytes. Dies ist der gleiche Wert wie das Deskriptorfeld SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|Die Anzahl der Bytes, die erforderlich sind, um die Darstellung von Zeichen dieser Daten zu speichern, ist der Zeichensatz ANSI und zweimal diese Zahl ist der Zeichensatz UNICODE. Dies ist die maximale Anzahl von Ziffern plus zwei, da die Daten als Zeichenfolge zurückgegeben werden und die Zeichen für die Ziffern, eine Anmeldung und ein Dezimaltrennzeichen erforderlich sind. Beispielsweise ist die Übertragung Länge einer Spalte, die als NUMERIC(10,3) definiert 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|Die Anzahl der Bytes, die erforderlich sind, um die Darstellung von Zeichen dieser Daten zu speichern, ist der Zeichensatz ANSI und zweimal diese Zahl der Zeichensatz UNICODE ist, da dieser Datentyp wird standardmäßig als Zeichenfolge zurückgegeben wird. Die Darstellung von Zeichen besteht aus 20 Zeichen: 19 Ziffern und eine Anmeldung, wenn signiert oder 20 Ziffern, wenn nicht signierte. Aus diesem Grund ist die Länge 20.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Alle Binärtypen [a]|Die Anzahl der Bytes, die erforderlich sind, um die definierten (für feste Typen) zu speichern oder (für Variablentypen) maximale Anzahl von Zeichen.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (die Größe der Struktur SQL_DATE_STRUCT oder SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (die Größe der Struktur SQL_TIMESTAMP_STRUCT).|  
|Alle Interval-Datentypen|34 (die Größe der Struktur Intervall).|  
|SQL_GUID|16 (die Größe der GUID-Struktur).|  
  
 [a] Wenn der Treiber die Spalten- oder Parameternamen Länge für Variablentypen ermitteln kann, gibt Sie SQL_NO_TOTAL zurück.

