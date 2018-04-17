---
title: Auswählen einer SQL-Grammatik | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 90aba694c610f34d2f6da93a3e5d155cb4fc4ab0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="choosing-an-sql-grammar"></a>Auswählen einer SQL-Grammatik
Die erste Entscheidung, die bei der SQL-Anweisungen Konstruieren der Grammatik verwendet wird. Zusätzlich zu den von verschiedenen normungsinstitutionen, z. B. Open Group, ANSI und ISO-Images Grammatiken, definiert praktisch jeder DBMS-Hersteller eine eigene Grammatik, von denen jede geringfügig vom Standard variiert.  
  
 [Anhang C: SQL-Grammatik](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), beschreibt die minimale SQL-Grammatik, die alle ODBC-Treiber unterstützen muss. Diese Grammatik ist eine Teilmenge der Ebene der SQL-92-Eintrag. Treiber unterstützen möglicherweise weitere Grammatik um den Zwischenspeicher, Full oder FIPS 127-2-Ebenen-Transitional definiert in SQL-92 entsprechen. Weitere Informationen finden Sie unter [mindestens-SQL-Grammatik](../../../odbc/reference/appendixes/sql-minimum-grammar.md) in Anhang C: SQL-Grammatik und SQL-92.  
  
 Anhang C definiert auch *escape-Zeichensequenzen* mit standard-Grammatik für die allgemein verfügbare Sprachfunktionen wie äußere Joins, unterliegen nicht der SQL-92-Grammatik. Weitere Informationen finden Sie unter [ODBC-Escapesequenzen](../../../odbc/reference/appendixes/odbc-escape-sequences.md) in Anhang C: SQL-Grammatik und [Escapesequenzen](../../../odbc/reference/develop-app/escape-sequences.md)weiter unten in diesem Abschnitt.  
  
 Die Grammatik, die ausgewählt wird beeinflusst, wie der Treiber die Anweisung verarbeitet. Treiber müssen SQL-92 SQL und der ODBC-definierten Escapesequenzen DBMS-spezifische SQL ändern. Da die meisten SQL-Grammatiken auf einem oder mehreren verschiedenen Standards basieren, werden die meisten Treiber nur wenig oder keine arbeiten, um die Vorgaben zu erfüllen. Häufig besteht nur Suchen nach den definiert Escapesequenzen durch ODBC und Ersetzen sie durch DBMS-spezifische Grammatik. Wenn ein Treiber Grammatik, die nicht erkannt wird trifft, wird die Grammatik DBMS-spezifische und übergibt die SQL-Anweisung ohne Änderung der Datenquelle für die Ausführung.  
  
 Aus diesem Grund sind tatsächlich zwei Optionen der Grammatik verwendet: die SQL-92-Grammatik (und die ODBC-Escapesequenzen) und einer DBMS-spezifische-Grammatik. Die beiden ist nur die SQL-92-Grammatik interoperabel, damit alle interoperable Anwendungen verwendet werden soll. Anwendungen, die nicht vollständig kompatibel sind, können die SQL-92-Grammatik oder Grammatik DBMS-spezifische verwenden. DBMS-spezifische Grammatiken haben zwei Vorteile: können sie alle Funktionen, die nicht von SQL-92 abgedeckt ausnutzen, und sie sind geringfügig schneller, da der Treiber nicht verfügt, sie zu ändern. Die zweite Funktion kann teilweise durch Festlegen der SQL_ATTR_NOSCAN-Anweisungsattribut, beenden, den Treiber von Suchen und Ersetzen von Escapesequenzen erzwungen werden.  
  
 Wenn die SQL-92-Grammatik verwendet wird, die Anwendung erkennen, wie sie vom Treiber durch den Aufruf geändert wurden **SQLNativeSql**. Dies ist häufig nützlich, beim Debuggen von Anwendungen. **SQLNativeSql** akzeptiert eine SQL-Anweisung, und gibt ihn zurück, nachdem der Treiber verändert wurde. Da diese Funktion in der Konformitätsgrad des Core-Schnittstelle ist, wird sie durch alle Treiber unterstützt.
