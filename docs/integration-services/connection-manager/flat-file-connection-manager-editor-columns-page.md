---
title: "Verbindungs-Manager-Editor f&#252;r Flatfiles (Seite Spalten) | Microsoft Docs"
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
  - "sql13.dts.designer.ffileconnection.columns.f1"
helpviewer_keywords: 
  - "Verbindungs-Manager-Editor für Flatfiles"
ms.assetid: 40ce7537-abd0-4973-97fd-6ccb90fddfa0
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# Verbindungs-Manager-Editor f&#252;r Flatfiles (Seite Spalten)
  Verwenden Sie die Seite **Spalten** im Dialogfeld **Verbindungs-Manager-Editor für Flatfiles** , um die Zeilen- und Spalteninformationen anzugeben und eine Vorschau der Datei anzuzeigen.  
  
 Weitere Informationen zum Verbindungs-Manager für Flatfiles finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
## Statische Optionen  
 **Name des Verbindungs-Managers**  
 Geben Sie einen eindeutigen Namen für die Flatfile-Verbindung im Workflow an. Der angegebene Name wird im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer angezeigt.  
  
 **Description**  
 Beschreiben Sie die Verbindung. Die bewährte Methode ist hierbei, die Verbindung zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
## Flatfileformat (dynamische Optionen)  
  
### Format = Mit Trennzeichen  
 **Zeilentrennzeichen**  
 Wählen Sie aus der Liste verfügbarer Zeilentrennzeichen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Zeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Zeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Zeilen dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Zeilen dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Zeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Zeilen dient ein senkrechter Strich.|  
  
 **Spaltentrennzeichen**  
 Wählen Sie aus der Liste verfügbarer Spaltentrennzeichen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Spalten dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Spalten dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Spalten dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Spalten dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Spalten dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Spalten dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Spalten dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Spalten dient ein senkrechter Strich.|  
  
 **Aktualisieren**  
 Zeigt durch Klicken auf **Aktualisieren** an, welche Auswirkung die Änderung der auszulassenden Trennzeichen hat. Diese Schaltfläche wird erst angezeigt, nachdem Sie andere Verbindungsoptionen geändert haben.  
  
 **Vorschau der Zeilen**  
 Zeigt Beispieldaten in der Flatfile an, die entsprechend den von Ihnen ausgewählten Optionen in Spalten und Zeilen unterteilt sind.  
  
 **Spalten zurücksetzen**  
 Entfernt durch Klicken auf **Spalten zurücksetzen** alle Spalten bis auf die ursprünglichen.  
  
### Format = Feste Breite  
 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale rote Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilenbreite**  
 Geben Sie erst die Länge der Zeile an, bevor Sie einzelnen Spalten Trennzeichen hinzufügen. Sie können auch die vertikale rote Linie im Vorschaufenster verschieben, um das Zeilenende zu kennzeichnen. Der Wert der Zeilenbreite wird automatisch aktualisiert.  
  
 **Spalten zurücksetzen**  
 Entfernt durch Klicken auf **Spalten zurücksetzen** alle Spalten bis auf die ursprünglichen.  
  
### Format = Rechter Flatterrand  
  
> [!NOTE]  
>  Bei Dateien mit rechtem Flatterrand haben die Spalten mit Ausnahme der letzten Spalte eine feste Breite. Die Trennung der letzten Spalte erfolgt mit einem Zeilentrennzeichen.  
  
 **Schriftart**  
 Wählen Sie die Schriftart aus, in der die Vorschaudaten angezeigt werden sollen.  
  
 **Quelldatenspalten**  
 Passen Sie die Zeilenbreite an, indem Sie die vertikale rote Zeilenmarkierungslinie verschieben, und passen Sie die Spaltenbreite an, indem Sie auf das Lineal am oberen Rand des Vorschaufensters klicken.  
  
 **Zeilentrennzeichen**  
 Wählen Sie aus der Liste verfügbarer Zeilentrennzeichen ein Trennzeichen aus, oder geben Sie den Trennzeichentext ein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Als Trennzeichen für Zeilen dient ein Wagenrücklauf.|  
|**{LF}**|Als Trennzeichen für Zeilen dient ein Zeilenvorschub.|  
|**Semikolon {;}**|Als Trennzeichen für Zeilen dient ein Semikolon.|  
|**Doppelpunkt {:}**|Als Trennzeichen für Zeilen dient ein Doppelpunkt.|  
|**Komma {,}**|Als Trennzeichen für Zeilen dient ein Komma.|  
|**Tabulator {t}**|Als Trennzeichen für Zeilen dient ein Tabulator.|  
|**Senkrechter Strich {&#124;}**|Als Trennzeichen für Zeilen dient ein senkrechter Strich.|  
  
 **Spalten zurücksetzen**  
 Entfernt durch Klicken auf **Spalten zurücksetzen** alle Spalten bis auf die ursprünglichen.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)   
 [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Erweitert“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)   
 [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Vorschau“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  