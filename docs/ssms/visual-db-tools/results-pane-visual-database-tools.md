---
title: Ergebnisbereich (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- result sets [SQL Server], queries
- synchronization [SQL Server], query results with definition
- displaying query results in grid
- grid showing query results [SQL Server]
- showing query results in grid
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- viewing query results
- queries [SQL Server], results
- Results pane
ms.assetid: 6309a1bc-a628-4141-8bb5-b35924bd19f9
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 462f9996dfc57b92e1388c58adbe198a1154032a
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="results-pane-visual-database-tools"></a>Results Pane (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Im Ergebnisbereich werden die Ergebnisse der zuletzt ausgeführten SELECT-Abfrage angezeigt. (Die Ergebnisse anderer Abfragetypen werden in Meldungsfeldern angezeigt.) Um den Ergebnisbereich zu öffnen, öffnen oder erstellen Sie eine Abfrage bzw. eine Sicht oder kehren zu den Daten einer Tabelle zurück. Wird der Ergebnisbereich standardmäßig nicht angezeigt, zeigen Sie im **Abfrage-Designer** auf **Bereich**, und klicken Sie dann auf **Ergebnisse**.  
  
## <a name="what-you-can-do-in-the-results-pane"></a>Mögliche Aktionen im Ergebnisbereich  
  
-   Anzeigen des Resultsets für die zuletzt ausgeführte SELECT-Abfrage in einem Datenblatt, das einer Kalkulationstabelle ähnelt.  
  
-   In Abfragen oder Sichten, die Daten aus einer einzelnen Tabelle oder Sicht anzeigen, können Sie die Werte in einzelnen Spalten im Resultset bearbeiten, neue Zeilen hinzufügen und vorhandene Zeilen löschen.  
  
## <a name="limitations-in-the-results-pane"></a>Einschränkungen im Ergebnisbereich  
  
-   Ergebnisse, die von Tabellenwert-Funktionen zurückgegeben werden, können nur in einigen Fällen aktualisiert werden.  
  
-   Abfragen oder Sichten, die Spalten von mehr als einer Tabelle oder Sicht beinhalten, können nicht aktualisiert werden.  
  
-   Von einer gespeicherten Prozedur zurückgegebene Ergebnisse können nicht aktualisiert werden.  
  
-   Abfragen oder Sichten, die GROUP BY-Klauseln oder DISTINCT-Klauseln enthalten, sind nicht aktualisierbar.  
  
## <a name="navigating-in-the-results-pane"></a>Navigieren im Ergebnisbereich  
Verwenden Sie die Navigationsleiste am unteren Rand des Ergebnisbereichs, um schnell durch die Datensätze zu navigieren.  
  
Die Navigationsleiste ist mit Schaltflächen versehen, um zu den ersten und letzten Datensatz zu gehen, den nächsten und vorhergehenden Datensatz, und zu einem bestimmten Datensatz.  
  
Um zu einem bestimmten Datensatz zu gelangen, geben Sie die Zahl der Zeile in das Textfeld der Navigationsleiste ein, und drücken Sie die EINGABETASTE.  
  
Weitere Informationen zum Verwenden von Tastenkombinationen im Abfrage- und Sicht-Designer finden Sie unter [Navigieren im Abfrage- und Sicht-Designer &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Synchronhalten des Resultsets mit der Abfragedefinition  
Während Sie mit den Ergebnissen einer Abfrage oder Sicht arbeiten, ist es möglich, dass die Datensätze im Ergebnisbereich nicht mehr mit der Abfragedefinition synchron sind. Wenn Sie z. B. eine Abfrage für vier von fünf Spalten einer Tabelle ausführen und dann den Diagrammbereich verwenden, um die fünfte Spalte zur Abfragedefinition hinzuzufügen, werden die Daten der fünften Spalte nicht automatisch dem Ergebnisbereich hinzugefügt. Führen Sie die Abfrage erneut aus, damit der Ergebnisbereich die neue Abfragedefinition wiedergibt.  
  
Wenn eine Abfrage geändert wird, werden in der unteren rechten Ecke des Ergebnisbereichs ein Warnsymbol und der Text "Abfrage geändert" angezeigt. Das Warnsymbol wird auch in der oberen linken Ecke des Bereichs angezeigt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen von Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-queries-visual-database-tools.md)  
[Ausführen von Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Diagrammbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Kriterienbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Verwenden von Daten im Ergebnisbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
