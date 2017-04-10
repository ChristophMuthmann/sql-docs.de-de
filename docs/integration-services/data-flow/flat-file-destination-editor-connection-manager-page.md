---
title: "Ziel-Editor f&#252;r Flatfiles (Seite Verbindungs-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.flatfiledestadapter.connection.f1"
helpviewer_keywords: 
  - "Ziel-Editor für Flatfiles"
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Ziel-Editor f&#252;r Flatfiles (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für Flatfiles** können Sie die Flatfile-Verbindung für das Ziel auswählen und angeben, ob die vorhandene Zieldatei überschrieben werden soll oder ob die Daten an die vorhandene Datei angehängt werden sollen. Das Flatfileziel schreibt Daten in eine Textdatei. Als Format für diese Textdatei können Trennzeichen, feste Breite, feste Breite mit Zeilentrennzeichen oder rechter Flatterrand gewählt werden.  
  
 Weitere Informationen zum Flatfileziel finden Sie unter [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md).  
  
## enthalten  
 **Verbindungs-Manager für Flatfiles**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus dem Listenfeld aus, oder erstellen Sie durch Klicken auf **Neu** eine neue Verbindung.  
  
 **Neu**  
 Erstellen Sie eine neue Verbindung mithilfe der Dialogfelder **Flatfileformat** und **Verbindungs-Manager-Editor für Flatfiles**.  
  
 Neben den standardmäßigen Flatfileformaten mit Trennzeichen, fester Breite oder rechtem Flatterrand verfügt das Dialogfeld **Flatfileformat** über eine vierte Option, **Feste Breite mit Zeilentrennzeichen**. Diese Option stellt einen Sonderfall des Formats mit rechtem Flatterrand dar, bei dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Pseudospalte als letzte Datenspalte hinzufügt. Diese Pseudospalte stellt sicher, dass die letzte Spalte über eine feste Breite verfügt.  
  
 Die Option **Feste Breite mit Zeilentrennzeichen** ist im **Verbindungs-Manager-Editor für Flatfiles**nicht verfügbar. Sofern erforderlich, können Sie diese Option im Editor emulieren. Um diese Option zu emulieren, wählen Sie im **Verbindungs-Manager-Editor für Flatfiles** auf der Seite **Allgemein**für **Format**die Option **Rechter Flatterrand**aus. Fügen Sie dann im Editor auf der Seite **Erweitert** eine neue Pseudospalte als letzte Datenspalte hinzu.  
  
 **Daten in der Datei überschreiben**  
 Gibt an, ob eine vorhandene Datei überschrieben, oder ob Daten angehängt werden sollen.  
  
 **Header**  
 Geben Sie einen in die Datei einzufügenden Textblock ein, bevor Daten geschrieben werden. Mithilfe dieser Option können Sie zusätzliche Informationen wie Spaltenüberschriften hinzufügen.  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Ziel-Editor für Flatfiles &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
  