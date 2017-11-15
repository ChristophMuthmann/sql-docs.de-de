---
title: Verwenden von Daten im Ergebnisbereich (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7b1a7f29bcba95aeb1af83746df29a5bee8ebff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>Verwenden von Daten im Ergebnisbereich (Visual Database Tools)
Nach der Ausführung einer Abfrage oder Sicht werden die Ergebnisse im Ergebnisbereich angezeigt. Sie können anschließend mit diesen Ergebnissen arbeiten. Sie können z. B. Zeilen hinzufügen und löschen, Daten eingeben oder ändern und bequem durch umfangreiche Resultsets navigieren.  
  
Die folgenden Informationen können Ihnen helfen, Probleme zu vermeiden und mit den Resultsets effektiv zu arbeiten.  
  
## <a name="returning-the-results-set"></a>Zurückgeben der Resultsets  
Sie können Ergebnisse von einer Abfrage oder einer Sicht zurückgeben und auswählen, ob Sie nur den Ergebnisbereich oder alle Bereiche öffnen möchten. In jedem Fall wird die Abfrage oder die Sicht im Abfrage- und Sicht-Designer geöffnet. Der Unterschied besteht darin, dass im ersten Fall nur der Ergebnisbereich anzeigt wird und im anderen Fall alle Fenster anzeigt werden, die im Dialogfeld Optionen ausgewählt wurden. In der Standardeinstellung werden alle vier Bereiche (Ergebnisse, SQL, Diagramm und Kriterien) angezeigt.  
  
Weitere Informationen finden Sie unter [Öffnen von Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-queries-visual-database-tools.md).  
  
Weitere Informationen zum Ändern des Designs der Abfrage oder der Sicht, sodass ein anderes Resultset oder die Datensätze in anderer Reihenfolge zurückgegeben werden, finden Sie unter [Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md).  
  
Sie können auch festlegen, ob Sie das ganze Resultset oder nur einen Teil davon auf zwei Arten zurückgeben möchten: indem Sie die Abfrage während der Ausführung beenden oder indem Sie vor der Abfrage auswählen, wie viele Ergebnisse zurückgegeben werden sollen.  
  
## <a name="navigating-in-the-results-pane"></a>Navigieren im Ergebnisbereich  
Verwenden Sie die Navigationsleiste am unteren Rand des Ergebnisbereichs, um schnell durch die Datensätze zu navigieren.  
  
Die Navigationsleiste ist mit Schaltflächen versehen, um zu den ersten und letzten Datensatz zu gehen, den nächsten und vorhergehenden Datensatz, und zu einem bestimmten Datensatz.  
  
Um zu einem bestimmten Datensatz zu gelangen, geben Sie die Zahl der Zeile in das Textfeld der Navigationsleiste ein, und drücken Sie die EINGABETASTE.  
  
Weitere Informationen zum Verwenden von Tastenkombinationen im Abfrage- und Sicht-Designer finden Sie unter [Navigieren im Abfrage- und Sicht-Designer &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="committing-changes-to-the-database"></a>Weitergeben der Änderungen an die Datenbank  
Im Ergebnisbereich wird ein Steuerelement für Vollständige Parallelität verwendet, sodass auf dem Datenblatt eine Kopie der Daten in der Datenbank statt einer kompletten Livesicht angezeigt wird. Dadurch wird nur dann ein Commit der Änderungen an die Datenbank ausgeführt, nachdem Sie den Cursor in einen Bereich außerhalb einer Zeile bewegt haben. Dadurch können mehrere Benutzer gleichzeitig mit der Datenbank arbeiten. Treten Konflikte auf (z. B. wenn ein anderer Benutzer dieselbe Zeile geändert hat, die bereits von Ihnen geändert wurde, und diese Änderung an die Datenbank weitergegeben hat, bevor Sie dies vornehmen konnten), erhalten Sie eine Meldung, in der der Konflikt mitgeteilt und entsprechende Lösungen angeboten werden.  
  
## <a name="undo-changes-using-esc"></a>Rückgängig machen von Änderungen mit ESC  
Sie können eine Änderung nur rückgängig machen, wenn noch kein Commit der Änderung an die Datenbank ausgeführt wurde. Die Daten werden nicht weitergegeben, wenn Sie den Cursor nicht in einen Bereich außerhalb des Datensatzes bewegt haben. Der Commit der Daten erfolgt auch nicht, wenn beim Fortbewegen des Cursors von einem Datensatz weg eine Fehlermeldung angezeigt wird, dass die Änderung nicht weitergegeben wird. Wenn die Änderung nicht weitergegeben wurde, können Sie die Änderung durch Drücken der ESC-TASTE rückgängig machen.  
  
Um alle Änderungen in einer Zeile rückgängig zu machen, wechseln Sie in eine Zelle in dieser Zeile, die Sie noch nicht bearbeitet haben, und drücken die ESC-TASTE.  
  
Um Änderungen in einer bestimmten Zelle rückgängig zu machen, die sie bearbeitet haben, gehen Sie zu der Zelle und drücken die ESC-TASTE.  
  
## <a name="adding-or-deleting-data-in-the-database"></a>Hinzufügen oder Löschen von Daten in der Datenbank  
Um zu sehen, wie Ihr Datenbankdesign funktioniert, müssen Sie möglicherweise Beispieldaten in die Datenbank eingeben. Diese Daten können Sie direkt in den Ergebnisbereich eingeben oder aus einem anderen Programm, z. B. Texteditor oder Excel, kopieren und in den Ergebnisbereich einfügen.  
  
Zusätzlich zum Kopieren von Zeilen in den Ergebnisbereich können Sie neue Datensätze hinzufügen oder bestehende Datensätze ändern oder löschen. Weitere Informationen finden Sie unter [Hinzufügen neuer Zeilen im Ergebnisbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-new-rows-in-the-results-pane-visual-database-tools.md), [Löschen von Zeilen im Ergebnisbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/delete-rows-in-the-results-pane-visual-database-tools.md) und [Bearbeiten von Zeilen im Ergebnisbereich &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/edit-rows-in-the-results-pane-visual-database-tools.md).  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>Hinweise zum Arbeiten mit NULL-Werten und leeren Zellen  
Wenn Sie auf eine leere Zeile klicken, um einen neuen Datensatz hinzuzufügen, beträgt der Anfangswert aller Spalten *NULL*. Wenn eine Spalte NULL-Werte zulässt, können Sie diese unverändert belassen.  
  
Wenn Sie einen Nicht-NULL-Wert durch NULL ersetzen möchten, geben Sie NULL (in Großbuchstaben) ein. Im Ergebnisbereich wird das Wort kursiv formatiert angezeigt, um darauf hinzuweisen, dass es nicht als Zeichenfolge, sondern als NULL-Wert erkannt werden soll.  
  
Geben Sie die Buchstaben ohne Anführungszeichen ein, um die Zeichenfolge "null" einzugeben. Solange mindestens einer der Buchstaben kleingeschrieben ist, wird der Wert als Zeichenfolge statt als NULL-Wert behandelt.  
  
Werte für Spalten mit einem binären Datentyp verfügen standardmäßig über NULL Werte. Diese Werte können im Ergebnisbereich nicht geändert werden.  
  
Um einen Leerraum anstelle von NULL einzugeben, löschen Sie den vorhandenen Text und bewegen den Cursor von der Zelle weg.  
  
## <a name="validating-data"></a>Überprüfen von Daten  
Der Abfrage- und Sicht-Designer kann einige Arten von Daten im Vergleich zu den Spalteneigenschaften überprüfen. Wenn Sie z. B. "abc" in eine Spalte mit einem float-Datentyp eingeben, erhalten Sie eine Fehlermeldung, und die Änderung wird nicht an die Datenbank übermittelt.  
  
Wenn Sie sich im Ergebnisbereich befinden, finden Sie am schnellsten den Datentyp einer Spalte heraus, indem Sie dort den Diagrammbereich öffnen und den Cursor über den Spaltennamen in der Tabelle oder das Tabellenwert-Objekt bewegen.  
  
> [!NOTE]  
> Die maximale Länge, die im Ergebnisbereich für einen Textdatentyp angezeigt werden kann, beträgt 2,147,483,647.  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Synchronhalten des Resultsets mit der Abfragedefinition  
Während Sie mit den Ergebnissen einer Abfrage oder Sicht arbeiten, ist es möglich, dass die Datensätze im Ergebnisbereich nicht mehr mit der Abfragedefinition synchron sind. Wenn Sie beispielsweise eine Abfrage für vier von fünf Spalten einer Tabelle ausgeführt haben und dann den Diagrammbereich verwendet haben, um die fünfte Spalte zur Abfragedefinition hinzuzufügen, werden die Daten der fünften Spalte nicht automatisch dem Ergebnisbereich hinzugefügt. Führen Sie die Abfrage erneut aus, damit der Ergebnisbereich die neue Abfragedefinition wiedergibt.  
  
Sie können feststellen, ob die neue Definition dargestellt wird - ein Alarmsymbol und der Text "Abfrage geändert" werden in der unteren rechten Ecke des Ergebnisbereichs angezeigt, und das Alarmsymbol wird auch in der oberen linken Ecke des Bereichs angezeigt.  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>Abstimmen von Änderungen, die von mehreren Benutzern vorgenommen wurden  
Während Sie mit den Ergebnissen einer Abfrage oder Sicht arbeiten, ist es möglich, dass die Datensätze von einem anderen Benutzer geändert werden, der auch mit der Datenbank arbeitet.  
  
Wenn dies geschieht, erhalten Sie eine Meldung, sobald Sie den Cursor aus der Zelle heraus bewegen, in der der Konflikt auftritt. Sie können anschließend die Änderung des anderen Benutzers überschreiben, Ihren Ergebnisbereich mit der Änderung des anderen Benutzers aktualisieren oder weiterhin Ihren Ergebnisbereich bearbeiten, ohne die Unterschiede abzustimmen. Wenn Sie die Unterschiede nicht abstimmen möchten, wird für die Änderungen kein Commit an die Datenbank ausgeführt.  
  
## <a name="limitations-in-the-results-pane"></a>Einschränkungen im Ergebnisbereich  
  
### <a name="what-can-not-be-updated"></a>Elemente, die nicht aktualisiert werden können  
Diese Tipps können Ihnen helfen, mit Daten im Ergebnisbereich erfolgreich zu arbeiten.  
  
-   Abfragen, die Spalten von mehr als einer Tabelle oder Sicht einschließen, können nicht aktualisiert werden.  
  
-   Sichten können nur aktualisiert werden, wenn die Datenbankeinschränkungen dies zulassen.  
  
-   Von einer gespeicherten Prozedur zurückgegebene Ergebnisse können nicht aktualisiert werden.  
  
-   Abfragen oder Sichten, die die Klauseln GROUP BY, DISTINCT oder TO XML verwenden, sind nicht aktualisierbar.  
  
-   Ergebnisse, die von Tabellenwert-Funktionen zurückgegeben werden, können nur in einigen Fällen aktualisiert werden.  
  
-   Daten in Spalten, die sich aus einem Ausdruck in der Abfrage ergeben.  
  
-   Daten, die nicht erfolgreich vom Anbieter übersetzt wurden.  
  
### <a name="what-can-not-be-represented-fully"></a>Elemente, die nicht vollständig dargestellt werden können  
Das, was die Datenbank an den Ergebnisbereich zurückgibt, wird größtenteils vom Anbieter der von Ihnen verwendeten Datenquelle verwaltet. Der Ergebnisbereich kann nicht immer die Daten von allen Datenbankmanagementsystemen übersetzen. Hier werden einige Fälle aufgeführt, bei denen dies so ist.  
  
-   Binäre Datentypen sind für Benutzer, die im Ergebnisbereich arbeiten, häufig nicht sinnvoll, und für den Download dieser Datentypen kann sehr viel Zeit benötigt werden. Deshalb werden sie als *<Binary data>* oder *Null*dargestellt.  
  
-   Genauigkeit und Skalierung können nicht immer bewahrt werden. Der Ergebnisbereich unterstützt beispielsweise eine Genauigkeit von 27. Liegen die Daten in einem Datentyp mit höherer Genauigkeit vor, können die Daten abgeschnitten oder als *<Unable to read data>*dargestellt werden.  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen grundlegender Vorgänge mit Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Angeben von Suchkriterien &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
