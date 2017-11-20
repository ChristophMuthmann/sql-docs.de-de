---
title: Spaltenzuordnungen (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1ed879f21396c3c8d588307eaf087daea8c44c3
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>Spaltenzuordnungen (SQL Server-Import/Export-Assistent)
  Nachdem Sie die zu kopierenden vorhandenen Tabellen und Ansichten ausgewählt oder die von Ihnen angegebene Abfrage überprüft und danach auf **Zuordnungen bearbeiten**geklickt haben, wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent das Dialogfeld **Spaltenzuordnungen** angezeigt. Auf dieser Seite angeben und konfigurieren die Zielspalten zum Empfangen von Daten aus den Quellspalten kopiert. Häufig müssen Sie nichts auf dieser Seite ändern.
  
Wenn Sie nicht möchten, dass für alle Spalten in der Tabelle zu kopieren, die Sie ausgewählt wird, ist dabei, die Sie auf dieser Seite ausführen können Spalten ausschließen nicht benötigter. Wählen Sie **ignorieren** in der **Ziel** Spalte die **Zuordnungen** Liste der Spalten, die Sie kopieren möchten.
 
## <a name="screen-shot-of-the-column-mappings-page"></a>Screenshot der Seite „Spaltenzuordnungen“ 
 Der folgende Screenshot zeigt ein Beispiel der **Spaltenzuordnungen** Dialogfeld des Assistenten. 
 
 In diesem Beispiel erstellt der Assistent eine neue Zieltabelle, weil **Zieltabelle erstellen** ausgewählt ist. Standardmäßig bietet der Assistent jede Spalte in die neue Zieltabelle, die mit dem gleichen Namen, Datentyp und Eigenschaften als die Quellspalte an. 
  
 ![Seite der Spalte Zuordnungen des Import / Export-Assistenten](../../integration-services/import-export-data/media/column-mappings.png "Spalte Zuordnungen Seite des Import / Export-Assistenten")  
  
## <a name="review-the-source-and-destination"></a>Überprüfen Sie die Quelle und Ziel 
![Spalte Zuordnungen Seite, Quelle und Ziel-Abschnitt](../../integration-services/import-export-data/media/column-mappings-page-source-and-destination-section.png)

 **Quelle**  
 Die ausgewählte Quelltabelle, Sicht oder Abfrage.  
  
 **Ziel**  
 Die ausgewählte Zieltabelle oder Sicht.  

## <a name="optionally-create-a-new-destination-table"></a>Erstellen Sie optional eine neue Zieltabelle
![Spalte Zuordnungen Seite "neue im Tabellenabschnitt"](../../integration-services/import-export-data/media/column-mappings-page-new-table-section.png)

 **Create destination table/file**  
 Erstellen Sie die Zieltabelle, wenn sie nicht bereits vorhanden ist.    
  
 **SQL bearbeiten**  
Klicken Sie auf **SQL bearbeiten** , um das Dialogfeld **SQL-Anweisung CREATE TABLE** zu öffnen. Verwenden Sie den automatisch generierten CREATE TABLE-Anweisung, oder ändern Sie es für Ihre Zwecke. Wenn Sie diese Anweisung manuell ändern, müssen Sie sicherstellen, dass die Liste der Spaltenzuordnungen die Änderung erkennt. Weitere Informationen finden Sie unter [SQL-Anweisung CREATE TABLE](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md).  

### <a name="sometimes-these-options-are-disabled"></a>In einigen Fällen sind diese Optionen deaktiviert.
Die **Zieltabelle erstellen** Option und die **SQL bearbeiten** Schaltfläche werden automatisch aktiviert, oder automatisch deaktiviert.

-   **Aktiviert.** Wenn Sie angegeben haben eine **neue** Zieltabelle auf die **Quelltabellen und Sichten auswählen** Seite der **Zieltabelle erstellen** automatisch ausgewählt ist und die  **SQL bearbeiten** Schaltfläche ist aktiviert.

-   **Deaktiviert.** Bei Auswahl einer **vorhandenen** Zieltabelle auf die **wählen Quelltabellen und-Sichten** Seite der **Zieltabelle erstellen** Option und die **SQL bearbeiten**  Schaltfläche deaktiviert werden. Wenn Sie eine neue Zieltabelle erstellen möchten, wechseln Sie zurück, um die **Quelltabellen und Sichten auswählen** Seite, und geben Sie den Namen des eine **neue** -Tabelle in der **Ziel** Spalte.  

## <a name="what-about-existing-data-in-the-destination"></a>Was ist mit der vorhandenen Daten in das Ziel?
![Spalte Seite "Zuordnungen", im Abschnitt ""](../../integration-services/import-export-data/media/column-mappings-page-options-section.png)

 **Delete rows in destination table/file**  
 Geben Sie an, ob die Daten aus einer vorhandenen Tabelle gelöscht werden sollen, bevor neue Daten geladen werden.  
  
 **Append rows to destination table/file**  
 Geben Sie an, ob die neuen Daten an die in der Tabelle bereits enthaltenen Daten angefügt werden sollen.  
  
 **Zieltabelle löschen und erneut erstellen**  
 Wählen Sie diese Option aus, um die Zieltabelle zu überschreiben. Diese Option ist nur verfügbar, wenn Sie den Assistenten verwendet, um die Zieltabelle zu erstellen. Die Zieltabelle wird nur gelöscht und erneut erstellt, wenn Sie das vom Assistenten erstellte Paket speichern und anschließend erneut ausführen. Dabei handelt es sich um eine praktische Option, wenn Sie Ihre Einstellungen mehr als einmal testen möchten.
  
 **IDENTITY_INSERT aktivieren**  
 Wählen Sie diese Option aus, damit vorhandene IDENTITY-Werte in den Quelldaten in eine IDENTITY-Spalte in der Zieltabelle eingefügt werden können. In der Standardeinstellung ist dies für die Identity-Zielspalte nicht zulässig.  
  
> [!TIP]
> Wenn Ihre vorhandenen Primärschlüssel in einer Identity-Spalte, einer automatisch nummerierten Spalte oder einem Äquivalent enthalten sind, müssen Sie diese Option auswählen, um die vorhandenen Primärschlüsselwerte beizubehalten.  Andernfalls weist die Identity-Zielspalte in der Regel neue Werte zu.  

## <a name="keep-your-autonumber-or-identity-values"></a>Halten Sie Ihre Autonumber oder die Identity-Werte
Wenn Sie Daten exportieren, die eine AutoWert-Spalte oder eine Identitätsspalte - verfügt z. B. Wenn Sie aus Microsoft Access - exportieren, stellen Sie sicher Auswahl **IDENTITY_INSERT aktivieren** wie sofort oben beschrieben.

## <a name="review-column-mappings"></a>Überprüfen Sie die spaltenzuordnungen
![Spalte Zuordnungen Seite "Zuordnungen im Abschnitt"](../../integration-services/import-export-data/media/column-mappings-page-mappings-section.png)

 **Zuordnungen**  
 Zeigt an wie jede Spalte in der Datenquelle einer Spalte im Ziel zugeordnet wird.
 
Die Liste **Zuordnungen** enthält die folgenden Spalten.  
  
-    **Quelle**  
     Zeigen Sie die einzelnen Quellspalten an.  
  
-   **Ziel**  
    Zeigen Sie die zugeordnete Zielspalte an, oder wählen Sie eine andere Spalte aus.
    
    Sie müssen nicht alle Spalten aus der Quelltabelle zu kopieren. Wählen Sie **Ziel** für Spalten auswählen, die ausgelassen werden sollen. Bevor Sie Spalten zuordnen, müssen Sie alle Spalten ignorieren, die nicht zugeordnet werden.  
  
-   **Typ**  
    Zeigen Sie den Datentyp für die Zielspalte an, oder wählen Sie einen anderen Datentyp aus.
  
-   **NULL zulassen**  
    Geben Sie an, ob die Zielspalte NULL-Werte zulässt.  
  
-   **Größe**  
    Geben Sie ggf. die Anzahl der Zeichen in der Zielspalte an.  
  
-    **Genauigkeit**  
    Geben Sie ggf. in der Zielspalte - d. h. die Anzahl der Ziffern - die Genauigkeit der numerischen Daten an.  
  
 -   **Dezimalstellen**  
    Geben Sie ggf. in der Zielspalte – d. h. die Anzahl der Dezimalstellen - die Skala numerischer Daten an.  
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie überprüft, und konfigurieren die Zielspalten empfangen die Daten aus den Quellspalten kopiert, und klicken Sie auf **OK**, **Spaltenzuordnungen** Dialogfeld wird wieder die **Quelle auswählen Tabellen und Sichten** Seite oder auf die **Flatfileziel konfigurieren** Seite. Weitere Informationen finden Sie unter [Quelltabellen und -sichten auswählen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) oder [Flatfileziel konfigurieren](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
  
 Wenn Sie eine Zuordnung festgelegt haben, die nicht erfolgreich in die Liste **Zuordnungen** übernommen werden kann, leitet Sie das Dialogfeld **Spaltenzuordnungen** zur Seite **Datentypzuordnung überprüfen** um. Auf dieser Seite können Sie die Warnungen überprüfen, Konvertierungsoptionen angeben und außerdem festlegen, wie Fehler behandelt werden sollen. Weitere Informationen finden Sie unter [Datentypzuordnung überprüfen](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Siehe auch
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)  
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


