---
title: CDC-Quelle | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.cdcsource.f1
- sql13.ssis.designer.cdcsource.connection.f1
- sql13.ssis.designer.cdcsource.columns.f1
- sql13.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d53ac25527e482ae043adeef1c56e5024cb78eb1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="cdc-source"></a>CDC-Quelle
  Die CDC-Quelle liest einen Bereich mit Änderungsdaten aus [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Änderungstabellen und übermittelt die Änderungen an die anderen SSIS-Downstreamkomponenten.  
  
 Der Bereich mit Änderungsdaten, der von CDC-Quelle gelesen wird, wird als CDC-Verarbeitungsbereich bezeichnet und mithilfe des CDC-Steuerungstasks bestimmt, der vor Beginn des aktuellen Datenflusses ausgeführt wird. Der CDC-Verarbeitungsbereich wird aus dem Wert einer Paketvariablen abgeleitet, die den Status der CDC-Verarbeitung für eine Gruppe von Tabellen verwaltet.  
  
 Die CDC-Quelle extrahiert Daten mithilfe einer Datenbanktabelle, Sicht oder SQL-Anweisung aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank.  
  
 Die CDC-Quelle verwendet die folgenden Konfigurationen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -ADO.NET-Verbindungs-Manager, um auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -CDC-Datenbank zuzugreifen. Weitere Informationen zum Konfigurieren der CDC-Quellverbindung finden Sie unter [Quellen-Editor für CDC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).  
  
-   Für CDC aktivierte Tabelle.  
  
-   Name der Aufzeichnungsinstanz der ausgewählten Tabelle (falls mehr als eine vorhanden ist).  
  
-   Änderungsverarbeitungsmodus  
  
-   Name der CDC-Statuspaketvariablen, auf deren Grundlage der CDC-Verarbeitungsbereich bestimmt wird. Die CDC-Quelle ändert diese Variable nicht.  
  
 Die von der CDC-Quelle zurückgegebenen Daten entsprechen den Daten, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-CDC-Funktionen **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** oder **cdc.fn_cdc_get_net_changes_\<capture-instance-name>** zurückgegeben werden (falls verfügbar). Die einzige optionale Hinzufügung ist die Spalte **__$initial_processing** , in der angegeben wird, ob sich der aktuelle Verarbeitungsbereich mit einem erstmaligen Ladevorgang der Tabelle überschneiden kann. Weitere Informationen zur erstmaligen Verarbeitung finden Sie unter [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 Die CDC-Quelle weist eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Die CDC-Quelle verfügt über eine Fehlerausgabe. Die Komponentenfehlerausgabe enthält die folgenden Ausgabespalten:  
  
-   **Fehlercode**: Der Wert beträgt immer -1.  
  
-   **Fehlerspalte**: Die Quellspalte, die den Fehler verursacht (für Konvertierungsfehler).  
  
-   **Fehlerzeilenspalten**: Die Datensatzdaten, die den Fehler verursachen.  
  
 Je nach Einstellung des Fehlerverhaltens unterstützt die CDC-Quelle das Zurückgeben von Fehlern (Datenkonvertierung, Abschneiden), die während des Extraktionsprozesses in der Fehlerausgabe auftreten.  
  
## <a name="data-type-support"></a>Datentypunterstützung  
 Die CDC-Quellkomponente für Microsoft unterstützt alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen, die den richtigen SSIS-Datentypen zugeordnet sind.  
  
## <a name="troubleshooting-the-cdc-source"></a>Problembehandlung der CDC-Quelle  
 Unten sind Informationen zum Durchführen einer Problembehandlung für die CDC-Quelle aufgeführt.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>Verwenden dieses Skripts zum Isolieren von Problemen und zum Reproduzieren in SQL Server Management Studio  
 Der CDC-Quellvorgang wird vom Vorgang des CDC-Steuerungstasks gesteuert, der vor dem Aufrufen der CDC-Quelle ausgeführt wurde. Der CDC-Steuerungstask bereitet den Wert der CDC-Statuspaketvariablen vor, damit die Start- und End-LSN darin enthalten sein kann. Es wird eine Funktion ausgeführt, die dem folgenden Skript entspricht:  
  
```sql
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 Dabei gilt:  
  
-   \<cdc-enabled-database-name> ist der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank, in der die Änderungstabellen enthalten sind.  
  
-   \<value-from-state-cs> ist der Wert, der in der CDC-Statusvariablen als CS/\<value-from-state-cs>/ (CS steht für Current-processing-range-Start) angegeben wird.  
  
-   \<value-from-state-ce> ist der Wert, der in der CDC-Statusvariablen als CE/\<value-from-state-ce>/ (CE steht für Current-processing-range-End) angegeben wird.  
  
-   \<mode> steht für die CDC-Verarbeitungsmodi. Die Verarbeitungsmodi haben einen der folgenden Werte: **All**, **All with Old Values**, **Net**, **Net with Update Mask**, **Net with Merge**.  
  
 Dieses Skript trägt zur Isolierung von Problemen bei, indem sie im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]reproduziert werden, wo sie leicht reproduziert und identifiziert werden können.  
  
#### <a name="sql-server-error-message"></a>SQL Server-Fehlermeldung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gibt möglicherweise die folgende Meldung zurück:  
  
 **Für die Prozedur oder Funktion cdc.fn_cdc_get_net_changes_\<..> wurden zu wenig Argumente bereitgestellt.**  
  
 Dieser Fehler gibt nicht an, dass ein Argument fehlt. Die Bedeutung ist, dass die Start- bzw. End-LSN-Werte in der CDC-Statusvariablen ungültig sind.  
  
## <a name="configuring-the-cdc-source"></a>Konfigurieren der CDC-Quelle  
 Sie können die CDC-Quelle programmgesteuert oder mit dem SSIS-Designer konfigurieren.  
  
 Weitere Informationen finden Sie in einem der folgenden Themen:  
  
-   [Quellen-Editor für CDC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [Quellen-Editor für CDC &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [Quellen-Editor für CDC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können.  
  
 So öffnen Sie das Dialogfeld **Erweiterter Editor** :  
  
-   Klicken Sie auf dem Bildschirm **Datenfluss** des [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekts mit der rechten Maustaste auf die CDC-Quelle, und wählen Sie **Erweiterten Editor anzeigen**.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Erweiterter Editor** festlegen können, finden Sie unter [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Benutzerdefinierte Eigenschaften der CDC-Quelle](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Extrahieren von Änderungsdaten mithilfe der CDC-Quelle](../../integration-services/data-flow/extract-change-data-using-the-cdc-source.md)  
  
## <a name="cdc-source-editor-connection-manager-page"></a>Quellen-Editor für CDC (Seite Verbindungs-Manager)
  Auf der Seite **Verbindungs-Manager** des Dialogfelds **Quellen-Editor für CDC** können Sie den ADO.NET-Verbindungs-Manager für die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Datenbank auswählen, aus der die CDC-Quelle Änderungszeilen liest (CDC-Datenbank). Nachdem Sie die CDC-Datenbank ausgewählt haben, müssen Sie eine aufgezeichnete Tabelle in der Datenbank auswählen.  
  
 Weitere Informationen zur CDC-Quelle finden Sie unter [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
### <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Verbindungs-Manager" des Quellen-Editors für CDC**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die CDC-Quelle enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die CDC-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für CDC**auf **Verbindungs-Manager**.  
  
### <a name="options"></a>enthalten  
 **ADO.NET-Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um eine neue Verbindung zu erstellen. Die Verbindung muss zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank hergestellt werden, die für CDC aktiviert ist und in der sich die ausgewählte Änderungstabelle befindet.  
  
 **Neu**  
 Klicken Sie auf **Neu**. Das Dialogfeld **ADO.NET-Verbindungs-Manager konfigurieren** , in dem Sie einen neuen Verbindungs-Manager erstellen können, wird geöffnet.  
  
 **CDC Table**  
 Wählen Sie die CDC-Quelltabelle mit den aufgezeichneten Änderungen aus, die Sie lesen und zur Verarbeitung an Downstream-SSIS-Komponenten senden möchten.  
  
 **Capture instance**  
 Wählen Sie den Namen der CDC-Aufzeichnungsinstanz mit der zu lesenden CDC-Tabelle aus, oder geben Sie ihn ein.  
  
 Eine aufgezeichnete Quelltabelle kann über eine oder zwei aufgezeichnete Instanzen zum Behandeln des nahtlosen Übergangs der Tabellendefinition mithilfe von Schemaänderungen verfügen. Wenn mehr als eine Aufzeichnungsinstanz für die aufzuzeichnende Quelltabelle definiert wird, müssen Sie hier die gewünschte Aufzeichnungsinstanz auswählen. Der Standardname einer Aufzeichnungsinstanz für eine Tabelle [Schema].[Tabelle] lautet \<Schema>_\<Tabelle>. Die tatsächlich verwendeten Namen der Aufzeichnungsinstanzen können jedoch abweichen. Die tatsächliche Tabelle, aus der gelesen wird, ist die CDC-Tabelle **cdc.\<Aufzeichnungsinstanz>_CT**.  
  
 **CDC Processing Mode**  
 Wählen Sie den Verarbeitungsmodus aus, der sich für die Behandlung Ihrer Verarbeitungsanforderungen am besten eignet. Folgende Optionen sind möglich:  
  
-   **All**: Gibt die Änderungen im aktuellen CDC-Bereich ohne **Vor Update** -Werte zurück.  
  
-   **All with old values:**Gibt die Änderungen im aktuellen CDC-Verarbeitungsbereich unter Einbeziehung der alten Werte (**Vor Update**) zurück. Für jeden Updatevorgang gibt es zwei Zeilen, eine mit den Werten vor dem Update und eine mit den Werten nach dem Update.  
  
-   **Net**: Gibt nur eine Änderungszeile pro Quellzeile zurück, die im aktuellen CDC-Verarbeitungsbereich geändert wurde. Wenn eine Quellzeile mehrmals aktualisiert wurde, wird die kombinierte Änderung erzeugt (Beispiel: Einfügen+Update wird als einzelner Updatevorgang und Update+Löschen als einzelner Löschvorgang erzeugt). Beim Arbeiten im Änderungsverarbeitungsmodus Net ist es möglich, die Änderungen auf Lösch-, Einfüge- und Updatevorgänge aufzuteilen und parallel zu behandeln, da die einzelne Quellzeile in mehr als einer Ausgabe vorhanden ist.  
  
-   **Net with update mask:** Dieser Modus ähnelt dem normalen Net-Modus, aber es werden außerdem boolesche Spalten mit dem Namensmuster **__$\<Spaltenname>\___Changed** hinzugefügt, die auf geänderte Spalten in der aktuellen Änderungszeile hinweisen.  
  
-   **Net with merge:**Dieser Modus ähnelt dem normalen Net-Modus, aber hierbei sind Einfüge- und Updatevorgänge zu einem einzelnen Mergevorgang (UPSERT) zusammengeführt.  
  
> [!NOTE]  
>  Für alle Nettoänderungsoptionen muss die Quelltabelle über einen Primärschlüssel oder einen eindeutigen Index verfügen. Für Tabellen ohne Primärschlüssel oder eindeutigen Index muss die Option **All** verwendet werden.  
  
 **Variable, die den CDC-Status enthält**  
 Wählen Sie die SSIS-Zeichenfolgenpaketvariable aus, in der der CDC-Status für den aktuellen CDC-Kontext verwaltet wird. Weitere Informationen zur CDC-Statusvariablen finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).  
  
 **Include reprocessing indicator column**  
 Aktivieren Sie dieses Kontrollkästchen, um eine spezielle Ausgabespalte mit dem Namen **__$reprocessing**zu erstellen.  
  
 Diese Spalte verfügt über den Wert **TRUE** , wenn sich der CDC-Verarbeitungsbereich mit dem ursprünglichen Verarbeitungsbereich überschneidet (der LSN-Bereich, der dem Zeitraum des erstmaligen Ladens entspricht) oder wenn ein CDC-Verarbeitungsbereich nach einem Fehler bei einer vorherigen Ausführung erneut verarbeitet wird. In dieser Indikatorspalte können SSIS-Entwickler Fehler unterschiedlich behandeln, wenn sie Änderungen erneut verarbeiten (z. B. können Aktionen, wie das Löschen einer nicht vorhandenen Zeile und ein fehlgeschlagener Einfügevorgang aufgrund eines doppelten Schlüssels, ignoriert werden).  
  
 Weitere Informationen finden Sie unter [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
## <a name="cdc-source-editor-columns-page"></a>Quellen-Editor für CDC (Seite Spalten)
  Auf der Seite **Spalten** des Dialogfelds **Quellen-Editor für CDC** können Sie jeder externen Spalte (Quellspalte) eine Ausgabespalte zuordnen.  
  
### <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Spalten" des Quellen-Editors für CDC**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die CDC-Quelle enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die CDC-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für CDC**auf **Spalten**.  
  
### <a name="options"></a>enthalten  
 **Verfügbare externe Spalten**  
 Eine Liste der in der Datenquelle verfügbaren externen Spalten. Mit der Tabelle können keine Spalten hinzugefügt oder gelöscht werden. Wählen Sie die zu verwendenden Spalten in der Datenquelle aus. Die ausgewählten Spalten werden der Liste **Externe Spalte** in der Reihenfolge hinzugefügt, in der Sie sie auswählen.  
  
 **Externe Spalte**  
 Eine Ansicht der externen Spalten (Quellspalten) in der Reihenfolge, in der sie angezeigt werden, wenn Sie Komponenten konfigurieren, die Daten aus der CDC-Quelle verwenden. Sie können diese Reihenfolge ändern, indem Sie zunächst die ausgewählten Spalten in der Liste **Verfügbare externe Spalten** löschen und anschließend die externen Spalten in einer anderen Reihenfolge in der Liste auswählen. Die ausgewählten Spalten werden der Liste **Externe Spalte** in der Reihenfolge hinzugefügt, in der Sie sie auswählen.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen ein. Standardmäßig wird der Name der ausgewählten externen Spalte (Quellspalte) verwendet, Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist. Der eingegebene Name wird im SSIS-Designer angezeigt.  
  
## <a name="cdc-source-editor-error-output-page"></a>Quellen-Editor für CDC (Seite Fehlerausgabe)
  Auf der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für CDC** können Sie Optionen für die Fehlerbehandlung auswählen.  
  
### <a name="task-list"></a>Aufgabenliste  
 **So öffnen Sie die Seite "Fehlerausgabe" des Quellen-Editors für CDC**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das die CDC-Quelle enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die CDC-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für CDC**auf **Fehlerausgabe**.  
  
### <a name="options"></a>enthalten  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen Spalten (Quellspalten) an, die im Dialogfeld **Quellen-Editor für CDC** auf der Seite **Verbindungs-Manager** ausgewählt wurden.  
  
 **Fehler**  
 Wählen Sie aus, wie die CDC-Quelle Fehler in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
 **Abschneiden**  
 Wählen Sie aus, wie die CDC-Quelle Kürzungen in einem Fluss behandeln soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
 **Description**  
 Wird nicht verwendet.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Wählen Sie aus, wie die CDC-Quelle im Fall eines Fehlers oder einer Kürzung mit den ausgewählten Zellen verfahren soll: Fehler ignorieren, Zeile umleiten oder Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoptionen auf die ausgewählten Zellen an.  
  
### <a name="error-handling-options"></a>Fehlerbehandlungsoptionen  
 Mit den folgenden Optionen konfigurieren Sie, wie die CDC-Quelle Fehler und Kürzungen behandelt.  
  
 **Fehler bei Komponente**  
 Bei einem Fehler oder beim Abschneiden von Daten wird der Datenflusstask nicht ausgeführt. Dies ist das Standardverhalten.  
  
 **Fehler ignorieren**  
 Der Fehler oder die Kürzung wird ignoriert, und die Datenzeile wird an die Ausgabe der CDC-Quelle umgeleitet.  
  
 **Zeile umleiten**  
 Der Fehler oder die Kürzung wird an die Fehlerausgabe der CDC-Quelle umgeleitet. In diesem Fall wird die Fehlerbehandlung der CDC-Quelle verwendet. Weitere Informationen finden Sie unter [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Blogeintrag, [Processing Modes for the CDC Source](http://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/), auf mattmasson.com.  
  
  
