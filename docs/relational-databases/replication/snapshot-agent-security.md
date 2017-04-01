---
title: "Sicherheit f&#252;r den Momentaufnahme-Agent | Microsoft Docs"
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
  - "sql13.rep.security.SSA.f1"
helpviewer_keywords: 
  - "Sicherheit für den Momentaufnahme-Agent (Dialogfeld)"
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Sicherheit f&#252;r den Momentaufnahme-Agent
  Mithilfe des Dialogfelds **Sicherheit für den Momentaufnahme-Agent** können Sie folgende Angaben machen:  
  
-   Das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Momentaufnahme-Agent auf dem Verteiler ausgeführt wird. Das Windows-Konto wird auch als *Prozesskonto*bezeichnet, da der Agentprozess unter diesem Konto ausgeführt wird.  
  
-   Der Kontext, unter dem der Momentaufnahme-Agent Verbindungen mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger herstellt. Die Verbindung kann entweder durch Identitätswechsel zum Windows-Konto oder unter dem Kontext eines von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos hergestellt werden.  
  
    > [!NOTE]  
    >  Der Momentaufnahme-Agent stellt Verbindungen mit dem Verleger her, auch wenn der Verleger und der Verteiler auf demselben Computer ausgeführt werden. Der Momentaufnahme-Agent stellt auch Verbindungen mit dem Verteiler her. Diese Verbindungen werden immer durch einen Identitätswechsel zum Windows-Konto hergestellt, unter dem der Agent ausgeführt wird.  
  
     Für Oracle-Verleger, geben Sie den Kontext an, unter dem der Snapshot-Agent eine Verbindung, auf dem Verleger in herstellt, die **Verlegereigenschaften** (Dialogfeld) (verfügbar über die **Verteilereigenschaften** im Dialogfeld). Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Alle Konten müssen gültig sein, und für jedes Konto muss das richtige Kennwort angegeben sein. Konten und Kennwörter werden erst bei der Ausführung eines Agents überprüft.  
  
## Optionen  
 **Prozesskonto**  
 Geben Sie das Windows-Konto an, unter dem der Momentaufnahme-Agent auf dem Verteiler ausgeführt wird. Das angegebene Windows-Konto muss folgende Bedingungen erfüllen:  
  
-   Zumindest Mitglied der **Db_owner** -Datenbankrolle in der Verteilungsdatenbank.  
  
-   Es muss über Schreibberechtigungen für die Momentaufnahme-Freigabe verfügen.  
  
 **Das Kennwort** und **Kennwort bestätigen**  
 In diese Felder geben Sie das Kennwort für das Windows-Konto ein.  
  
 **Verbindung mit dem Verleger herstellen**  
 Auswählen, ob der Snapshot-Agent Verbindungen mit dem Verleger durch Identitätswechsel des Kontos im angegebenen die **Prozesskonto** Textfeld oder mithilfe einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konto. Wenn Sie sich für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto entscheiden, müssen Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzernamen und ein Kennwort eingeben.  
  
> [!NOTE]  
>  Es wird empfohlen, kein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konto zu verwenden und stattdessen festzulegen, dass der Agent die Identität des Windows-Kontos annimmt.  
  
 Das Windows-Konto oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die Verbindung verwendete Konto muss zumindest Mitglied der **Db_owner** festen Datenbankrolle in der Publikationsdatenbank.  
  
## Siehe auch  
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  