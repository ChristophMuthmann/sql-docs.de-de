---
title: Tools im Abfrage- und Sicht-Designer (Visual Database Tools) | Microsoft-Dokumentation
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
f1_keywords:
- vdt.querydesigner
- vdt.pane.diagram
- vdt.pane.grid
- vdt.dlgbox.querybuilder
- vdt.pane.sql
- vdt.pane.results
helpviewer_keywords:
- Query Designer [SQL Server], panes
- View Designer, panes
- Query Designer [SQL Server], components
- View Designer, components
ms.assetid: 12e4b5a5-b793-4b6c-a0e5-c450c49bf26f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46301b8538b1d2c7eec7b1523c18bdba21fb9a33
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="query-and-view-designer-tools-visual-database-tools"></a>Tools im Abfrage- und Sicht-Designer (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Beim Erstellen von Abfragen, Sichten, Inlinefunktionen oder gespeicherten Prozeduren mit einer einzelnen Anweisung stehen Ihnen im Designer vier Bereiche zur Verfügung: der Diagrammbereich, der Kriterienbereich, der SQL-Bereich und der Ergebnisbereich.  
  
![Abfragedesigner](../../ssms/visual-db-tools/media/vs_queryviewdsgpanes.gif "Abfragedesigner")  
  
-   Der Diagrammbereich zeigt die Tabellen sowie weitere Tabellenwertobjekte an, für die eine Abfrage ausgeführt wird. Jedes Rechteck stellt eine Tabelle oder ein Tabellenwertobjekt dar und gibt die verfügbaren Datenspalten an. Joins werden durch Linien zwischen den Rechtecken angezeigt. Weitere Informationen finden Sie unter [Diagrammbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md).  
  
-   Im Kriterienbereich wird ein Datenblatt ähnlich einer Kalkulationstabelle angezeigt. In dem Datenblatt können Sie Optionen festlegen, z. B. welche Datenspalten angezeigt, welche Zeilen ausgewählt oder wie Zeilen gruppiert werden sollen. Weitere Informationen finden Sie unter [Kriterienbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md).  
  
-   Im SQL-Bereich wird die SQL-Anweisung für die Abfrage oder Sicht angezeigt. Sie können die vom Designer erstellte SQL-Anweisung bearbeiten oder eine eigene SQL-Anweisung eingeben. Dieser Bereich ist besonders hilfreich bei der Eingabe von SQL-Anweisungen, die nicht im Diagramm- oder Kriterienbereich erstellt werden können, z. B. bei Union-Abfragen. Weitere Informationen finden Sie unter [SQL-Bereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
-   Im Ergebnisbereich wird ein Datenblatt mit den in der Abfrage oder Sicht abgerufenen Daten angezeigt. Im Abfrage- und Sicht-Designer enthält dieser Bereich die Ergebnisse der zuletzt ausgeführten SELECT-Abfrage. Sie können die Datenbank durch Bearbeiten der Zellenwerte im Datenblatt ändern, und Sie können Zeilen hinzufügen oder löschen. Weitere Informationen finden Sie unter [Ergebnisbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md).  
  
Sie können jeden dieser Bereiche verwenden, um eine Abfrage oder Sicht zu erstellen oder anzuzeigen. Beispielsweise können Sie eine anzuzeigende Spalte im Diagrammbereich auswählen, im Kriterienbereich eingeben oder im SQL-Bereich in eine SQL-Anweisung einbinden.  
  
## <a name="displaying-and-hiding-panes"></a>Anzeigen und Ausblenden von Bereichen  
Klicken Sie mit der rechten Maustaste auf die Entwurfsoberfläche, zeigen Sie auf **Bereich**, und klicken Sie dann auf den Namen des Bereichs, um einen Bereich auszublenden oder einen nicht sichtbaren Bereich anzuzeigen. Wenn der Abfrage- und Sicht-Designer im Abfrage-Designermodus geöffnet wird, ist der Bereich **Ergebnisse** nicht verfügbar.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Öffnen des Abfrage- und Sicht-Designers &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-the-query-and-view-designer-visual-database-tools.md)  
[SQL-Editor &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-editor-visual-database-tools.md)  
  
