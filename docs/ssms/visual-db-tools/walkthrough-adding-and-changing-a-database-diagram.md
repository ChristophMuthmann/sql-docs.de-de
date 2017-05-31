---
title: "Exemplarische Vorgehensweise: Hinzufügen und Ändern von Datenbankdiagrammen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database diagrams [SQL Server], about database diagrams
- database diagrams [SQL Server], designing
- database diagrams [SQL Server], creating
ms.assetid: 228caa0d-8f24-46ab-86d1-b6d8631322bc
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2c1a211f11917f54f0f2c69bd2d1b96034cba41
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="walkthrough-adding-and-changing-a-database-diagram"></a>Exemplarische Vorgehensweise: Hinzufügen und Ändern von Datenbankdiagrammen
In dieser exemplarischen Vorgehensweise wird das Erstellen und Ändern eines Datenbankdiagramms und das Ausführen von Änderungen an der Datenbank mithilfe der Datenbankdiagrammkomponente erläutert. Es wird in Einzelschritten erklärt, wie Diagrammen Tabellen hinzugefügt werden, wie Beziehungen zwischen Tabellen erstellt werden, wie Einschränkungen und Indizes für Spalten erstellt werden und wie die Ebene der Informationen geändert wird, die für die einzelnen Tabellen angezeigt werden.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Wenn Sie diese exemplarische Vorgehensweise abschließen möchten, müssen folgende Voraussetzungen erfüllt sein:  
  
-   Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mit der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] -Beispieldatenbank  
  
-   Ein Konto mit Rechten als Datenbankbesitzer ( **dbo** )  
  
> [!NOTE]  
> Wenn Sie versuchen, über ein Konto Änderungen vorzunehmen, das nicht über ausreichende Rechte zum Ändern von Tabellen verfügt, wird eine Fehlermeldung angezeigt.  
  
## <a name="creating-a-diagram"></a>Erstellen eines Diagramms  
  
#### <a name="to-create-a-new-database-diagram"></a>So erstellen Sie ein neues Datenbankdiagramm  
  
1.  Klicken Sie im Menü **Ansicht** auf **Objekt-Explorer**.  
  
2.  Öffnen Sie den Knoten Datenbanken und dann den Knoten [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] .  
  
3.  Klicken Sie mit der rechten Maustaste auf den Knoten Datenbankdiagramme, und wählen Sie **Neues Datenbankdiagramm** aus.  
  
    Wenn die Datenbank nicht über die zum Erstellen von Diagrammen erforderlichen Objekte verfügt, wird folgende Meldung angezeigt: **Dieser Datenbank fehlt mindestens eines der Unterstützungsobjekte, die erforderlich sind, damit Diagramme für die Datenbank erstellt werden können. Möchten Sie es erstellen?** Klicken Sie auf **Ja**.  
  
    Das Dialogfeld **Tabelle hinzufügen** wird angezeigt.  
  
4.  Wählen Sie **Adresstyp (Person)** und **Adresse (Person)** aus, und klicken Sie auf **Hinzufügen**.  
  
    Dem Diagramm werden zwei Tabellen hinzugefügt.  
  
5.  Schließen Sie das Dialogfeld **Tabelle hinzufügen** .  
  
#### <a name="to-view-different-column-data"></a>So zeigen Sie unterschiedliche Spaltendaten an  
  
1.  Klicken Sie mit der rechten Maustaste auf die `Address` -Tabelle. Zeigen Sie im Kontextmenü auf **Tabellensicht**, und klicken Sie dann auf **Standard**.  
  
    Im Tabellenraster werden drei Spalten angezeigt: **Spaltenname**, **Datentyp**und **NULL-Werte zulassen**.  
  
2.  Klicken Sie mit der rechten Maustaste auf die `Address` -Tabelle, klicken Sie auf **Tabellensicht** , und wählen Sie **Schlüssel**aus.  
  
    Im Tabellenraster wird eine Spalte mit den Tabellenspaltennamen angezeigt. Es werden nur solche Spalten angezeigt, die an Indizes beteiligt sind.  
  
## <a name="creating-new-tables"></a>Erstellen neuer Tabellen  
  
#### <a name="to-create-tables-within-diagram-designer"></a>So erstellen Sie Tabellen im Datenbank-Designer  
  
1.  Klicken Sie mit der rechten Maustaste auf den Datenbank-Designer außerhalb der vorhandenen Tabellen, und wählen Sie **Neue Tabelle**aus.  
  
2.  Klicken Sie im Dialogfeld **Namen auswählen** auf **OK** , um den Standardnamen **Table1**zu übernehmen.  
  
    Ein neues Tabellenraster mit drei Spalten wird angezeigt: **Spaltenname**, **Datentyp**und **NULL-Werte zulassen**.  
  
3.  Fügen Sie **Table1**folgende Informationen hinzu:  
  
    |**Spaltenname**|**Datentyp**|**NULL-Werte zulassen**|  
    |-------------------|-----------------|-------------------|  
    |**T1col1**|**int**|Überprüft|  
    |**T1col2**|**varchar(50)**|Überprüft|  
    |**T1col3**|**float**|Überprüft|  
  
4.  Klicken Sie mit der rechten Maustaste auf `T1col1` , und wählen Sie **Primärschlüssel festlegen**aus.  
  
    Neben dem Spaltennamen wird ein Schlüsselsymbol angezeigt.  
  
5.  Klicken Sie im Menü **Datei** auf **Diagramm1 speichern**.  
  
6.  Klicken Sie im Dialogfeld **Namen auswählen** auf **OK** , um den Standardnamen **Diagram1**zu übernehmen.  
  
7.  Das Dialogfeld **Speichern** wird angezeigt, und in einer Meldung wird darüber informiert, dass `Table1` in der Datenbank gespeichert wird. Klicken Sie auf **Ja**.  
  
## <a name="modifying-table-structure"></a>Ändern der Tabellenstruktur  
Im Datenbank-Designer können Sie CHECK-Einschränkungen hinzufügen und Beziehungen zwischen Tabellen herstellen.  
  
#### <a name="to-create-check-constraints"></a>So erstellen Sie CHECK-Einschränkungen  
  
1.  Klicken Sie in `Table1`mit der rechten Maustaste in die `T1col3` -Zeile, und wählen Sie **CHECK-Einschränkungen**aus.  
  
    Das Dialogfeld **CHECK-Einschränkungen** wird angezeigt.  
  
2.  Klicken Sie auf **Hinzufügen**.  
  
    In der Liste **CHECK-Einschränkung (ausgewählt)** wird eine neue Einschränkung mit dem Standardnamen `CK_Table1`angezeigt.  
  
3.  Wählen Sie im Raster die **Ausdruck** -Zeile aus, und klicken Sie auf die Schaltfläche mit den Auslassungspunkten.  
  
    Das Dialogfeld **CHECK-Einschränkungsausdruck** wird angezeigt.  
  
4.  Geben Sie **T1col3 > 5** ein, und klicken Sie auf **OK**.  
  
    `Table1` verfügt jetzt über die Einschränkung, dass alle in `T1col3` eingegebenen Werte größer als 5 sein müssen.  
  
5.  Klicken Sie auf **Schließen**.  
  
#### <a name="to-create-relationships-between-tables"></a>So erstellen Sie Beziehungen zwischen Tabellen  
  
1.  Erstellen Sie im Datenbank-Designer eine neue Tabelle mit dem Namen `Table2` und mit folgenden Spalten:  
  
    |**Spaltenname**|**Datentyp**|**NULL-Werte zulassen**|  
    |-------------------|-----------------|-------------------|  
    |**T2col1**|**int**|nicht aktiviert|  
    |**T2col2**|**varchar(50)**|Überprüft|  
    |**T2col3**|**xml**|Überprüft|  
  
    > [!NOTE]  
    > Die Spalten in einer Fremdschlüsselbeziehung, die sich auf der Seite des Primärschlüssels befinden, müssen Teil eines Primärschlüssels oder einer Unique-Einschränkung sein.  
  
2.  Ziehen Sie `T2col1` in `T1col1`.  
  
    Es werden zwei Dialogfelder angezeigt: **Fremdschlüsselbeziehung** im Hintergrund und **Tabellen und Spalten** im Vordergrund.  
  
3.  Klicken Sie auf **OK** , um die neue Beziehung zu speichern.  
  
4.  Klicken Sie erneut auf **OK** .  
  
## <a name="creating-indexes"></a>Erstellen von Indizes  
Sie können für die meisten Datentypen (einschließlich XML) Indizes erstellen.  
  
#### <a name="to-create-a-standard-index"></a>So erstellen Sie einen Standardindex  
  
1.  Klicken Sie mit der rechten Maustaste auf `Table1` , und wählen Sie **Indizes/Schlüssel**aus.  
  
    Das Dialogfeld **Indizes/Schlüssel** wird angezeigt.  
  
2.  Klicken Sie auf **Hinzufügen**.  
  
    In der Liste **Primärschlüssel/eindeutiger Schlüssel oder Index (ausgewählt)** wird ein neuer Index mit einem Standardnamen wie `IX_Table1`angezeigt.  
  
3.  Wählen Sie die **Spalten** -Zeile aus, und klicken Sie auf die Schaltfläche mit den Auslassungspunkten.  
  
    Das Dialogfeld **Indexspalten** wird angezeigt.  
  
4.  Klicken Sie auf den Dropdownpfeil unter **Spaltenname** , und wählen Sie `T1col2`aus.  
  
    > [!NOTE]  
    > Sie können diesem Index zusätzliche Spalten hinzufügen, indem Sie die Zelle unter `T1col2` auswählen und einen anderen Spaltennamen auswählen.  
  
5.  Klicken Sie auf **OK** , um diesen Index zu speichern.  
  
6.  Klicken Sie im Dialogfeld **Indizes/Schlüssel** auf **Schließen** .  
  
#### <a name="to-create-an-xml-index"></a>So erstellen Sie einen XML-Index  
  
1.  Klicken Sie mit der rechten Maustaste auf `T2col1` , und wählen Sie **Primärschlüssel festlegen**aus.  
  
    > [!NOTE]  
    > Voraussetzung für das Hinzufügen eines XML-Index ist es, dass eine andere Spalte in der Tabelle als gruppierter Primärschlüssel festgelegt wurde.  
  
2.  Klicken Sie mit der rechten Maustaste auf die `T2col3` -Zeile in `Table2` , und wählen Sie **XML-Indizes**aus.  
  
    Das Dialogfeld **XML-Indizes** wird angezeigt.  
  
3.  Klicken Sie auf **Hinzufügen**.  
  
    Ein XML-Index mit Standardwerten wird der Liste **XML-Index (ausgewählt)** hinzugefügt.  
  
4.  Klicken Sie auf **Schließen**.  
  
    > [!NOTE]  
    > XML-Indizes werden auf Spaltenbasis erstellt. Dabei ist der erste XML-Index primär, und alle weiteren Indizes sind sekundär.  
  
## <a name="saving-the-diagram"></a>Speichern des Diagramms  
Sämtliche von Ihnen an einem Diagramm vorgenommenen Änderungen werden erst nach dem Speichern des Diagramms an die Datenbank gesendet. Wenn Probleme oder Konflikte auftreten, wird ein Dialogfeld mit weiteren Informationen angezeigt.  
  
#### <a name="to-save-a-database-diagram"></a>So speichern Sie ein Datenbankdiagramm  
  
1.  Wählen Sie im Menü **Datei** die Option **Diagramm1 speichern**aus.  
  
    Das Dialogfeld **Speichern** wird angezeigt. Wenn **Warnung bei betroffenen Tabellen** aktiviert ist, werden Informationen zu neuen oder geänderten Tabellen aufgeführt.  
  
2.  Klicken Sie auf **OK**.  
  
3.  Wenn Fehler aufgetreten sind, wird das Dialogfeld **Benachrichtigung nach dem Speichervorgang** angezeigt, das die Fehler und deren Ursachen enthält. Beheben Sie die Fehler, und speichern Sie das Diagramm anschließend erneut.  
  
## <a name="next-steps"></a>Nächste Schritte  
Hierbei handelt es sich um ein einfaches Diagramm, das nur zwei vorhandene und zwei neue Tabellen enthält. Damit wird jedoch das Potenzial zur Diagrammdarstellung einer vorhandenen Datenbank oder zur visuellen Erstellung eines neuen Schemas veranschaulicht. Mit folgenden Funktionen können Sie Ihre Fähigkeiten vertiefen:  
  
-   Erstellen neuer Diagramme mit Gruppen verbundener Tabellen  
  
-   Anpassen der für jede Tabelle angezeigten Informationsmenge  
  
-   Ändern des Layouts und Hinzufügen von Anmerkungen  
  
-   Kopieren des Diagramms in eine Bitmap  
  
## <a name="see-also"></a>Siehe auch  
[Anpassen des Umfangs der in Diagrammen angezeigten Informationen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)  
[Einrichten im Datenbankdiagramm-Designer &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
[Hinzufügen von Tabellen zu Diagrammen &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
[Erstellen von Beziehungen zwischen Tabellen in einem Diagramm &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/create-relationships-between-tables-on-a-diagram-visual-database-tools.md)  
[Erstellen von XML-Indizes](http://msdn.microsoft.com/en-us/6ecac598-355d-4408-baf7-1b2e8d4cf7c1)  
[Kopieren eines Datenbankdiagrammimages in die Zwischenablage &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/copy-an-image-of-a-database-diagram-to-the-clipboard-visual-database-tools.md)  
[Verwenden von Diagrammlayout &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  

