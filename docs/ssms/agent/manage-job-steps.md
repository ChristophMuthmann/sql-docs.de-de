---
title: Verwalten von Auftragsschritten | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server replication]
- job steps [SQL Server Agent]
- jobs [SQL Server Agent], Integration Services package step
- executable programs as job steps
- operating systems [SQL Server], job steps
- Transact-SQL job step
- job steps [Transact-SQL]
- Integration Services packages, job steps
- replication job steps [SQL Server]
- logs [SQL Server], jobs
- SQL Server Agent jobs, job steps
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: 51352afc-a0a4-428b-8985-f9e58bb57c31
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5f9ecad6fcec2596f26351839311cc8b647e094e
ms.lasthandoff: 04/11/2017

---
# <a name="manage-job-steps"></a>Verwalten von Auftragsschritten
Ein Auftragsschritt ist eine Aktion, die der Auftrag auf einer Datenbank oder einem Server ausführt. Jeder Auftrag muss mindestens einen Auftragsschritt aufweisen. Folgende Auftragsschritte sind möglich:  
  
-   Ausführbare Programme und Betriebssystembefehle.  
  
-   [!INCLUDE[tsql](../../includes/tsql_md.md)] Anweisungen, einschließlich gespeicherter Prozeduren und erweiterter gespeicherter Prozeduren.  
  
-   PowerShell-Skripts.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] ActiveX-Skripts.  
  
-   Replikationstasks.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Aufgaben.  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] Pakete.  
  
Jeder Auftragsschritt wird in einem bestimmten Sicherheitskontext ausgeführt. Wenn der Auftragsschritt einen Proxy erfordert, wird er im Sicherheitskontext der Anmeldeinformationen des Proxys ausgeführt. Wenn ein Auftragsschritt keinen Proxy erfordert, wird er im Kontext des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkontos ausgeführt. Nur Mitglieder der festen Serverrolle sysadmin können Aufträge erstellen, die nicht ausdrücklich einen Proxy angeben.  
  
Weil Auftragsschritte im Kontext eines bestimmten [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Benutzers ausgeführt werden, muss dieser Benutzer über die Berechtigungen und Konfigurationen verfügen, die für die Ausführung des Auftragsschritts erforderlich sind. Wenn Sie beispielsweise einen Auftrag erstellen, der einen Laufwerkbuchstaben oder einen UNC-Pfad (Universal Naming Convention) erfordert, können die Auftragsschritte unter Ihrem Windows-Benutzerkonto ausgeführt werden, während die Tasks getestet werden. Allerdings muss der Windows-Benutzer für den Auftragsschritt auch über die notwendigen Berechtigungen, die Laufwerkbuchstabenkonfigurationen oder den Zugriff auf das erforderliche Laufwerk verfügen. Andernfalls erzeugt der Auftragsschritt einen Fehler. Um dieses Problem zu verhindern, stellen Sie sicher, dass der Proxy für jeden Auftragsschritt über die notwendigen Berechtigungen für den Task verfügt, von dem der Auftragsschritt ausgeführt wird. Weitere Informationen finden Sie unter [Sicherheit und Schutz (Datenbankmodul)](http://msdn.microsoft.com/en-us/dfb39d16-722a-4734-94bb-98e61e014ee7).  
  
## <a name="job-step-logs"></a>Auftragsschrittprotokolle  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent kann die Ausgabe bestimmter Auftragsschritte entweder in eine Betriebssystemdatei oder in die sysjobstepslogs-Tabelle der msdb-Datenbank schreiben. Von den folgenden Auftragsschritttypen können Ausgaben in beide Ziele geschrieben werden:  
  
-   Ausführbare Programme und Betriebssystembefehle.  
  
-   [!INCLUDE[tsql](../../includes/tsql_md.md)] Anweisungen verwendet werden.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Aufgaben.  
  
Nur von Auftragsschritten, die von Benutzern ausgeführt werden, die Mitglieder der festen Serverrolle sysadmin sind, können Auftragsschrittausgaben in Betriebssystemdateien geschrieben werden. Wenn die Auftragsschritte von Benutzern ausgeführt werden, die Mitglieder der festen Datenbankrolle SQLAgentUserRole, SQLAgentReaderRole oder SQLAgentOperatorRole der msdb-Datenbank sind, kann die Ausgabe dieser Auftragsschritte nur in die sysjobstepslogs-Tabelle geschrieben werden.  
  
Auftragsschritte werden automatisch gelöscht, wenn Aufträge oder Auftragsschritte gelöscht werden.  
  
> [!NOTE]  
> Das Protokollieren von Replikationstasks und [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] -Paketauftragsschritten wird vom jeweiligen Subsystem durchgeführt. Sie können zum Konfigurieren der Auftragsschrittprotokollierung nicht den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent für diese Art von Auftragsschritten verwenden.  
  
## <a name="executable-programs-and-operating-system-commands-as-job-steps"></a>Ausführbare Programme und Betriebssystembefehle als Auftragsschritte  
Ausführbare Programme und Betriebssystembefehle können als Auftragsschritte verwendet werden. Diese Dateien können die Dateierweiterungen BAT, CMD, COM oder EXE aufweisen.  
  
Wenn Sie ein ausführbares Programm oder einen Betriebssystembefehl als Auftragsschritt verwenden, müssen Sie Folgendes angeben:  
  
-   Den Prozessexitcode, der zurückgegeben wird, wenn der Befehl erfolgreich ausgeführt wurde.  
  
-   Den auszuführenden Befehl. Beim Ausführen eines Betriebssystembefehls handelt es sich hierbei einfach um den Befehl selbst. Bei einem externen Programm ist dies der Name des Programms und die Argumente für das Programm, z. B.: **C:\Programme\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe -e -q "sp_who"**.  
  
    > [!NOTE]  
    > Sie müssen den vollständigen Pfad zur ausführbaren Datei angeben, wenn diese sich nicht in dem Verzeichnis befindet, das im Systempfad oder dem Pfad für den Benutzer angegeben ist, als der der Auftragsschritt ausgeführt wird.  
  
## <a name="transact-sql-job-steps"></a>Transact-SQL-Auftragsschritte  
Beim Erstellen eines [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritts müssen Sie folgende Schritte durchführen:  
  
-   Identifizieren der Datenbank, in der Sie den Auftrag ausführen.  
  
-   Eingeben der auszuführenden [!INCLUDE[tsql](../../includes/tsql_md.md)] -Anweisung. Von der Anweisung wird möglicherweise eine gespeicherte Prozedur oder eine erweiterte gespeicherte Prozedur aufgerufen.  
  
Sie können auch eine vorhandene [!INCLUDE[tsql](../../includes/tsql_md.md)] -Datei als Befehl für den Auftragsschritt öffnen.  
  
[!INCLUDE[tsql](../../includes/tsql_md.md)] Auftragsschritte verwenden keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Proxys. Stattdessen wird der Auftragsschritt als Besitzer des Auftragsschritts bzw. als [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto ausgeführt, wenn der Besitzer des Auftragsschritts Mitglied der festen Serverrolle sysadmin ist. Mitglieder der festen Serverrolle „sysadmin“ können auch angeben, dass [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritte unter dem Kontext eines anderen Benutzers ausgeführt werden, indem der *database_user_name* -Parameter der gespeicherten Prozedur „sp_add_jobstep“ verwendet wird. Weitere Informationen finden Sie unter [sp_add_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/97900032-523d-49d6-9865-2734fba1c755).  
  
> [!NOTE]  
> Ein einzelner [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritt kann mehrere Batches enthalten. [!INCLUDE[tsql](../../includes/tsql_md.md)] Auftragsschritte können mehrere eingebettete GO-Befehle enthalten.  
  
## <a name="powershell-scripting-job-steps"></a>PowerShell-Skript-Auftragsschritte  
Wenn Sie einen PowerShell-Skript-Auftragsschritt erstellen, müssen Sie eins von zwei Elementen als Befehl für den Schritt angeben:  
  
-   Den Text eines PowerShell-Skripts.  
  
-   Eine vorhandene PowerShell-Skriptdatei, die geöffnet werden soll.  
  
Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent PowerShell-Subsystem öffnet eine PowerShell-Sitzung und lädt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] PowerShell-Snap-Ins. Das als Auftragsschrittbefehl verwendete PowerShell-Skript kann auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] PowerShell-Anbieter und auf Cmdlets verweisen. Weitere Informationen über das Schreiben von PowerShell-Skripts mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] PowerShell-Snap-Ins finden Sie unter [SQL Server PowerShell](http://msdn.microsoft.com/en-us/89b70725-bbe7-4ffe-a27d-2a40005a97e7).  
  
## <a name="activex-scripting-job-steps"></a>ActiveX-Skript-Auftragsschritte  
  
> [!IMPORTANT]  
> Der ActiveX-Skript-Auftragsschritt wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] aus dem [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.  
  
Wenn Sie einen ActiveX-Skriptauftragsschritt erstellen, ist Folgendes notwendig:  
  
-   Identifizieren der Skriptsprache, in der der Auftragsschritt geschrieben ist.  
  
-   Erstellen des ActiveX-Skripts.  
  
Sie können auch eine vorhandene ActiveX-Skriptdatei als Befehl für den Auftragsschritt öffnen. ActiveX-Skriptbefehle können alternativ auch extern (beispielsweise mithilfe von Microsoft Visual Basic) kompiliert und anschließend als ausführbare Programme ausgeführt werden.  
  
Handelt es sich bei dem Befehl eines Auftragsschritts um ein ActiveX-Skript, können Sie das SQLActiveScriptHost-Objekt verwenden, um Ausgaben in das Verlaufsprotokoll des Auftragsschritts zu drucken oder COM-Objekte zu erstellen. Bei SQLActiveScriptHost handelt es sich um ein globales Objekt, das vom Hostsystem des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents in den Skriptnamensbereich eingefügt wird. Das Objekt verfügt über zwei Methoden („Print“ und „CreateObject“). Das folgende Beispiel veranschaulicht, wie ActiveX-Skripts in Visual Basic Scripting Edition (VBScript) funktionieren.  
  
```  
' VBScript example for ActiveX Scripting job step  
' Create a Dmo.Server object. The object connects to the  
' server on which the script is running.  
  
Set oServer = CreateObject("SQLDmo.SqlServer")  
oServer.LoginSecure = True  
oServer.Connect "(local)"  
'Disconnect and destroy the server object  
oServer.DisConnect  
Set oServer = nothing  
```  
  
## <a name="replication-job-steps"></a>Replikationsauftragsschritte  
Wenn Sie Veröffentlichungen und Abonnements mithilfe der Replikation erstellen, werden standardmäßig Replikationsaufträge erstellt. Der Typ der erstellten Aufträge wird durch den Typ der Replikation (Momentaufnahme, Transaktion oder Merge) und die verwendeten Optionen bestimmt.  
  
Replikationsauftragsschritte aktivieren einen dieser Replikations-Agents:  
  
-   Momentaufnahme-Agent (Momentaufnahmeauftrag)  
  
-   Protokolllese-Agent (Protokollleserauftrag)  
  
-   Verteilungs-Agent (Verteilungsauftrag)  
  
-   Merge-Agent (Mergeauftrag)  
  
-   Warteschlangenlese-Agent (Warteschlangenleser-Auftrag)  
  
Beim Einrichten der Replikation können Sie zwischen drei Ausführungsarten für die Replikations-Agents wählen: immer nach dem Start des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents, bei Bedarf oder gemäß einem Zeitplan. Weitere Informationen zu Replikations-Agents finden Sie unter [Replikations-Agents (Übersicht)](http://msdn.microsoft.com/en-us/a35ecd7d-f130-483c-87e3-ddc8927bb91b).  
  
## <a name="analysis-services-job-steps"></a>Analysis Services-Auftragsschritte  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent unterstützt zwei unterschiedliche Typen von Analysis Services-Auftragsschritten: Befehlsauftragsschritte und Abfrageauftragsschritte.  
  
### <a name="analysis-services-command-job-steps"></a>Analysis Services-Befehlsauftragsschritte  
Wenn Sie einen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] -Befehlsauftragsschritt erstellen, müssen Sie folgende Schritte durchführen:  
  
-   Identifizieren der OLAP-Datenbank, in der Sie den Auftragsschritt ausführen.  
  
-   Eingeben der auszuführenden Anweisung. Bei der Anweisung muss es sich um eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] **-Methode von XML für** handeln. Die Anweisung enthält möglicherweise keinen vollständigen SOAP-Umschlag (Simple Object Access Protocol) und keine XML für die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] **Discover** handeln. Hinweis: Während [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] vollständige SOAP-Umschläge und die **Discover** -Methode unterstützt, ist das bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragsschritten nicht der Fall.  
  
### <a name="analysis-services-query-job-steps"></a>Analysis Services-Abfrageauftragsschritte  
Wenn Sie einen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] -Abfrageauftragsschritt erstellen, müssen Sie folgende Schritte durchführen:  
  
-   Identifizieren der OLAP-Datenbank, in der Sie den Auftragsschritt ausführen.  
  
-   Eingeben der auszuführenden Anweisung. Bei der Anweisung muss es sich um eine MDX-Abfrage handeln (Multidimensional Expressions, mehrdimensionale Ausdrücke).  
  
Weitere Informationen zu MDX finden Sie unter [Grundlegendes zur MDX-Anweisung (MDX)](http://msdn.microsoft.com/en-us/a560383b-bb58-472e-95f5-65d03d8ea08b).  
  
## <a name="integration-services-packages"></a>Integration Services-Pakete  
Wenn Sie einen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] -Paketauftragsschritt erstellen, müssen Sie folgende Schritte durchführen:  
  
-   Identifizieren der Paketquelle.  
  
-   Identifizieren des Paketspeicherorts.  
  
-   Identifizieren der Konfigurationsdateien, wenn diese für das Paket erforderlich sind.  
  
-   Identifizieren der Befehlsdateien, wenn diese für das Paket erforderlich sind.  
  
-   Identifizieren der für das Paket zu verwendenden Überprüfung. Sie können beispielsweise angeben, dass das Paket signiert werden oder eine bestimmte Paket-ID aufweisen muss.  
  
-   Identifizieren der Datenquellen für das Paket.  
  
-   Identifizieren der Protokollanbieter für das Paket.  
  
-   Angeben von Variablen und Werten, die vor dem Ausführen des Pakets festgelegt werden.  
  
-   Identifizieren von Ausführungsoptionen.  
  
-   Hinzufügen oder Ändern von Befehlszeilenoptionen.  
  
Hinweis: Wenn Sie das Paket im SSIS-Katalog bereitgestellt und Sie **SSIS-Katalog** als Paketquelle angegeben haben, werden viele dieser Konfigurationsinformationen automatisch vom Paket abgerufen. Auf der Registerkarte **Konfiguration** können Sie die Umgebung, Parameterwerte, Verbindungs-Manager-Werte und Eigenschaftenüberschreibungen angeben und ob das Paket in einer 32-Bit-Laufzeitumgebung ausgeführt wird.  
  
Informationen zum Erstellen von Auftragsschritten, von denen [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] -Pakete ausgeführt werden, finden Sie unter [Aufträge des SQL Server-Agents für Pakete](http://msdn.microsoft.com/en-us/ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|||  
|-|-|  
|**Description**|**Thema**|  
|Beschreibt, wie ein Auftragsschritt mit einem ausführbaren Programm erstellt wird.|[Erstellen eines CmdExec-Auftragsschritts](../../ssms/agent/create-a-cmdexec-job-step.md)|  
|Beschreibt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Berechtigungen zurückgesetzt werden.|[Konfigurieren eines Benutzers zum Erstellen und Verwalten von SQL Server-Agent-Aufträgen](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)|  
|Beschreibt, wie ein [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritt erstellt wird.|[Erstellen eines Transact-SQL-Auftragsschritts](../../ssms/agent/create-a-transact-sql-job-step.md)|  
|Beschreibt, wie Optionen für Transact-SQL-Auftragsschritte für den Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent erstellt werden.|[Definieren von Optionen für Transact-SQL-Auftragsschritte](../../ssms/agent/define-transact-sql-job-step-options.md)|  
|Beschreibt, wie ein ActiveX-Skript-Auftragsschritt erstellt wird.|[Erstellen eines ActiveX-Skript-Auftragsschritts](../../ssms/agent/create-an-activex-script-job-step.md)|  
|Beschreibt, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftragsschritte erstellt und definiert werden, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Analysis Services-Befehle und -Abfragen ausführen.|[Erstellen eines Analysis Services-Auftragsschritts](../../ssms/agent/create-an-analysis-services-job-step.md)|  
|Beschreibt, welche Aktion [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausführen sollte, wenn während der Auftragsausführung ein Fehler auftritt.|[Set Job Step Success or Failure Flow](../../ssms/agent/set-job-step-success-or-failure-flow.md)|  
|Beschreibt, wie Auftragsschrittdetails im Dialogfeld Auftragsschritt-Eigenschaften angezeigt werden.|[Anzeigen von Auftragsschrittinformationen](../../ssms/agent/view-job-step-information.md)|  
|Beschreibt, wie ein Auftragsschrittprotokoll des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents gelöscht wird.|[Löschen eines Auftragsschrittprotokolls](../../ssms/agent/delete-a-job-step-log.md)|  
  
## <a name="see-also"></a>Siehe auch  
[sysjobstepslogs (Transact-SQL)](http://msdn.microsoft.com/en-us/128c25db-0b71-449d-bfb2-38b8abcf24a0)  
[Erstellen von Aufträgen](../../ssms/agent/create-jobs.md)  
[sp_add_job (Transact-SQL)](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  

