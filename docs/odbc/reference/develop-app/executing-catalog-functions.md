---
title: Ausführen von Katalogfunktionen | Microsoft Docs
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
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2953039c912571ce43e38046001eb182bb42ddaf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="executing-catalog-functions"></a>Ausführen von Katalogfunktionen
Da eine Katalogfunktion auf ein Resultset erstellt wird, entspricht dies dem Ausführen alle Ergebnis Satz – Generieren von SQL-Anweisung. Tatsächlich werden Katalogfunktionen durch Ausführen von vordefinierten SQL-Anweisungen oder zum Aufrufen von vordefinierte Schritte ausführen, die mit dem Treiber oder DBMS geliefert werden häufig implementiert. Fast alles, das für SQL-Anweisungen gilt, die Resultsets erstellen gilt auch für Katalogfunktionen. Beispielsweise SQL_ATTR_MAX_ROWS-Anweisungsattribut begrenzt die Anzahl der Zeilen, die von der Katalogfunktion zurückgegeben, ebenso, wie sie die Anzahl von zurückgegebenen Zeilen beschränkt eine **wählen** Anweisung.  
  
 Um eine Katalogfunktion auszuführen, ruft eine Anwendung nur die Funktion.  
  
 Weitere Informationen zu Katalogfunktionen, finden Sie unter [Katalogfunktionen](../../../odbc/reference/develop-app/catalog-functions.md).
