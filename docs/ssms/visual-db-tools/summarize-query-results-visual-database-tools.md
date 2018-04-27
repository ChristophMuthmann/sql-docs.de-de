---
title: Zusammenfassen von Abfrageergebnissen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- summarizing query results
- queries [SQL Server], results
- aggregate queries [SQL Server]
ms.assetid: c9e15350-ed57-4d95-814d-815fbebfd86b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf1e57b23b8a8442e7bd74f96c7046c75fee9564
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="summarize-query-results-visual-database-tools"></a>Zusammenfassen von Abfrageergebnissen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Wenn Sie Aggregatabfragen erstellen, folgen diese bestimmten logischen Prinzipien. Beispielsweise können Sie keine Inhalte aus einzelnen Zeilen einer zusammenfassenden Abfrage anzeigen lassen. Der Abfrage- und Sicht-Designer unterstützt Sie bei der Einhaltung dieser Prinzipien durch das Verhalten von [Diagrammbereich](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) und [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) .  
  
Wenn Sie sich mit den für Aggregatabfragen gültigen Prinzipien und dem Verhalten des Abfrage- und Sicht-Designers vertraut machen, hilft dies beim Entwurf logisch richtiger Aggregatabfragen. Als vorrangiges Prinzip ist zu beachten, dass Aggregatabfragen ausschließlich zusammenfassende Informationen liefern können. Ein Großteil der folgenden Prinzipien beschreibt daher die Methoden, mit denen Sie in einer Aggregatabfrage auf einzelne Datenspalten verweisen können.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
[Verwenden von Spalten in Aggregatabfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
Erläutert Konzepte zum Gruppieren und Zusammenfassen von Spalten mithilfe der Klauseln GROUP BY, WHERE und HAVING.  
  
[Zählen der Zeilen in einer Tabelle &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md)  
Erläutert schrittweise, wie Sie die Anzahl von Zeilen in einer Tabelle ermitteln, oder die Anzahl von Zeilen, die bestimmte Kriterien erfüllen.  
  
[Wertzusammenfassung oder -aggregation für alle Zeilen in einer Tabelle &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md)  
Erläutert schrittweise, wie alle Zeilen zusammengefasst werden, anstatt einen Satz gruppierter Zeilen zu erstellen.  
  
[Wertzusammenfassung oder -aggregation über benutzerdefinierte Ausdrücke &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-using-custom-expressions-visual-database-tools.md)  
Erläutert schrittweise, wie Sie Zusammenfassungen oder Aggregate mithilfe von Ausdrücken anstelle mithilfe vordefinierter Klauseln erstellen können.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
Stellt Links zu Themen bereit, die die Verwendung des Abfrage- und Sicht-Designers erläutern.  
  
