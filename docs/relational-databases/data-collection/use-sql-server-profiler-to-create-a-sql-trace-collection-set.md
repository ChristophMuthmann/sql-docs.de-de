---
title: "Verwenden von SQL Server Profiler zum Erstellen eines Sammlungssatzes für die SQL-Ablaufverfolgung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQL Trace collector set
ms.assetid: b6941dc0-50f5-475d-82eb-ce7c68117489
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a826e1f5ad16cf35ffb9a5ba7e1ee869c115751
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="use-sql-server-profiler-to-create-a-sql-trace-collection-set"></a>Verwenden von SQL Server Profiler zum Erstellen eines Sammlungssatzes für die SQL-Ablaufverfolgung
  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] können Sie die serverseitigen Ablaufverfolgungsfunktionen von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] nutzen, um eine Ablaufverfolgungsdefinition für das Erstellen eines Sammlungssatzes zu exportieren, der den generischen Sammlertyp für die SQL-Ablaufverfolgung verwendet. Dieser Vorgang besteht aus zwei Teilen:  
  
1.  Sie erstellen und exportieren eine [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ablaufverfolgung.  
  
2.  Sie schreiben einen neuen Sammlungssatz auf der Grundlage einer exportierten Ablaufverfolgung.  
  
 Das Szenario für die folgenden Verfahren umfasst das Sammeln von Daten zu einer gespeicherten Prozedur, deren Ausführung 80 Millisekunden oder länger dauert. Um diese Verfahren durchzuführen, sollten Sie folgende Aufgaben ausführen können:  
  
-   Verwenden von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zum Erstellen und Konfigurieren einer Ablaufverfolgung  
  
-   Verwenden von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Öffnen, Bearbeiten und Ausführen einer Abfrage  
  
### <a name="create-and-export-a-sql-server-profiler-trace"></a>Erstellen und Exportieren einer SQL Server Profiler-Ablaufverfolgung  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]den [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. (Klicken Sie im Menü **Extras** auf **SQL Server Profiler**.)  
  
2.  Klicken Sie im Dialogfeld **Verbindung mit Server herstellen** auf **Abbrechen**.  
  
3.  Vergewissern Sie sich bei diesem Szenario, dass die Werte der Dauer für die Anzeige in Millisekunden (Standard) konfiguriert sind. Führen Sie hierzu folgende Schritte aus:  
  
    1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
    2.  Stellen Sie im Bereich **Anzeigeoptionen** sicher, dass das Kontrollkästchen "Werte in der Spalte 'Dauer' in Mikrosekunden anzeigen" deaktiviert ist.  
  
    3.  Klicken Sie auf **OK** , um das Dialogfeld **Allgemeine Optionen** zu schließen.  
  
4.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**.  
  
5.  Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** den gewünschten Server aus, und klicken Sie anschließend auf **Verbinden**.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften** wird angezeigt.  
  
6.  Gehen Sie auf der Registerkarte **Allgemein** wie folgt vor:  
  
    1.  Geben Sie im Feld **Ablaufverfolgungsname** den gewünschten Namen für die Ablaufverfolgung ein. In diesem Beispiel ist der Ablaufverfolgungsname **SPgt80**.  
  
    2.  Wählen Sie in der Liste **Vorlage verwenden**die Vorlage zur Verwendung für die Ablaufverfolgung aus. Klicken Sie in diesem Beispiel auf **TSQL_SPs**.  
  
7.  Gehen Sie auf der Registerkarte **Ereignisauswahl** wie folgt vor:  
  
    1.  Geben Sie die Ereignisse zur Verwendung mit der Ablaufverfolgung an. Deaktivieren Sie in diesem Beispiel alle Kontrollkästchen in der Spalte **Ereignisse** , mit Ausnahme von **ExistingConnection** und **SP:Completed**.  
  
    2.  Aktivieren Sie in der unteren rechten Ecke das Kontrollkästchen **Alle Spalten anzeigen** .  
  
    3.  Klicken Sie auf die Zeile **SP:Completed** .  
  
    4.  Führen Sie einen Bildlauf durch die Zeile in der Spalte **Dauer** aus, und aktivieren Sie das Kontrollkästchen **Dauer** .  
  
8.  Klicken Sie in der unteren rechten Ecke auf **Spaltenfilter** , um das Dialogfeld **Filter bearbeiten** zu öffnen. Führen Sie im Dialogfeld **Filter bearbeiten** Folgendes durch:  
  
    1.  Klicken Sie in der Filterliste auf **Dauer**.  
  
    2.  Erweitern Sie im Fenster für den booleschen Operator den Knoten **Größer oder gleich** , geben Sie **80** als Wert ein, und klicken Sie auf **OK**.  
  
9. Klicken Sie auf **Ausführen** , um die Ablaufverfolgung zu starten.  
  
10. Klicken Sie auf der Symbolleiste auf **Ausgewählte Ablaufverfolgung beenden** oder **Ausgewählte Ablaufverfolgung anhalten**.  
  
11. Zeigen Sie im Menü **Datei** auf **Exportieren**, zeigen Sie auf **Skript für Ablaufverfolgungsdefinition erstellen**, und klicken Sie dann auf **Für den Auflistsatz der SQL-Ablaufverfolgung**.  
  
12. Geben Sie im Dialogfeld **Speichern unter** im Feld **Dateiname** den gewünschten Namen für die Ablaufverfolgungsdefinition ein, und speichern Sie sie am gewünschten Ort. In diesem Beispiel ist der Dateiname gleich dem Namen der Ablaufverfolgung (SPgt80).  
  
13. Klicken Sie auf **OK** , wenn die Meldung angezeigt wird, dass die Datei erfolgreich gespeichert wurde, und schließen Sie [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="script-a-new-collection-set-from-a-sql-server-profiler-trace"></a>Schreiben eines neuen Sammlungssatzes auf der Grundlage einer SQL Server Profiler-Ablaufverfolgung  
  
1.  Zeigen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]im Menü **Datei** auf **Öffnen** , und klicken Sie dann auf **Datei**.  
  
2.  Suchen Sie im Dialogfeld **Datei öffnen** die zuvor erstellte Datei (SPgt80), und öffnen Sie sie.  
  
     Die von Ihnen gespeicherte Ablaufverfolgung wird in einem Abfragefenster geöffnet und in einem Skript zusammengeführt, das Sie ausführen können, um den neuen Sammlungssatz zu erstellen.  
  
3.  Führen Sie einen Bildlauf durch das Skript durch, und nehmen Sie die folgenden Ersetzungen vor, wie im Text des Skriptkommentars angegeben:  
  
    -   Ersetzen Sie **SQLTrace Collection Set Name Here** durch den Namen, den Sie für den Sammlungssatz verwenden möchten. Nennen Sie in diesem Beispiel den Sammlungssatz **SPROC_CollectionSet**.  
  
    -   Ersetzen Sie **SQLTrace Collection Item Name Here** durch den Namen, den Sie für das Sammelelement verwenden möchten. Nennen Sie in diesem Beispiel das Sammelelement **SPROC_Collection_Item**.  
  
4.  Klicken Sie auf **Ausführen** , um die Abfrage auszuführen und den Sammlungssatz zu erstellen.  
  
5.  Überprüfen Sie im Objekt-Explorer, ob der Sammlungssatz erstellt wurde. Führen Sie hierzu folgende Schritte aus:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Verwaltung**, und klicken Sie dann auf **Aktualisieren**.  
  
    2.  Erweitern Sie **Verwaltung**und anschließend **Datensammlung**.  
  
     Der Sammlungssatz **SPROC_CollectionSet** wird auf derselben Ebene wie der Knoten **Systemdaten-Sammlungssätze** angezeigt. Der Sammlungssatz ist in der Standardeinstellung deaktiviert.  
  
6.  Bearbeiten Sie im Objekt-Explorer die Eigenschaften von SPROC_CollectionSet, wie Sammlungsmodus und Uploadzeitplan. Folgen Sie den gleichen Schritten, die Sie auch für die Systemdaten-Sammlungssätze ausführen würden, die mit dem Datensammler bereitgestellt werden.  
  
## <a name="example"></a>Beispiel  
 Das folgende Codebeispiel ist das abschließende Skript. Dabei handelt es sich um das Ergebnis der in den vorherigen Schritten aufgezeigten Anweisungen.  
  
```  
/*************************************************************/  
-- SQL Trace collection set generated from SQL Server Profiler  
-- Date: 11/19/2007  12:55:31 AM  
/*************************************************************/  
  
USE msdb  
GO  
  
BEGIN TRANSACTION  
BEGIN TRY  
  
-- Define collection set  
-- ***  
-- *** Replace 'SqlTrace Collection Set Name Here' in the   
-- *** following script with the name you want  
-- *** to use for the collection set.  
-- ***  
DECLARE @collection_set_id int;  
EXEC [dbo].[sp_syscollector_create_collection_set]  
    @name = N'SPROC_CollectionSet',  
    @schedule_name = N'CollectorSchedule_Every_15min',  
    @collection_mode = 0, -- cached mode needed for Trace collections  
    @logging_level = 0, -- minimum logging  
    @days_until_expiration = 5,  
    @description = N'Collection set generated by SQL Server Profiler',  
    @collection_set_id = @collection_set_id output;  
SELECT @collection_set_id;  
  
-- Define input and output variables for the collection item.  
DECLARE @trace_definition xml;  
DECLARE @collection_item_id int;  
  
-- Define the trace parameters as an XML variable  
SELECT @trace_definition = convert(xml,   
N'<ns:SqlTraceCollector xmlns:ns"DataCollectorType" use_default="0">  
<Events>  
  <EventType name="Sessions">  
    <Event id="17" name="ExistingConnection" columnslist="1,2,14,26,3,35,12" />  
  </EventType>  
  <EventType name="Stored Procedures">  
    <Event id="43" name="SP:Completed" columnslist="1,2,26,34,3,35,12,13,14,22" />  
  </EventType>  
</Events>  
<Filters>  
  <Filter columnid="13" columnname="Duration" logical_operator="AND" comparison_operator="GE" value="80000L" />  
</Filters>  
</ns:SqlTraceCollector>  
');  
  
-- Retrieve the collector type GUID for the trace collector type.  
DECLARE @collector_type_GUID uniqueidentifier;  
SELECT @collector_type_GUID = collector_type_uid FROM [dbo].[syscollector_collector_types] WHERE name = N'Generic SQL Trace Collector Type';  
  
-- Create the trace collection item.  
-- ***  
-- *** Replace 'SqlTrace Collection Item Name Here' in   
-- *** the following script with the name you want to  
-- *** use for the collection item.  
-- ***  
EXEC [dbo].[sp_syscollector_create_collection_item]  
   @collection_set_id = @collection_set_id,  
   @collector_type_uid = @collector_type_GUID,  
   @name = N'SPROC_Collection_Item',  
   @frequency = 900, -- specified the frequency for checking to see if trace is still running  
   @parameters = @trace_definition,  
   @collection_item_id = @collection_item_id output;  
SELECT @collection_item_id;  
  
COMMIT TRANSACTION;  
END TRY  
  
BEGIN CATCH  
ROLLBACK TRANSACTION;  
DECLARE @ErrorMessage nvarchar(4000);  
DECLARE @ErrorSeverity int;  
DECLARE @ErrorState int;  
DECLARE @ErrorNumber int;  
DECLARE @ErrorLine int;  
DECLARE @ErrorProcedure nvarchar(200);  
SELECT @ErrorLine = ERROR_LINE(),  
       @ErrorSeverity = ERROR_SEVERITY(),  
       @ErrorState = ERROR_STATE(),  
       @ErrorNumber = ERROR_NUMBER(),  
       @ErrorMessage = ERROR_MESSAGE(),  
       @ErrorProcedure = ISNULL(ERROR_PROCEDURE(), '-');  
RAISERROR (14684, @ErrorSeverity, 1 , @ErrorNumber, @ErrorSeverity, @ErrorState, @ErrorProcedure, @ErrorLine, @ErrorMessage);  
END CATCH;  
GO  
```  
  
  
