---
title: "Verwalten der Codeformatierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Festlegen von Einzügen für Code [SQL Server]"
  - "Anzeigen von URLs"
  - "Codeformatierung [SQL Server Management Studio]"
  - "Reduzieren von Text"
  - "Formate [SQL Server], Codeformatierung in SQL Server Management Studio"
  - "Ausblenden von Text"
  - "Formate [SQL Server]"
  - "Text [SQL Server], Codeformate"
  - "Automatischer Einzug"
  - "Konvertieren von Text in Kleinbuchstaben"
  - "Abfrage-Editor [SQL Server Management Studio], Verwalten von Codeformaten"
  - "In Code angezeigte URL [SQL Server Management Studio]"
  - "Konvertieren von Text in Großbuchstaben"
  - "Text [SQL Server]"
  - "Aufheben des Einzugs für Code"
ms.assetid: ddbac4d2-6bdc-4467-a352-e869ec880eed
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Verwalten der Codeformatierung
  Mit dem Editor können Sie Code formatieren, z. B. mit Einzug, ausgeblendetem Text, URLs usw. Außerdem können Sie mit dem intelligenten Einzug den Code automatisch bei der Eingabe formatieren.  
  
## Einzug  
 Für den Texteinzug stehen drei verschiedene Stile zur Auswahl. Außerdem können Sie angeben, aus wie vielen Leerzeichen ein Einzug oder Tabstopp besteht und ob der Editor für den Einzug Tabulatoren oder Leerzeichen verwenden soll.  
  
#### So wählen Sie einen Einzugsstil aus  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Klicken Sie auf den Ordner, und wählen Sie die Option **Alle Sprachen** aus, um den Einzug für alle Sprachen festzulegen.  
  
4.  Klicken Sie auf **Tabstopps**.  
  
5.  Klicken Sie auf eine der folgenden Optionen:  
  
    -   **Keiner**. Der Cursor wechselt zum Anfang der nächsten Zeile.  
  
    -   **Block**. Der Cursor richtet die nächste Zeile an der vorherigen Zeile aus.  
  
    -   **Intelligent** (Standard). Der Sprachdienst bestimmt den passenden Einzugsstil.  
  
    > [!NOTE]  
    >  Für einige Sprachen sind nicht alle drei Einzugsoptionen verfügbar.  
  
#### So ändern Sie die Einstellungen für Tabulatoreinzug  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Wählen Sie den Ordner für **Alle Sprachen** aus, um den Einzug für alle Sprachen festzulegen.  
  
4.  Klicken Sie auf **Tabstopps**.  
  
5.  Zum Angeben von Tabulatorzeichen beim Verwenden von Tabstopps und Einzügen klicken Sie auf **Tabulatoren beibehalten**. Zum Angeben von Leerzeichen wählen Sie die Option **Leerzeichen einfügen**aus.  
  
     Wenn Sie **Leerzeichen einfügen**auswählen, geben Sie die Anzahl der Leerzeichen für die einzelnen Tabstopps oder Einzüge unter **Tabulatorgröße** bzw. **Einzugsgröße**an.  
  
#### So ziehen Sie Code ein  
  
1.  Wählen Sie den Text aus, den Sie einziehen möchten.  
  
2.  Drücken Sie die TAB-TASTE, oder klicken Sie auf der Standardsymbolleiste auf die Schaltfläche **Einzug** .  
  
#### So heben Sie den Einzug für Code auf  
  
1.  Wählen Sie den Text aus, für den Sie den Einzug aufheben möchten.  
  
2.  Drücken Sie UMSCHALT+TAB, oder klicken Sie auf der Standardsymbolleiste auf die Schaltfläche **Einzug aufheben**.  
  
#### So ziehen Sie den gesamten Code automatisch ein  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Klicken Sie auf **Alle Sprachen**.  
  
4.  Klicken Sie auf **Tabstopps**.  
  
5.  Klicken Sie auf **Intelligent**.  
  
> [!NOTE]  
>  Die Option **Intelligent** ist für einige Sprachen nicht verfügbar.  
  
#### So konvertieren Sie Leerzeichen in Tabstopps  
  
1.  Wählen Sie den Text aus, dessen Leerzeichen in Tabstopps konvertiert werden sollen.  
  
2.  Zeigen Sie im Menü **Bearbeiten** auf **Erweitert**, und klicken Sie dann auf **Auswahl mit Tabstopps versehen**.  
  
#### So konvertieren Sie Tabstopps in Leerzeichen  
  
1.  Wählen Sie den Text aus, dessen Tabstopps in Leerzeichen konvertiert werden sollen.  
  
2.  Zeigen Sie im Menü **Bearbeiten** auf **Erweitert**, und klicken Sie dann auf **Tabstopps aus Auswahl entfernen**.  
  
 Das Verhalten dieser Befehle hängt von den Tabulatoreinstellungen im Dialogfeld **Optionen** ab. Wenn die Tabulatoreinstellung z. B. 4 lautet, wird durch den Befehl **Auswahl mit Tabstopps versehen** für jeweils vier aufeinander folgende Leerzeichen ein Tabstopp erstellt. Entsprechend werden durch den Befehl **Tabstopps aus Auswahl entfernen** für jeden Tabstopp vier Leerzeichen erstellt.  
  
## Konvertieren von Text in Groß- und Kleinschreibung  
 Sie können Text mit den entsprechenden Befehlen vollständig in Groß- oder Kleinbuchstaben konvertieren.  
  
#### So wandeln Sie Text in Groß- oder Kleinbuchstaben um  
  
1.  Wählen Sie den Text aus, den Sie konvertieren möchten.  
  
2.  Zum Konvertieren von Text in Großbuchstaben drücken Sie STRG+UMSCHALT+U, oder klicken Sie im Menü **Bearbeiten** im Untermenü **Erweitert** auf **In Großbuchstaben umwandeln**.  
  
3.  Zum Konvertieren von Text in Kleinbuchstaben drücken Sie STRG+UMSCHALT+L, oder klicken Sie im Menü **Bearbeiten** im Untermenü **Erweitert** auf **In Kleinbuchstaben umwandeln**.  
  
> [!NOTE]  
>  Eine vollständige Liste der Tastenkombinationen finden Sie unter [Tastenkombinationen für SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md).  
  
## Anzeigen von und Verknüpfen mit URLs  
 Sie können im Code klickbare URLs erstellen und anzeigen. Standardmäßig haben die URLs folgende Eigenschaften:    
  
-   Sie sind unterstrichen.  
  
-   Der Mauszeiger nimmt die Form einer Hand an, wenn Sie ihn über eine URL bewegen.  
  
-   Wenn die URL gültig ist, wird sie geöffnet, wenn Sie darauf klicken.  
  
#### So zeigen Sie eine klickbare URL an  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Klicken Sie auf **Text-Editor**.  
  
3.  Zum Ändern der Option für nur eine Sprache klicken Sie auf den entsprechenden Sprachordner, und klicken Sie dann auf **Allgemein**. Zum Ändern der Option für alle Sprachen klicken Sie auf **Alle Sprachen** , und klicken Sie dann auf **Allgemein**.  
  
4.  Wählen Sie die Option **Einfaches Klicken für URLs aktivieren** aus.  
  
  