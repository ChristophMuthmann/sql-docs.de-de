---
title: Excel-Ziel | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 794d9041bc3057d2737c88e2815d98a9d441beb3
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="excel-destination"></a>Excel-Ziel
  Das Excel-Ziel lädt Daten in Arbeitsblätter oder Bereiche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Arbeitsmappen.  

> [!IMPORTANT]
> Ausführliche Informationen über das Herstellen einer Verbindung mit Excel-Dateien sowie Einschränkungen und bekannte Probleme beim Laden von Daten aus oder in Excel-Dateien finden Sie unter [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md).
  
## <a name="access-modes"></a>Zugriffsmodi  
 Das Excel-Ziel stellt drei verschiedene Datenzugriffsmodi zum Laden von Daten bereit:  
  
-   Eine Tabelle oder Sicht.  
  
-   Eine in einer Variablen angegebene Tabelle oder Sicht.  
  
-   Die Ergebnisse einer SQL-Anweisung. Bei der Abfrage kann es sich um eine parametrisierte Abfrage handeln.  
  
## <a name="configure-the-excel-destination"></a>Konfigurieren des Excel-Ziels  
 Das Excel-Ziel verwendet einen Excel-Verbindungs-Manager zum Herstellen einer Verbindung mit einer Datenquelle. Dieser Verbindungs-Manager gibt die zu verwendende Arbeitsmappendatei an. Weitere Informationen finden Sie unter [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 Das Excel-Ziel weist eine reguläre Eingabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält alle Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Weitere Informationen zum Festlegen der Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Ziel-Editor für Excel (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für Excel** können Sie Informationen zur Datenquelle angeben und eine Vorschau der Ergebnisse anzeigen. Das Excel-Ziel lädt Daten in ein Arbeitsblatt oder einen benannten Bereich einer [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsmappe.  
  
> [!NOTE]  
>  Die **CommandTimeout** -Eigenschaft des Excel-Ziels ist nicht im **Ziel-Editor für Excel**verfügbar, kann jedoch mit dem Dialogfeld **Erweiterter Editor**festgelegt werden. Darüber hinaus sind bestimmte Optionen für schnelles Laden nur im Dialogfeld **Erweiterter Editor**verfügbar. Weitere Informationen zu diesen Eigenschaften finden Sie im Abschnitt Excel-Ziel von [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Statische Optionen  
 **Excel-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Excel-Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Excel-Verbindungs-Manager** eine neue Verbindung.  
  
 **Datenzugriffsmodus**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Description|  
|------------|-----------------|  
|Tabelle oder Sicht|Lädt Daten aus einem Arbeitsblatt oder dem benannten Bereich einer Excel-Datenquelle.|  
|Variable für Tabellenname oder Sichtname|Geben Sie den Namen des Arbeitsblatts oder Bereichs in einer Variablen an.<br /><br /> **Verwandte Informationen:** [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL-Befehl|Lädt Daten mithilfe einer SQL-Abfrage in das Excel-Ziel.|  
  
 **Name der Excel-Tabelle**  
 Wählen Sie in der Dropdownliste das Excel-Ziel aus. Wenn die Liste leer ist, klicken Sie auf **Neu**.  
  
 **Neu**  
 Klicken Sie auf **Neu** , um das Dialogfeld **Tabelle erstellen** zu öffnen. Wenn Sie auf **OK**klicken, erstellt das Dialogfeld die Excel-Datei, auf die der **Excel-Verbindungs-Manager** zeigt.  
  
 **Vorhandene Daten anzeigen**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
### <a name="data-access-mode-dynamic-options"></a>Dynamische Optionen (Datenzugriffsmodus)  
  
#### <a name="data-access-mode--table-or-view"></a>Datenzugriffsmodus = Tabelle oder Sicht  
 **Name der Excel-Tabelle**  
 Wählen Sie in der Liste der in der Datenquelle verfügbaren Objekte den Namen des Arbeitsblatts oder des benannten Bereichs aus.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Datenzugriffsmodus = Variable für Tabellenname oder Sichtname  
 **Variablenname**  
 Wählen Sie die Variable aus, die den Namen des Arbeitsblatts oder des benannten Bereichs enthält.  
  
#### <a name="data-access-mode--sql-command"></a>Datenzugriffsmodus = SQL-Befehl  
 **SQL-Befehlstext**  
 Geben Sie den Text einer SQL-Abfrage ein, und erstellen Sie die Abfrage, indem Sie auf **Abfrage erstellen**klicken. Wahlweise können Sie auch nach der Datei suchen, die den Abfragetext enthält, indem Sie auf **Durchsuchen**klicken.  
  
 **Abfrage erstellen**  
 Mithilfe des Dialogfelds **Abfrage-Generator** können Sie die SQL-Abfrage visuell erstellen.  
  
 **Durchsuchen**  
 Mithilfe des Dialogfelds **Öffnen** können Sie nach der Datei suchen, die den Text der SQL-Abfrage enthält.  
  
 **Abfrage analysieren**  
 Überprüft die Syntax des Abfragetexts.  
  
## <a name="excel-destination-editor-mappings-page"></a>Ziel-Editor für Excel (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** des Dialogfelds **Ziel-Editor für Excel** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
### <a name="options"></a>Tastatur  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten in der Tabelle Zielspalten zuordnen.  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Zielspalten in der Tabelle Eingabespalten zuordnen.  
  
 **Eingabespalte**  
 Zeigen Sie die in obiger Tabelle ausgewählten Eingabespalten an. Die Zuordnungen können Sie mithilfe der Liste **Verfügbare Eingabespalten**ändern.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, und ob sie zugeordnet sind.  
  
## <a name="excel-destination-editor-error-output-page"></a>Ziel-Editor für Excel (Seite Fehlerausgabe)
  Auf der Seite **Erweitert** in **Ziel-Editor für Excel** können Sie die Optionen für die Fehlerbehandlung angeben.  
  
### <a name="options"></a>Tastatur  
 **Eingabe oder Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für Excel** im Knoten **Verbindungs-Manager**ausgewählt wurden.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Gibt an, was im Falle einer Kürzung geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Beschreibung**  
 Zeigt die Beschreibung des Fehlers an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Load data from or to Excel with SQL Server Integration Services (SSIS) (Laden von Daten aus oder in Excel mit SQL Server Integration Services (SSIS))](../load-data-to-from-excel-with-ssis.md)  
 [Excel-Quelle](../../integration-services/data-flow/excel-source.md)   
[Excel-Verbindungs-Manager](../connection-manager/excel-connection-manager.md)