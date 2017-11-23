---
title: "SQL-92-Kompatibilität | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7e611136116edd4f6b978f7fc09bd7acf2bf1e8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sql-92-compliance"></a>SQL-92-Kompatibilität
Der ODBC-Datenbanktreiber Desktop und der zugrunde liegenden Microsoft Jet-Datenbankmodul sind nicht SQL-92 kompatibel. Sie unterstützen viele Funktionen, die in SQL-92 definiert wurden. Einige Funktionen, die vom Treiber unterstützt werden in SQL-92 nicht unterstützt. Weitere Informationen finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*. Es folgen die wichtigsten Unterschiede zwischen den beiden:  
  
-   Die Desktop-Datenbanktreiber verwendete SQL unterstützt leistungsfähigere Ausdrücke als die angegebene SQL-92.  
  
-   Andere Regeln gelten für das BETWEEN-Prädikat.  
  
-   Die vom Desktop-Datenbanktreiber und ANSI SQL verwendeten SQL unterstützt verschiedene Schlüsselwörter.  
  
 Die folgenden SQL-92-Funktionen werden von der Microsoft Jet SQL nicht unterstützt:  
  
-   Sicherheitsanweisungen, z. B. GRANT und SPERREN.  
  
-   DISTINCT mit Aggregatfunktion verweisen.  
  
 Die folgenden Funktionen sind Verbesserungen im SQL zum Datenbanktreiber Desktop, die nicht von SQL-92 angegeben werden:  
  
-   Die TRANSFORM-Anweisung bietet Unterstützung für Kreuztabellenabfragen.  
  
-   Weitere Aggregatfunktionen (**StDev** und **VarP**).  
  
> [!NOTE]  
>  Desktop-Datenbanktreiber unterstützen die ANSI-Standardsyntax nicht für % (Prozent) und _ (Unterstrich) * (Sternchen) und? (Fragezeichen).
