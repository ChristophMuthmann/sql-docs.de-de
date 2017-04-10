---
title: "WMI-Datenleser (Task) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.wmidatareadertask.f1"
helpviewer_keywords: 
  - "WQL [Integration Services]"
  - "WMI-Datenleser (Task) [Integration Services]"
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# WMI-Datenleser (Task)
  Der Task WMI-Datenleser führt Abfragen mithilfe von WQL (WMI Query Language) aus, womit Informationen von WMI zu einem Computersystem zurückgegeben werden. Der Task WMI-Datenleser kann für folgende Zwecke verwendet werden:  
  
-   Abfragen der Windows-Ereignisprotokolle auf einem lokalen Computer oder einem Remotecomputer und Schreiben der Informationen in eine Datei oder Variable.  
  
-   Abrufen von Informationen zum Vorhandensein, zum Status oder zu Eigenschaften von Hardwarekomponenten und Ermitteln mithilfe dieser Informationen, ob andere Tasks in der Ablaufsteuerung ausgeführt werden sollten.  
  
-   Abrufen einer Liste der Anwendungen und Ermitteln der installierten Version jeder Anwendung.  
  
 Es gibt folgende Möglichkeiten, um den Task WMI-Datenleser zu konfigurieren:  
  
-   Geben Sie den zu verwendenden WMI-Verbindungs-Manager an.  
  
-   Geben Sie die Quelle der WQL-Abfrage an. Die Abfrage kann in einer Taskeigenschaft gespeichert sein, die Abfrage kann aber auch außerhalb des Tasks in einer Variablen oder einer Datei gespeichert sein.  
  
-   Definieren Sie das Format der WQL-Abfrageergebnisse. Der Task unterstützt ein Tabellen-, Eigenschaftsname/Wert-Paar- oder Eigenschaftswertformat.  
  
-   Geben Sie das Ziel der Abfrage an. Das Ziel kann eine Variable oder eine Datei sein.  
  
-   Geben Sie an, ob das Abfrageziel überschrieben, beibehalten oder angefügt wird.  
  
 Falls es sich bei der Quelle oder dem Ziel um eine Datei handelt, verwendet der Task WMI-Datenleser einen Dateiverbindungs-Manager zum Herstellen einer Verbindung mit der Datei. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Der Task WMI-Datenleser verwendet einen WMI-Verbindungs-Manager zum Herstellen einer Verbindung mit dem Server, von dem er WMI-Informationen liest. Weitere Informationen finden Sie unter [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
## WQL-Abfrage  
 WQL ist ein Dialekt von SQL mit Erweiterungen zur Unterstützung der WMI-Ereignisbenachrichtigung und sonstigen WMI-spezifischen Funktionen. Weitere Informationen zu WQL finden Sie in der WMI-Dokumentation in der [MSDN Library](http://go.microsoft.com/fwlink/?linkid=7022).  
  
> [!NOTE]  
>  Die WMI-Klassen variieren in den verschiedenen Windows-Versionen.  
  
 Die folgende WQL-Abfrage gibt Einträge aus dem Anwendungsereignisprotokoll zurück.  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 Die folgende WQL-Abfrage gibt Informationen zum logischen Datenträger zurück.  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 Die folgende WQL-Abfrage gibt eine Liste der QFE-Updates (Quick Fix Engineering) für das Betriebssystem zurück.  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## Verfügbare benutzerdefinierte Meldungen für die Protokollierung für den Task 'WMI-Datenleser'  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task WMI-Datenleser aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Zeigt an, dass das Lesen der WMI-Daten begonnen wurde.|  
|**WMIDataReaderOperation**|Berichtet die vom Task ausgeführte WQL-Abfrage.|  
  
## Konfiguration des Tasks "WMI-Datenleser"  
 Eigenschaften können Sie programmgesteuert oder mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „WMI-Datenleser“ &#40;Seite „WMI-Optionen“&#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## Verwandte Aufgaben  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  