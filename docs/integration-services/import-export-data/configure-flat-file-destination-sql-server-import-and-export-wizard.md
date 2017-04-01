---
title: "Flatfileziel konfigurieren (SQL Server-Import/Export-Assistent) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.configureflatfiledest.f1"
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Flatfileziel konfigurieren (SQL Server-Import/Export-Assistent)
  Wenn Sie ein Flatfileziel ausgewählt haben, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent **Flatfileziel konfigurieren** an, nachdem Sie eine Tabelle zum Kopieren angegeben oder eine Abfrage bereitgestellt haben. Auf dieser Seite geben Sie Formatierungsoptionen für das Flatfileziel an. Optional können Sie die Zuordnung einzelner Spalten überprüfen und eine Vorschau von Beispieldaten anzeigen.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Screenshot der Seite „Flatfileziel konfigurieren“  
 Der folgende Screenshot zeigt die Seite **Flatfileziel konfigurieren** des Assistenten an.
 
 In diesem Beispiel möchte der Benutzer eine typische CSV-Datei (comma-separated values, durch Trennzeichen getrennte Werte) erstellen, d.h. jede Datenzeile in der Ausgabe mit einem Wagenrücklauf in Kombination mit einem Zeilenvorschub abschließen und Datenspalten innerhalb jeder Zeile mit einem Komma trennen.

 ![Configure flat file page of the Import and Export Wizard](../../integration-services/import-export-data/media/flat-file.png "Configure flat file page of the Import and Export Wizard")  
  
## <a name="pick-a-source-table"></a>Wählen Sie eine Quelltabelle aus. 
 **Quelltabelle oder -sicht**  
 Wählen Sie die Quelltabelle oder -sicht aus.  

## <a name="specify-the-row-and-column-delimiters"></a>Angeben der Zeilen- und Spaltentrennzeichen
 **Zeilentrennzeichen**  
 Wählen Sie ein Trennzeichen für Zeilen aus der Liste aus. Es gibt keine Option zum Angeben eines benutzerdefinierten Zeilentrennzeichens.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Trennen von Zeilen mit einem Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Trennen von Zeilen mit einem Wagenrücklauf.|  
|**{LF}**|Trennen von Zeilen mit einem Zeilenvorschub.|  
|**Semikolon {;}**|Trennen von Zeilen mit einem Semikolon.|  
|**Doppelpunkt {:}**|Trennen von Zeilen mit einem Doppelpunkt.|  
|**Komma {,}**|Trennen von Zeilen mit einem Komma.|  
|**Tabulator {t}**|Trennen von Zeilen mit einem Tabstoppzeichen.|  
|**Senkrechter Strich {&#124;}**|Trennen von Zeilen mit einem senkrechten Strich.|  
  
 **Spaltentrennzeichen**  
 Wählen Sie ein Trennzeichen für Spalten aus der Liste aus. Es gibt keine Option zum Angeben eines benutzerdefinierten Spaltentrennzeichens.  
  
|Wert|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Trennen von Spalten mit einem Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Trennen von Spalten mit einem Wagenrücklauf.|  
|**{LF}**|Trennen von Spalten mit einem Zeilenvorschub.|  
|**Semikolon {;}**|Trennen von Spalten mit einem Semikolon.|  
|**Doppelpunkt {:}**|Trennen von Spalten mit einem Doppelpunkt.|  
|**Komma {,}**|Trennen von Spalten mit einem Komma.|  
|**Tabulator {t}**|Trennen von Spalten mit einem Tabstoppzeichen.|  
|**Senkrechter Strich {&#124;}**|Trennen von Spalten mit einem senkrechten Strich.|  

## <a name="optionally-edit-column-mappings-and-preview-sample-data"></a>Optionales Bearbeiten der Spaltenzuordnungen und Anzeigen einer Vorschau mit Beispieldaten

**Zuordnungen bearbeiten**   
Klicken Sie optional auf **Zuordnungen bearbeiten**, um das Dialogfeld **Spaltenzuordnungen** für die ausgewählte Tabelle anzuzeigen. Verwenden Sie das Dialogfeld **Spaltenzuordnungen**, um Folgendes auszuführen.
-   Überprüfen Sie die Zuordnung einzelner Spalten zwischen der Quelle und dem Ziel.
-   Wenn Sie nur eine Teilmenge von Spalten kopieren möchten, wählen Sie **ignore** für Spalten aus, die Sie nicht kopieren möchten.

Weitere Informationen finden Sie unter [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vorschau**  
Klicken Sie optional auf **Vorschau**, um bis zu 200 Zeilen mit Beispieldaten im Dialogfeld **Datenvorschau** anzuzeigen. Dadurch können Sie sicherstellen, dass der Assistent die Daten kopieren wird, die Sie kopieren möchten. Weitere Informationen finden Sie unter [Datenvorschau](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Nachdem Sie die Daten in der Vorschau anzeigen, sollten Sie die Optionen ändern, die Sie auf den vorherigen Seiten des Assistenten ausgewählt haben. Wechseln Sie zum Vornehmen dieser Änderungen zurück auf die Seite **Flatfileziel konfigurieren**, und klicken Sie anschließend auf **Zurück**, um zu vorherigen Seiten zurückzukehren, auf denen Sie Ihre Auswahl ändern können.  

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie Formatierungsoptionen für die Zielflatfile angegeben haben, ist die nächste Seite **Paket speichern und ausführen**. Auf dieser Seite geben Sie an, ob der Vorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie möglicherweise auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket speichern, das der Assistent erstellt hat, um es anzupassen und später wiederzuverwenden. Weitere Informationen finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
