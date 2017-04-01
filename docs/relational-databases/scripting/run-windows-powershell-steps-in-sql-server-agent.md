---
title: "Ausf&#252;hren von Windows PowerShell-Schritten in SQL Server-Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Ausf&#252;hren von Windows PowerShell-Schritten in SQL Server-Agent
  Führen Sie die SQL Server PowerShell-Skripts mithilfe des SQL Server-Agent nach Zeitplan aus.  
  
1.  **Vorbereitungen:**  [Einschränkungen](#LimitationsRestrictions)  
  
2.  **Zur Ausführung von PowerShell von SQL Server-Agent mit:**  [PowerShell-Auftragsschritt](#PShellJob), [Eingabeaufforderungs-Auftragsschritt](#CmdExecJob)  
  
## Vorbereitungen  
 Es gibt mehrere Typen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Auftragsschritten. Jeder Typ ist einem Subsystem zugeordnet, das eine bestimmte Umgebung implementiert, wie eine Replikations-Agent- oder Eingabeaufforderungsumgebung. Sie können Windows PowerShell-Skripts schreiben und die Skripts dann mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent in Aufträge integrieren, die zu festgelegten Zeiten oder in Reaktion auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ereignisse ausgeführt werden. Windows PowerShell-Skripts können mit entweder einem Eingabeaufforderungs-Auftragsschritt oder einem PowerShell-Auftragsschritt ausgeführt werden.  
  
1.  Verwenden Sie einen PowerShell-Auftragsschritt, damit das Subsystem des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent das Hilfsprogramm **sqlps** ausführt, das PowerShell 2.0 startet und das **sqlps** -Modul importiert.  
  
2.  Verwenden Sie einen Auftragsschritt an einer Eingabeaufforderung, um &lt;ui&gt;PowerShell.exe&lt;/ui&gt; auszuführen, und geben Sie ein Skript an, das das **sqlps** -Modul importiert.  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
  
> [!CAUTION]  
>  Jeder Auftragsschritt des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents, der PowerShell mit dem Modul **sqlps** ausführt, startet einen Prozess, der etwa 20 MB Arbeitsspeicher in Anspruch nimmt. Die gleichzeitige Ausführung einer großen Anzahl von Windows PowerShell-Auftragsschritten kann sich negativ auf die Leistung auswirken.  
  
##  <a name="PShellJob"></a> Erstellen eines PowerShell-Auftragsschritts  
 **So erstellen Sie einen PowerShell-Auftragsschritt**  
  
1.  Erweitern Sie **SQL Server-Agent**, erstellen Sie einen neuen Auftrag, oder klicken Sie mit der rechten Maustaste auf einen vorhandenen Auftrag, und klicken Sie dann auf **Eigenschaften**. Weitere Informationen zum Erstellen eines Auftrags finden Sie unter [Erstellen von Aufträgen](../../ssms/agent/create-jobs.md).  
  
2.  Klicken Sie im Dialogfeld **Auftragseigenschaften** auf die Seite **Schritte** und dann auf **Neu**.  
  
3.  Geben Sie im Dialogfeld **Neuer Auftragsschritt** unter **Schrittname**einen Schrittnamen für den Auftrag ein.  
  
4.  Klicken Sie in der Liste **Typ** auf **PowerShell**.  
  
5.  Wählen Sie in der Liste **Ausführen als** das Proxykonto mit den Anmeldeinformationen für den Auftrag aus.  
  
6.  Geben Sie im Feld **Befehl** die PowerShell-Skriptsyntax ein, die für den Auftragsschritt ausgeführt wird. Klicken Sie alternativ auf **Öffnen** , und wählen Sie eine Datei aus, die die Skriptsyntax enthält.  
  
7.  Klicken Sie auf die Seite **Erweitert** , um die folgenden Optionen für den Auftragsschritt festzulegen: welche Aktion bei der erfolgreichen oder fehlerhaften Ausführung des Auftragsschrittes jeweils auszuführen ist, wie oft der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent versuchen soll, den Auftragsschritt auszuführen, und wie viele Wiederholungsversuche unternommen werden sollen.  
  
##  <a name="CmdExecJob"></a> Erstellen eines Eingabeaufforderungs-Auftragsschritts  
 **So erstellen Sie einen CmdExec-Auftragsschritt**  
  
1.  Erweitern Sie **SQL Server-Agent**, erstellen Sie einen neuen Auftrag, oder klicken Sie mit der rechten Maustaste auf einen vorhandenen Auftrag, und klicken Sie dann auf **Eigenschaften**. Weitere Informationen zum Erstellen eines Auftrags finden Sie unter [Erstellen von Aufträgen](../../ssms/agent/create-jobs.md).  
  
2.  Klicken Sie im Dialogfeld **Auftragseigenschaften** auf die Seite **Schritte** und dann auf **Neu**.  
  
3.  Geben Sie im Dialogfeld **Neuer Auftragsschritt** unter **Schrittname**einen Schrittnamen für den Auftrag ein.  
  
4.  Wählen Sie in der Liste **Typ** den Eintrag **Betriebssystem (CmdExec)** aus.  
  
5.  Wählen Sie in der Liste **Ausführen als** das Proxykonto mit den Anmeldeinformationen für den Auftrag aus. Standardmäßig werden CmdExec-Auftragsschritte im Kontext des Kontos des SQL Server-Agent-Dienstes ausgeführt.  
  
6.  Geben Sie in das Feld **Prozessexitcode eines erfolgreichen Befehls** einen Wert zwischen 0 und 999999 ein.  
  
7.  Geben Sie im Feld **Befehl** "powershell.exe" zusammen mit Parametern, die das auszuführende PowerShell-Skript angeben, ein.  
  
8.  Klicken Sie auf die Seite **Erweitert** , um Optionen für Auftragsschritte festzulegen, z. B. welche Aktion bei der erfolgreichen oder fehlerhaften Ausführung des Auftragsschrittes jeweils auszuführen ist, wie oft der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent versuchen soll, den Auftragsschritt auszuführen, und in welche Datei der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent die Auftragsschrittausgabe schreiben soll. Nur Mitglieder der festen Serverrolle **sysadmin** können die Auftragsschrittausgabe in eine Betriebssystemdatei schreiben.  
  
## Siehe auch  
 [SQL Server-PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  