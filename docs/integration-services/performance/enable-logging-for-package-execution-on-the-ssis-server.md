---
title: "Aktivieren der Protokollierung f&#252;r die Paketausf&#252;hrung auf dem SSIS-Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1"
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Aktivieren der Protokollierung f&#252;r die Paketausf&#252;hrung auf dem SSIS-Server
  In diesem Thema wird beschrieben, wie Sie den Protokolliergrad für ein Paket festlegen oder ändern, wenn Sie ein auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server bereitgestelltes Paket ausführen. Der Protokolliergrad, den Sie beim Ausführen des Pakets festlegen, überschreibt die Paketprotokollierung, die Sie zur Entwurfszeit in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] konfigurieren. Weitere Informationen finden Sie unter [Aktivieren der Paketprotokollierung in SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md).  
  
 Sie können nun in den **Servereigenschaften** von SQL Server in der Eigenschaft **Serverprotokolliergrad** einen Standardwert für den serverweiten Protokolliergrad festlegen. Sie können sich zwischen einem der in diesem Thema beschriebenen integrierten Protokolliergrade oder einem vorhandenen benutzerdefinierten Protokolliergrad entscheiden. Der ausgewählte Protokolliergrad wird standardmäßig auf alle im SSIS-Katalog bereitgestellten Pakete angewendet. Er gilt standardmäßig auch für SQL Agent-Auftragsschritte, die ein SSIS-Paket ausführen.  
  
 Sie können den Protokolliergrad für ein einzelnes Paket auch mithilfe einer der folgenden Methoden angeben. In diesem Thema wird die erste Methode behandelt.  
  
-   Konfigurieren einer Instanz einer Paketausführung mithilfe des Dialogfelds "Paket ausführen"  
  
-   Das Festlegen von Parametern für eine Instanz mithilfe von [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
-   Das Konfigurieren eines Auftrags des SQL Server-Agents für eine Paketausführung mit dem Dialogfeld "Neuer Auftragsschritt".  
  
## Festlegen des Protokolliergrads für ein Paket mithilfe des Dialogfelds „Paket ausführen“  
  
1.  Navigieren Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] zum Paket im Objekt-Explorer.  
  
2.  Klicken Sie mit der rechten Maustaste auf das Paket, und wählen Sie **Ausführen** aus.  
  
3.  Wählen Sie im Dialogfeld **Paket ausführen** die Registerkarte **Erweitert** aus.  
  
4.  Wählen Sie unter **Protokolliergrad** den Protokolliergrad aus. Dieses Thema enthält eine Beschreibung der verfügbaren Werte.  
  
5.  Nehmen Sie ggf. weitere Einstellungen für die Paketkonfiguration vor, und klicken Sie anschließend auf **OK**, um das Paket auszuführen.  
  
## Auswählen eines Protokolliergrads  
 Die folgenden integrierten Protokolliergrade sind verfügbar. Sie können auch einen vorhandenen benutzerdefinierten Protokolliergrad auswählen. Dieses Thema enthält eine Beschreibung benutzerdefinierter Protokolliergrade.  
  
|Protokolliergrad|Description|  
|-------------------|-----------------|  
|InclusionThresholdSetting|Die Protokollierung ist deaktiviert. Nur der Status der Ausführung von Paketen wird protokolliert.|  
|Standard|Alle Ereignisse werden protokolliert, außer benutzerdefinierten und Diagnose-Ereignissen. Dies ist der Standardwert.|  
|RuntimeLineage|Sammelt die Daten, die zum Nachverfolgen von Informationen über die Datenherkunft im Datenfluss benötigt werden. Sie können diese Herkunftsinformationen analysieren, um die Herkunftsbeziehung zwischen Tasks zuzuordnen. Unabhängige Softwareentwickler (ISVs) und Entwickler können mit diesen Informationen benutzerdefinierte Herkunftszuordnungstools erstellen.|  
|Leistung|Nur Leistungsstatistiken sowie OnError- und OnWarning-Ereignisse werden protokolliert.<br /><br /> In dem Bericht **Ausführungsleistung** wird die aktive Zeit und die Gesamtzeit für Datenflusskomponenten des Pakets angezeigt. Diese Informationen sind verfügbar, wenn der Protokolliergrad der letzten Paketausführung auf **Leistung** oder **Ausführlich** festgelegt wurde. Weitere Informationen finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/reports-for-the-integration-services-server.md).<br /><br /> In der [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md)-Sicht werden die Start- und Beendigungszeiten der Datenflusskomponenten für jede Ausführungsphase angezeigt. In dieser Sicht werden die Informationen für diese Komponenten nur angezeigt, wenn der Protokolliergrad der Paketausführung auf **Leistung** oder **Ausführlich** festgelegt ist.|  
|Ausführlich|Alle Ereignisse werden protokolliert, einschließlich benutzerdefinierter Ereignisse und Diagnose-Ereignissen.<br /><br /> Zu benutzerdefinierten Ereignissen zählen auch die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Tasks protokollierten Ereignisse. Weitere Informationen zu benutzerdefinierten Ereignissen finden Sie unter [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).<br /><br /> Ein Beispiel für ein Diagnoseereignis ist das **DiagnosticEx**-Ereignis. Immer wenn ein „Paket ausführen“-Task ein untergeordnetes Paket ausführt, erfasst dieses Ereignis die an untergeordnete Pakete übergebenen Parameterwerte.<br /><br /> Das **DiagnosticEx**-Ereignis hilft Ihnen auch dabei, die Namen der Spalten abzurufen, in denen Fehler auf Zeilenebene auftreten. Dieses Ereignis schreibt eine Herkunftszuordnung für den Datenfluss in das Protokoll. Sie können den Spaltennamen dann in dieser Herkunftszuordnung nachschlagen, und zwar anhand des von einer Fehlerausgabe erfassten Spaltenbezeichners.  Weitere Informationen finden Sie unter [Error Handling in Data](../../integration-services/data-flow/error-handling-in-data.md).<br /><br /> Der Wert der Meldungsspalte für **DiagnosticEx** ist XML-Text. Fragen Sie zum Anzeigen des Meldungstexts für eine Paketausführung die Sicht [catalog.operation_messages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) ab. Beachten Sie, dass Leerraum in der XML-Ausgabe beim **DiagnosticEx** -Ereignis nicht beibehalten wird, um die Größe des Protokolls zu verringern. Kopieren Sie das Protokoll in einen XML-Editor wie z.B. Visual Studio, der XML-Formatierung und Syntaxhervorhebung unterstützt, um die Lesbarkeit zu verbessern.<br /><br /> In der [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md)-Sicht wird eine Zeile angezeigt, sobald eine Datenflusskomponente Daten zur Paketausführung an eine Downstreamkomponente sendet. Der Protokolliergrad muss auf **Ausführlich** festgelegt werden, um diese Informationen in der Sicht zu erfassen.|  
  
## Erstellen und Verwalten benutzerdefinierter Protokolliergrade mithilfe des Dialogfelds „Customized Logging Level Management“ (Verwaltung benutzerdefinierter Protokolliergrade)  
 Sie können benutzerdefinierte Protokolliergrade erstellen, die nur die von Ihnen gewünschten Statistiken und Ereignisse sammeln. Optional können Sie auch den Kontext von Ereignissen erfassen, der Variablenwerte, Verbindungszeichenfolgen und Komponenteneigenschaften umfasst. Wenn Sie ein Paket ausführen, können Sie überall dort einen benutzerdefinierten Protokolliergrad auswählen, wo Sie auch einen integrierten Protokolliergrad auswählen können.  
  
> [!TIP]  
>  Die **IncludeInDebugDump**-Eigenschaft der Variablen muss auf **TRUE** festgelegt werden, damit die Werte der Paketvariablen erfasst werden.  
  
1.  Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mit der rechten Maustaste auf die SSISDB-Datenbank, und wählen Sie **Customized Logging Level** (Angepasster Protokolliergrad) aus, um das Dialogfeld **Verwaltung des angepassten Protokolliergrads** zu öffnen. So erstellen und verwalten Sie angepasste Protokolliergrade. Die Liste **Angepasste Protokolliergrade** enthält alle vorhandenen angepassten Protokolliergrade.  
  
2.  Klicken Sie zum **Erstellen** eines neuen angepassten Protokolliergrads auf **Erstellen**, und stellen Sie anschließend einen Namen und eine Beschreibung bereit. Wählen Sie auf den Registerkarten **Statistiken** und **Ereignisse** die Statistiken und Ereignisse aus, die Sie sammeln möchten. Wählen Sie optional auf der Registerkarte **Ereignisse** für einzelne Ereignisse **Kontext einschließen** aus. Klicken Sie anschließend auf **Speichern**.  
  
3.  Wählen Sie zum **Aktualisieren** eines vorhandenen angepassten Protokolliergrads diesen in der Liste aus, konfigurieren Sie ihn erneut, und klicken Sie anschließend auf **Speichern**.  
  
4.  Wählen Sie zum **Löschen** eines vorhandenen angepassten Protokolliergrads diesen in der Liste aus, und klicken Sie anschließend auf **Löschen**.  
  
 **Berechtigungen für benutzerdefinierte Protokolliergrade.**  
  
-   Alle Benutzer der SSISDB-Datenbank können benutzerdefinierte Protokolliergrade sehen und beim Ausführen von Paketen einen benutzerdefinierten Protokolliergrad auswählen.  
  
-   Nur Benutzer in der ssis_admin- oder der sysadmin-Rolle können benutzerdefinierte Protokolliergrade erstellen, aktualisieren oder löschen.  
  
## Siehe auch  
 [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)   
 [Aktivieren der Paketprotokollierung in SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)  
  
  