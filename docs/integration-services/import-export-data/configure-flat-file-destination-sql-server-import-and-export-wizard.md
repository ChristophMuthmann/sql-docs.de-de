---
title: Flatfileziel konfigurieren (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
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
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a9384b498ea78369278261a3334504e5d1b29b58
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Flatfileziel konfigurieren (SQL Server-Import/Export-Assistent)
  Wenn Sie ein Flatfile-Ziel ausgewählt haben, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent **Flatfileziel konfigurieren** an, nachdem Sie angegeben haben, dass Sie eine Tabelle kopieren möchten, oder nachdem Sie eine Abfrage bereitgestellt haben. Auf dieser Seite geben Sie Formatierungsoptionen für das Flatfileziel an. Optional können Sie die Zuordnung einzelner Spalten überprüfen und eine Vorschau von Beispieldaten anzeigen.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Screenshot der Seite „Flatfileziel konfigurieren“  
 Der folgende Screenshot zeigt ein Beispiel für die Seite **Flatfileziel konfigurieren** des Assistenten an.
 
 In diesem Beispiel hat der Benutzer die folgenden Optionen zum Erstellen einer typischen CSV-Datei (mit kommagetrennten Werten) angegeben.
-   **Zeilentrennzeichen**. Jede Datenzeile in der Ausgabe endet mit einer Wagenrücklauf-Zeilenvorschub-Kombination.
-   **Spaltentrennzeichen**. Die Datenspalten in jeder Zeile sind durch Kommas getrennt.

 ![Konfigurieren einer Flatfileseite des Import/Export-Assistenten](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>Auswählen einer Quelltabelle
 **Quelltabelle oder -sicht**  
-   Wenn Sie auf einer vorherigen Seite angegeben haben, dass Sie eine Tabelle kopieren möchten, wählen Sie die Quelltabelle oder -sicht aus der Dropdownliste.
-   Wenn Sie eine Abfrage bereitgestellt haben, ist `"Query"` als einzige Option ausgewählt.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>Festlegen von Zeilen- und Spaltentrennzeichen für die Ausgabe
 **Zeilentrennzeichen**  
 Wählen Sie aus der Liste das Trennzeichen zum Trennen von Zeilen in der Ausgabe aus. Es gibt keine Option zum Angeben eines *benutzerdefinierten* Zeilentrennzeichens.  
  
|value|Description|  
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
 Wählen Sie aus der Liste das Trennzeichen zum Trennen von Spalten in der Ausgabe aus. Es gibt keine Option zum Angeben eines *benutzerdefinierten* Spaltentrennzeichens.  
  
|value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Trennen von Spalten mit einem Wagenrücklauf in Kombination mit einem Zeilenvorschub.|  
|**{CR}**|Trennen von Spalten mit einem Wagenrücklauf.|  
|**{LF}**|Trennen von Spalten mit einem Zeilenvorschub.|  
|**Semikolon {;}**|Trennen von Spalten mit einem Semikolon.|  
|**Doppelpunkt {:}**|Trennen von Spalten mit einem Doppelpunkt.|  
|**Komma {,}**|Trennen von Spalten mit einem Komma.|  
|**Tabulator {t}**|Trennen von Spalten mit einem Tabstoppzeichen.|  
|**Senkrechter Strich {&#124;}**|Trennen von Spalten mit einem senkrechten Strich.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Optionales Überprüfen der Spaltenzuordnungen und Anzeigen der Datenvorschau

**Zuordnungen bearbeiten**   
Klicken Sie optional auf **Zuordnungen bearbeiten**, um das Dialogfeld **Spaltenzuordnungen** für die ausgewählte Tabelle anzuzeigen. Verwenden Sie das Dialogfeld **Spaltenzuordnungen** , um Folgendes auszuführen.
-   Überprüfen Sie die Zuordnung einzelner Spalten zwischen der Quelle und dem Ziel.
-   Wenn Sie nur eine Teilmenge von Spalten kopieren möchten, wählen Sie **ignore** für Spalten aus, die Sie nicht kopieren möchten.

Weitere Informationen finden Sie unter [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vorschau**  
Klicken Sie optional auf **Vorschau**, um bis zu 200 Zeilen mit Beispieldaten im Dialogfeld **Datenvorschau** anzuzeigen. Dadurch können Sie sicherstellen, dass der Assistent die Daten kopieren wird, die Sie kopieren möchten. Weitere Informationen finden Sie unter [Datenvorschau](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Nachdem Sie die Daten in der Vorschau anzeigen, sollten Sie die Optionen ändern, die Sie auf den vorherigen Seiten des Assistenten ausgewählt haben. Wechseln Sie zum Vornehmen dieser Änderungen zurück auf die Seite **Flatfileziel konfigurieren** , und klicken Sie anschließend auf **Zurück** , um zu vorherigen Seiten zurückzukehren, auf denen Sie Ihre Auswahl ändern können.  

## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie Formatierungsoptionen für die Zielflatfile angegeben haben, ist die nächste Seite **Paket speichern und ausführen**. Auf dieser Seite geben Sie an, ob der Vorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie Ihre Einstellungen möglicherweise auch als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket speichern, um es anzupassen und später wiederzuverwenden. Weitere Informationen finden Sie unter [Paket speichern und ausführen](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  

