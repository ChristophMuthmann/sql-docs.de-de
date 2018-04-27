---
title: Verwenden des Abfrage- und Sicht-Designers bei internationalen Daten | Microsoft-Dokumentation
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
- Visual Database Tools [SQL Server], international data
- queries [SQL Server], international data
- languages [SQL Server], Query and View Designer
- international considerations [SQL Server], Query and View Designer
- Criteria pane
- View Designer, international data
- Query Designer [SQL Server], international data
- localized information in Query and View Designer [SQL Server]
- global considerations [SQL Server], Query and View Designer
- SQL pane [Visual Database Tools]
- multiple language support [SQL Server], Query and View Designer
ms.assetid: 4b51c56f-f902-4e72-b919-e36127369b63
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2590467f823e4dedaf33bc2c4f5aa48920032b51
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="use-the-query-and-view-designer-with-international-data-visual-database-tools"></a>Verwenden des Abfrage- und Sicht-Designers bei internationalen Daten (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Sie können den [Abfrage- und Sicht-Designer](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) mit Daten in jeder Sprache und mit jeder Version des Betriebssystems Windows verwenden. In den folgenden Richtlinien werden die Unterschiede erläutert und Informationen zur Datenverwaltung in internationalen Anwendungen bereitgestellt.  
  
## <a name="localized-information-in-the-criteria-and-sql-panes"></a>Lokalisierte Informationen im Kriterien- und im SQL-Bereich  
Wenn Sie eine Abfrage im Kriterienbereich erstellen, können Sie die Informationen in dem Format eingeben, das den Ländereinstellungen von Windows auf dem Computer entspricht. Wenn Sie z. B. nach Daten suchen, können Sie die Daten in den Spalten Kriterien in dem für Sie gewohnten Format eingeben, wobei jedoch folgende Ausnahmen zu beachten sind:  
  
-   Lange Datenformate werden nicht unterstützt.  
  
-   Währungssymbole sollten im Kriterienbereich nicht eingegeben werden.  
  
-   Währungssymbole werden im Ergebnisbereich nicht angezeigt.  
  
    > [!NOTE]  
    > Sie können im Ergebnisbereich zwar das Währungssymbol eingeben, das den Ländereinstellungen von Windows auf dem Computer entspricht, das Symbol wird jedoch entfernt und im Ergebnisbereich nicht angezeigt.  
  
-   Ein unäres Minus wird immer links angezeigt (z. B. -1), unabhängig von den in den Ländereinstellungen gewählten Optionen.  
  
Dagegen müssen Daten und Schlüsselwörter im SQL-Bereich immer im ANSI-Format (U.S.) angegeben werden. Beispielsweise fügt der Abfrage- und Sicht-Designer beim Erstellen einer Abfrage alle SQL-Schlüsselwörter wie SELECT oder FROM im ANSI-Format ein. Achten Sie beim Hinzufügen von Elementen zu Anweisungen im SQL-Bereich darauf, für diese Elemente die ANSI-Standardform zu verwenden.  
  
Wenn Sie im Kriterienbereich Daten in einem gebietsspezifischen Format eingeben, wandelt der Abfrage- und Sicht-Designer diese Eingaben für den SQL-Bereich automatisch in das ANSI-Format um. Wenn die Ländereinstellungen des Computers z. B. auf die Option Deutsch (Standard) festgelegt sind, können Sie im Kriterienbereich ein Datum u. a. im Format "31.12.96" eingeben. Allerdings wird das Datum im SQL-Bereich im ANSI-Datums- und Zeitformat als `{ ts '1996-12-31 00:00:00' }.` angezeigt. Wenn Sie Daten direkt im SQL-Bereich eingeben, müssen Sie diese im ANSI-Format eingeben.  
  
## <a name="sort-order"></a>Sortierreihenfolge  
Die in Abfragen für Daten verwendete Sortierreihenfolge wird durch die verwendete Datenbank vorgegeben. Im Dialogfeld Ländereinstellungen von Windows ausgewählte Optionen haben keinen Einfluss auf die Sortierreihenfolge für Abfragen. Sie haben jedoch die Möglichkeit, für einzelne Abfragen eine spezielle Reihenfolge für die Zeilenausgabe anzufordern.  
  
## <a name="using-double-byte-characters"></a>Verwenden von Doppelbytezeichen  
Sie können DBCS-Zeichen für Literalwerte und für Namen von Datenbankobjekten, wie Tabellen- und Sichtnamen oder Aliase, eingeben. Weiterhin sind DBCS-Zeichen in Parameternamen und Parametermarkierungszeichen zulässig. In SQL-Elementen, z. B. Funktionsnamen oder SQL-Schlüsselwörtern, dürfen DBCS-Zeichen jedoch nicht verwendet werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
