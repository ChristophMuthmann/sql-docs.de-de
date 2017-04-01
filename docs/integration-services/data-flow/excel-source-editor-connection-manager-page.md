---
title: "Quellen-Editor f&#252;r Excel (Seite Verbindungs-Manager) | Microsoft Docs"
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
  - "sql13.dts.designer.excelsourceadapter.connection.f1"
helpviewer_keywords: 
  - "Quellen-Editor für Excel"
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Quellen-Editor f&#252;r Excel (Seite Verbindungs-Manager)
  Mithilfe des Knotens **Verbindungs-Manager** im Dialogfeld **Quellen-Editor für Excel** können Sie eine [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsmappe für die Quelle auswählen. Die Excel-Quelle liest Daten aus einem Arbeitsblatt oder dem benannten Bereich einer vorhandenen Arbeitsmappe.  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft der Excel-Quelle ist nicht im **Quellen-Editor für Excel**verfügbar, kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt Excel-Quelle von [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
 Weitere Informationen zur Excel-Quelle finden Sie unter [Excel Source](../../integration-services/data-flow/excel-source.md).  
  
## Statische Optionen  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Excel-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Excel-Verbindungs-Manager** einen neuen Verbindungs-Manager.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Wert|Description|  
|-----------|-----------------|  
|Tabelle oder Sicht|Ruft Daten aus einem Arbeitsblatt oder dem benannten Bereich einer Excel-Datei ab.|  
|Variable für Tabellenname oder Sichtname|Geben Sie den Namen des Arbeitsblatts oder Bereichs in einer Variablen an.<br /><br /> **Relevante Informationen:** [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md)|  
|SQL-Befehl|Ruft mithilfe einer SQL-Abfrage Daten aus einer Excel-Datei ab. Informationen zur Abfragesyntax finden Sie unter [Excel Source](../../integration-services/data-flow/excel-source.md).|  
|SQL-Befehl aus Variable|Gibt den SQL-Abfragetext in einer Variablen an.|  
  
 **Vorschau**  
 Zeigt mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
## Dynamische Optionen (Datenzugriffsmodus)  
  
### Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Excel-Tabelle**  
 Wählen Sie in der Liste der in der Excel-Arbeitsmappe verfügbaren Objekte den Namen des Arbeitsblatts oder des benannten Bereichs aus.  
  
### Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen des Arbeitsblatts oder des benannten Bereichs enthält.  
  
### Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text der SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen** klicken. Wahlweise können Sie auch nach der Datei mit dem Abfragetext suchen, indem Sie auf **Durchsuchen** klicken.  
  
 **Parameter**  
 Wenn Sie eine parametrisierte Abfrage eingeben und im Abfragetext ? als Parameterplatzhalter verwenden, können Sie den Paketvariablen mithilfe des Dialogfelds **Abfrageparameter festlegen** Abfrageeingabeparameter zuordnen.  
  
 **Abfrage erstellen**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
### Datenzugriffsmodus = SQL-Befehl aus Variable  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Text für die SQL-Abfrage enthält.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Quellen-Editor für Excel &#40;Seite Spalten&#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Quellen-Editor für Excel &#40;Seite Fehlerausgabe&#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Excel-Verbindungs-Manager](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Schleife durch Excel-Dateien und Tabellen mit einem Foreach-Schleifencontainer](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  