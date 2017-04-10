---
title: "Ablaufverfolgung (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45823fc8-723a-49f2-9a11-94d241245cfd
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "erikre"
caps.handback.revision: 7
---
# Ablaufverfolgung (Master Data Services)
  Die Datei "Web.config" enthält einen Ablaufverfolgungsabschnitt, wie unten dargestellt. Dieser Abschnitt ist neu in . [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
```  
<sources>  
      <!-- Adjust the switch value to control the types of messages that should be logged.   
           http://msdn.microsoft.com/en-us/library/system.diagnostics.sourcelevels  
           Use the a switchValue of Verbose to generate a full log. Please be aware that   
           the trace file can get quite large very quickly -->  
      <source name="MDS" switchType="System.Diagnostics.SourceSwitch" switchValue="Warning, ActivityTracing">  
        <listeners>  
          <!-- Set a directory path where the service account you chose while setting up Master Data Services has read and write privileges.  
               Default path is Logs in WebApplication folder, for example C:\Program Files\Microsoft SQL Server\130\Master Data Services\WebApplication  
               New log file will be created every day or every 10 mb.  
               When directory size hits the 200mb limitation, the oldest file will be deleted.-->  
          <add name="FileTraceListener"  
               type="Microsoft.MasterDataServices.Core.Logging.FileTraceListener, Microsoft.MasterDataServices.Core"   
               initializeData="DirectoryPath = Logs; FileSizeInMb = 10; MaxDirectorySizeInMb = 200"/>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
  
```  
  
 Folgendes Verhalten ist das Standardverhalten für die Ablaufverfolgung.  
  
-   Ablaufverfolgung wird für Warnungs- und ActivityTracing-Nachrichten aktiviert.  
  
     Weitere Informationen finden Sie unter [SourceLevels-Enumeration](https://msdn.microsoft.com/en-us/library/system.diagnostics.sourcelevels).  
  
-   Die Protokolle werden im Ordner "Logs" unter dem Ordner "WebApplication" gespeichert. Der Standardspeicherort ist "C:\Programme\Microsoft SQL Server\130\Master Data Services\WebApplication\Logs".  
  
-   Die Datei wird für jeden Tag oder für jeweils 10 MB erstellt.  
  
-   Wenn die Größe 200 MB erreicht, wird das älteste Protokoll gelöscht.  
  
-   Das Protokollformat ist CSV. In der folgenden Tabelle wird das Protokollformat beschrieben.  
  
    |Element|Description|  
    |-------------|-----------------|  
    |Zeit|Zeitpunkt des Ablaufverfolgungseintrags.|  
    |CorrelationID|Eine Korrelations-ID wird für jede Anforderung zugewiesen. Alle Ablaufverfolgungen, die durch diese Anforderung ausgelöst werden, haben die gleiche Korrelations-ID.<br /><br /> Tritt ein Fehler in der Benutzeroberfläche auf, wird die Korrelations-ID in der Fehlermeldung angezeigt.|  
    |Vorgang|Vorgangsname anfordern. Wenn die Anforderung eine Web-UI-Anforderung ist, ist der Vorgangsname die URL. Wenn die Anforderung eine API-Anforderung ist, ist der Vorgangsname der Dienstname.|  
    |Ebene|Ebene dieses Ablaufverfolgungseintrags.|  
    |MessageBox|Nachrichtentext der Ablaufverfolgung|  
  
## Externe Ressourcen  
 Blogbeitrag [Troubleshooting Logging Improvement](http://go.microsoft.com/fwlink/p/?LinkId=615377) (Problembehandlung der Protokollierungsverbesserung) auf msdn.com.  
  
  