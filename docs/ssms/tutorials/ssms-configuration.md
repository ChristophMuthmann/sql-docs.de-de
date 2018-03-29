---
Title: 'Tutorial: SQL Server Management Studio Components and Configuration'
description: Ein Tutorial, in dem die Komponenten und grundlegenden Konfigurationsoptionen für Ihre SQL Server Management Studio-Umgebung erläutert werden.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/16/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 8cdb4f258f62b425be78e9f6b4628d69e304c7ba
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-sql-server-management-studio-components-and-configuration"></a>Tutorial: SQL Server Management Studio-Komponenten und -Konfiguration
In diesem Tutorial werden die verschiedenen Fensterkomponenten in SQL Server Management Studio (SSMS) und einige grundlegende Konfigurationsoptionen für Ihren Arbeitsbereich erläutert. In diesem Artikel erhalten Sie Informationen zu Folgendem: 

> [!div class="checklist"]
> * Den verschiedenen Komponenten der SSMS-Umgebung
> * Ändern des Umgebungslayouts und Zurücksetzen des Layouts auf den Standard
> * Maximieren des Abfrage-Editors
> * Ändern der Schriftart 
> * Konfigurieren von Startoptionen 
> * Zurücksetzen der Konfiguration auf den Standard 

## <a name="prerequisites"></a>Voraussetzungen
Zur Durchführung dieses Tutorials benötigen Sie SQL Server Management Studio.  

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="sql-server-management-studio-components"></a>Komponenten von SQL Server Management Studio
In diesem Abschnitt werden die unterschiedlichen im Arbeitsbereich verfügbaren Fensterkomponenten und ihre Zwecke erläutert. 

- Die einzelnen Fensterkomponenten können geschlossen werden, indem in der Ecke der Titelleiste auf das „X“ geklickt wird. Sie können anschließend wieder über das Dropdownfeld **Ansicht** im Hauptmenü geöffnet werden. 

    ![Menü 'Ansicht'](media/ssms-configuration/viewmenu.png)

- **Objekt-Explorer** (F8): Objekt-Explorer enthält eine Strukturansicht aller Datenbankobjekte eines Servers. Dazu können die Datenbanken der SQL Server-Datenbank-Engine, der Analysis Services, der Reporting Services und der Integration Services zählen. Der Objekt-Explorer umfasst Informationen zu allen Servern, mit denen eine Verbindung besteht. 
    
    ![Objekt-Explorer](media/ssms-configuration/objectexplorer.png)
- **Abfragefenster** (Strg + N): Sobald Sie auf **Neue Abfrage** geklickt haben, können Sie in diesem Fenster Ihre T-SQL-Abfragen (Transact-SQL) eingeben. Auch die Ergebnisse Ihrer Abfragen werden hier angezeigt.
    
    ![Neues Abfragefenster](media/ssms-configuration/newquery.png)

- **Eigenschaften** (F4): Diese Fensterkomponente wird sichtbar, sobald das **Abfragefenster** geöffnet wird und grundlegende Eigenschaften der Abfrage angezeigt werden. So werden beispielsweise der Zeitpunkt, zu dem eine Abfrage gestartet wurde, die Anzahl der zurückgegebenen Zeilen und Verbindungsdetails angezeigt.  

    ![Eigenschaften](media/ssms-configuration/properties.png)

- **Vorlagenbrowser** (Strg + Alt + T): Im Vorlagenbrowser befinden sich einige vorgefertigte T-SQL-Vorlagen. Mithilfe dieser Vorlagen können Sie verschiedene Funktionen ausführen, wie z.B. das Erstellen oder Sichern einer Datenbank. 

    ![Vorlagenbrowser](media/ssms-configuration/templates.png)

- **Details zu Objekt-Explorer**(F7): Dies ist eine detailliertere Ansicht von Objekt-Explorer, in der Sie mehrere Objekte gleichzeitig bearbeiten können. Im Fenster „Details zu Objekt-Explorer“ können Sie beispielsweise mehrere Datenbanken gleichzeitig auswählen und diese entweder löschen oder ausarbeiten. 

    ![Details zum Objekt-Explorer](media/ssms-configuration/objectexplorerdetails.PNG) 
 

    

## <a name="change-the-environmental-layout"></a>Ändern des Umgebungslayouts 
Dieser Abschnitt behandelt die Bearbeitung des Umgebungslayouts, wie z.B. das Verschieben der verschiedenen Fenster. 

-  Die einzelnen Fensterkomponenten können verschoben werden, indem der Titel gedrückt gehalten und das Fenster gezogen wird. 
- Sie können angeheftet und losgelöst werden, indem Sie auf das Reißzweckensymbol in der Titelleiste klicken:
    
    ![Anheften von Objekten](media/ssms-configuration/pushpin.png)

- An jeder Fensterkomponente befindet sich ein Dropdownpfeil, über den das Fenster auf verschiedene Weise bearbeitet werden kann: 

    ![Fensteroptionen](media/ssms-configuration/windowoptions.png)

- Sobald Sie mindestens zwei Fenster geöffnet haben, können sie vertikal oder horizontal im Registerkartenformat angeordnet werden, sodass beide Abfragefenster gleichzeitig sichtbar sind. Klicken Sie hierzu mit der rechten Maustaste auf den Titel der Abfrage, und wählen Sie die gewünschte Option für das Registerkartenformat aus. 
 
    ![Optionen für das Registerkartenformat der Abfrage](media/ssms-configuration/querytabbedoptions.png)

    - Dies ist die **Horizontale Registerkartengruppe**: ![Horizontale Registerkartengruppe](media/ssms-configuration/horizontaltab.png)     
    
    - Dies ist die **Vertikale Registerkartengruppe**:  
        ![Vertikale Registerkartengruppe](media/ssms-configuration/verticaltabgroup.png)
        

    - Wenn Sie die Registerkarten wieder zusammenführen möchten, klicken Sie erneut mit der rechten Maustaste auf den Abfragetitel und auf **Move to Next Tab Group** (Zur nächsten Registerkartengruppe wechseln) oder auf **Move to Previous Tab Group** (Zur vorherigen Registerkartengruppe wechseln):
    
        ![Registerkarten der Abfrage zusammenführen](media/ssms-configuration/mergetabgroups.png)

- Klicken Sie zum Wiederherstellen des standardmäßigen Umgebungslayouts auf das Menü **Fenster** > **Fensterlayout zurücksetzen**:
 
    ![Fensterlayout wiederherstellen](media/ssms-configuration/resetwindowlayout.png)
    
## <a name="maximize-query-editor"></a>Maximieren des Abfrage-Editors
Der Abfrage-Editor kann in den Vollbildmodus maximiert werden.

1. Klicken Sie im Fenster des Abfrage-Editors auf eine beliebige Stelle.
2. Drücken Sie UMSCHALT+ALT+EINGABETASTE, um zwischen dem Vollbildmodus und dem normalen Modus zu wechseln. 

Diese Tastenkombination gilt für jedes Dokumentfenster. 



## <a name="change-basic-settings"></a>Ändern der Standardeinstellungen
In diesem Abschnitt wird erläutert, wie einige grundlegende Einstellungen in SSMS geändert werden können. Diese Optionen sind unter der Menüoption **Tools** zu finden:

  ![Menü 'Extras'](media/ssms-configuration/tools.png)


- Die hervorgehobene Symbolleiste kann durch Navigieren zum Menü **Tools** > **Anpassen** geändert werden:

    ![Symbolleiste anpassen](media/ssms-configuration/toolbar.png)

### <a name="change-the-font"></a>Ändern der Schriftart
- Die Schriftart kann über das Menü **Tools** > **Optionen** > **Schriftarten und Farben** geändert werden:

     ![Schriftarten und Farben](media/ssms-configuration/fontsandcolors.png)

### <a name="change-the-startup-options"></a>Ändern der Startoptionen
- Die Startoptionen bestimmen, wie Ihr Arbeitsbereich beim ersten Starten von SSMS aussieht. Diese können über das Menü **Tools** > **Optionen** > **Start** konfiguriert werden:
 
    ![Startoptionen](media/ssms-configuration/startup.png)

### <a name="reset-settings-to-default"></a>Zurücksetzen auf die Standardeinstellungen
- All diese Einstellungen können über das Menü **Tools** > **Einstellungen importieren und exportieren** importiert und exportiert werden. 

    ![Einstellungen importieren und exportieren](media/ssms-configuration/settings.png)
    - Dort können Sie auch all Ihre Einstellungen auf den Standardwert zurücksetzen. 


## <a name="next-steps"></a>Nächste Schritte
Im nächsten Artikel erhalten Sie weitere nützliche Informationen zu SSMS, wie z.B. wo Sie Ihr eigenes SQL Server-Fehlerprotokoll finden und was der Name Ihrer SQL-Instanz ist. 

Für weitere Informationen zum nächsten Artikel blättern
> [!div class="nextstepaction"]
> [Schaltfläche „Nächste Schritte“](ssms-tricks.md)
 
 




