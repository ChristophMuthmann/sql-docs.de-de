---
title: "Datentypzuordnung überprüfen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.reviewissues.f1
ms.assetid: 0625c4f9-b8ff-4593-b884-39398b9d43af
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f73734f20bcda435f099066852d84101192fb212
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="review-data-type-mapping-sql-server-import-and-export-wizard"></a>Datentypzuordnung überprüfen (SQL Server-Import/Export-Assistent)
Wenn Sie eine Datentypzuordnung festgelegt haben, die nicht erfolgreich in die **Zuordnungungsliste** im Dialogfeld **Spaltenzuordnungen** übernommen werden konnte, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent die Seite **Datentypzuordnung überprüfen** an. Überprüfen Sie auf dieser Seite die detaillierten Informationen über Datentypkonvertierungen, die der Assistent ausführen muss, damit die Quelldaten mit den Zieldaten kompatibel sind. Diese Informationen enthalten visuelle Hinweise, um Datentypkonvertierungen, die voraussichtlich fehlerfrei ablaufen, von Konvertierungen zu unterscheiden, die zu Fehlern oder Kürzungen führen könnten. Sie entscheiden für jede Konvertierung, ob Sie die vom Assistenten vorgeschlagene Konvertierung übernehmen möchten. Außerdem geben Sie an, wie mit möglicherweise auftretenden Fehlern verfahren werden soll.   
  
> [!TIP]
> Sie können auf der Seite **Datentypzuordnung überprüfen** keine Datentypzuordnungen ändern. Sie können jedoch auf **Zurück** klicken, um zurück auf die Seite **Quelltabellen und -sichten auswählen** zu gelangen. Klicken Sie anschließend auf **Zuordnungen bearbeiten** , um das Dialogfeld **Spaltenzuordnungen** erneut zu öffnen. Im Dialogfeld **Spaltenzuordnungen** können Sie Datentypzuordnungen angeben, die größere Erfolgsaussichten haben. Gehen Sie zu **Spaltenzuordnungen** , um erneut einen Blick auf das Dialogfeld [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)zu werfen.  
  
## <a name="screen-shot-of-the-review-data-type-mapping-page"></a>Screenshot der Seite Datentypzuordnung überprüfen
 Der folgende Screenshot zeigt ein Beispiel für das Dialogfeld **Datentypzuordnung überprüfen** des Assistenten.
 
 In diesem Beispiel:
 -   Der Benutzer hat im Dialogfeld **Spaltenzuordnungen** eine möglicherweise fehlerhafte Zuordnung angegeben.
 -   Das Warnsymbol in der Zeile der Liste **Tabelle** gibt an, dass ein Problem beim Konvertieren von mindestens einer Spalte mit Daten von den Abfrageergebnissen in einen kompatiblen Datentyp in der Zieltabelle aufgetreten ist.
 -   Das Warnsymbol in der ersten Zeile in der Liste **Datentypzuordnung** gibt an, dass die Zuordnung des Datentyps **int** der Quellspalte zum Datentyp **smalldatetime** der Zielspalte möglicherweise zu einem Datenverlust führt.
 
 ![Seite „Datentypzuordnung überprüfen“ des Import/Export-Assistenten](../../integration-services/import-export-data/media/review-mapping.png "Review Data Type Mapping page of the Import and Export Wizard") 
 
## <a name="review-the-source-and-destination-tables"></a>Überprüfen der Quell- und Zielschematabellen  
 Der obere Abschnitt der Seite **Datentypenzuordnung überprüfen** besteht aus der Liste **Tabelle** , in der die Tabellen aufgelistet sind, die aus der Quelle in das Ziel kopiert werden sollen. Wählen Sie eine Tabelle in der Liste **Tabelle** aus, um Konvertierungsinformationen zu einer einzelnen Tabelle zu sehen. Die Konvertierungsinformationen für die einzelnen Spalten der ausgewählten Tabelle werden im Raster **Datentypzuordnung** im unteren Abschnitt der Seite angezeigt.

In diesem Beispiel werden die Ergebnisse der Abfrage, die der Benutzer angegeben hat, in die Tabelle „Sales.CustomerNew2“ am Ziel kopiert. Das Warnsymbol gibt an, dass ein Problem beim Konvertieren von mindestens einer Spalte mit Daten von den Abfrageergebnissen in einen kompatiblen Datentyp in der Zieltabelle aufgetreten ist.

![Review mapping – tables](../../integration-services/import-export-data/media/review-mapping-tables.png)
  
 In der folgenden Tabelle werden die Spalten in der Liste **Tabelle** beschrieben.  
  
|Column|Description|  
|------------|-----------------|  
|(Quellsymbol)|Gibt die Wahrscheinlichkeit des Erfolgs für die Datentypkonvertierungen an:<br /> - Ein **grünes** Häkchen gibt an, dass der Assistent erwartet, dass alle Datentypkonvertierungen für diese Tabelle erfolgreich sind.<br />- Ein **gelbes** Warnsymbol gibt an, dass Sie die einzelnen Konvertierungen überprüfen sollten, die der Assistent ausführt. Um diese Konvertierungen zu prüfen, wählen Sie die Tabelle aus und prüfen dann die Konvertierungen für einzelne Spalten in der Liste **Datentypzuordnung** .<br />- Ein **rotes** Fehlersymbol gibt an, dass der Assistent einige der Konvertierungen für diese Tabelle nicht zuverlässig ausführen kann.|  
|**Quelle**|Der Name der Quelltabelle.|  
|(Zielsymbol)|Gibt an, ob das Ziel bereits vorhanden ist oder vom Assistenten erstellt wird:<br /> - Ein Tabellensymbol gibt an, dass es sich bei dem Ziel um eine vorhandene Tabelle handelt.<br />- Ein Tabellensymbol mit einer Sonne gibt an, dass es sich bei dem Ziel um eine neue Tabelle handelt, die der Assistent erstellt.|  
|**Ziel**|Der Name der Zieltabelle|  
  
## <a name="review-the-data-type-mappings"></a>Überprüfen der Datentypzuordnungen  
 Im mittleren Abschnitt der Seite **Datentypzuordnung überprüfen** befindet sich die Liste **Datentypzuordnung** . Dieses Raster enthält detaillierte Konvertierungsinformationen über die Spalten in der Quelltabelle, die im oberen Bereich der Seite in der Liste **Tabelle** ausgewählt ist.

In diesem Beispiel wird jede Spalte an der Quelle in eine Spalte mit dem gleichen Namen und Datentyp am Ziel kopiert. Das Warnsymbol in der ersten Zeile in der Liste **Datentypzuordnung** gibt an, dass die Zuordnung des Datentyps **int** der Quellspalte zum Datentyp **smalldatetime** der Zielspalte möglicherweise zu einem Datenverlust führt.
 
![Überprüfung der Zuordnung – Zuordnungen](../../integration-services/import-export-data/media/review-mapping-mappings.png)  

In der folgenden Tabelle werden die Spalten in der Liste **Datentypzuordnung** beschrieben. 

|Column|Description|  
|------------|-----------------|  
|(Konvertierungssymbol)|Gibt die Wahrscheinlichkeit des Erfolgs für die Datentypkonvertierungen an:<br /> - Ein **grünes** Häkchen gibt an, dass der Assistent erwartet, dass die Datentypkonvertierung für diese Spalte erfolgreich ist.<br />- Ein **gelbes** Warnsymbol gibt an, dass Sie die Konvertierung überprüfen sollten, die der Assistent ausführt. Doppelklicken Sie auf die Spalte, um das Dialogfeld **Spaltenkonvertierungsdetails** anzuzeigen und die Konvertierung zu überprüfen. Weitere Informationen finden Sie im Dialogfeld [Spaltenkonvertierungsdetails](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).<br />- Ein **rotes** Fehlersymbol gibt an, dass der Assistent die Konvertierung nicht zuverlässig ausführen kann.|  
|**Quellspalte**|Der Name der Quellspalte|  
|**Quelltyp**|Der Datentyp der Quellspalte|  
|**Zielspalte**|Der Name der Zielspalte|  
|**Zieltyp**|Der Datentyp der Zielspalte|  
|**Konvertieren**|Geben Sie an, ob die geplante Konvertierung fortgesetzt werden soll:<br /> - Aktivieren Sie das Kontrollkästchen, damit der Assistent mit der geplanten Konvertierung fortfährt.<br />- Deaktivieren Sie das Kontrollkästchen, um die Datentypkonvertierung abzubrechen.|  
|**On Error**|Geben Sie an, wie der Assistent Fehler behandelt:<br /> - Verwenden Sie die Einstellung **Bei Fehler (global)** , die Sie unten auf dieser Seite angeben können.<br />- Import- oder Exportprozess beim Auftreten eines Fehlers beenden.<br />- Fehler ignorieren.|  
|**Bei Kürzung**|Geben Sie an, wie der Assistent Kürzungen behandelt:<br /> - Verwenden Sie die Einstellung **Bei Kürzung (global)** , die Sie unten auf dieser Seite angeben können.<br />- Import- oder Exportprozess beim Auftreten eines Fehlers beenden.<br />- Kürzung ignorieren.|  

> [!TIP]
> Doppelklicken Sie auf eine beliebige Zeile in der Liste, um detaillierte Informationen über die Konvertierung einer bestimmten Datenspalte zu sehen. Das Dialogfeld **Spaltenkonvertierungsdetails** wird geöffnet und zeigt ausführlichere Konvertierungsinformationen für die Spalte an. Weitere Informationen finden Sie im Dialogfeld [Spaltenkonvertierungsdetails](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md).
 
## <a name="specify-global-error-handling-options"></a>Angeben globaler Fehlerbehandlungsoptionen  
 Im unteren Abschnitt der Seite **Datentypzuordnung überprüfen** können Sie Fehlerbehandlungsoptionen angeben, die standardmäßig für alle Spalten gelten. Diese Einstellungen gelten für alle Konvertierungen, bei denen die Option **Global verwenden** in der Spalte **On Error** (Bei Fehler) oder **Bei abgeschnittenen Daten** der Liste **Datentypzuordnung** aktiviert ist.   

Dieses Beispiel zeigt die Standardwerte für die zwei Optionen zur globalen Fehlerbehandlung.

![Überprüfung der Zuordnung – Zuordnung](../../integration-services/import-export-data/media/review-mapping-errors.png)

 **Bei Fehler (global)**  
 Geben Sie an, wie der Assistent Fehler behandelt:  
 -   Import- oder Exportprozess beim Auftreten eines Fehlers beenden. Dies ist der Standardwert.
 -   Fehler ignorieren und den Import- oder Exportprozess fortsetzen.  
  
 **Bei Kürzung (global)**  
 Geben Sie an, wie der Assistent mit abgeschnittenen Daten umgeht:  
 -   Import- oder Exportprozess beim Auftreten eines Fehlers beenden. Dies ist der Standardwert.
 -   Kürzung ignorieren und den Import- oder Exportprozess fortsetzen.  
   
## <a name="whats-next"></a>Wie geht es weiter?  
 Nachdem Sie die Warnungen überprüft und Konvertierungs- und Fehlerbehandlungsoptionen angegeben haben, leitet Sie die Seite **Datentypzuordnung überprüfen** zurück zum Dialogfeld **Spaltenzuordnungen** . Weitere Informationen finden Sie unter [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Siehe auch
[Zuordnung von Datentypen mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

