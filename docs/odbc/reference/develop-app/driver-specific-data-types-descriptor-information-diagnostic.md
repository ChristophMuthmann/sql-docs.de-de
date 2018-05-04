---
title: Treiber-spezifische Typen - Daten, Beschreibung, Informationen Diagnose | Microsoft Docs
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
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7dbc0ca0584d5dd9c7e8dbfc1cfa5d23831d764
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnose Typen und Attribute
Treiber können Treiber-spezifische Werte für Folgendes zuordnen:  
  
-   **SQL Data Type Indicators** diese kommen in *ParameterType* in **SQLBindParameter** und *DataType* in **SQLGetTypeInfo** und zurückgegebenes **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**,  **SQLDescribeParam**, **SQLProcedureColumns**, und **SQLSpecialColumns**.  
  
-   **Deskriptorfelder** diese kommen in *FieldIdentifier* in **SQLColAttribute**, **SQLGetDescField**, und **SQLSetDescField**.  
  
-   **Diagnosefelder** diese kommen in *DiagIdentifier* in **SQLGetDiagField** und **SQLGetDiagRec**.  
  
-   **Typen von Informationen** diese kommen in *Infotyp* in **SQLGetInfo**.  
  
-   **Verbindungs- und Anweisungsattribute** diese kommen in *Attribut* in **SQLGetConnectAttr**, **SQLGetStmtAttr**,  **SQLSetConnectAttr**, und **SQLSetStmtAttr**.  
  
 Für jedes dieser Elemente, es gibt zwei Sätze an Werten: Werte, die für die Verwendung von ODBC reserviert und Werte, die vom Treiber für die Verwendung reserviert. Vor der Implementierung treiberspezifische Werte, muss ein Treiber-Writer für treiberspezifische-Typ, ein Feld oder jedes Attribut einen Wert vom Open Group anfordern. Verwenden Sie für die Treiberentwicklung neuer den Bereich in der folgenden Tabelle beschrieben. Der ODBC 3.8-Treiber-Manager generiert keinen Fehler, wenn ein Unbekannter Wert, die nicht im Bereich verwendet wird unten beschriebenen. Allerdings generiert höhere Versionen des Treiber-Managers Fehler, wenn unbekannte Werte empfangen werden, die nicht im Bereich enthalten sind.  
  
 Wenn dieser Werte wird in einer ODBC-Funktion übergeben werden, muss der Treiber überprüfen, ob der Wert gültig ist. Treiber zurückgeben SQLSTATE HYC00 (optionales Feature nicht implementiert) für treiberspezifische-Werte, die für andere Treiber gelten.  
  
 Beginnend mit ODBC 3.8, können Treiber Writer treiberspezifischen Attribute in einem reservierten Bereich zuordnen.  
  
> [!NOTE]  
>  Der ODBC 3.8-Treiber-Manager überprüft weder erzwingt diese Bereiche für die Abwärtskompatibilität. Eine zukünftige Version des Treiber-Managers können sie jedoch erzwingen.  
  
|Attributtyp|ODBC-Datentyp|Treiberspezifische Bereich Basis|Treiberspezifische Bereichsgrenzen|ODBC-Konstante für treiberspezifische Wertebereich Basis|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|SQL-Datentyp, Indikatoren|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Deskriptorfelder|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Diagnosefelder|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Typen von Informationen|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Verbindungsattribute|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Anweisungsattribute|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Treiber-spezifische Datentypen, deskriptorfelder Diagnosefelder, Informationstypen, Anweisungsattribute und Verbindungsattribute müssen in der Treiberdokumentation beschrieben werden. Wenn dieser Werte wird in einer ODBC-Funktion übergeben werden, muss der Treiber überprüfen, ob der Wert gültig ist. Treiber zurückgeben SQLSTATE HYC00 (optionales Feature nicht implementiert) für treiberspezifische-Werte, die für andere Treiber gelten.  
  
 Die Basiswerte werden definiert, um die Entwicklung zu vereinfachen. Bestimmte diagnostische Treiberattribute können z. B. im folgenden Format definiert werden:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
