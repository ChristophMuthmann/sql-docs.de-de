---
title: Melden Sie sich Eigenschaften | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b76b9011d6c138669d75fb9ff3caebf6f74bc00a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="log-properties"></a>Protokolleigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] werden die in den folgenden Tabellen aufgeführten Protokollservereigenschaften unterstützt. Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
## <a name="general"></a>Allgemein  
 **File**  
 Eine Zeichenfolge, die den Namen der Serverprotokolldatei anzeigt. Diese Eigenschaft gilt nur, wenn für die Protokollierung eine Datei auf dem Datenträger anstelle einer Datenbanktabelle (das Standardverhalten) verwendet wird.  
  
 Der Standardwert für diese Eigenschaft ist msmdsrv.log.  
  
 **FileBufferSize**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **MessageLogs**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="error-log"></a>Fehlerprotokoll  
 Sie können diese Eigenschaften auf Serverinstanzebene festlegen, um die Standardwerte für die Fehlerkonfiguration zu ändern, die in anderen Tools und in Designern verfügbar sind. Finden Sie unter [Fehlerkonfiguration für Cubes, Partitionen und Dimensionsverarbeitung &#40;SSAS – mehrdimensional&#41; ](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md) und <xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A> für Weitere Informationen.  
  
 **ErrorLog\ErrorLogFileName**  
 Diese Eigenschaft wird standardmäßig während des vom Server ausgeführten Verarbeitungsvorgangs verwendet.  
  
 **ErrorLog\ErrorLogFileSize**  
 Diese Eigenschaft wird standardmäßig während des vom Server ausgeführten Verarbeitungsvorgangs verwendet.  
  
 **ErrorLog\KeyErrorAction**  
 Gibt die Aktion an, die bei Auftreten eines **KeyNotFound** -Fehlers vom Server ausgeführt wird. Gültige Serverreaktionen auf diesen Fehler sind:  
  
-   **ConvertToUnknown** weist den Server an, den Fehlerschlüsselwert dem unbekannten Element zuzuordnen.  
  
-   **DiscardRecord** weist den Server an, den Datensatz auszuschließen.  
  
 **ErrorLog\KeyErrorLogFile**  
 Dies ist ein benutzerdefinierter Dateiname, der über die Dateierweiterung .log verfügen und in einem Ordner gespeichert sein muss, für den das Dienstkonto Lese-/Schreibberechtigungen besitzt. Die Protokolldatei enthält nur Fehler, die während der Verarbeitung generiert wurden. Verwenden Sie Flight Recorder, wenn Sie ausführlichere Informationen benötigen.  
  
 **ErrorLog\KeyErrorLimit**  
 Dies ist die maximale Anzahl von Datenintegritätsfehlern, die der Server toleriert, bevor die Verarbeitung fehlschlägt. Der Wert -1 steht für eine unbegrenzte Anzahl. Der Standardwert ist 0 und bewirkt, dass die Verarbeitung nach Auftreten des ersten Fehlers beendet wird. Sie können ihn auch auf eine ganze Zahl festlegen.  
  
 **ErrorLog\KeyErrorLimitAction**  
 Gibt die Aktion an, die vom Server ausgeführt wird, nachdem die Obergrenze von Schlüsselfehlern erreicht wurde. Gültige Serverreaktionen auf diese Aktion sind:  
  
-   **StopProcessing** weist den Server an, die Verarbeitung zu beenden, sobald die Fehlergrenze erreicht ist.  
  
-   **StopLogging** weist den Server an, die Fehlerprotokollierung bei Erreichen der Fehlergrenze zu beenden, die Verarbeitung jedoch weiterhin zuzulassen.  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 Gibt die Aktion an, die bei Auftreten eines **KeyNotFound** -Fehlers vom Server ausgeführt wird. Gültige Serverreaktionen auf diesen Fehler sind:  
  
-   **IgnoreError** weist den Server an, die Verarbeitung fortzusetzen, ohne den Fehler zu protokollieren oder auf den Grenzwert für Schlüsselfehler anzurechnen. Wenn Sie den Fehler ignorieren, lassen Sie einfach die weitere Verarbeitung zu, ohne dass die Fehleranzahl erhöht oder der Fehler auf dem Bildschirm angezeigt oder in der Protokolldatei erfasst wird. Der betreffende Datensatz weist ein Datenintegritätsproblem auf und kann der Datenbank nicht hinzugefügt werden. Der Datensatz wird abhängig von der **KeyErrorAction** -Eigenschaft entweder verworfen oder dem unbekannten Element hinzugefügt.  
  
-   **ReportAndContinue** weist den Server an, den Fehler zu protokollieren, auf den Grenzwert für Schlüsselfehler anzurechnen und die Verarbeitung fortzusetzen. Der für den Fehler verantwortliche Datensatz wird verworfen oder in das unbekannte Element konvertiert.  
  
-   **ReportAndStop** weist den Server an, den Fehler zu protokollieren und die Verarbeitung unabhängig vom Grenzwert für Schlüsselfehler sofort zu beenden. Der für den Fehler verantwortliche Datensatz wird verworfen oder in das unbekannte Element konvertiert.  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 Gibt die Aktion an, die vom Server ausgeführt wird, wenn ein doppelter Schlüssel gefunden wird. Folgende Werte sind möglich: **IgnoreError** – die Verarbeitung wird fortgesetzt, als wäre der Fehler nicht aufgetreten; **ReportAndContinue** – der Fehler wird protokolliert und die Verarbeitung fortgesetzt; **ReportAndStop** – der Fehler wird protokolliert und die Verarbeitung sofort beendet, selbst wenn die Fehleranzahl unterhalb der Fehlergrenze liegt.  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 Gibt die Aktion an, die vom Server ausgeführt wird, wenn ein NULL-Schlüssel in ein unbekanntes Element konvertiert wurde. Folgende Werte sind möglich: **IgnoreError** – die Verarbeitung wird fortgesetzt, als wäre der Fehler nicht aufgetreten; **ReportAndContinue** – der Fehler wird protokolliert und die Verarbeitung fortgesetzt; **ReportAndStop** – der Fehler wird protokolliert und die Verarbeitung sofort beendet, selbst wenn die Fehleranzahl unterhalb der Fehlergrenze liegt.  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 Gibt die Aktion an, die vom Server ausgeführt wird, wenn die Eigenschaft **NullProcessing** eines Dimensionsattributs auf **Error** festgelegt ist. Wenn für ein bestimmtes Attribut kein NULL-Wert zulässig ist, wird ein Fehler generiert. Durch diese Fehlerkonfigurationseigenschaft wird der nächste Schritt initiiert, der darin besteht, den Fehler zu melden und die Verarbeitung fortzusetzen, bis die Fehlergrenze erreicht ist. Folgende Werte sind möglich: **IgnoreError** – die Verarbeitung wird fortgesetzt, als wäre der Fehler nicht aufgetreten; **ReportAndContinue** – der Fehler wird protokolliert und die Verarbeitung fortgesetzt; **ReportAndStop** – der Fehler wird protokolliert und die Verarbeitung sofort beendet, selbst wenn die Fehleranzahl unterhalb der Fehlergrenze liegt.  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 Diese Eigenschaft wird standardmäßig während des vom Server ausgeführten Verarbeitungsvorgangs verwendet.  
  
 **ErrorLog\IgnoreDataTruncation**  
 Diese Eigenschaft wird standardmäßig während des vom Server ausgeführten Verarbeitungsvorgangs verwendet.  
  
## <a name="exception"></a>Exception  
 **Exception\CreateAndSendCrashReports**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Exception\CrashReportsFolder**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Exception\SQLDumperFlagsOn**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Exception\SQLDumperFlagsOff**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Exception\MiniDumpFlagsOn**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Exception\MinidumpErrorList**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="flight-recorder"></a>Flight Recorder  
 **FlightRecorder\Enabled**  
 Eine boolesche Eigenschaft, die anzeigt, ob deie Funktion Flight Recorder aktiviert ist.  
  
 **FlightRecorder\FileSizeMB**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die Größe der auf dem Datenträger gespeicherten Flight Recorder-Datei in MB definiert.  
  
 **FlightRecorder\LogDurationSec**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die definiert, wie oft der Flight Recorder von neuem beginnt (in Sekunden).  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 Eine aus einer Zeichenfolge bestehende Eigenschaft, die den Namen der Momentaufnahmedefinitionsdatei definiert. Diese Datei enthält Ermittlungsbefehle, die beim Erstellen einer Momentaufnahme an den Server ausgegeben werden.  
  
 Der Standardwert für diese Eigenschaft ist leer. Dies bedeutet, dass standardmäßig der Dateiname FlightRecorderSnapshotDef.xml verwendet wird.  
  
 **FlightRecorder\SnapshotFrequencySec**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die Momentaufnahmehäufigkeit in Sekunden angibt.  
  
 **FlightRecorder\TraceDefinitionFile**  
 Eine aus einer Zeichenfolge bestehende Eigenschaft, die den Namen der Ablaufverfolgungs-Definitionsdatei für den Flight Recorder angibt.  
  
 Der Standardwert für diese Eigenschaft ist leer. Dies bedeutet, dass standardmäßig die Datei FlightRecorderTraceDef.xml verwendet wird.  
  
## <a name="query-log"></a>Abfrageprotokoll  
 **Gilt für:** Nur mehrdimensionaler Servermodus  
  
 **QueryLog\QueryLogFileName**  
 Eine Zeichenfolge, die den Namen der Abfrageprotokolldatei angibt. Diese Eigenschaft gilt nur, wenn für die Protokollierung eine Datei auf dem Datenträger anstelle einer Datenbanktabelle (das Standardverhalten) verwendet wird.  
  
 **QueryLog\QueryLogSampling**  
 Eine ganze 32-Bit-Zahl mit Vorzeichen, die die Stichprobenrate des Abfrageprotokolls angibt.  
  
 Der Standardwert für diese Eigenschaft ist 10. Dies bedeutet, dass eine von 10 Serverabfragen protokolliert wird.  
  
 **QueryLog\QueryLogFileSize**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **QueryLog\QueryLogConnectionString**  
 Eine Zeichenfolge, die die Verbindung mit der Abfrageprotokolldatenbank angibt.  
  
 **QueryLog\QueryLogTableName**  
 Eine Zeichenfolge, die den Namen der Abfrageprotokolltabelle angibt.  
  
 Der Standardwert für diese Eigenschaft ist OlapQueryLog.  
  
 **QueryLog\CreateQueryLogTable**  
 Eine boolesche Eigenschaft, die angibt, ob die Abfrageprotokolltabelle erstellt werden soll.  
  
 Der Standardwert für diese Eigenschaft ist FALSE. Dies bedeutet, dass der Server nicht automatisch die Protokolltabelle erstellt und keine Abfrageereignisse protokolliert.  
  
> [!NOTE]  
>  Weitere Informationen zum Konfigurieren des Abfrageprotokolls finden Sie unter [Configuring the Analysis Services Query Log](http://go.microsoft.com/fwlink/?LinkId=81890)(Konfigurieren des Abfrageprotokolls von Analysis Services).  
  
## <a name="trace"></a>Ablaufverfolgung  
 **Trace\TraceBackgroundDistributionPeriod**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceBackgroundFlushPeriod**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceFileBufferSize**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceMaxRowsetSize**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceProtocolTraffic**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceReportFQDN**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceRequestParameters**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 Eine erweiterte Eigenschaft, die nur mithilfe der Schritte in [!INCLUDE[msCoName](../../includes/msconame-md.md)] geändert werden sollte.  
  
## <a name="see-also"></a>Siehe auch  
 [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
