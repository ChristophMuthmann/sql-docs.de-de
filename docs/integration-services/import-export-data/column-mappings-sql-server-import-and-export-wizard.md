---
title: Spaltenzuordnungen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fc3edf9fab16758bfeb6f99549329b69f3da0352
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Spaltenzuordnungen (SQL Server-Import/Export-Assistent)
  Nachdem Sie die zu kopierenden vorhandenen Tabellen und Ansichten ausgewählt oder die von Ihnen angegebene Abfrage überprüft und danach auf **Zuordnungen bearbeiten**geklickt haben, wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent das Dialogfeld **Spaltenzuordnungen** angezeigt. Auf dieser Seite können Sie die Zielspalten für die aus den Quellspalten zu kopierenden Daten angeben und konfigurieren. Häufig müssen Sie auf dieser Seite nichts ändern.
  
Wenn Sie nicht alle Spalten der ausgewählten Tabelle kopieren möchten, können Sie auf dieser Seite die Spalten ausschließen, die Sie nicht benötigen. Wählen Sie in der Spalte **Ziel** der Liste **Zuordnungen** **Ignorieren** für die Spalten aus, die Sie nicht kopieren möchten.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Screenshot der Seite „Spaltenzuordnungen“ 
 Der folgende Screenshot zeigt ein Beispiel für das Dialogfeld **Spaltenzuordnungen** des Assistenten. 
 
 In diesem Beispiel erstellt der Assistent eine neue Zieltabelle, weil **Zieltabelle erstellen** ausgewählt ist. Standardmäßig weist der Assistent jeder Spalte in der neuen Zieltabelle die Namen, Datentypen und Eigenschaften zu, die denen der zugehörigen Quelltabelle entsprechen. 
  
 ![Seite „Spaltenzuordnungen“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/column-mappings.png "Column mappings page of the Import and Export Wizard")  
  
## <a name="review-the-source-and-destination"></a>Überprüfen der Quelle und des Ziels 
![Seite „Spaltenzuordnungen“, Abschnitt „Quelle und Ziel“](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Quelle**  
 Die ausgewählte Quelltabelle, -sicht oder -abfrage.  
  
 **Ziel**  
 Die ausgewählte Zieltabelle oder -sicht.  

## <a name="optionally-create-a-new-destination-table"></a>Optionales Erstellen einer neuen Zieltabelle
![Seite „Spaltenzuordnungen“, Abschnitt „Neue Tabelle“](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Create destination table/file**  
 Erstellen Sie die Zieltabelle, falls diese noch nicht vorhanden ist.    
  
 **SQL bearbeiten**  
Klicken Sie auf **SQL bearbeiten** , um das Dialogfeld **SQL-Anweisung CREATE TABLE** zu öffnen. Verwenden Sie die automatisch generierte Anweisung CREATE TABLE, oder passen Sie sie an Ihre Anforderungen an. Wenn Sie diese Anweisung manuell ändern, müssen Sie sicherstellen, dass die Liste der Spaltenzuordnungen die Änderung erkennt. Weitere Informationen finden Sie unter [SQL-Anweisung CREATE TABLE](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>Manchmal sind diese Optionen deaktiviert
Die Option **Create destination table/file** (Zieltabelle/-datei erstellen) und die Schaltfläche **SQL bearbeiten** sind entweder automatisch aktiviert oder automatisch deaktiviert.

-   **Aktiviert.** Wenn Sie eine **neue** Zieltabelle auf der Seite **Quelltabellen und -sichten auswählen** angegeben haben, wird die Option **Zieltabelle erstellen** automatisch ausgewählt, und die Schaltfläche **SQL bearbeiten** wird aktiviert.

-   **Deaktiviert.** Wenn Sie eine **vorhandene** Zieltabelle auf der Seite **Quelltabellen und -sichten auswählen** ausgewählt haben, werden die Option **Zieltabelle erstellen** und die Schaltfläche **SQL bearbeiten** deaktiviert. Wenn Sie eine neue Zieltabelle erstellen möchten, wechseln Sie zurück zur Seite **Quelltabellen und -sichten auswählen**, und geben Sie den Namen einer **neuen Tabelle** in die Spalte **Ziel** ein.  

## <a name="what-about-existing-data-in-the-destination"></a>Im Ziel vorhandene Daten
![Seite „Spaltenzuordnungen“, Abschnitt „Optionen“](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Delete rows in destination table/file**  
 Geben Sie an, ob die Daten aus einer vorhandenen Tabelle gelöscht werden sollen, bevor neue Daten geladen werden.  
  
 **Append rows to destination table/file**  
 Geben Sie an, ob die neuen Daten an die in der Tabelle bereits enthaltenen Daten angefügt werden sollen.  
  
 **Zieltabelle löschen und erneut erstellen**  
 Wählen Sie diese Option aus, um die Zieltabelle zu überschreiben. Diese Option ist nur verfügbar, wenn Sie den Assistenten verwendet haben, um die Zieltabelle zu erstellen. Die Zieltabelle wird nur gelöscht und erneut erstellt, wenn Sie das vom Assistenten erstellte Paket speichern und anschließend erneut ausführen. Dabei handelt es sich um eine praktische Option, wenn Sie Ihre Einstellungen mehr als einmal testen möchten.
  
 **IDENTITY_INSERT aktivieren**  
 Wählen Sie diese Option aus, damit vorhandene IDENTITY-Werte in den Quelldaten in eine IDENTITY-Spalte in der Zieltabelle eingefügt werden können. In der Standardeinstellung ist dies für die Identity-Zielspalte nicht zulässig.  
  
> [!TIP]
> Wenn Ihre vorhandenen Primärschlüssel in einer Identity-Spalte, einer automatisch nummerierten Spalte oder einem Äquivalent enthalten sind, müssen Sie diese Option auswählen, um die vorhandenen Primärschlüsselwerte beizubehalten.  Andernfalls weist die Identity-Zielspalte in der Regel neue Werte zu.  

## <a name="keep-your-autonumber-or-identity-values"></a>Beibehalten Ihrer automatischen Nummerierung oder Identitätswerte
Wenn Sie Daten exportieren (z.B. aus Microsoft Access), die über eine automatisch nummerierte Spalte oder eine Identitätsspalte verfügen, stellen Sie sicher, dass Sie **IDENTITY_INSERT aktivieren** wie zuvor beschrieben ausgewählt haben.

## <a name="review-column-mappings"></a>Überprüfen der Spaltenzuordnungen
![Seite „Spaltenzuordnungen“, Abschnitt „Zuordnungen“](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Zuordnungen**  
 Zeigt an wie jede Spalte in der Datenquelle einer Spalte im Ziel zugeordnet wird.
 
Die Liste **Zuordnungen** enthält die folgenden Spalten.  
  
-    **Quelle**  
     Zeigen Sie jede Quellspalte an.  
  
-   **Ziel**  
    Zeigen Sie die zugeordnete Zielspalte an, oder wählen Sie eine andere Spalte aus.
    
    Sie müssen nicht alle Spalten aus der Quelltabelle kopieren. Wählen Sie **Ziel** für Spalten auswählen, die ausgelassen werden sollen. Bevor Sie Spalten zuordnen, müssen Sie alle Spalten ignorieren, die nicht zugeordnet werden.  
  
-   **Typ**  
    Zeigen Sie den Datentyp für die Zielspalte an, oder wählen Sie einen anderen Datentyp aus.
  
-   **NULL zulassen**  
    Geben Sie an, ob die Zielspalte NULL-Werte zulässt.  
  
-   **Größe**  
    Geben Sie ggf. die Anzahl der Zeichen in der Zielspalte an.  
  
-    **Genauigkeit**  
    Geben Sie ggf. die Genauigkeit der numerischen Daten (d.h. die Anzahl von Ziffern) in der Zielspalte an.  
  
 -   **Dezimalstellen**  
    Geben Sie ggf. den Bereich (d.h. die Anzahl von Dezimalstellen) der numerischen Daten in der Zielspalte an.  
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie die Zielspalten überprüft und konfiguriert haben, um die aus den Quellspalten kopierten Daten zu erhalten, und auf **OK** geklickt haben, leitet das Dialogfeld **Spaltenzuordnungen** Sie zurück zur Seite **Quelltabellen und -sichten auswählen** oder **Flatfileziel konfigurieren**. Weitere Informationen finden Sie unter [Quelltabellen und -sichten auswählen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) oder [Flatfileziel konfigurieren](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Wenn Sie eine Zuordnung festgelegt haben, die nicht erfolgreich in die Liste **Zuordnungen** übernommen werden kann, leitet Sie das Dialogfeld **Spaltenzuordnungen** zur Seite **Datentypzuordnung überprüfen** um. Auf dieser Seite können Sie die Warnungen überprüfen, Konvertierungsoptionen angeben und außerdem festlegen, wie Fehler behandelt werden sollen. Weitere Informationen finden Sie unter [Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Siehe auch
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

