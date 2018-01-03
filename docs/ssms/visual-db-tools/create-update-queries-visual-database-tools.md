---
title: Erstellen von Updateabfragen (Visual Database Tools) | Microsoft-Dokumentation
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
- tables [SQL Server], updating
- queries [SQL Server], types
- Update query
- updating tables
ms.assetid: 178b7b75-8078-4e61-b2a8-4719b9d8033d
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 42a7e0708746c29755ddf512b69c62ec7a091c2c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-update-queries-visual-database-tools"></a>Erstellen von Updateabfragen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Mit einer Aktualisierungsabfrage können Sie in einem Vorgang den Inhalt mehrerer Zeilen ändern. Sie können beispielsweise in der Tabelle `titles` eine Updateabfrage verwenden, um den Preis aller Bücher eines bestimmten Herausgebers um 10 % zu erhöhen.  
  
Beim Erstellen einer Updateabfrage müssen folgende Angaben gemacht werden:  
  
-   Die zu aktualisierende Tabelle  
  
-   Die Spalten, deren Inhalt Sie aktualisieren möchten  
  
-   Der Wert oder Ausdruck, der zum Aktualisieren der einzelnen Spalten verwendet werden soll  
  
-   Suchbedingungen zum Definieren der zu aktualisierenden Zeilen  
  
Die folgende Abfrage aktualisiert beispielsweise die Tabelle `titles` , indem der Preis sämtlicher Titel eines Herausgebers um 10 % erhöht wird:  
  
```  
UPDATE titles  
SET price = price * 1.1  
WHERE (pub_id = '0766')  
```  
  
> [!CAUTION]  
> Eine ausgeführte Updateabfrage kann nicht rückgängig gemacht werden. Erstellen Sie vorsichtshalber vor Ausführung der Abfrage eine Sicherungskopie der Daten.  
  
### <a name="to-create-an-update-query"></a>So erstellen Sie eine Updateabfrage  
  
1.  Fügen Sie dem Diagrammbereich die zu aktualisierende Tabelle hinzu.  
  
2.  Zeigen Sie im Menü **Abfrage-Designer** auf **Typ ändern**, und klicken Sie dann auf **Aktualisieren**.  
  
    > [!NOTE]  
    > Wenn beim Starten der Updateabfrage mehr als eine Tabelle im Diagrammbereich angezeigt wird, zeigt der Abfrage- und Sicht-Designer das [Dialogfeld „Zieltabelle für eingefügte Ergebnisse auswählen“](../../ssms/visual-db-tools/choose-target-table-for-insert-values-dialog-box-visual-database-tools.md) an, in dem Sie zur Eingabe des Namens der zu aktualisierenden Tabelle aufgefordert werden.  
  
3.  Aktivieren Sie im Diagrammbereich das Kontrollkästchen für die Spalten, für die Sie neue Werte eingeben wollen. Diese Spalten werden im Kriterienbereich angezeigt. Spalten werden nur aktualisiert, wenn sie der Abfrage hinzugefügt werden.  
  
4.  Geben Sie im Kriterienbereich in der Spalte **Neuer Wert** den Updatewert für die Spalte ein. Sie können Literalwerte, Spaltennamen oder Ausdrücke eingeben. Der Wert muss dem Datentyp der zu aktualisierenden Spalte entsprechen (oder mit diesem kompatibel sein).  
  
    > [!CAUTION]  
    > Der Abfrage- und Sicht-Designer kann nicht überprüfen, ob ein Wert von der Länge her in die zu aktualisierende Spalte passt. Bei Eingabe eines zu langen Werts kann dieser ohne vorherige Warnung verkürzt werden. Wenn beispielsweise die Spalte `name` eine Länge von 20 Zeichen aufweist, Sie aber einen aus 25 Zeichen bestehenden Updatewert angeben, werden die letzten 5 Zeichen möglicherweise abgeschnitten.  
  
5.  Definieren Sie die zu aktualisierenden Zeilen, indem Sie in der Spalte **Filter** Suchbedingungen eingeben. Weitere Informationen finden Sie unter [Angeben von Suchbedingungen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Wenn Sie keine Suchbedingung angeben, werden alle Zeilen der angegebenen Tabelle aktualisiert.  
  
    > [!NOTE]  
    > Wenn Sie dem Kriterienbereich eine Spalte zum Verwenden in einer Suchbedingung hinzufügen, wird sie vom Abfrage- und Sicht-Designer auch der Liste der zu aktualisierenden Spalten hinzugefügt. Wenn Sie eine Spalte für eine Suchbedingung verwenden, aber nicht aktualisieren möchten, deaktivieren Sie das Kontrollkästchen in dem Rechteck neben dem Spaltennamen, das die Tabelle oder das Tabellenwertobjekt darstellt.  
  
Beim Ausführen einer Updateabfrage werden keine Ergebnisse im [Ergebnisbereich](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)angezeigt. Stattdessen wird eine Meldung mit der Anzahl der geänderten Zeilen ausgegeben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Unterstützte Abfragetypen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
