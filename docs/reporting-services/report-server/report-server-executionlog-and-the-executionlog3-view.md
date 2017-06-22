---
title: Berichtsserver-Server ExecutionLog und die ExecutionLog3-Ansicht | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [Reporting Services], execution
- execution logs [Reporting Services]
ms.assetid: a7ead67d-1404-4e67-97e7-4c7b0d942070
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f54e9b1c9aa0a17634048f91932c4aad2d69888b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="report-server-executionlog-and-the-executionlog3-view"></a>Berichtsserver-Sichten ExecutionLog und ExecutionLog3
  Das Berichtsserver-Ausführungsprotokoll von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]enthält Informationen zu den Berichten, die auf dem Server bzw. auf mehreren Servern in einer Bereitstellung für horizontales Skalieren im einheitlichen Modus oder in einer SharePoint-Farm ausgeführt werden. Anhand des Ausführungsprotokolls des Berichtsservers können Sie feststellen, wie oft ein Bericht angefordert wird, welche Ausgabeformate am meisten verwendet werden und wie viele Millisekunden Verarbeitungszeit für die einzelnen Verarbeitungsphasen aufgewendet werden. Das Protokoll enthält Informationen über die Zeit, die für die Ausführung der Datasetabfrage eines Berichts aufgewendet wurde, und die Zeit, die für die Verarbeitung der Daten aufgewendet wurde. Wenn Sie Berichtsserveradministrator sind, können Sie die Protokollinformationen überprüfen und Aufgaben mit langer Laufzeit identifizieren sowie den Berichtsautoren zu den Bereichen des Berichts (Dataset oder Verarbeitung) Vorschläge zur Verbesserung machen.  
  
 Für den SharePoint-Modus konfigurierte Berichtsserver können auch die SharePoint-ULS-Protokolle verwenden. Weitere Informationen finden Sie unter [Aktivieren von Reporting Services-Ereignissen für das SharePoint-Ablaufverfolgungsprotokoll &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)  
  
##  <a name="bkmk_top"></a> Anzeigen von Protokollinformationen  
 Die Berichtsserverausführung protokolliert Daten zur Berichtsausführung in einer internen Datenbanktabelle. Die Informationen aus der Tabelle sind in SQL Server-Sichten verfügbar.  
  
 Das Berichtsausführungsprotokoll wird in der Berichtsserver-Datenbank gespeichert, die standardmäßig **ReportServer**genannt wird. Die SQL-Ansichten enthalten die Ausführungsprotokollinformationen. Die Ansichten "2" und "3" wurden in aktuelleren Versionen hinzugefügt und enthalten neue Felder, oder sie enthalten Felder mit benutzerfreundlicheren Namen als die vorherigen Versionen. Die älteren Ansichten bleiben im Produkt, sodass es keinerlei Auswirkungen auf benutzerdefinierte Anwendungen, die von ihnen abhängen, gibt. Wenn keine Abhängigkeit von einer älteren Sicht vorliegt, z.B. ExecutionLog, wird empfohlen, die neueste Sicht, ExecutionLog**3**, zu verwenden.  
  
 In diesem Thema:  
  
-   [Konfigurationseinstellungen für einen Berichtsserver im SharePoint-Modus](#bkmk_sharepoint)  
  
-   [Konfigurationseinstellungen für einen Berichtsserver im einheitlichen Modus](#bkmk_native)  
  
-   [Protokollierungsfelder (ExecutionLog3)](#bkmk_executionlog3)  
  
-   [Das AdditionalInfo-Feld](#bkmk_additionalinfo)  
  
-   [Protokollierungsfelder (ExecutionLog2)](#bkmk_executionlog2)  
  
-   [Protokollierungsfelder (ExecutionLog)](#bkmk_executionlog)  
  
##  <a name="bkmk_sharepoint"></a> Konfigurationseinstellungen für einen Berichtsserver im SharePoint-Modus  
 Sie können die Berichtsausführungsprotokollierung in den Systemeinstellungen einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung aktivieren oder deaktivieren.  
  
 Standardmäßig werden Protokolleinträge 60 Tage gespeichert. Einträge, die dieses Datum überschreiten, werden um 2.00 Uhr entfernt. täglich um 2:00 Uhr entfernt. Für eine länger vorhandene Installation stehen Informationen jeweils nur 60 Tage lang zur Verfügung.  
  
 Sie können keine Beschränkungen für die Anzahl der Zeilen oder die Art der protokollierten Einträge festlegen.  
  
 **So aktivieren Sie die Protokollierung der Ausführung:**  
  
1.  Klicken Sie in der SharePoint-Zentraladministration in der Gruppe **Anwendungsverwaltung** auf **Dienstanwendungen verwalten** .  
  
2.  Klicken Sie auf den Namen der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung, die Sie konfigurieren möchten.  
  
3.  Klicken Sie auf **Systemeinstellungen**.  
  
4.  Wählen Sie **Protokollierung der Ausführung aktivieren** im Abschnitt **Protokollierung** aus.  
  
5.  Klicken Sie auf **OK**.  
  
 **So aktivieren Sie die ausführliche Protokollierung:**  
  
 Sie müssen das Protokollieren wie in den vorherigen Schritten beschrieben aktivieren und anschließend Folgendes durchführen:  
  
1.  Suchen Sie auf der Seite **Systemeinstellungen** Ihrer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung den Abschnitt **Benutzerdefiniert** .  
  
2.  Ändern Sie **ExecutionLogLevel** in **Ausführlich**. Dieses Feld ist ein Texteingabefeld, und die zwei möglichen Werte sind **Ausführlich** und **Normal**.  
  
##  <a name="bkmk_native"></a> Konfigurationseinstellungen für einen Berichtsserver im einheitlichen Modus  
 Sie können die Protokollierung der Berichtsausführung auf der Seite "Servereigenschaften" in SQL Server Management Studio aktivieren oder deaktivieren. **EnableExecutionLogging** ist eine erweiterte Eigenschaft.  
  
 Standardmäßig werden Protokolleinträge 60 Tage gespeichert. Einträge, die dieses Datum überschreiten, werden um 2.00 Uhr entfernt. täglich um 2:00 Uhr entfernt. Für eine länger vorhandene Installation stehen Informationen jeweils nur 60 Tage lang zur Verfügung.  
  
 Sie können keine Beschränkungen für die Anzahl der Zeilen oder die Art der protokollierten Einträge festlegen.  
  
 **So aktivieren Sie die Protokollierung der Ausführung:**  
  
1.  Starten Sie SQL Server Management Studio mit Administratorprivilegien. Klicken Sie z. B. mit der rechten Maustaste auf das Management Studio-Symbol, und klicken Sie auf "Ausführen als Administrator".  
  
2.  Stellen Sie eine Verbindung mit dem gewünschten Berichtsserver her.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Servernamen, und klicken Sie auf **Eigenschaften**. Wenn die Option "Eigenschaften" deaktiviert ist, überprüfen Sie, dass Sie SQL Server Management Studio mit Administratorprivilegien ausgeführt haben.  
  
4.  Klicken Sie auf die Seite **Protokollierung** .  
  
5.  Wählen Sie **Protokollierung der Berichtsausführung aktivieren**aus.  
  
 **So aktivieren Sie die ausführliche Protokollierung:**  
  
 Sie müssen das Protokollieren wie in den vorherigen Schritten beschrieben aktivieren und anschließend Folgendes durchführen:  
  
1.  Klicken Sie im Dialogfeld **Servereigenschaften** auf die Seite **Erweitert** .  
  
2.  Ändern Sie im Abschnitt **Benutzerdefiniert** den Wert für **ExecutionLogLevel** in **Ausführlich**. Dieses Feld ist ein Texteingabefeld, und die zwei möglichen Werte sind **Ausführlich** und **Normal**.  
  
##  <a name="bkmk_executionlog3"></a> Protokollierungsfelder (ExecutionLog3)  
 Dieser Sicht wurde ein zusätzlicher Leitungsdiagnoseknoten in der XML-basierten Spalte **AdditionalInfo** hinzugefügt. Die Spalte AdditionalInfo enthält eine XML-Struktur von 1:n zusätzlichen Informationsfeldern. Folgendes ist eine Beispiel-Transact-SQL-Anweisung, um Zeilen aus der Ansicht ExecutionLog3 abzurufen. Im Beispiel wird davon ausgegangen, dass der Name der Berichtsserver-Datenbank **ReportServer**lautet:  
  
```  
Use ReportServer  
select * from ExecutionLog3 order by TimeStart DESC  
```  
  
 In der folgenden Tabelle werden die Daten beschrieben, die im Berichtsausführungsprotokoll aufgezeichnet werden  
  
|Column|Description|  
|------------|-----------------|  
|InstanceName|Name der Berichtsserverinstanz, die die Anforderung verarbeitet hat. Wenn die Umgebung mehr als einen Berichtsserver hat, können Sie die zu überwachende InstanceName-Verteilung analysieren und bestimmen, ob der Netzwerklastenausgleich Anforderungen auf der anderen Seite von Berichtsservern wie erwartet verteilt.|  
|ItemPath|Pfad, in dem ein Bericht oder Berichtselement gespeichert wird.|  
|UserName|Benutzer-ID.|  
|ExecutionID|Der interne einer Anforderung zugeordnete Bezeichner. Anforderungen für die selben Benutzersitzungen besitzen dieselbe Ausführungs-ID.|  
|RequestType|Mögliche Werte:<br /><br /> Interaktiv<br /><br /> Abonnement<br /><br /> <br /><br /> Das Analysieren von nach RequestType=Subscription gefilterten und nach TimeStart sortierten Protokolldaten enthüllt möglicherweise Zeiträume starker Abonnementnutzung und Sie möchten vielleicht einige der Berichtsabonnements in eine andere Zeit ändern.|  
|Format|Renderingformat.|  
|Parameter|Parameterwerte, die für die Berichtsausführung verwendet werden.|  
|ItemAction|Mögliche Werte:<br /><br /> Render<br /><br /> Sort<br /><br /> BookMarkNavigation<br /><br /> DocumentNavigation<br /><br /> GetDocumentMap<br /><br /> Findstring<br /><br /> Execute<br /><br /> RenderEdit|  
|TimeStart|Anfangs- und Beendigungszeit für die Verarbeitung eines Berichts.|  
|TimeEnd||  
|TimeDataRetrieval|Anzahl von Millisekunden, die zum Abrufen der Daten benötigt werden.|  
|TimeProcessing|Anzahl von Millisekunden, die zum Verarbeiten des Berichts benötigt werden.|  
|TimeRendering|Anzahl von Millisekunden, die zum Rendern des Berichts benötigt werden.|  
|Quelle|Quelle der Berichtsausführung. Mögliche Werte:<br /><br /> Live<br /><br /> Cache: Gibt eine zwischengespeicherte Ausführung an, Datasetabfragen werden z. B. nicht live ausgeführt.<br /><br /> Momentaufnahme<br /><br /> Verlauf<br /><br /> Ad-hoc: Gibt entweder einen auf einem dynamisch erstellten Berichtsmodell basierenden Drillthroughbericht oder einen Berichts-Generator-Bericht an, von dem eine Vorschau auf einem Client mithilfe des Berichtsservers zum Verarbeiten und Rendern angezeigt wird.<br /><br /> Sitzung: Gibt eine Anschlussanforderung in einer bereits eingerichteten Sitzung an.  Beispiel: Die ursprüngliche Anforderung besteht im Anzeigen von Seite 1, die Anschlussanforderung ist das Exportieren in Excel mit dem aktuellen Sitzungsstatus.<br /><br /> RDCE: Gibt eine Berichtsdefinitionsanpassungs-Erweiterung (Report Definition Customization Extension, RDCE) an. Eine benutzerdefinierte RDCE-Erweiterung kann eine Berichtsdefinition dynamisch anpassen, bevor sie bei der Berichtsausführung an das Verarbeitungsmodul übergeben wird.|  
|Status|Status (entweder rsSuccess oder ein Fehlercode; beim Auftreten mehrerer Fehler wird nur der erste Fehler aufgezeichnet).|  
|ByteCount|Größe von gerenderten Berichten in Bytes.|  
|RowCount|Anzahl der von Abfragen zurückgegebenen Zeilen.|  
|AdditionalInfo|Ein XML-Eigenschaftenbehälter, der weitere Informationen zur Ausführung enthält. Der Inhalt kann für jede Zeile anders sein.|  
  
##  <a name="bkmk_additionalinfo"></a> Das AdditionalInfo-Feld  
 Das AdditionalInfo-Feld ist ein XML-Eigenschaftenbehälter oder eine Struktur, die weitere Informationen zur Ausführung enthält. Der Inhalt kann für jede Zeile im Protokoll anders sein.  
  
 Im Folgenden sehen Sie Beispiele für den Inhalt des AddtionalInfo-Felds für die Standardprotokollierung und die ausführliche Protokollierung:  
  
 **Beispiel für die Standardprotokollierung von AddtionalInfo**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>147</ConnectionOpenTime>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>642</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>63</ExecuteReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>157</TotalTimeDataRetrieval>  
          <ExecuteReaderTime>60</ExecuteReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 **Beispiel für die ausführliche Protokollierung von AdditionalInfo**  
  
```  
<AdditionalInfo>  
  <ProcessingEngine>2</ProcessingEngine>  
  <ScalabilityTime>  
    <Pagination>0</Pagination>  
    <Processing>0</Processing>  
  </ScalabilityTime>  
  <EstimatedMemoryUsageKB>  
    <Pagination>0</Pagination>  
    <Processing>6</Processing>  
  </EstimatedMemoryUsageKB>  
  <DataExtension>  
    <SQL>1</SQL>  
  </DataExtension>  
  <Connections>  
    <Connection>  
      <ConnectionOpenTime>127</ConnectionOpenTime>  
      <DataSource>  
        <Name>DataSource1</Name>  
        <DataExtension>SQL</DataExtension>  
      </DataSource>  
      <DataSets>  
        <DataSet>  
          <Name>DataSet1</Name>  
          <RowsRead>16</RowsRead>  
          <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>33</ExecuteReaderTime>  
          <DataReaderMappingTime>30</DataReaderMappingTime>  
          <DisposeDataReaderTime>1</DisposeDataReaderTime>  
        </DataSet>  
        <DataSet>  
          <Name>DataSet2</Name>  
          <RowsRead>3</RowsRead>  
          <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
          <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
          <ExecuteReaderTime>1</ExecuteReaderTime>  
          <DataReaderMappingTime>0</DataReaderMappingTime>  
          <DisposeDataReaderTime>0</DisposeDataReaderTime>  
        </DataSet>  
      </DataSets>  
    </Connection>  
  </Connections>  
</AdditionalInfo>  
  
```  
  
 Im Folgenden sehen Sie Werte, die Sie im AdditionalInfo-Feld finden:  
  
-   **ProcessingEngine**  
  
     1=SQL Server 2005, 2=Das neue bedarfsgesteuerte Verarbeitungsmodul. Wenn eine Mehrzahl der Berichte immer noch den Wert 1 anzeigt, können Sie prüfen, wie sie umgestaltet werden sollen, damit sie das neuere und effizientere bedarfsgesteuerte Verarbeitungsmodul verwenden.  
  
     `<ProcessingEngine>2</ProcessingEngine>`  
  
-   **ScalabilityTime**  
  
     Die Anzahl der Millisekunden, die für skalierungsrelevante Operationen im Verarbeitungsmodul benötigt werden. Der Wert 0 gibt an, dass keine zusätzliche Zeit für Skalierungsoperationen aufgebracht wurde. Ein Wert 0 gibt auch an, dass die Anforderung nicht unter unzureichendem Arbeitsspeicher erfolgte.  
  
    ```  
    <ScalabilityTime>  
        <Processing>0</Processing>  
    </ScalabilityTime>  
    ```  
  
-   **EstimatedMemoryUsageKB**  
  
     Eine Schätzung des Höhepunktarbeitsspeichers, in Kilobyte, verbraucht von jeder Komponente während einer bestimmten Anforderung.  
  
    ```  
    <EstimatedMemoryUsageKB>  
        <Processing>38</Processing>  
    </EstimatedMemoryUsageKB>  
    ```  
  
-   **DataExtension**  
  
     Die Typen von Datenerweiterungen oder Datenquellen, die im Bericht verwendet werden. Die Zahl ist eine Anzahl von Vorkommen der speziellen Datenquelle.  
  
    ```  
    <DataExtension>  
       <DAX>2</DAX>  
    </DataExtension>  
    ```  
  
-   **ExternalImages**  
  
     Hinzugefügt in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
     Der Wert wird in Millisekunden angegeben. Diese Daten können bei der Diagnose von Leistungsproblemen verwendet werden. Die zum Abrufen von Bildern von einem externen Webserver benötigte Zeit verlangsamt möglicherweise die gesamte Berichtsausführung.  
  
    ```  
    <ExternalImages>  
        <Count>3</Count>  
        <ByteCount>9268</ByteCount>  
        <ResourceFetchTime>9</ResourceFetchTime>  
    </ExternalImages>  
    ```  
  
-   **Verbindungen**  
  
     Hinzugefügt in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
     Eine Struktur mit mehreren Ebenen  
  
    ```  
    <Connections>  
        <Connection>  
          <ConnectionOpenTime>127</ConnectionOpenTime>  
          <DataSource>  
            <Name>DataSource1</Name>  
            <DataExtension>SQL</DataExtension>  
          </DataSource>  
          <DataSets>  
            <DataSet>  
              <Name>DataSet1</Name>  
              <RowsRead>16</RowsRead>  
              <TotalTimeDataRetrieval>655</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>94</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>33</ExecuteReaderTime>  
              <DataReaderMappingTime>30</DataReaderMappingTime>  
              <DisposeDataReaderTime>1</DisposeDataReaderTime>  
            </DataSet>  
            <DataSet>  
              <Name>DataSet2</Name>  
              <RowsRead>3</RowsRead>  
              <TotalTimeDataRetrieval>16</TotalTimeDataRetrieval>  
              <QueryPrepareAndExecutionTime>2</QueryPrepareAndExecutionTime>  
              <ExecuteReaderTime>1</ExecuteReaderTime>  
              <DataReaderMappingTime>0</DataReaderMappingTime>  
              <DisposeDataReaderTime>0</DisposeDataReaderTime>  
            </DataSet>  
          </DataSets>  
        </Connection>  
    </Connections>  
  
    ```  
  
##  <a name="bkmk_executionlog2"></a> Protokollierungsfelder (ExecutionLog2)  
 Diese Ansicht hat einige neue Felder hinzugefügt und einige andere umbenannt. Folgendes ist eine Beispiel-Transact-SQL-Anweisung, mit der Sie Zeilen aus der Ansicht ExecutionLog2 abrufen können. Im Beispiel wird davon ausgegangen, dass der Name der Berichtsserver-Datenbank **ReportServer**lautet:  
  
```  
Use ReportServer  
select * from ExecutionLog2 order by TimeStart DESC  
```  
  
 In der folgenden Tabelle werden die Daten beschrieben, die im Berichtsausführungsprotokoll aufgezeichnet werden  
  
|Column|Description|  
|------------|-----------------|  
|InstanceName|Name der Berichtsserverinstanz, die die Anforderung verarbeitet hat.|  
|ReportPath|Die Pfadstruktur zum Bericht.  Zum Beispiel ein Bericht mit dem Namen "Test", der der Stammordner im Berichts-Manager ist, würde den ReportPath "/test" aufweisen.<br /><br /> Ein Bericht mit dem Namen "Test", der im Ordner "Samples" im Berichts-Manager gespeichert ist, weist den ReportPath “/Samples/test/” auf|  
|UserName|Benutzer-ID.|  
|ExecutionID||  
|RequestType|Anforderungstyp (Benutzer oder System).|  
|Format|Renderingformat.|  
|Parameter|Parameterwerte, die für die Berichtsausführung verwendet werden.|  
|ReportAction|Mögliche Werte: Render, Sort, BookMarkNavigation, DocumentNavigation, GetDocumentMap, Findstring|  
|TimeStart|Anfangs- und Beendigungszeit für die Verarbeitung eines Berichts.|  
|TimeEnd||  
|TimeDataRetrieval|Zeitaufwand (in Millisekunden) für das Abfragen der Daten, das Verarbeiten des Berichts und das Rendern des Berichts.|  
|TimeProcessing||  
|TimeRendering||  
|Quelle|Quelle der Berichtsausführung (1=Live, 2=Cache, 3=Snapshot 4=History).|  
|Status|Status (entweder rsSuccess oder ein Fehlercode; beim Auftreten mehrerer Fehler wird nur der erste Fehler aufgezeichnet).|  
|ByteCount|Größe von gerenderten Berichten in Bytes.|  
|RowCount|Anzahl der von Abfragen zurückgegebenen Zeilen.|  
|AdditionalInfo|Ein XML-Eigenschaftenbehälter, der weitere Informationen zur Ausführung enthält.|  
  
##  <a name="bkmk_executionlog"></a> Protokollierungsfelder (ExecutionLog)  
 Folgendes ist eine Beispiel-Transact-SQL-Anweisung, mit der Sie Zeilen aus der Ansicht ExecutionLog abrufen können. Im Beispiel wird davon ausgegangen, dass der Name der Berichtsserver-Datenbank **ReportServer**lautet:  
  
```  
Use ReportServer  
select * from ExecutionLog order by TimeStart DESC  
  
```  
  
 In der folgenden Tabelle werden die Daten beschrieben, die im Berichtsausführungsprotokoll aufgezeichnet werden  
  
|Column|Description|  
|------------|-----------------|  
|InstanceName|Name der Berichtsserverinstanz, die die Anforderung verarbeitet hat.|  
|ReportID|Berichts-ID.|  
|UserName|Benutzer-ID.|  
|RequestType|Mögliche Werte:<br /><br /> True = Eine Abonnementanforderung<br /><br /> False = Eine interaktive Anforderung|  
|Format|Renderingformat.|  
|Parameter|Parameterwerte, die für die Berichtsausführung verwendet werden.|  
|TimeStart|Anfangs- und Beendigungszeit für die Verarbeitung eines Berichts.|  
|TimeEnd||  
|TimeDataRetrieval|Zeitaufwand (in Millisekunden) für das Abfragen der Daten, das Verarbeiten des Berichts und das Rendern des Berichts.|  
|TimeProcessing||  
|TimeRendering||  
|Quelle|Quelle der Berichtsausführung. Mögliche Werte: (1=Live, 2=Cache, 3=Snapshot, 4=History, 5=Adhoc, 6=Session, 7=RDCE).|  
|Status|Mögliche Werte: rsSuccess, rsProcessingAborted oder ein Fehlercode. Wenn mehrere Fehler auftreten, wird nur der erste Fehler aufgezeichnet.|  
|ByteCount|Größe von gerenderten Berichten in Bytes.|  
|RowCount|Anzahl der von Abfragen zurückgegebenen Zeilen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivieren von Reporting Services-Ereignissen für das SharePoint-Ablaufverfolgungsprotokoll &#40;ULS&#41;](../../reporting-services/report-server/turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)   
 [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Fehler- und Ereignisreferenz &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
