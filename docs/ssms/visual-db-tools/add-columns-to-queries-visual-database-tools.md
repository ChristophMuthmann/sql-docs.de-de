---
title: "Hinzufügen von Spalten zu Abfragen (Visual Database Tools)| Microsoft-Dokumentation"
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
- inserting columns
- columns [SQL Server], adding
- queries [SQL Server], columns
- adding columns
ms.assetid: 82f3ba72-3d72-4fb1-8179-2a953a782787
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6b326ef23c2840be683faa499ceeb40293afa5b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="add-columns-to-queries-visual-database-tools"></a>Hinzufügen von Spalten zu Abfragen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Wenn Sie in einer Abfrage eine Spalte verwenden möchten, müssen Sie diese der Abfrage hinzufügen. Sie haben die Möglichkeit, eine hinzugefügte Spalte im Abfrageergebnis anzeigen zu lassen und sie zum Sortieren, Durchsuchen oder Zusammenfassen des Spalteninhalts zu verwenden. Sie können festlegen, welche der in der Abfrage verwendeten Spalten beim Ausführen der Abfrage im Ergebnisbereich angezeigt werden. Weitere Informationen finden Sie unter [Entfernen von Spalten aus Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md).  
  
> [!NOTE]  
> Wählen Sie zum Anzeigen des Datentyps einer Spalte im Abfrage- und Sicht-Designer die Tabelle oder das Tabellenwertobjekt im **Diagrammbereich** aus, und klicken Sie im Eigenschaftenfenster auf „Spaltenliste“. Klicken Sie dann auf das **Auslassungszeichen (...)** , um das Dialogfeld **Spaltenliste** zu öffnen.  
  
Für alle Zwecke, für die Sie eine Spalte in einer Abfrage verwenden, können Sie auch einen Ausdruck verwenden, der aus einer beliebigen Kombination von Spalten, Zeichen, Operatoren und Funktionen bestehen kann.  
  
### <a name="to-add-an-individual-column"></a>So fügen Sie eine einzelne Spalte hinzu  
  
-   Aktivieren Sie im **Diagrammbereich**das Kontrollkästchen neben der einzufügenden Spalte.  
  
    -oder-  
  
-   Gehen Sie im **Kriterienbereich**zur ersten leeren Zeile des Datenblatts, klicken Sie in das Feld in der Spalte mit dem Namen **Spalte** , und wählen Sie in der Dropdownliste einen Spaltennamen aus.  
  
### <a name="to-add-all-columns-for-one-table-or-table-valued-object"></a>So fügen Sie alle Spalten einer Tabelle oder eines Tabellenwertobjekts hinzu  
  
-   Aktivieren Sie im **Diagrammbereich**das Kontrollkästchen neben **\&#42;(Alle Spalten)**.  
  
### <a name="to-add-all-columns-for-all-tables-and-table-structured-objects"></a>So fügen Sie alle Spalten sämtlicher Tabellen und Objekte mit Tabellenstruktur hinzu  
  
1.  Vergewissern Sie sich, dass im Bereich **Tabellenvorgänge** keine Joinlinien markiert sind.  
  
2.  Klicken Sie mit der rechten Maustaste auf einen leeren Bereich im Entwurfsfenster, und wählen Sie im Kontextmenü die Option **Eigenschaften** aus.  
  
3.  Klicken Sie im Eigenschaftenfenster auf **Alle Spalten ausgeben** , und wählen Sie in der Dropdownliste die Option **Ja** oder **Nein** .  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Entfernen von Spalten aus Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-query-results-visual-database-tools.md)  
[Entfernen von Spalten aus Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/remove-columns-from-queries-visual-database-tools.md)  
[Angeben von Suchkriterien &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[Zusammenfassen von Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
