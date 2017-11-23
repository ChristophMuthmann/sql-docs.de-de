---
title: SQLSTATEs | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c45bbcbf03c4377e8ff162c3cd28ddf7128810b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs bieten ausführliche Informationen zur Ursache einer Warnung oder Fehler. Die SQLSTATEs in diesem Handbuch basiert auf solche, die in der ISO/IEF CLI-Spezifikation, obwohl diese SQLSTATEs, die mit Instant Messaging-Diensten beginnen für ODBC spezifisch sind.  
  
 Im Gegensatz zu den Rückgabecodes die SQLSTATEs in diesem Handbuch werden die Richtlinien und Treiber sind nicht erforderlich, um zurückzugeben. Aus diesem Grund während der Treiber den entsprechenden SQLSTATE für alle Fehler bzw. der Warnung, die sie kann ermitteln, zurückgeben soll, sollten Anwendungen nicht gezählt auf diese immer auftritt. Die Gründe hierfür gibt es zwei Gründe:  
  
-   **Unvollständigkeit** Obwohl dieses Handbuchs eine große Anzahl von Fehlern und Warnungen und mögliche Ursachen für diesen Fehler und Warnungen aufführt, ist nicht vollständig und wahrscheinlich nie werden; Treiber Implementierungen einfach zu viele unterscheiden sich. Alle angegebener Treiber wird wahrscheinlich nicht zurückgegeben werden, alle die SQLSTATEs aufgeführt, die in diesem Handbuch und möglicherweise SQLSTATEs nicht aufgeführt, in diesem Handbuch zurück.  
  
-   **Komplexität** einige Datenbank Module – insbesondere relationale Datenbankmodule – Tausenden von Fehlern und Warnungen zurückgegeben. Die Treiber für diese Module sind wahrscheinlich nicht alle diese Fehler zuordnen und Warnungen, um SQLSTATEs aufgrund des Aufwands beteiligt sind, die Inexactness der Zuordnungen, die Größe der resultierende Code und den Tiefstwert des resultierenden Codes, die häufig Programmierung zurückgibt Fehler, die zur Laufzeit nie auftreten sollten. Aus diesem Grund Treiber sollten möglichst viele Fehler zuzuordnen und Warnungen wie sinnvoll scheint, und ordnen Sie unbedingt diese Fehler und Warnungen auf die Anwendungslogik basiert möglicherweise, z. B. SQLSTATE 01004 (Daten abgeschnitten).  
  
 Da SQLSTATEs nicht zuverlässig zurückgegeben werden, wird sie in die meisten Anwendungen nur für den Benutzer zusammen mit ihrer zugeordneten diagnosemeldung aus, die zugeschnitten häufig auf den genauen Fehler oder Warnung, die aufgetreten ist, und der systemeigene Fehlercode angezeigt. Es gibt selten eine Beeinträchtigung der Funktionalität im diese Vorgehensweise wird auf, da Anwendungen Programmierlogik trotzdem für die meisten SQLSTATEs basieren können. Nehmen wir beispielsweise an **SQLExecDirect** SQLSTATE 42000 (Syntaxfehler oder zugriffsverletzung) zurückgegeben. Wenn die SQL-Anweisung, die diesen Fehler verursacht hat hartcodierte oder von der Anwendung erstellt, dies ist ein Programmierfehler, und der Code korrigiert werden muss. Wenn die SQL-Anweisung, die vom Benutzer eingegeben wird, dies ist ein Fehler, und die Anwendung erledigt hat, die durch die Benutzer über das Problem informiert werden kann.  
  
 Wenn Anwendungen SQLSTATEs Programmierlogik basieren, sollten sie für den SQLSTATE nicht zurückgegeben werden sollen oder einem anderen SQLSTATE zurückgegeben werden darauf vorbereitet sein. Genau die SQLSTATEs zuverlässig zurückgegeben werden kann nur auf die Erfahrung mit zahlreichen Treiber basieren. Allerdings ist eine allgemeine Richtlinie, dass SQLSTATEs für Fehler, die in der Treiber oder Treiber-Managers, im Gegensatz zu der Datenquelle auftreten wahrscheinlicher zuverlässig zurückgegeben werden sollen. Beispielsweise die meisten Treiber SQLSTATE HYC00 wahrscheinlich zurückgeben (optionales Feature nicht implementiert), während weniger Treiber SQLSTATE 42021 wahrscheinlich zurückgeben (Spalte ist bereits vorhanden).  
  
 Die folgenden SQLSTATEs zur Laufzeit Fehler oder Warnungen an, und eignen sich gut in die Programmierlogik basieren. Allerdings besteht keine Garantie, die alle Treiber, die sie zurückgeben.  
  
-   01004 (Daten wurden abgeschnitten.)  
  
-   01 s 02 (Optionswert wurde geändert)  
  
-   HY008 (der Vorgang wurde abgebrochen.)  
  
-   HYC00 (optionales Feature nicht implementiert)  
  
-   HYT00 (Timeout ist abgelaufen)  
  
 SQLSTATE HYC00 (optionales Feature nicht implementiert) ist besonders wichtig, weil es die einzige Möglichkeit besteht, in dem eine Anwendung zu bestimmen kann, ob ein Treiber ein bestimmtes Attribut der Anweisung oder Verbindung unterstützt.  
  
 Eine vollständige Liste der SQLSTATEs und welche Funktionen zurückzugeben, finden Sie unter [Anhang A: ODBC-Fehlercodes](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Eine ausführliche Erläuterung der Bedingungen, unter denen jede Funktion eine bestimmte SQLSTATE zurückgeben kann, finden Sie unter dieser Funktion.
