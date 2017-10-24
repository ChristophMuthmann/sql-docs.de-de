---
title: "Vorgänge in Analysis Services protokolliert | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: aa1db060-95dc-4198-8aeb-cffdda44b140
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e23d96e675fba4ed740b8adbb8402d3ae7fd06e2
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="log-operations-in-analysis-services"></a>Protokollvorgänge in Analysis Services
  Eine Analysis Services-Instanz protokolliert Serverbenachrichtigungen, Fehler und Warnungen in der Datei "msmdsrv.log" – eine Datei für jede Instanz, die Sie installieren. Administratoren finden in diesem Protokoll Einblicke in routinemäßige und außergewöhnliche Ereignisse. In neueren Versionen wurde die Protokollierung verbessert, um weitere Informationen zu erfassen. Protokolldatensätze enthalten jetzt die Produktversion und Editionsinformationen sowie Prozessor, Speicher, Konnektivität und blockierende Ereignisse. Sie können die gesamte Änderungsliste unter [Protokollierungsverbesserungen](http://support.microsoft.com/kb/2965035)einsehen.  
  
 Neben dem integrierten Protokollierungsfeature verwenden viele Administratoren und Entwickler auch die von der Analysis Services-Community bereitgestellten Tools zum Sammeln von Daten zu Servervorgängen, wie z.B. **ASTrace**. Die Download-Links finden Sie unter [Microsoft SQL Server Community Samples: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/) (Microsoft SQL Server-Community-Beispiele: Analysis Services).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Speicherort und Arten von Protokollen](#bkmk_location)  
  
-   [Allgemeine Informationen zu den Konfigurationseinstellungen der Protokolldatei](#bkmk_general)  
  
-   [MSMDSRV-Dienstprotokolldatei](#bkmk_msmdsrv)  
  
-   [Abfrageprotokolle](#bkmk_querylog)  
  
-   [Miniabbilddateien (.mdmp)](#bkmk_mdmp)  
  
-   [Tipps und Best Practices](#bkmk_tips)  
  
> [!NOTE]  
>  Wenn Sie Informationen zur Protokollierung suchen, interessiert Sie möglicherweise auch die Ablaufverfolgung von Vorgängen, die Verarbeitungs- und Abfrageausführungspfade anzeigen. Ablaufverfolgungsobjekte für die Ad-hoc- und die andauernde Ablaufverfolgung (z.B. Überwachung des Cubezugriffs), sowie Empfehlungen dazu, wie Sie Flight Recorder, SQL Server Profiler und xEvents optimal verwenden, finden Sie über die Links auf dieser Seite: [Überwachen einer Analysis Services-Instanz](../../analysis-services/instances/monitor-an-analysis-services-instance.md).  
  
##  <a name="bkmk_location"></a> Speicherort und Arten von Protokollen  
 Analysis Services stellt die unten beschriebenen Protokolle zur Verfügung.  
  
|Dateiname oder Speicherort|Typ|Syntaxelemente|Standardmäßig ein|  
|---------------------------|----------|--------------|-------------------|  
|Msmdsrv.log|Fehlerprotokoll|Routinemäßige Überwachung und grundlegende Problembehandlung|Ja|  
|OlapQueryLog-Tabelle in einer relationalen Datenbank|Abfrageprotokoll|Sammeln von Eingaben für den Assistenten für die Nutzungsoptimierung|Nein|  
|SQLDmp\<Guid > .mdmp-Dateien|Abstürze und Ausnahmen|Umfassende Problembehandlung|Nein|  
  
 Es wird dringend empfohlen, den folgenden Link für zusätzliche Informationsquellen zu nutzen, die in diesem Thema nicht behandelt werden: [Initial data collection tips from Microsoft Support](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)(Tipps vom Microsoft Support zur anfänglichen Datensammlung).  
  
##  <a name="bkmk_general"></a> Allgemeine Informationen zu den Konfigurationseinstellungen der Protokolldatei  
 Sie finden Abschnitte für jedes Protokoll in der Serverkonfigurationsdatei "msmdsrv.ini" im Verzeichnis "\Programme\Microsoft SQL Server\MSAS13.MSSQLSERVER\OLAP\Config folder". Anweisungen zum Bearbeiten der Datei finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md) .  
  
 Wenn möglich wird empfohlen, die Eigenschaften für die Protokollierung auf der Servereigenschaftenseite von Management Studio festzulegen. In einigen Fällen müssen Sie die Datei "msmdsrv.ini" jedoch direkt bearbeiten, um Einstellungen zu konfigurieren, die nicht in den Verwaltungstools angezeigt werden.  
  
 ![Abschnitt der Config-Datei mit protokolleinstellungen](../../analysis-services/instances/media/ssas-logfilesettings.png "Abschnitt der Config-Datei mit protokolleinstellungen")  
  
##  <a name="bkmk_msmdsrv"></a> MSMDSRV-Dienstprotokolldatei  
 Analysis Services protokolliert Servervorgänge in der Datei „msmdsrv.log“ (eine pro Instanz) im Verzeichnis „\Programme\Microsoft SQL Server\\<Instanz\>\Olap\Log“.  
  
 Diese Protokolldatei wird bei jedem Dienstneustart geleert. In früheren Versionen mussten Administratoren manchmal den Dienst neu starten, nur um die Protokolldatei zu leeren, bevor sie so groß wurde, dass sie nicht mehr verwendet werden konnte. Dies ist nicht mehr erforderlich. Mit den Konfigurationseinstellungen, die in SQL Server 2012 SP2 und höher eingeführt wurden, erhalten Sie die Kontrolle über die Größe der Protokolldatei und des dazugehörigen Verlaufs:  
  
-   **MaxFileSizeMB** gibt die maximale Protokolldateigröße in Megabytes an. Der Standardwert ist 256. Ein gültiger Ersatzwert muss eine positive ganze Zahl sein. Wenn **MaxFileSizeMB** erreicht ist, benennt Analysis Services die aktuelle Datei in „msmdsrv{aktueller Zeitstempel}.log“ um und beginnt eine neue Datei „msmdsrv.log“.  
  
-   **MaxNumberFiles** gibt die Aufbewahrung älterer Protokolldateien an. Der Standardwert ist 0 (deaktiviert). Sie können den Wert in eine positive ganze Zahl ändern, um Versionen der Protokolldatei beizubehalten. Wenn **MaxNumberFiles** erreicht ist, löscht Analysis Services die Datei mit dem ältesten Zeitstempel im Namen.  
  
 Um diese Einstellungen zu verwenden, führen Sie folgende Schritte aus:  
  
1.  Öffnen Sie die Datei "msmdsrv.ini" im Editor.  
  
2.  Kopieren Sie die folgenden zwei Zeilen:  
  
    ```  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    ```  
  
3.  Fügen Sie diese zwei Zeilen in den Abschnitt "Log" der Datei "msmdsrv.ini" ein, unterhalb des Dateinamens für "msmdsrv.log". Beide Einstellungen müssen manuell hinzugefügt werden. Es gibt keine Platzhalter dafür in der Datei "msmdsrv.ini".  
  
     Die geänderte Konfigurationsdatei sollte wie folgt aussehen:  
  
    ```  
    <Log>  
    <File>msmdsrv.log</File>  
    <MaxFileSizeMB>256</MaxFileSizeMB>  
    <MaxNumberOfLogFiles>5</MaxNumberOfLogFiles>  
    <FileBufferSize>0</FileBufferSize>  
  
    ```  
  
4.  Bearbeiten Sie die Werte bei Bedarf.  
  
5.  Speichern Sie die Datei.  
  
6.  Starten Sie den Dienst neu.  
  
##  <a name="bkmk_querylog"></a> Abfrageprotokolle  
 Der Begriff "Abfrageprotokoll" ist ein wenig irreführend, da hierin keine der MDX- oder DAX-Abfrageaktivitäten Ihrer Benutzer protokolliert werden. Stattdessen sammelt dieses Protokoll Daten zu von Analysis Services generierten Abfragen, die anschließend als Dateneingabe im verwendungsbasierten Optimierung-Assistenten verwendet werden. Die im Abfrageprotokoll gesammelten Daten dienen nicht zur direkten Analyse. Insbesondere werden die Datasets in Bitarrays beschrieben, wobei eine 0 oder 1 angibt, welche Teile des Datasets in der Abfrage enthalten sind. Diese Daten sind für den Assistenten vorgesehen.  
  
 Bei der Abfrageüberwachung und Problembehandlung verwenden viele Entwickler und Administratoren das Communitytool **ASTrace**zum Überwachen von Abfragen. Sie können auch SQL Server Profiler, xEvents oder eine Analysis Services-Ablaufverfolgung verwenden. Links zu weiteren Informationen finden Sie unter [Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md) .  
  
 Wann sollten Sie das Abfrageprotokoll verwenden? Es wird empfohlen, das Abfrageprotokoll im Rahmen einer Übung zur Abfrageleistungsoptimierung zu aktivieren, die den verwendungsbasierten Optimierung-Assistenten umfasst. Das Abfrageprotokoll ist erst vorhanden, nachdem Sie das Feature aktiviert, die unterstützenden Datenstrukturen erstellt und Eigenschaften festgelegt haben, die von Analysis Services zum Suchen und Ausfüllen des Protokolls verwendet werden.  
  
 Führen Sie die folgenden Schritte aus, um das Abfrageprotokoll zu aktivieren:  
  
1.  Erstellen Sie eine relationale SQL Server-Datenbank zum Speichern des Abfrageprotokolls.  
  
2.  Gewähren Sie dem Analysis Services-Dienstkonto ausreichende Berechtigungen für die Datenbank. Das Konto benötigt die Berechtigung zum Erstellen einer Tabelle, zum Schreiben in die Tabelle und zum Lesen aus der Tabelle.  
  
3.  Klicken Sie in SQL Server Management Studio mit der rechten Maustaste auf **Analysis Services** | **Eigenschaften** | **Allgemein**, und legen Sie **CreateQueryLogTable** auf „true“ fest.  
  
4.  Ändern Sie ggf. **QueryLogSampling** oder **QueryLogTableName** , wenn Sie Stichprobenabfragen mit einer anderen Rate durchführen oder einen anderen Namen für die Tabelle verwenden möchten.  
  
 Die Abfrageprotokolltabelle wird erst dann erstellt, wenn Sie genügend MDX-Abfragen zur Erfüllung der Stichprobenanforderungen ausgeführt haben. Wenn Sie z. B. den Standardwert 10 beibehalten, müssen Sie mindestens zehn Abfragen ausführen, bevor die Tabelle erstellt wird.  
  
 Die Abfrageprotokolleinstellungen gelten serverweit. Die von Ihnen angegebenen Einstellungen werden von allen auf diesem Server ausgeführten Datenbanken verwendet.  
  
 ![Abfrage-protokolleinstellungen in Management Studio](../../analysis-services/instances/media/ssas-querylogsettings.png "abfrageprotokolleinstellungen in Management Studio")  
  
 Führen Sie nach der Festlegen der Konfigurationseinstellungen mehrmals eine MDX-Abfrage aus. Wenn die Stichprobenanforderung auf 10 festgelegt sind, wird führen Sie die Abfrage elf Mal aus. Überprüfen Sie, ob die Tabelle erstellt wurde. Stellen Sie in Management Studio eine Verbindung mit dem relationalen Datenbankmodul her, öffnen Sie den Datenbankordner, öffnen Sie den Ordner **Tabellen** , und überprüfen Sie, ob **OlapQueryLog** vorhanden ist. Wenn Sie die Tabelle nicht sofort sehen, aktualisieren Sie den Ordner, um Änderungen am Inhalt zu übernehmen.  
  
 Lassen Sie das Abfrageprotokoll ausreichend Daten für den verwendungsbasierten Optimierung-Assistenten sammeln. Wenn die Abfragemengen zyklisch sind, erfassen Sie genügend Datenverkehr, um eine repräsentative Menge von Daten zu erhalten. Anweisungen zum Ausführen des Assistenten finden Sie unter [Assistent für verwendungsbasierte Optimierung](https://msdn.microsoft.com/library/ms189706.aspx) .  
  
 Weitere Informationen zur Abfrageprotokollkonfiguration finden Sie unter [Konfigurieren des Abfrageprotokolls von Analysis Services](http://technet.microsoft.com/library/Cc917676) . Dieses Dokument ist zwar ziemlich alt, die Abfrageprotokollkonfiguration hat sich jedoch in neueren Versionen nicht geändert, und die darin enthaltenen Informationen gelten weiterhin.  
  
##  <a name="bkmk_mdmp"></a> Miniabbilddateien (.mdmp)  
 Abbilddateien erfassen Daten, die für die Analyse außergewöhnlicher Ereignisse verwendet werden. Analysis Services generiert automatisch Miniabbilder (.mdmp) als Reaktion auf einen Serverabsturz oder bei Ausnahme- und einigen Konfigurationsfehlern. Das Feature ist aktiviert, sendet aber Absturzberichte nicht automatisch.  
  
 Absturzberichte werden über den Abschnitt "Exception" in der Datei "Msmdsrv.ini" konfiguriert. Diese Einstellungen steuern die Generierung von Abbilddateien des Arbeitsspeichers. Der folgende Codeausschnitt zeigt die Standardwerte:  
  
```  
<Exception>  
<CreateAndSendCrashReports>1</CreateAndSendCrashReports>  
<CrashReportsFolder/>  
<SQLDumperFlagsOn>0x0</SQLDumperFlagsOn>  
<SQLDumperFlagsOff>0x0</SQLDumperFlagsOff>  
<MiniDumpFlagsOn>0x0</MiniDumpFlagsOn>  
<MiniDumpFlagsOff>0x0</MiniDumpFlagsOff>  
<MinidumpErrorList>0xC1000000, 0xC1000001, 0xC102003F, 0xC1360054, 0xC1360055</MinidumpErrorList>  
<ExceptionHandlingMode>0</ExceptionHandlingMode>  
<CriticalErrorHandling>1</CriticalErrorHandling>  
<MaxExceptions>500</MaxExceptions>  
<MaxDuplicateDumps>1</MaxDuplicateDumps>  
</Exception>  
```  
  
 **Konfigurieren von Absturzberichten**  
  
 Sofern vom Microsoft Support nicht anders angegeben, verwenden die meisten Administratoren die Standardeinstellungen. Der ältere KB-Artikel bietet weiterhin Anweisungen zum Konfigurieren von Abbilddateien: [Konfigurieren von Analysis Services zum Generieren von Speicherabbilddateien](http://support.microsoft.com/kb/919711).  
  
 Die Konfigurationseinstellung, die wahrscheinlich geändert werden muss, ist die **CreateAndSendCrashReports** -Einstellung, die bestimmt, ob eine Speicherabbilddatei generiert wird.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Deaktiviert die Speicherabbilddatei. Alle anderen Einstellungen im Abschnitt "Exception" werden ignoriert.|  
|1|(Standard) Aktiviert die Speicherabbilddatei, sendet sie aber nicht.|  
|2|Aktiviert das Feature und sendet automatisch einen Fehlerbericht an Microsoft.|  
  
 **CrashReportsFolder** ist der Speicherort der Abbilddateien. Standardmäßig werden MDMP-Dateien und die zugehörigen Protokolldatensätze im Ordner "\Olap\Log" gespeichert.  
  
 **SQLDumperFlagsOn** wird verwendet, um ein vollständiges Speicherabbild zu generieren. Vollständige Speicherabbilder sind standardmäßig nicht aktiviert. Sie können diese Eigenschaft auf **0x34**festlegen.  
  
 Die folgenden Links enthalten weitere Hintergrundinformationen:  
  
-   [Tiefere Einblicke in SQL Server mithilfe von Miniabbildern](http://blogs.msdn.com/b/sqlcat/archive/2009/09/11/looking-deeper-into-sql-server-using-minidumps.aspx)  
  
-   [Erstellen einer Abbilddatei für den Benutzermodus](http://support.microsoft.com/kb/931673)  
  
-   [Verwenden des Hilfsprogramms Sqldumper.exe zum Erstellen einer Abbilddatei in SQL Server](http://support.microsoft.com/kb/917825)  
  
##  <a name="bkmk_tips"></a> Tipps und Best Practices  
 In diesem Abschnitt werden kurz die Tipps aus diesem Artikel zusammengefasst.  
  
-   Konfigurieren Sie die Datei "msmdsrv.log", um die Größe und Anzahl der msmdsrv-Protokolldateien zu steuern. Die Einstellungen sind nicht standardmäßig aktiviert, fügen Sie diese daher nach der Installation hinzu. Weitere Informationen finden Sie in diesem Thema unter [MSMDSRV-Dienstprotokolldatei](#bkmk_msmdsrv) .  
  
-   Lesen Sie diesen Blogbeitrag vom Microsoft-Kundensupport, um zu erfahren, welche Ressourcen die Mitarbeiter zum Abrufen von Informationen zu Servervorgängen verwenden: [Initial Data Collection](http://blogs.msdn.com/b/as_emea/archive/2012/01/02/initial-data-collection-for-troubleshooting-analysis-services-issues.aspx)(Anfängliche Datensammlung).  
  
-   Verwenden Sie ASTrace2012, statt ein Abfrageprotokoll auszuführen, um herauszufinden, wer Cubes abfragt. Das Abfrageprotokoll dient in der Regel zur Bereitstellung von Eingaben für den verwendungsbasierten Optimierung-Assistenten, und die erfassten Daten können nicht einfach gelesen oder interpretiert werden. ASTrace2012 ist ein Communitytool, das weit verbreitet ist und die Abfragevorgänge erfasst. Weitere Informationen finden Sie unter [Microsoft SQL Server Community Samples: Analysis Services](https://sqlsrvanalysissrvcs.codeplex.com/)(Microsoft SQL Server-Community-Beispiele: Analysis Services).  
  
## <a name="see-also"></a>Siehe auch  
 [Analysis Services-Instanzverwaltung](../../analysis-services/instances/analysis-services-instance-management.md)   
 [Einführung in die Überwachung von Analysis Services mit SQL Server Profiler](../../analysis-services/instances/introduction-to-monitoring-analysis-services-with-sql-server-profiler.md)   
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  

