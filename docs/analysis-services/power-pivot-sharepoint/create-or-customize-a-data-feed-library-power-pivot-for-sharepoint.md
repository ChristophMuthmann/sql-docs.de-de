---
title: "Erstellen oder Anpassen einer Datenfeedbibliothek (Power Pivot f&#252;r SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenfeedbibliothek"
  - "Datenfeeds [Analysis Services mit SharePoint]"
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 22
---
# Erstellen oder Anpassen einer Datenfeedbibliothek (Power Pivot f&#252;r SharePoint)
  Eine *Datenfeedbibliothek* ist eine zweckgebundene SharePoint-Bibliothek, mit der Sie Atom-Datendienstdokumente (.atomsvc) registrieren und freigeben können. Diese Dokumente enthalten XML-Datenfeeds in [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen oder anderen Clientanwendungen, die das Atom-Datenfeedformat unterstützen. Eine Datenfeedbibliothek unterscheidet sich von anderen SharePoint-Bibliotheken, da sie folgende Möglichkeiten bietet:  
  
-   Erstellen oder Bearbeiten eines *Datendienstdokuments*, das zum Angeben einer HTTP-Verbindung mit einem bestimmten Feed verwendet wird.  
  
-   Freigeben und Verwalten von Datendienstdokumenten an einem zentralen Speicherort.  
  
-   Visuelles Kennzeichnen von Datendienstdokumenten durch ein Symbol, damit Dienstdokumente leicht von anderen in der gleichen Bibliothek gespeicherten Dokumenten unterschieden werden können: ![GMNI_IconDataFeed](../../analysis-services/power-pivot-sharepoint/media/gmni-icondatafeed.png "GMNI_IconDataFeed")  
  
 Eine Datenfeedbibliothek enthält immer Datendienstdokumente (ATOMSVC-Dateien) und nie den Datenfeed selbst. Im Gegensatz zu einem Datenfeed, der aus statischen XML-Daten besteht, gibt das Datendienstdokument eine URL zu einem Dienst oder einer Anwendung an, der bzw. die auf Anforderung einen Feed generiert, und stellt wiederverwendbare Verbindungsinformationen für wiederholbare Importvorgänge bereit.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Erforderliche Komponenten](#prereq)  
  
 [Erstellen einer neuen Datenfeedbibliothek](#createlib)  
  
 [Hinzufügen des Inhaltstyps für Datenfeeds zu einer Bibliothek](#addtolib)  
  
##  <a name="prereq"></a> Erforderliche Komponenten  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Funktion muss für die Websites aktiviert werden, für die Sie die Datenfeedbibliothek erstellen. Wenn der Vorlagentyp für Datenfeedbibliotheken nicht verfügbar ist, liegt dies höchstwahrscheinlich daran, dass diese Voraussetzung nicht erfüllt wurde. Weitere Informationen finden Sie unter [Activate Power Pivot Feature Integration for Site Collections in Central Administration](../../analysis-services/power-pivot-sharepoint/activate power pivot integration for site collections in ca.md).  
  
 Sie müssen Websitebesitzer sein, um die Bibliothek erstellen zu können.  
  
##  <a name="createlib"></a> Erstellen einer neuen Datenfeedbibliothek  
 Das Erstellen einer Datenfeedbibliothek ist der erste Schritt zur Aktivierung von Datenfeeds für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Arbeitsmappen. Da eine Datenfeedbibliothek Anwendungs- und Verwaltungsseiten für Datendienstdokumente bereitstellt, muss diese Bibliothek vorhanden sein, bevor Sie ein neues Dokument erstellen können.  
  
 Eine Datenfeedbibliothek basiert auf einer integrierten Vorlage und einem vorkonfigurierten *Inhaltstyp für Datendienstdokumente*, der Eigenschaften und Verhaltensweisen für ein Datendienstdokument definiert.  
  
1.  Klicken Sie in der oberen linken Ecke der Seite auf **Websiteaktionen** .  
  
2.  Klicken Sie auf **Weitere Optionen**...  
  
3.  Klicken Sie unter Bibliotheken auf **Datenfeedbibliothek**.  
  
4.  Geben Sie Namen, Beschreibung, Start- und Versionseinstellungen ein. Geben Sie auch beschreibende Informationen an, um Benutzern die Identifikation dieser Bibliothek als Speicherort für Datendienstdokumente zu erleichtern.  
  
5.  Klicken Sie auf **Erstellen**.  
  
 Im Schnellstart-Navigationsbereich für die aktuelle Website wird ein Link zur Datenfeedbibliothek angezeigt.  
  
 Nachdem Sie eine Bibliothek erstellt haben, können Sie mit ihrer Hilfe Datendienstdokumente erstellen. Weitere Informationen finden Sie unter [Verwenden von Datenfeeds &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="addtolib"></a> Hinzufügen des Inhaltstyps für Datenfeeds zu einer Bibliothek  
 Wenn Sie keine dedizierte Datenfeedbibliothek erstellen, aber trotzdem Datendienstdokumente von einer SharePoint-Website erstellen und verwalten möchten, können Sie den Inhaltstyp für Datendienstdokumente für eine beliebige Bibliothek manuell hinzufügen und konfigurieren, die Sie zum Freigeben von Datendienstdokumenten (ATOMSVC-Dateien) verwenden möchten.  
  
 Sie müssen mindestens über die Listenverwaltungsberechtigung verfügen, um einen Inhaltstyp hinzuzufügen und zu konfigurieren. Diese Berechtigung ist in die Berechtigungsebene "Entwerfen" und höher integriert.  
  
 Die folgenden Schritte müssen für jede Bibliothek wiederholt werden, in der Sie Dokumente für die Datenfeedregistrierung erstellen oder bearbeiten möchten.  
  
#### Schritt 1: Aktivieren der Inhaltstypverwaltung  
  
1.  Öffnen Sie die Dokumentbibliothek, für die Sie mehrere Inhaltstypen aktivieren möchten.  
  
2.  Klicken Sie im SharePoint-Menüband in den Bibliothekstools auf **Bibliothek**.  
  
3.  Klicken Sie auf **Einstellungen**.  
  
4.  Klicken Sie auf **Bibliothekeinstellungen**.  
  
5.  Klicken Sie unter Allgemeine Einstellungen auf **Erweiterte Einstellungen**.  
  
6.  Klicken Sie unter Inhaltstypen im Abschnitt Verwaltung von Inhaltstypen zulassen? auf **Ja**.  
  
7.  Klicken Sie auf **OK**.  
  
#### Schritt 2: Fügen Sie einen Inhaltstyp für Datendienstdokumente hinzu  
  
1.  Klicken Sie im Abschnitt Inhaltstypen auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**. Falls diese Seite nicht angezeigt wird, wechseln Sie zurück zur Website und klicken unter Bibliothekstools auf **Bibliothek** und dann auf **Bibliothekseinstellungen**.  
  
2.  Klicken Sie unter Inhaltstypen auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**.  
  
3.  Wählen Sie unter Websiteinhaltstypen auswählen aus: die Option **Business Intelligence**aus.  
  
4.  Klicken Sie in der Liste der verfügbaren Websiteinhaltstypen auf **Datendienstdokumente**und dann auf **Hinzufügen** , um den ausgewählten Inhaltstyp in die Liste der hinzuzufügenden Inhaltstypen zu verschieben.  
  
5.  Klicken Sie auf **OK**.  
  
#### Schritt 3: Überprüfen der Datendienstdokumentkonfiguration  
  
1.  Öffnen Sie die Homepage der Website.  
  
2.  Öffnen Sie die Bibliothek.  
  
3.  Klicken Sie im SharePoint-Menüband auf **Dokumente**.  
  
4.  Klicken Sie auf den Pfeil nach unten in Neues Dokument, und wählen Sie **Datendienstdokument**aus. Die Seite Neues Datendienstdokument sollte angezeigt werden.  
  
## Siehe auch  
 [Verwenden von Datenfeeds &#40;Power Pivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)   
 [Löschen einer Power Pivot-Datenfeedbibliothek](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)   
 [PowerPivot-Serververwaltung und -konfiguration in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Power Pivot-Datenfeeds](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  