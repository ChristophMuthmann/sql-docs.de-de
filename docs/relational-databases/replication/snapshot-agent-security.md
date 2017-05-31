---
title: "Sicherheit für den Momentaufnahme-Agent | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.security.SSA.f1
helpviewer_keywords:
- Snapshot Agent Security dialog box
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a3834548fba6eb52e57836eefdb9f8917cb35d0
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="snapshot-agent-security"></a>Sicherheit für den Momentaufnahme-Agent
  Mithilfe des Dialogfelds **Sicherheit für den Momentaufnahme-Agent** können Sie folgende Angaben machen:  
  
-   Das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto, unter dem der Momentaufnahme-Agent auf dem Verteiler ausgeführt wird. Das Windows-Konto wird auch als *Prozesskonto*bezeichnet, da der Agentprozess unter diesem Konto ausgeführt wird.  
  
-   Der Kontext, unter dem der Momentaufnahme-Agent Verbindungen mit dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger herstellt. Die Verbindung kann entweder durch Identitätswechsel zum Windows-Konto oder unter dem Kontext eines von Ihnen angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos hergestellt werden.  
  
    > [!NOTE]  
    >  Der Momentaufnahme-Agent stellt Verbindungen mit dem Verleger her, auch wenn der Verleger und der Verteiler auf demselben Computer ausgeführt werden. Der Momentaufnahme-Agent stellt auch Verbindungen mit dem Verteiler her. Diese Verbindungen werden immer durch einen Identitätswechsel zum Windows-Konto hergestellt, unter dem der Agent ausgeführt wird.  
  
     Geben Sie für Oracle-Verleger im Dialogfeld **Verlegereigenschaften** den Kontext an, unter dem der Momentaufnahme-Agent eine Verbindung mit dem Verleger herstellt (das Dialogfeld ist vom Dialogfeld **Verteilereigenschaften** aus verfügbar). Weitere Informationen finden Sie unter [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Alle Konten müssen gültig sein, und für jedes Konto muss das richtige Kennwort angegeben sein. Konten und Kennwörter werden erst bei der Ausführung eines Agents überprüft.  
  
## <a name="options"></a>Optionen  
 **Process account**  
 Geben Sie das Windows-Konto an, unter dem der Momentaufnahme-Agent auf dem Verteiler ausgeführt wird. Das angegebene Windows-Konto muss folgende Bedingungen erfüllen:  
  
-   Es muss mindestens Mitglied der festen Datenbankrolle **db_owner** in der Verteilungsdatenbank sein.  
  
-   Es muss über Schreibberechtigungen für die Momentaufnahme-Freigabe verfügen.  
  
 **Kennwort** und **Kennwort bestätigen**  
 In diese Felder geben Sie das Kennwort für das Windows-Konto ein.  
  
 **Verbindung mit dem Verleger herstellen**  
 Wählen Sie aus, ob der Momentaufnahme-Agent die Verbindungen mit dem Verleger entweder durch Annahme der Identität des im Textfeld **Prozesskonto** angegebenen Kontos oder mithilfe eines [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Kontos herstellen soll. Wenn Sie sich für ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto entscheiden, müssen Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzernamen und ein Kennwort eingeben.  
  
> [!NOTE]  
>  Es wird empfohlen, kein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto zu verwenden und stattdessen festzulegen, dass der Agent die Identität des Windows-Kontos annimmt.  
  
 Das für die Verbindung verwendete Windows-Konto bzw. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konto muss mindestens Mitglied der festen Datenbankrolle **db_owner** in der Veröffentlichungsdatenbank sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Anmeldeinformationen und Kennwörtern bei der Replikation](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Sicherheitsmodell des Replikations-Agents](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replikations-Agents (Übersicht)](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
