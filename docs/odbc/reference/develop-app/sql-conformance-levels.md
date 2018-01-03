---
title: "SQL-Übereinstimmungsebenen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d397eef2bec5e803cca97f05d009708273a05473
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sql-conformance-levels"></a>SQL-Übereinstimmungsebenen
Die Ebene der SQL-92-Grammatik unterstützt, die von einem Treiber wird angegeben, als durch einen Aufruf zurückgegebene Wert **SQLGetInfo** mit dem Typ der SQL_SQL_CONFORMANCE-Informationen. Dies gibt an, ob der Treiber den Eintrag, FIPS Transitional, zwischen- oder vollständige Ebenen, die in SQL-92 definierten entspricht.  
  
 Alle ODBC-Treiber müssen die minimale SQL-Grammatik, die in beschriebenen unterstützen [minimale SQL-Grammatik](../../../odbc/reference/appendixes/sql-minimum-grammar.md) in Anhang C: SQL-Grammatik. Diese Grammatik ist eine Teilmenge der Ebene der SQL-92-Eintrag. Treiber möglicherweise unterstützen zusätzliche SQL und werden entsprechen, die auf die SQL-92-Eintrag, zwischen- oder Full oder der FIPS 127-2-Transitional-Ebene. Treiber, die einer bestimmten Ebene der SQL-92 oder FIPS 127-2 entsprechen, können zusätzliche Funktionen in einer höheren Ebenen unterstützt noch nicht vollständig konform auf dieser Ebene. Um zu bestimmen, ob eine Funktion unterstützt wird, sollte eine Anwendung aufrufen **SQLGetInfo** mit dem Datentyp der entsprechenden Informationen. Der Konformitätsgrad des SQL-Funktion wird in den Typ der entsprechenden Informationen beschrieben. (Siehe die [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) funktionsbeschreibung.)
