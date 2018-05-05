---
title: Konfigurieren von Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: distributed-replay
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aee11dde-daad-439b-b594-9f4aeac94335
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f60d8849c32aa52ac2dba616a17d0e1e6fc4734b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="configure-distributed-replay"></a>Konfigurieren von Distributed Replay
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Die Konfigurationsdetails für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay werden in XML-Dateien auf dem Distributed Replay-Controller, den Clients und am Installationsort des Verwaltungstools angegeben. Hierzu gehören die folgenden Dateien:  
  
-   [Controllerkonfigurationsdatei](#DReplayController)  
  
-   [Clientkonfigurationsdatei](#DReplayClient)  
  
-   [Vorverarbeitungskonfigurationsdatei](#PreprocessConfig)  
  
-   [Wiedergabekonfigurationsdatei](#ReplayConfig)  
  
##  <a name="DReplayController"></a> Controllerkonfigurationsdatei: DReplayController.config  
 Beim Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller-Diensts wird der Protokolliergrad aus der Controllerkonfigurationsdatei `DReplayController.config`geladen. Diese Datei befindet sich in dem Ordner, in dem Sie den Distributed Replay Controller-Dienst installiert haben:  
  
 **\<Controllerinstallationspfad>\DReplayController.config**  
  
 Der in der Controllerkonfigurationsdatei angegebene Protokolliergrad enthält die folgenden Informationen:  
  
|Einstellung|XML-Element|Description|Zulässige Werte|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Protokolliergrad|`<LoggingLevel>`|Gibt den Protokolliergrad für den Controllerdienst an.|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|Nein. Der Standardwert ist `CRITICAL`.|  
  
### <a name="example"></a>Beispiel  
 In diesem Beispiel wird eine Controllerkonfigurationsdatei gezeigt, die geändert wurde, um `INFORMATION` - und `WARNING` -Protokolleinträge zu unterdrücken.  
  
```  
<?xml version='1.0'?>  
<Options>  
<LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="DReplayClient"></a> Clientkonfigurationsdatei: DReplayClient.config  
 Beim Starten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay-Clientdiensts werden Konfigurationseinstellungen aus der Clientkonfigurationsdatei `DReplayClient.config`geladen. Diese Datei befindet sich auf jedem Client in dem Ordner, in dem Sie den Distributed Replay-Clientdienst installiert haben:  
  
 **\<Clientinstallationspfad>\DReplayClient.config**  
  
 In der Clientkonfigurationsdatei werden die folgenden Einstellungen angegeben:  
  
|Einstellung|XML-Element|Description|Zulässige Werte|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Controller|`<Controller>`|Gibt den Computernamen des Controllers an. Der Client versucht, sich durch Herstellen einer Verbindung mit dem Controller bei der Distributed Replay Utility-Umgebung zu registrieren.|Sie können mit "`localhost`" oder "`.`" auf den lokalen Computer verweisen.|Nein. Standardmäßig versucht der Client, sich bei der Controllerinstanz zu registrieren, die lokal ("`.`") ausgeführt wird, sofern sie vorhanden ist.|  
|Clientarbeitsverzeichnis|`<WorkingDirectory>`|Der lokale Pfad auf dem Client, unter dem die Dispatchdateien gespeichert werden.<br /><br /> Die Dateien in diesem Verzeichnis werden bei der nächsten Wiedergabe überschrieben.|Ein vollständiger Verzeichnisname, der mit dem Laufwerkbuchstaben beginnt.|Nein. Wenn kein Wert angegeben ist, werden die Dispatchdateien am selben Speicherort wie die Standardclientkonfigurationsdatei gespeichert. Wenn ein Wert angegeben wird und dieser Ordner nicht auf dem Client vorhanden ist, wird der Clientdienst nicht gestartet.|  
|Clientergebnisverzeichnis|`<ResultDirectory>`|Der lokale Pfad auf dem Client, unter dem die Ergebnisdatei der Ablaufverfolgung aus der Wiedergabeaktivität (für den Client) gespeichert wird.<br /><br /> Die Dateien in diesem Verzeichnis werden bei der nächsten Wiedergabe überschrieben.|Ein vollständiger Verzeichnisname, der mit dem Laufwerkbuchstaben beginnt.|Nein. Wenn kein Wert angegeben ist, wird die Ergebnisdatei der Ablaufverfolgung am selben Speicherort wie die Standardclientkonfigurationsdatei gespeichert. Wenn ein Wert angegeben wird und dieser Ordner nicht auf dem Client vorhanden ist, wird der Clientdienst nicht gestartet.|  
|Protokolliergrad|`<LoggingLevel>`|Der Protokolliergrad für den Clientdienst.|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|Nein. Der Standardwert ist `CRITICAL`.|  
  
### <a name="example"></a>Beispiel  
 In diesem Beispiel wird eine Clientkonfigurationsdatei gezeigt, die geändert wurde, um anzugeben, dass der Controllerdienst auf einem anderen Computer (mit dem Namen `Controller1`) ausgeführt wird. Das `WorkingDirectory` -Element und das `ResultDirectory` -Element wurden für die Verwendung des Ordners `c:\ClientWorkingDir` bzw. `c:\ResultTraceDir`konfiguriert. Der Standardwert des Protokolliergrads wurde geändert, um `INFORMATION` - und `WARNING` -Protokolleinträge zu unterdrücken.  
  
```  
<?xml version='1.0'?>  
<Options>  
    <Controller>Controller1</Controller>  
    <WorkingDirectory>c:\ClientWorkingDir</WorkingDirectory>  
    <ResultDirectory>c:\ResultTraceDir</ResultDirectory>  
    <LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="PreprocessConfig"></a> Vorverarbeitungskonfigurationsdatei: DReplay.exe.preprocess.config  
 Wenn Sie das Verwaltungstool verwenden, um die Vorverarbeitungsphase zu initiieren, lädt das Verwaltungstool die Vorverarbeitungseinstellungen aus der Vorverarbeitungskonfigurationsdatei `DReplay.exe.preprocess.config`.  
  
 Verwenden Sie die Standardkonfigurationsdatei oder den Parameter **-c** des Verwaltungstools, um den Speicherort einer geänderten Vorverarbeitungskonfigurationsdatei anzugeben. Weitere Informationen zur Verwendung der Vorverarbeitungsoption des Verwaltungstools finden Sie unter [Vorverarbeitungsoption &#40;Verwaltungstool „Distributed Replay“&#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md).  
  
 Die Standardkonfigurationsdatei für die Vorverarbeitung befindet sich in dem Ordner, in dem Sie das Verwaltungstool installiert haben:  
  
 **\<Installationspfad des Verwaltungstools>\DReplayAdmin\DReplay.exe.preprocess.config**  
  
 Die Vorverarbeitungskonfigurationseinstellungen werden in XML-Elementen angegeben, die untergeordnete Elemente des `<PreprocessModifiers>` -Elements in der Vorverarbeitungskonfigurationsdatei sind. Dazu gehören folgende Einstellungen:  
  
|Einstellung|XML-Element|Description|Zulässige Werte|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Systemsitzungsaktivitäten einschließen|`<IncSystemSession>`|Gibt an, ob Systemsitzungsaktivitäten während der Aufzeichnung in die Wiedergabe eingeschlossen werden.|`Yes` &#124; `No`|Nein. Der Standardwert ist `No`.|  
|Maximale Leerlaufzeit|`<MaxIdleTime>`|Legt die maximale Leerlaufzeit auf eine absolute Zahl (in Sekunden) fest.|Eine ganze Zahl >= -1.<br /><br /> `-1` gibt an, dass der ursprüngliche Wert in der ursprünglichen Ablaufverfolgungsdatei unverändert bleibt.<br /><br /> `0` gibt an, dass zu einem beliebigen Zeitpunkt Aktivitäten erfolgen.|Nein. Der Standardwert ist `-1`.|  
  
### <a name="example"></a>Beispiel  
 Die Standardkonfigurationsdatei für die Vorverarbeitung:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
##  <a name="ReplayConfig"></a> Wiedergabekonfigurationsdatei: DReplay.exe.replay.config  
 Wenn Sie das Verwaltungstool verwenden, um die Ereigniswiedergabephase zu initiieren, lädt das Verwaltungstool die Wiedergabeeinstellungen aus der Wiedergabekonfigurationsdatei `DReplay.exe.replay.config`.  
  
 Verwenden Sie die Standardkonfigurationsdatei oder den Parameter **-c** des Verwaltungstools, um den Speicherort einer geänderten Wiedergabekonfigurationsdatei anzugeben. Weitere Informationen zur Verwendung der Wiedergabeoption des Verwaltungstools finden Sie unter [Wiedergabeoption &#40;Verwaltungstool „Distributed Replay“&#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md).  
  
 Die Standardkonfigurationsdatei für die Wiedergabe befindet sich in dem Ordner, in dem Sie das Verwaltungstool installiert haben:  
  
 **\<Installationspfad des Verwaltungstools>\DReplayAdmin\DReplay.exe.replay.config**  
  
 Die Wiedergabekonfigurationseinstellungen werden in XML-Elementen angegeben, die untergeordnete Elemente des `<ReplayOptions>` -Elements und des `<OutputOptions>` -Elements der Wiedergabekonfigurationsdatei sind.  
  
### <a name="replayoptions-element"></a>\<ReplayOptions >-Element  
 Im `<ReplayOptions>` -Element der Wiedergabekonfigurationsdatei werden die folgenden Einstellungen angegeben:  
  
|Einstellung|XML-Element|Description|Zulässige Werte|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (der Testserver)|`<Server>`|Gibt den Namen des Servers und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz an, mit der eine Verbindung hergestellt werden soll.|*Servername*[\\*Instanzname*]<br /><br /> Sie können zum Darstellen des lokalen Hosts nicht "`localhost`" oder "`.`" verwenden.|Nein, wenn der Servername bereits mit dem **-s***target server*-Parameter für die **replay**-Option des Verwaltungstools angegeben wurde.|  
|Sequenzierungsmodus|`<SequencingMode>`|Gibt den für die Ereignisplanung verwendeten Modus an.|`synchronization` &#124; `stress`|Nein. Der Standardwert ist `stress`.|  
|Belastungsskalagranularität|`<StressScaleGranularity>`|Gibt an, ob im Belastungsmodus alle Verbindungen auf dem Dienstprofilbezeichner (Service Profile Identifier, SPID) zusammen (SPID) oder unabhängig voneinander (Verbindung) skaliert werden sollen.|SPID &#124; Verbindung|Ja. Der Standardwert ist `SPID`.|  
|Verbindungszeitskala|`<ConnectTimeScale>`|Wird verwendet, um die Verbindungszeit im Belastungsmodus zu skalieren.|Eine ganze Zahl zwischen `1` und `100`.|Nein. Der Standardwert ist `100`.|  
|Reaktionszeitskala|`<ThinkTimeScale>`|Dient zum Skalieren der Reaktionszeit im Belastungsmodus.|Eine ganze Zahl zwischen `0` und `100`.|Nein. Der Standardwert ist `100`.|  
|Verbindungspooling verwenden|`<UseConnectionPooling>`|Gibt an, ob Verbindungspooling auf jedem Distributed Replay-Client aktiviert wird.|Ja &#124; Nein|Ja. Der Standardwert ist `Yes`.|  
|Systemüberwachungsintervall|`<HealthmonInterval>`|Gibt an (in Sekunden), wie oft die Systemüberwachung ausgeführt werden soll.<br /><br /> Dieser Wert wird nur im Synchronisierungsmodus verwendet.|Ganze Zahl >= 1<br /><br /> (zum Deaktivieren`-1` )|Nein. Der Standardwert ist `60`.|  
|Timeout der Abfrage|`<QueryTimeout>`|Gibt den Wert für das Timeout der Abfrage in Sekunden an. Dieser Wert ist nur wirksam, bis die erste Zeile zurückgegeben wurde.|Ganze Zahl >= 1<br /><br /> (zum Deaktivieren`-1` )|Nein. Der Standardwert ist `3600`.|  
|Threads pro Client|`<ThreadsPerClient>`|Gibt die Anzahl der Wiedergabethreads an, die für jeden Wiedergabeclient verwendet werden sollen.|Eine ganze Zahl zwischen `1` und `512`.|Nein. Wenn kein Wert angegeben ist, wird von Distributed Replay der Wert `255`verwendet.|  
  
### <a name="outputoptions-element"></a>\<OutputOptions >-Element  
 Im `<OutputOptions>` -Element der Wiedergabekonfigurationsdatei werden die folgenden Einstellungen angegeben:  
  
|Einstellung|XML-Element|Description|Zulässige Werte|Required|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Zeilenanzahl aufzeichnen|`<RecordRowCount>`|Gibt an, ob die Zeilenanzahl für jedes Resultset aufgezeichnet werden soll.|`Yes` &#124; `No`|Nein. Der Standardwert ist `Yes`.|  
|Resultset aufzeichnen|`<RecordResultSet>`|Gibt an, ob der Inhalt aller Resultsets aufgezeichnet werden soll.|`Yes` &#124; `No`|Nein. Der Standardwert ist `No`.|  
  
### <a name="example"></a>Beispiel  
 Die Standardkonfigurationsdatei für die Wiedergabe:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server></Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Befehlszeilenoptionen für das Verwaltungstool &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [SQL Server Distributed Replay Forum](http://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Verwenden von Distributed Replay für den Auslastungstest von SQL Server: Teil 2](http://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Verwenden von Distributed Replay für den Auslastungstest von SQL Server – Teil 1](http://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
