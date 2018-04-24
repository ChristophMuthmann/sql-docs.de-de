---
title: Verwenden von Token in Auftragsschritten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- security [SQL Server Agent], enabling alert job step tokens
- SQL Server Agent jobs, job steps
- tokens [SQL Server]
- escape macros [SQL Server Agent]
ms.assetid: 105bbb66-0ade-4b46-b8e4-f849e5fc4d43
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dee38135bfb00f3cec22d0c10236775c07821e85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-tokens-in-job-steps"></a>Verwenden von Token in Auftragsschritten
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent ermöglicht die Verwendung von Token in [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschrittskripts. Durch die Verwendung von Token verfügen Sie beim Schreiben von Auftragsschritten über dieselbe Flexibilität, die die Verwendung von Variablen beim Schreiben von Softwareprogrammen bietet. Die von Ihnen in ein Auftragsschrittskript eingefügten Token werden vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zur Ausführungszeit ersetzt, bevor der Auftragsschritt vom [!INCLUDE[tsql](../../includes/tsql_md.md)] -Subsystem ausgeführt wird.  
  
> [!IMPORTANT]  
> Mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] Service Pack 1 wurde die Syntax der Token für die Arbeitsschritte des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents geändert. Damit Auftragsschritte fehlerfrei ausgeführt werden können, müssen alle in Auftragsschritten verwendete Token von einem Escapemakro begleitet werden. Das Verwenden von Escapemakros und das Aktualisieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragsschritten, in denen Token verwendet werden, wird in den folgenden Abschnitten "Grundlegendes zum Verwenden von Token", "[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Token und -Makros" und "Aktualisieren von Auftragsschritten für die Verwendung von Makros" beschrieben. Außerdem wurde auch die [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] -Syntax, in der zur Auszeichnung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragsschritten eckige Klammern verwendet wurden (z. B. "`[DATE]`") geändert. Jetzt müssen Sie Tokennamen in runde Klammern einschließen und ein Dollarzeichen (`$`) an den Anfang der Tokensyntax setzen. Zum Beispiel:  
>   
> `$(ESCAPE_`*Makroname*`(DATE))`  
  
## <a name="understanding-using-tokens"></a>Grundlegendes zum Verwenden von Token  
  
> [!IMPORTANT]  
> Jeder Windows-Benutzer mit Schreibberechtigungen für das Windows-Ereignisprotokoll kann auf Auftragsschritte zugreifen, die durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Warnungen oder WMI-Warnungen aktiviert werden. Zur Vermeidung dieses Sicherheitsrisikos sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Tokens, die in von Warnungen aktivierten Aufträgen verwendet werden können, standardmäßig deaktiviert. Dabei handelt es sich um folgende Token: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG**und **WMI(***Eigenschaft***)**. Beachten Sie, dass in dieser Version die Verwendung von Token auf alle Warnungen ausgeweitet ist.  
>   
> Wenn Sie diese Token verwenden müssen, stellen Sie zuvor sicher, dass ausschließlich Mitglieder von vertrauenswürdigen Windows-Sicherheitsgruppen, wie der Administratorengruppe, über Schreibberechtigungen für das Ereignisprotokoll des Computers verfügen, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird. Klicken Sie dann zum Aktivieren dieser Token im Objekt-Explorer mit der rechten Maustaste auf **SQL Server-Agent** , wählen Sie **Eigenschaften**, und wählen Sie anschließend auf der Seite **Warnungssystem** die Option **Token für alle Auftragsantworten auf Warnungen ersetzen** aus.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent-Token können einfach und effizient ersetzt werden: Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ersetzt das Token durch ein genaues Zeichenfolgenliteral. Die Groß- und Kleinschreibung ist bei Token grundsätzlich zu beachten. Dies muss in den Auftragsschritten berücksichtigt werden, damit die verwendeten Token richtig angegeben werden oder die Ersatzzeichenfolge in den richtigen Datentyp konvertiert wird.  
  
Mit der folgenden Anweisung können Sie z. B. den Namen der Datenbank in einem Auftragsschritt drucken:  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
In diesem Beispiel wird das Makro **ESCAPE_SQUOTE** mit dem Token **A-DBN** eingefügt. Zur Laufzeit wird das Token **A-DBN** durch den entsprechenden Datenbanknamen ersetzt. Das Escapemakro umgeht alle einfachen Anführungszeichen, die möglicherweise unbeabsichtigt in der Zeichenfolge, durch die das Token ersetzt werden soll, übergeben werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent ersetzt in der endgültigen Zeichenfolge jedes einfache Anführungszeichen durch zwei einfache Anführungszeichen.  
  
Wenn beispielsweise als Ersatz für das Token die Zeichenfolge `AdventureWorks2012'SELECT @@VERSION --`übergeben wird, wird im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragsschritt der folgende Befehl ausgeführt:  
  
`PRINT N'Current database name is AdventureWorks2012''SELECT @@VERSION --' ;`  
  
In diesem Fall wird die eingefügte Anweisung `SELECT @@VERSION`nicht ausgeführt. Stattdessen wird durch das überzählige einfache Anführungszeichen der Server veranlasst, die eingefügte Anweisung als Zeichenfolge zu analysieren. Wenn die Zeichenfolge, durch die das Token ersetzt werden soll, keine einfachen Anführungszeichen enthält, werden keine Zeichen umgangen, und der Auftragsschritt mit dem Token wird wie beabsichtigt ausgeführt.  
  
Verwenden Sie zum Debuggen der Tokenverwendung in Auftragsschritten Druckanweisungen, wie z. B. `PRINT N'$(ESCAPE_SQUOTE(SQLDIR))'` , und speichern Sie die Auftragsschrittausgabe in einer Datei oder Tabelle. Auf der Seite **Erweitert** des Dialogfelds **Auftragsschritt-Eigenschaften** können Sie eine Datei oder Tabelle für die Auftragsschrittausgabe angeben.  
  
## <a name="sql-server-agent-tokens-and-macros"></a>SQL Server-Agent-Token und -Makros  
In der folgenden Tabelle sind die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent unterstützten Token und Makros aufgelistet und beschrieben.  
  
### <a name="sql-server-agent-tokens"></a>SQL Server-Agent-Token  
  
|Token|Description|  
|---------|---------------|  
|**(A-DBN)**|Datenbankname. Wenn der Auftrag durch eine Warnung ausgeführt wird, ersetzt der Wert des Datenbanknamens dieses Token im Auftragsschritt automatisch.|  
|**(A-SVR)**|Servername. Wenn der Auftrag durch eine Warnung ausgeführt wird, ersetzt der Wert des Servernamens dieses Token im Auftragsschritt automatisch.|  
|**(A-ERR)**|Fehlernummer. Wenn der Auftrag durch eine Warnung ausgeführt wird, ersetzt der Wert der Fehlernummer dieses Token im Auftragsschritt automatisch.|  
|**(A-SEV)**|Fehlerschweregrad. Wenn der Auftrag durch eine Warnung ausgeführt wird, ersetzt der Wert des Fehlerschweregrads dieses Token im Auftragsschritt automatisch.|  
|**(A-MSG)**|Meldungstext. Wenn der Auftrag durch eine Warnung ausgeführt wird, ersetzt der Wert des Meldungstexts dieses Token im Auftragsschritt automatisch.|  
|**(JOBNAME)**|Der Name des Auftrags.|  
|**(STEPNAME)**|Der Name des Schrittes.|  
|**(DATE)**|Das aktuelle Datum (im Format YYYYMMDD).|  
|**(INST)**|Der Instanzname. Für eine Standardinstanz erhält dieses Token den Standardinstanznamen: MSSQLSERVER.|  
|**(JOBID)**|Auftrags-ID.|  
|**(MACH)**|Computername.|  
|**(MSSA)**|Name des Master-SQLServerAgent-Diensts.|  
|**(OSCMD)**|Das Präfix des Programms, das zur Ausführung der **CmdExec** -Auftragsschritte verwendet wird.|  
|**(SQLDIR)**|Verzeichnis, in dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] installiert ist. Der Standardwert lautet "C:\Programme\Microsoft SQL Server\MSSQL".|  
|**(SQLLOGDIR)**|Ersetzungstoken für den Pfad des SQL Server-Fehlerprotokollordners – beispielsweise $(ESCAPE_SQUOTE(SQLLOGDIR)).|  
|**(STEPCT)**|Die Angabe, wie oft dieser Schritt ausgeführt wurde (ohne Abbrüche). Mit diesem Token kann der Schrittbefehl den Abbruch einer aus mehreren Schritten bestehenden Schleife erzwingen.|  
|**(STEPID)**|Schritt-ID.|  
|**(SRVR)**|Name des Computers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ausgeführt wird. Wenn es sich bei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Instanz um eine benannte Instanz handelt, ist auch der Name der Instanz angegeben.|  
|**(TIME)**|Die aktuelle Zeit (im Format HHMMSS).|  
|**(STRTTM)**|Uhrzeit (im Format HHMMSS), zu der die Ausführung des Auftrags begonnen hat.|  
|**(STRTDT)**|Datum (im Format YYYYMMDD), an dem die Ausführung des Auftrags begonnen hat.|  
|**(WMI(***Eigenschaft***))**|Bei Aufträgen, die als Antwort auf WMI-Warnungen ausgeführt werden, ist dies der Wert der durch *property*angegebenen Eigenschaft. In `$(WMI(DatabaseName))` ist beispielsweise der Wert der **DatabaseName** -Eigenschaft für das WMI-Ereignis angegeben, das die Ausführung der Warnung verursacht hat.|  
  
### <a name="sql-server-agent-escape-macros"></a>SQL Server-Agent-Escapemakros  
  
|Escapemakros|Description|  
|-----------------|---------------|  
|**$(ESCAPE_SQUOTE(***Tokenname***))**|Umgeht einfache Anführungszeichen (') in der Token-Ersetzungszeichenfolge. Ein einfaches Anführungszeichen wird durch zwei einfache Anführungszeichen ersetzt.|  
|**$(ESCAPE_DQUOTE(***Tokenname***))**|Umgeht doppelte Anführungszeichen (") in der Token-Ersetzungszeichenfolge. Ein doppeltes Anführungszeichen wird durch zwei doppelte Anführungszeichen ersetzt.|  
|**$(ESCAPE_RBRACKET(***Tokenname***))**|Umgeht rechte eckige Klammern (]) in der Token-Ersetzungszeichenfolge. Ersetzt jede rechte eckige Klammer durch zwei rechte eckige Klammern.|  
|**$(ESCAPE_NONE(***Tokenname***))**|Ersetzt Token, ohne irgendein Zeichen in der Zeichenfolge zu umgehen. Dieses Makro wird zur Unterstützung der Abwärtskompatibilität in Umgebungen bereitgestellt, in denen Token-Ersetzungszeichenfolgen nur von vertrauenswürdigen Benutzern erwartet werden. Weitere Informationen finden Sie weiter unten im Abschnitt zum Aktualisieren von Auftragsschritten für die Verwendung von Makros.|  
  
## <a name="updating-job-steps-to-use-macros"></a>Aktualisieren von Auftragsschritten für die Verwendung von Makros  
Seit [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] Service Pack 1 können Auftragsschritte, die Token ohne Escapemakros enthalten, nicht ausgeführt werden. In diesen Fällen wird eine Fehlermeldung zurückgegeben, die darauf hinweist, dass der Auftragsschritt ein oder mehrere Token enthält, die mit einem Makro versehen werden müssen, bevor der Auftrag ausgeführt werden kann.  
  
Im [!INCLUDE[msCoName](../../includes/msconame_md.md)] Knowledge Base-Artikel 915845 zu [SQL Server-Agent-Auftragsschritten mit Token, die in SQL Server 2005 Service Pack 1 nicht ausgeführt werden können](http://support.microsoft.com/kb/915845), ist ein Skript enthalten, mit dem Sie alle Ihre Auftragsschritte, in denen Token verwendet werden, mit dem Makro **ESCAPE_NONE** aktualisieren können. Nach dem Verwenden dieses Skripts sollten Sie so bald wie möglich die Auftragsschritte, in denen Token verwendet werden, überprüfen und das **ESCAPE_NONE** -Makro durch ein für den Kontext des Auftragsschritts geeignetes Escapemakro ersetzen.  
  
Die folgende Tabelle beschreibt, wie die symbolische Ersetzung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent behandelt wird. Um die Tokenersetzung durch Warnungen ein- oder auszuschalten, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **SQL Server-Agent** , wählen Sie **Eigenschaften**, und aktivieren bzw. deaktivieren Sie anschließend auf der Seite **Warnungssystem** das Kontrollkästchen **Token für alle Auftragsantworten auf Warnungen ersetzen** .  
  
|Tokensyntax|Tokenersetzung durch Warnungen aktiviert|Tokenersetzung durch Warnungen deaktiviert|  
|----------------|------------------------------|-------------------------------|  
|ESCAPE-Makro verwendet|Alle Token in Auftragsschritten werden erfolgreich ersetzt.|Durch Warnungen aktivierte Token werden nicht ersetzt. Dabei handelt es sich um folgende Token: **A-DBN**, **A-SVR**, **A-ERR**, **A-SEV**, **A-MSG** und **WMI(***Eigenschaft***)**. Andere, statische Token werden erfolgreich ersetzt.|  
|Kein ESCAPE-Makro verwendet|Alle Auftragsschritte mit Token werden nicht ausgeführt.|Alle Auftragsschritte mit Token werden nicht ausgeführt.|  
  
## <a name="token-syntax-update-examples"></a>Beispiele für Updates der Tokensyntax  
  
### <a name="a-using-tokens-in-non-nested-strings"></a>A. Verwenden von Token in nicht geschachtelten Zeichenfolgen  
Im folgenden Beispiel wird gezeigt, wie Sie ein einfaches, nicht geschachteltes Skript mit dem entsprechenden Escapemakro aktualisieren. Vor dem Ausführen des Updateskripts verwendet das folgende Auftragsschrittskript ein Auftragsschritttoken, um den entsprechenden Datenbanknamen zu drucken:  
  
`PRINT N'Current database name is $(A-DBN)' ;`  
  
Nach dem Ausführen des Updateskripts wird vor dem `ESCAPE_NONE` -Token ein `A-DBN` -Makro eingefügt. Da die Druckzeichenfolge durch einfache Anführungszeichen begrenzt wird, müssen Sie den Auftragsschritt aktualisieren, indem Sie das `ESCAPE_SQUOTE` -Makro folgendermaßen einfügen:  
  
`PRINT N'Current database name is $(ESCAPE_SQUOTE(A-DBN))' ;`  
  
### <a name="b-using-tokens-in-nested-strings"></a>B. Verwenden von Token in geschachtelten Zeichenfolgen  
In Auftragsschritten, in denen Token in geschachtelten Zeichenfolgen oder Anweisungen verwendet werden, sollten die geschachtelten Anweisungen als Einzelanweisungen neu geschrieben werden, bevor die entsprechenden Escapemakros eingefügt werden.  
  
Betrachten Sie z. B. den folgenden Auftragsschritt, der das Token `A-MSG` verwendet und nicht mit einem Escapemakro aktualisiert wurde:  
  
`PRINT N'Print ''$(A-MSG)''' ;`  
  
Nach dem Ausführen des Updateskripts wird mit dem Token ein `ESCAPE_NONE` -Makro eingefügt. In diesem Fall müssten Sie das Skript jedoch ohne Verwenden von Schachtelungen folgendermaßen neu schreiben und das `ESCAPE_SQUOTE` -Makro einfügen, damit die in der Token-Ersetzungszeichenfolge möglicherweise übergebenen Begrenzungszeichen richtig umgangen werden:  
  
<pre>DECLARE @msgString nvarchar(max)  
SET @msgString = '$(ESCAPE_SQUOTE(A-MSG))'  
SET @msgString = QUOTENAME(@msgString,'''')  
PRINT N'Print ' + @msgString ;</pre>  
  
Beachten Sie auch, dass in diesem Beispiel mit der Funktion QUOTENAME das Anführungszeichen festgelegt wird.  
  
### <a name="c-using-tokens-with-the-escapenone-macro"></a>C. Verwenden von Token mit dem ESCAPE_NONE-Makro  
Das folgende Beispiel ist Teil eines Skripts, mit dem die Auftrags-ID ( `job_id` ) aus der `sysjobs` -Tabelle abgerufen wird und mithilfe des `JOBID` -Tokens die zuvor im Skript als binärer Datentyp deklarierte `@JobID` -Variable aufgefüllt wird. Beachten Sie, dass mit dem `ESCAPE_NONE` -Token das `JOBID` -Makro verwendet wird, da für binäre Datentypen keine Begrenzungszeichen erforderlich sind. In diesem Fall muss der Auftragsschritt nach Ausführen des Updateskripts nicht aktualisiert werden.  
  
<pre>SELECT * FROM msdb.dbo.sysjobs  
WHERE @JobID = CONVERT(uniqueidentifier, $(ESCAPE_NONE(JOBID))) ;</pre>  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Implementieren von Aufträgen](../../ssms/agent/implement-jobs.md)  
[Verwalten von Auftragsschritten](../../ssms/agent/manage-job-steps.md)  
  
