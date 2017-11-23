---
title: Cmdlet "Invoke-ASCmd" | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2896b74a-3911-4b3f-89ab-bb375bdb34d8
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6e5d1fba56fd4cee4c736a583d8af2fe8ec6f986
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="invoke-ascmd-cmdlet"></a>Invoke-ASCmd-Cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Ermöglicht Datenbankadministratoren die Ausführung von XMLA-Skripts, MDX-Abfragen (Multidimensional Expressions), DMX-Anweisungen (Data Mining Extensions) oder TMSL-Skripts (Tabular Model Scripting Language).  
  
 In einer SQL Server 2016-Instanz von Analysis Services wird TMSL nur im tabellarischen Servermodus unterstützt.  
  
 Wenn Sie Datenbanken oder andere Objekte erstellen möchten, sollten Sie dieses Cmdlet mit einer Skript-Eingabedatei verwenden.  
  
## <a name="syntax"></a>Syntax  
 `Invoke-ASCmd –Query <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
 `Invoke-ASCmd –InputFile <string> [-Server <string>] [-Database <string>] [-Credential <PSCredential>] [-ConnectionTimeout <int>] [-QueryTimeout <int>] [-Variable <string[]>] [-TraceFile <string>] [-TraceFileFormat <TraceFileFormatOption>] [-TraceFileDelimiter <string>] [-TraceTimeout <int>] [-TraceLevel <TraceLevelOption>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Das Invoke-ASCmd-Cmdlet kann Abfragen oder Skripts ausführen, die in Eingabedateien enthalten sind.  
  
 Für XMLA werden die folgenden Befehle unterstützt: Alter, Backup, Batch, BeginTransaction, Cancel, ClearCache, CommitTransaction, Create, Delete, DesignAggregations, Drop, Insert, Lock, MergePartitions, NotifyTableChange, Process, Restore, RollbackTransaction, Statement (zum Ausführen von MDX-Abfragen und DMX-Anweisungen), Subscribe, Synchronize, Unlock, Update, UpdateCells.  
  
 Für TMSL: Alter, Create, Delete, MergePartitions, Process, Update.  
  
 Dieses Cmdlet unterstützt den –Credential-Parameter, der verwendet werden kann, wenn Sie die Analysis Services-Instanz für HTTP-Zugriff konfigurierten. Der –Credential-Parameter verwendet ein PSCredential-Objekt, das eine Windows-Benutzeridentität bereitstellt. Beim Herstellen einer Verbindung mit Analysis Services nimmt wird die Identität dieses Benutzers dann von IIS angenommen. Die Identität muss über Systemadministratorberechtigungen für die Analysis Services-Instanz verfügen, um ein Skript ausführen zu können.  
  
## <a name="parameters"></a>Parameter  
  
### <a name="-query-string"></a>-Abfrage \<Zeichenfolge >  
 Gibt das eigentliche Skript, die Abfrage oder die Anweisung direkt an der Befehlszeile und nicht in einer Datei an. Sie können auch eine Abfrage als Pipelineeingabe angeben. Sie müssen einen Wert für den Parameter **–InputFile** oder für den Parameter **–Query** angeben, wenn Sie **Invoke-AsCmd**verwenden.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByValue)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-inputfile-string"></a>-Eingabedatei \<Zeichenfolge >  
 Gibt die Datei an, in der das XMLA-Skript, die MDX-Abfrage, die DMX-Anweisung bzw. das TMSL-Skript (in JSON) enthalten ist. Sie müssen einen Wert für den Parameter **–InputFile** oder für den Parameter **–Query** angeben, wenn Sie **Invoke-AsCmd**verwenden.  
  
|||  
|-|-|  
|Erforderlich?|true|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-server-string"></a>-Server \<Zeichenfolge >  
 Gibt die Analysis Services-Instanz an, zu der das Cmdlet eine Verbindung herstellt und auf der es ausgeführt wird. Wenn kein Servername angegeben wird, wird eine Verbindung mit localhost hergestellt. Für Standardinstanzen geben Sie nur den Servernamen an. Verwenden Sie für benannte Instanzen das Format "servername\instanzenname". Verwenden Sie für HTTP-Verbindungen das Format "http[s]://server[:port]/virtualdirectory/msmdpump.dll".  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|localhost|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-database-string"></a>-Datenbank \<Zeichenfolge >  
 Gibt die Datenbank an, für die eine MDX-Abfrage oder eine DMX-Anweisung ausgeführt wird. Der database-Parameter wird ignoriert, wenn das Cmdlet ein XMLA-Skript ausführt, da in XMLA-Skripts der Datenbankname bereits eingebettet ist.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<"PSCredential" >  
 Gibt ein PSCredential-Objekt an, das einen Windows-Benutzernamen und ein -Kennwort angegeben werden. Geben Sie diesen Parameter nur an, wenn die Analysis Services-Instanz mit der Standardauthentifizierung für HTTP-Zugriff konfiguriert wird. Für systemeigene Verbindungen, die integrierte Sicherheit verwenden, wird dieser Parameter ignoriert.  
  
 Wenn dieser Parameter vorhanden ist, werden die Anmeldeinformationen, die es bereitstellt, an die Verbindungszeichenfolge angefügt. Beim Herstellen einer Verbindung mit Analysis Services wird die Identität dieses Benutzers dann von IIS angenommen. Wenn keine Anmeldeinformationen angegeben sind, wird das Windows-Standardkonto des Benutzers, der das Tool ausführt, verwendet.  
  
 Um diesen Parameter verwenden zu können, müssen Sie zuerst ein PSCredential-Objekt erstellen. Hierbei verwenden Sie Get-Credential, um den Benutzernamen und das Passwort anzugeben (z.B. `$Cred=Get-Credential “adventure-works\admin”`). Sie können dieses Objekt anschließend an den –Credential-Parameter `(-Credential:$Cred`) übergeben.  
  
   Weitere Informationen zum HTTP-Zugriff finden Sie unter [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|True (ByValue)|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-connectiontimeout-int"></a>-ConnectionTimeout \<Int >  
 Gibt an, nach wie vielen Sekunden bei der Verbindung mit der Analysis Services-Instanz ein Timeout auftritt. Der Timeoutwert muss einer ganzen Zahl zwischen 0 und 65534 entsprechen. Wenn 0 angegeben wird, verursachen Verbindungsversuche kein Timeout.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|30|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-querytimeout-int"></a>-QueryTimeout \<Int >  
 Gibt an, nach wie vielen Sekunden ein Timeout bei Abfragen auftritt. Wenn Sie keinen Timeoutwert angeben, erfolgt für Abfragen kein Timeout. Der Timeoutwert muss einer ganzen Zahl zwischen 1 und 65.535 entsprechen.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|30|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-variable-string"></a>-Variable \<string [] >  
 Gibt zusätzliche Skriptvariablen an. Jede Variable besteht aus einem Name-Wert-Paar. Wenn der Wert eingebettete Leerzeichen oder Steuerzeichen enthält, muss er in doppelte Anführungszeichen eingeschlossen werden. Verwenden Sie ein PowerShell-Array, um mehrere Variablen und ihre Werte anzugeben.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-tracefile-string"></a>– TraceFile \<Zeichenfolge >  
 Identifiziert beim Ausführen eines XMLA-Skripts, einer MDX-Abfrage oder einer DMX-Anweisung eine Datei, die Analysis Services-Ablaufverfolgungsereignisse empfängt. Wenn die Datei bereits vorhanden ist, wird sie automatisch überschrieben (mit Ausnahme der Ablaufverfolgungsdateien, die mit den Parametereinstellungen -TraceLevel:Duration und –TraceLevel:DurationResult erstellt wurden). (Ablaufverfolgungsdateien, die mit der Parametereinstellung '–TraceLevel:Duration' und '–TraceLevel:DurationResult' erstellt werden, sind hiervon ausgenommen.) Dateinamen mit Leerzeichen müssen in Anführungszeichen (" ") eingeschlossen werden. Wenn der Dateiname ungültig ist, wird eine Fehlermeldung generiert.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-tracefileformat-string"></a>-TraceFileFormat \<Zeichenfolge >  
 Gibt das Dateiformat für den –TraceFile-Parameter an (falls dieser Parameter angegeben wird). Die verfügbaren Optionen sind "Text" oder "csv". Der Standardwert ist ".csv".  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|csv|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-tracefiledelimiter-string"></a>-TraceFileDelimiter \<Zeichenfolge >  
 Gibt an, welches Zeichen als Trennzeichen für die Ablaufverfolgungsdatei verwendet wird, wenn "csv" als Format für die Ablaufverfolgungsdatei angegeben wird. Standardmäßig wird | (Pipezeichen oder senkrechter Strich) verwendet.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert||  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-tracetimeout-int"></a>-TraceTimeout \<Int >  
 Gibt an, wie viele Sekunden das Analysis Services-Modul wartet, bevor die Ablaufverfolgung beendet wird (wenn der –TraceFile-Parameter angegeben wird). Die Ablaufverfolgung gilt als beendet, wenn während des angegebenen Zeitraums keine Meldungen zur Ablaufverfolgung aufgezeichnet wurden. Standardmäßig beträgt der Timeoutwert für die Ablaufverfolgung 5 Sekunden.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|5|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="-tracelevel-traceleveloption"></a>TraceLevel - \<TraceLevelOption >  
 Gibt an, welche Daten in der Ablaufverfolgungsdatei gesammelt und aufgezeichnet werden. Mögliche Werte sind High, Medium, Low, Duration, DurationResult.  
  
|||  
|-|-|  
|Erforderlich?|false|  
|Position?|benannt|  
|Standardwert|High|  
|Pipelineeingabe akzeptieren?|false|  
|Platzhalterzeichen akzeptieren?|false|  
  
### <a name="commonparameters"></a>\<Allgemeine Parameter >  
 Dieses Cmdlet unterstützt die gängigen Parameter: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer und -OutVariable. Weitere Informationen finden Sie unter [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Mit dem Eingabetyp wird festgelegt, welchen Typ von Objekten Sie über die Pipeline an das Cmdlet übergeben können. Der Rückgabetyp bezeichnet den Typ der vom Cmdlet zurückgegebenen Objekte.  
  
|||  
|-|-|  
|Eingaben|PSObject|  
|Ausgaben|String|  
  
## <a name="example-1-xmla-input-file"></a>Beispiel 1 (XMLA-Eingabedatei)  
  
```  
Invoke-ASCmd –InputFile:"C:\MyFolder\DiscoverConnections.xmla"  
```  
  
 Dieser Befehl führt ein XMLA-Skript aus, das die Liste der aktiven Verbindungen auf dem Server zurückgibt. Die Datei" DiscoverConnections.xmla" enthält das folgende XMLA-Skript:  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
<RequestType>DISCOVER_CONNECTIONS</RequestType>  
<Restrictions />  
   <Properties>  
      <PropertyList>  
         <Content>Data</Content>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="example-2-tmsl-input-file"></a>Beispiel 2 (TMSL-Eingabedatei)  
 Dieses Beispiel ist mit dem ersten identisch, allerdings handelt es sich hier um ein TMSL-Skript (JSON), weshalb eine tabellarische Instanz von SQL Server 2016 erforderlich ist. Sie können das TMSL-Skript in SQL Server Management Studio generieren.  
  
 Wenn Sie über mehrere Instanzen verfügen und Ihre tabellarische Instanz eine benannte Instanz ist, müssen Sie auch den Servernamen angeben:  
  
```  
Invoke-ASCmd –InputFile "C:\folder-name\T1200-NewDB.json" -Server "server-name\instance-name"  
```  
  
## <a name="example-3-query"></a>Beispiel 3 (Abfrage)  
  
```  
Invoke-ASCmd -Database:"Adventure Works DW" -Query:"<Discover xmlns='urn:schemas-microsoft-com:xml analysis'><RequestType>DISCOVER_DATASOURCES</RequestType><Restrictions></Restrictions><Properties></Properties></Discover>"  
```  
  
 Die Discover XMLA-Abfrage gibt verfügbare Datenquellen für den Analysis-Server zurück, sowie die Informationen, die erforderlich sind, um eine Verbindung mit ihnen herzustellen. Die Ergebnisse werden in XML angegeben. Für verbesserte Lesbarkeit können Sie die Ausgabe an eine XML-Datei übergeben (fügen Sie dem Befehl z.B. `| Out-file C:\Results\XMLAQueryOutput.xml` an) und die Ergebnisse in einem Browser oder einer anderen Anwendung anzeigen, die strukturiertes XML unterstützt.  
  
  
  
