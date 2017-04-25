---
title: Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes | Microsoft-Dokumentation
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
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af137c019a7f96769b801d01f882e1d98b0da2ea
ms.lasthandoff: 04/11/2017

---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes
In diesem Thema wird beschrieben, wie Sie den SQL Server-Agent-Dienst in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]starten, beenden oder neu starten.  
  
Sie können den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst so konfigurieren, dass er automatisch zusammen mit dem Betriebssystem gestartet wird, oder ihn manuell starten, wenn Sie Aufträge ausführen müssen. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst kann beendet oder angehalten werden, um Aufträge, Operatorbenachrichtigungen und Warnungen auszusetzen.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   [Starten, Beenden oder Neustarten des SQL Server-Agent-Diensts mit SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent muss als Dienst ausgeführt werden, um administrative Tasks zu automatisieren. Weitere Informationen finden Sie unter [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md).  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten wird nur im Objekt-Explorer angezeigt, wenn Sie die Berechtigung besitzen, ihn zu verwenden.  
  
### <a name="Security"></a>Sicherheit  
  
#### <a name="Permissions"></a>Berechtigungen  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent muss zur Verwendung der Anmeldeinformationen eines Kontos konfiguriert werden, das Mitglied der festen Serverrolle **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ist, um seine Funktionen ausführen zu können. Das Konto muss über die folgenden Windows-Berechtigungen verfügen:  
  
-   Anmelden als Dienst (SeServiceLogonRight)  
  
-   Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)  
  
-   Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)  
  
-   Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)  
  
Weitere Informationen zu den Windows-Berechtigungen, die für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto erforderlich sind, finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) und [Einrichten von Windows-Dienstkonten](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>So können Sie den SQL Server-Agent-Dienst starten, beenden oder neu starten  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, auf dem Sie den SQL Server-Agent-Dienst verwalten möchten.  
  
2.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Agent**, und wählen Sie dann **Starten**, **Beenden**oder **Neu starten**aus.  
  
3.  Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.  
  
4.  Klicken Sie bei der Frage, ob die Aktion ausgeführt werden soll, auf **Ja**.  
  
Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Starten, Beenden, Anhalten, Fortsetzen und Neustarten des Datenbankmoduls, SQL Server-Agent oder des SQL Server-Browsers](http://msdn.microsoft.com/en-us/32660a02-e5a1-411a-9e57-7066ca459df6)  
  
-   [Autostart SQL Server Agent &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/agent/autostart-sql-server-agent-sql-server-management-studio.md)  
  

