---
title: SQL-Typ-IDs | Microsoft Docs
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
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f3a9270e698f7f0ff12bd12c02de865a3c6f2b3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sql-type-identifiers"></a>SQL-Typ-IDs
Jede Datenquelle definiert eine eigene SQL-Datentypen. ODBC definiert die Typ-IDs und beschreibt die allgemeinen Eigenschaften des SQL-Datentypen, die jeden Typ-ID zugeordnet werden können. Es ist treiberspezifische wie jeder Datentyp in der zugrunde liegenden Datenquelle eine SQL-Typ-ID des ODBC zugeordnet ist.  
  
 SQL_CHAR ist z. B. der Typ-ID für eine Spalte mit Zeichen fester Länge, in der Regel zwischen 1 und 254 Zeichen. Diese Eigenschaften entsprechen dem CHAR-Datentyp in vielen SQL-Datenquellen gefunden. Daher, wenn eine Anwendung ermittelt, dass der Typ-ID für eine Spalte SQL_CHAR ist, können sie davon ausgehen, dass es wahrscheinlich mit einer CHAR-Spalte zu verarbeiten. Jedoch sollte immer noch prüfen, dass die Bytelänge der Spalte vor dem vorausgesetzt es zwischen 1 und 254 Zeichen lang ist. der Treiber für eine nicht-SQL-Datenquelle, z. B. möglicherweise eine Spalte mit fester Länge Zeichen von 500 Zeichen SQL_CHAR oder SQL_LONGVARCHAR, zugeordnet, da keines von beiden ist eine genaue Übereinstimmung.  
  
 ODBC definiert eine Vielzahl von SQL-Typ-IDs. Der Treiber ist jedoch nicht erforderlich, können alle diese Bezeichner verwenden. Stattdessen werden nur diese Bezeichner die SQL-Datentypen unterstützt verfügbar machen muss von der zugrunde liegenden Datenquelle verwendet. Wenn die zugrunde liegenden Datenquelle zu SQL-Datentypen unterstützt welche keine Typbezeichner entspricht, der Treiber zusätzliche Typbezeichner definieren kann. Weitere Informationen finden Sie unter [Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnosetypen und Attribute](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Eine vollständige Beschreibung der SQL-Typ-IDs, finden Sie unter [C-Datentypen](../../../odbc/reference/appendixes/c-data-types.md) in Anhang D:-Datentypen.
