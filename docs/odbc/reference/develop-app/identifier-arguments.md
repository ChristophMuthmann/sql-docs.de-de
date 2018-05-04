---
title: Bezeichner Argumente | Microsoft Docs
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
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d483c50928d93ecd64419726eb77ae162f221f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="identifier-arguments"></a>Identifier-Argumente
Wenn eine Zeichenfolge in einem Argument Bezeichner in Anführungszeichen eingeschlossen ist, wird der Treiber entfernt führende und nachfolgende Leerzeichen und behandelt, als solcher die Zeichenfolge in Anführungszeichen. Wenn die Zeichenfolge nicht in Anführungszeichen eingeschlossen ist, entfernt der Treiber nachfolgende Leerzeichen und Aufteilungen die Zeichenfolge in Großbuchstaben. Wird ein ID-Argument auf ein null-Zeiger gibt SQL_ERROR und SQLSTATE HY009 zurück (Ungültige Verwendung von null-Zeiger), es sei denn, das Argument ein Katalogname ist und Kataloge werden nicht unterstützt.  
  
 Diese Argumente werden als Bezeichner Argumente behandelt, wenn das SQL_ATTR_METADATA_ID-Anweisungsattribut auf SQL_TRUE festgelegt ist. In diesem Fall werden der Unterstrich (_) und das Prozentzeichen (%) als das tatsächliche Zeichen, nicht als Suche Muster Zeichen behandelt werden. Diese Argumente werden als gewöhnliche Argument oder eine Pattern-Argument, je nach dem Argument behandelt, wenn dieses Attribut auf SQL_FALSE festgelegt ist.  
  
 Obwohl von Bezeichnern, die Sonderzeichen in SQL-Anweisungen mit Anführungszeichen versehen werden müssen, müssen sie nicht in Anführungszeichen gesetzt werden beim Übergeben als Argumente für Katalog-Funktion, da Anführungszeichen Katalogfunktionen übergeben wörtlich interpretiert werden. Nehmen wir beispielsweise an den Bezeichner Anführungszeichen (d. h. treiberspezifische und die zurückgegebenen über **SQLGetInfo**) ist ein doppeltes Anführungszeichen ("). Der erste Aufruf von **SQLTables** gibt ein Resultset mit Informationen über die "Accounts Payable" Tabelle während der zweite Aufruf Informationen über die "Accounts Payable" Tabelle zurückgibt, das ist, was wahrscheinlich nicht beabsichtigt war.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Bezeichner in Anführungszeichen werden verwendet, um einen Spaltennamen "true" aus einer Pseudo-Spalte mit dem gleichen Namen, z. B. ROWID in Oracle zu unterscheiden. Wenn ein Argument einer Funktion Katalog "ROWID" übergeben wird, funktioniert die Funktion mit der ROWID Pseudo-Spalte, falls vorhanden. Wenn die Pseudo-Spalte nicht vorhanden ist, funktioniert die Funktion, mit der Spalte "ROWID". Wenn ein Argument einer Funktion Katalog ROWID übergeben wird, funktioniert die Funktion, mit der ROWID-Spalte.  
  
 Weitere Informationen zu Bezeichnern finden Sie unter [Bezeichner in Anführungszeichen](../../../odbc/reference/develop-app/quoted-identifiers.md).
