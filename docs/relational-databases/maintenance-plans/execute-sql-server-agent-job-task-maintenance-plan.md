---
title: "Task &#39;Auftrag des SQL Server-Agents ausf&#252;hren&#39; (Wartungsplan) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.maint.executejob.f1"
helpviewer_keywords: 
  - "Auftrag des SQL Server-Agents ausführen (Dialogfeld für den Task)"
ms.assetid: 4ed75956-ebb8-4d8c-9c16-fc0eb00bd3a0
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# Task &#39;Auftrag des SQL Server-Agents ausf&#252;hren&#39; (Wartungsplan)
  Verwenden Sie das Dialogfeld **Task 'Auftrag des SQL Server-Agents ausführen'** , um Aufträge des Microsoft SQL Server-Agents innerhalb eines Wartungsplans auszuführen. Diese Option ist nicht verfügbar, wenn für die ausgewählte Verbindung keine Aufträge des SQL Server-Agents vorliegen.  
  
 Dieser Task verwendet die Anweisung **.sp_start_job**.  
  
## Liste der Benutzeroberflächenelemente  
 **Verbindung**  
 Wählen Sie die Serververbindung aus, die bei der Ausführung dieses Tasks verwendet werden soll.  
  
 **Neu**  
 Erstellen Sie eine neue Serververbindung, die bei der Ausführung dieses Tasks verwendet werden soll. Das Dialogfeld **Neue Verbindung** wird im Folgenden beschrieben.  
  
 **Verfügbare Aufträge des SQL Server-Agents**  
 Wählen Sie den auszuführenden Auftrag aus. Im Raster werden **Auftragsname** und **Beschreibung** angezeigt, um die Aufträge zu kennzeichnen.  
  
 **T-SQL anzeigen**  
 Zeigt die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen an, die für diesen Task auf dem Server auf Basis der ausgewählten Optionen ausgeführt werden.  
  
> [!NOTE]  
>  Wenn die Anzahl der betroffenen Objekte groß ist, kann die Anzeige erhebliche Zeit in Anspruch nehmen.  
  
## Neue Verbindung (Dialogfeld)  
 **Verbindungsname**  
 Geben Sie einen Namen für die neue Verbindung ein.  
  
 **Wählen Sie einen Servernamen aus, oder geben Sie ihn ein.**  
 Wählen Sie den Server aus, zu dem bei der Ausführung dieses Tasks eine Verbindung hergestellt werden soll.  
  
 **Aktualisieren**  
 Mithilfe dieser Option aktualisieren Sie die Liste der verfügbaren Server.  
  
 **Geben Sie Informationen zum Anmelden am Server ein**  
 Legt fest, wie die Authentifizierung gegenüber dem Server stattfindet.  
  
 **Integrierte Sicherheit von Windows NT verwenden**  
 Stellt mithilfe der Microsoft Windows-Authentifizierung eine Verbindung zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
 **Bestimmten Benutzernamen und bestimmtes Kennwort verwenden**  
 Stellt mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung eine Verbindung zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her. Diese Option ist nicht verfügbar.  
  
 **Benutzername**  
 Stellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
 **Kennwort**  
 Stellt ein Kennwort für den Gebrauch bei der Authentifizierung bereit. Diese Option ist nicht verfügbar.  
  
## Siehe auch  
 [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)   
 [Erstellen eines Auftrags](../../ssms/agent/create-a-job.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  