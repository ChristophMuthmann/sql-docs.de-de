---
title: "Sicherheit f&#252;r den Protokolllese-Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.LRA.f1"
helpviewer_keywords: 
  - "Sicherheit für den Protokolllese-Agent (Dialogfeld)"
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Sicherheit f&#252;r den Protokolllese-Agent
  Mithilfe des Dialogfelds **Sicherheit für den Protokolllese-Agent** können Sie folgende Angaben machen:  
  
-   Das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Protokolllese-Agent auf dem Verteiler ausgeführt wird. Das Windows-Konto wird auch als *Prozesskonto*bezeichnet, da der Agentprozess unter diesem Konto ausgeführt wird.  
  
-   Der Kontext, unter dem der Protokolllese-Agent Verbindungen mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger aufbaut. Die Verbindung kann entweder durch Identitätswechsel zum Windows-Konto oder unter dem Kontext eines von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos hergestellt werden.  
  
    > [!NOTE]  
    >  Der Protokolllese-Agent stellt Verbindungen mit dem Verleger her, auch wenn der Verleger und der Verteiler auf demselben Computer ausgeführt werden. Der Protokolllese-Agent stellt auch Verbindungen mit dem Verteiler her. Diese Verbindungen werden immer durch einen Identitätswechsel zum Windows-Konto hergestellt, unter dem der Agent ausgeführt wird.  
  
     Für Oracle-Verleger, geben Sie den Kontext an, unter dem der Protokolllese-Agent eine Verbindung, auf dem Verleger in herstellt, die **Verlegereigenschaften** (Dialogfeld) (verfügbar über die **Verteilereigenschaften** im Dialogfeld). Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Alle Konten müssen gültig sein, und für jedes Konto muss das richtige Kennwort angegeben sein. Konten und Kennwörter werden erst bei der Ausführung eines Agents überprüft.  
  
## Optionen  
 **Prozesskonto**  
 Geben Sie das Windows-Konto an, unter dem der Protokolllese-Agent auf dem Verteiler ausgeführt wird. Das Windows-Konto, das Sie angeben, muss mindestens Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.  
  
 **Das Kennwort** und **Kennwort bestätigen**  
 In diese Felder geben Sie das Kennwort für das Windows-Konto ein.  
  
 **Verbindung mit dem Verleger herstellen**  
 Auswählen, ob der Protokolllese-Agent Verbindungen mit dem Verleger durch Identitätswechsel des Kontos im angegebenen die **Prozesskonto** Textfeld oder mithilfe einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konto. Wenn Sie sich für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto entscheiden, müssen Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzernamen und ein Kennwort eingeben.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie auswählen, um das Windows-Benutzerkonto zu imitieren, anstatt mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konto.  
  
 Das Windows-Konto oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verbindung verwendete Konto muss zumindest Mitglied der **Db_owner** festen Datenbankrolle in der Publikationsdatenbank.  
  
## Siehe auch  
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  