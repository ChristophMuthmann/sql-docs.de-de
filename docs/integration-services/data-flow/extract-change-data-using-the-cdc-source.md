---
title: "Extrahieren von &#196;nderungsdaten mithilfe der CDC-Quelle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Extrahieren von &#196;nderungsdaten mithilfe der CDC-Quelle
  Das Paket muss bereits mindestens einen Datenflusstask und einen CDC-Steuerungstask enthalten, damit Sie eine CDC-Quelle hinzufügen und konfigurieren können.  
  
 Weitere Informationen zum CDC-Steuerungstask finden Sie unter [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 Weitere Informationen zur CDC-Quelle finden Sie unter [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
### So extrahieren Sie Änderungsdaten mithilfe einer CDC-Quelle  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie die CDC-Quelle dann aus der **Toolbox**auf die Entwurfsoberfläche.  
  
4.  Doppelklicken Sie auf die CDC-Quelle.  
  
5.  Wählen Sie im Dialogfeld **Quellen-Editor für CDC** auf der Seite **Verbindungs-Manager** in der Liste einen vorhandenen ADO.NET-Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um eine neue Verbindung zu erstellen. Die Verbindung sollte zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank hergestellt werden, die die zu lesenden Änderungstabellen enthält.  
  
6.  Wählen Sie die **CDC-Tabelle** aus, in der Sie Änderungen verarbeiten möchten.  
  
7.  Wählen Sie den Namen der **CDC-Aufzeichnungsinstanz** mit der zu lesenden CDC-Tabelle aus, oder geben Sie ihn ein.  
  
     Eine aufgezeichnete Quelltabelle kann über eine oder zwei aufgezeichnete Instanzen zum Behandeln des nahtlosen Übergangs der Tabellendefinition mithilfe von Schemaänderungen verfügen. Wenn mehr als eine Aufzeichnungsinstanz für die aufzuzeichnende Quelltabelle definiert wird, müssen Sie hier die gewünschte Aufzeichnungsinstanz auswählen. Der Standardname der Aufzeichnungsinstanz für eine Tabelle [Schema].[Tabelle] ist \<Schema>_\<Tabelle>, aber die tatsächlich verwendeten Aufzeichnungsinstanznamen können davon abweichen. Die tatsächliche Tabelle, aus der gelesen wird, ist die CDC-Tabelle **cdc .<Aufzeichnungsinstanz>_CT**.  
  
8.  Wählen Sie den Verarbeitungsmodus aus, der sich für die Behandlung Ihrer Verarbeitungsanforderungen am besten eignet. Folgende Optionen sind möglich:  
  
    -   **All**: Gibt die Änderungen im aktuellen CDC-Bereich ohne **Vor Update** -Werte zurück.  
  
    -   **All with old values:** Gibt die Änderungen im aktuellen CDC-Verarbeitungsbereich unter Einbeziehung der alten Werte (**Vor Update**) zurück. Für jeden Updatevorgang gibt es zwei Zeilen, eine mit den Werten vor dem Update und eine mit den Werten nach dem Update.  
  
    -   **Net**: Gibt nur eine Änderungszeile pro Quellzeile zurück, die im aktuellen CDC-Verarbeitungsbereich geändert wurde. Wenn eine Quellzeile mehrmals aktualisiert wurde, wird die kombinierte Änderung erzeugt (Beispiel: Einfügen+Update wird als einzelner Updatevorgang und Update+Löschen als einzelner Löschvorgang erzeugt). Beim Arbeiten im Änderungsverarbeitungsmodus Net ist es möglich, die Änderungen auf Lösch-, Einfüge- und Updatevorgänge aufzuteilen und parallel zu behandeln, da die einzelne Quellzeile in mehr als einer Ausgabe vorhanden ist.  
  
    -   **Net with update mask:** Dieser Modus ähnelt dem normalen Net-Modus, aber es werden außerdem boolesche Spalten mit dem Namensmuster **__$<Spaltenname>\___Changed** hinzugefügt, die auf geänderte Spalten in der aktuellen Änderungszeile hinweisen.  
  
    -   **Net with merge:** Dieser Modus ähnelt dem normalen Net-Modus, aber hierbei sind Einfüge- und Updatevorgänge zu einem einzelnen Mergevorgang (UPSERT) zusammengeführt.  
  
9. Wählen Sie die SSIS-Zeichenfolgenpaketvariable aus, in der der CDC-Status für den aktuellen CDC-Kontext verwaltet wird. Weitere Informationen zur CDC-Statusvariablen finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).  
  
10. Aktivieren Sie das Kontrollkästchen **reprocessing-Indikatorspalte einschließen**, um eine spezielle Ausgabespalte mit dem Namen **__$reprocessing** zu erstellen. Diese Spalte hat den Wert **TRUE**, wenn sich der CDC-Verarbeitungsbereich mit dem ursprünglichen Verarbeitungsbereich überschneidet (der LSN-Bereich, der dem Zeitraum des erstmaligen Ladens entspricht) oder wenn ein CDC-Verarbeitungsbereich nach einem Fehler bei einer vorherigen Ausführung erneut verarbeitet wird. In dieser Indikatorspalte können SSIS-Entwickler Fehler unterschiedlich behandeln, wenn sie Änderungen erneut verarbeiten (z. B. können Aktionen, wie das Löschen einer nicht vorhandenen Zeile und ein fehlgeschlagener Einfügevorgang aufgrund eines doppelten Schlüssels, ignoriert werden).  
  
     Weitere Informationen finden Sie unter [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
11. Um die Zuordnung zwischen externen Spalten und Ausgabespalten zu aktualisieren, klicken Sie auf **Spalten** und wählen in der Liste **Externe Spalte** verschiedene Spalten aus.  
  
12. Aktualisieren Sie optional die Werte der Ausgabespalten, indem Sie Werte in der Liste **Ausgabespalte** löschen.  
  
13. Klicken Sie auf **Fehlerausgabe**, um die Fehlerausgabe zu konfigurieren.  
  
14. Sie können auf **Vorschau** klicken, um bis zu 200 Datenzeilen anzuzeigen, die von der CDC-Quelle extrahiert werden.  
  
15. Klicken Sie auf **OK**.  
  
## Siehe auch  
 [Quellen-Editor für CDC &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Quellen-Editor für CDC &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)   
 [Quellen-Editor für CDC &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  