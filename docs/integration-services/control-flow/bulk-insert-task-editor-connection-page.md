---
title: "Masseneinf&#252;gungstask-Editor (Seite Verbindung) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.bulkinserttask.connection.f1"
helpviewer_keywords: 
  - "Masseneinfügungstask-Editor"
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Masseneinf&#252;gungstask-Editor (Seite Verbindung)
  Mithilfe der Seite **Verbindung** im Dialogfeld **Masseneinfügungstask-Editor** können Sie die Quelle und das Ziel des Masseneinfügevorgangs und das zu verwendende Format angeben.  
  
 Informationen zum Arbeiten mit Masseneinfügungen finden Sie unter [Masseneinfügungstask](../../integration-services/control-flow/bulk-insert-task.md) und [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## enthalten  
 **Verbindung**  
 Wählen Sie einen OLE DB-Verbindungs-Manager in der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um eine neue Verbindung zu erstellen.  
  
 **Verwandte Themen:** [OLE DB-Verbindungs-Manager](../../integration-services/connection-manager/ole-db-connection-manager.md), [OLE DB-Verbindungs-Manager konfigurieren](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 **DestinationTable**  
 Geben Sie den Namen der Zieltabelle oder Zielsicht ein, oder wählen Sie aus der Liste eine Tabelle oder Sicht aus.  
  
 **Format**  
 Wählen Sie die Quelle des Formats für die Masseneinfügung aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Use File**|Wählen Sie eine Datei mit Formatspezifikationen aus. Nach Auswahl dieser Option wird die dynamische Option **FormatFile**angezeigt.|  
|**Specify**|Geben Sie das Format an. Nach Auswahl dieser Option werden die dynamischen Optionen **RowDelimiter** und **ColumnDelimiter**angezeigt.|  
  
 **File**  
 Wählen Sie einen Datei- oder Flatfileverbindungs-Manager in der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um eine neue Verbindung zu erstellen.  
  
 Der Speicherort ist relativ zum SQL Server-Datenbankmodul, das im Verbindungs-Manager für diesen Task angegeben wurde. Das SQL Server-Datenbankmodul muss auf die Textdatei zugreifen können, und zwar entweder auf einer lokalen Festplatte des Servers oder über eine Freigabe oder einem SQL Server zugeordneten Laufwerk. Auf die Datei wird nicht von der SSIS-Laufzeit zugegriffen.  
  
 Wenn Sie auf die Quelldatei mithilfe eines Flatfileverbindungs-Managers zugreifen, verwendet der Masseneinfügungstask nicht das im Flatfileverbindungs-Manager angegebene Format. Stattdessen verwendet der Masseneinfügungstask entweder das in einer Formatdatei angegebene Format oder die Werte der Eigenschaften RowDelimiter und ColumnDelimiter des Tasks.  
  
 **Verwandte Themen:** [Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md), [Dateiverbindungs-Manager-Editor](../../integration-services/connection-manager/file-connection-manager-editor.md), [Verbindungs-Manager für Flatfiles](../../integration-services/connection-manager/flat-file-connection-manager.md), [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Allgemein“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md), [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Spalten“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md), [Verbindungs-Manager-Editor für Flatfiles &#40;Seite „Erweitert“&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)  
  
 **Tabellen aktualisieren**  
 Aktualisieren Sie die Liste der Tabellen und Sichten.  
  
## Format (dynamische Optionen)  
  
### Format = Use File  
 **FormatFile**  
 Geben Sie den Pfad der Formatdatei ein, oder klicken Sie auf die Schaltfläche mit den drei Punkten (**…**), um nach der Formatdatei zu suchen.  
  
### Format = Specify  
 **RowDelimiter**  
 Geben Sie das Zeilentrennzeichen in der Quelldatei an. Der Standardwert ist **{CR}{LF}**.  
  
 **ColumnDelimiter**  
 Geben Sie das Spaltentrennzeichen in der Quelldatei an. Der Standardwert ist **Tabstopp**.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Masseneinfügungstask-Editor &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)   
 [Masseneinfügungstask-Editor &#40;Seite „Optionen“&#41;](../../integration-services/control-flow/bulk-insert-task-editor-options-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  