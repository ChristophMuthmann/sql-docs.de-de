---
title: Festlegen des Dienststartkontos für den SQL Server-Agent | Microsoft-Dokumentation
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
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 37582f52b59a254c12b7b8981b1298d525fa31fa
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/10/2018
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Das Dienststartkonto des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents definiert das Windows-Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ausgeführt wird, sowie die zugehörigen Netzwerkberechtigungen. In diesem Thema wird beschrieben, wie Sie das Dienstkonto für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Konfigurations-Manager in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]festlegen.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Sicherheit](#Security)  
  
-   [So legen Sie das Dienststartkonto für den SQL Server-Agent mit SQL Server Management Studio fest](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   Seit [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]muss das Dienststartkonto für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent nicht mehr ein Mitglied der Administratorengruppe von [!INCLUDE[msCoName](../../includes/msconame_md.md)] sein. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienststartkonto muss jedoch ein Mitglied der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Serverrolle „sysadmin“ sein. Das Konto muss Mitglied der „msdb“-Datenbankrolle „TargetServersRole“ auf dem Masterserver sein, um die Multiserver-Auftragsverarbeitung verwenden zu können.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten wird nur im Objekt-Explorer angezeigt, wenn Sie die Berechtigung besitzen, ihn zu verwenden.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent muss zur Verwendung der Anmeldeinformationen eines Kontos konfiguriert werden, das Mitglied der festen Serverrolle **sysadmin** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ist, um seine Funktionen ausführen zu können. Das Konto muss über die folgenden Windows-Berechtigungen verfügen:  
  
-   Anmelden als Dienst (SeServiceLogonRight)  
  
-   Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)  
  
-   Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)  
  
-   Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)  
  
Weitere Informationen zu den Windows-Berechtigungen, die für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienstkonto erforderlich sind, finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) und [Einrichten von Windows-Dienstkonten](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>So legen Sie das Dienststartkonto für den SQL Server-Agent fest  
  
1.  Klicken Sie in **Registrierte Server**auf das Pluszeichen, um **Datenbankmodul**zu erweitern.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Lokale Servergruppen** zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Serverinstanz, auf der Sie das Dienststartkonto festlegen möchten, und wählen Sie dann **SQL Server-Konfigurations-Manager**aus.  
  
4.  Klicken Sie im Dialogfeld **Benutzerkontensteuerung** auf **Ja**.  
  
5.  Wählen Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Konfigurations-Manager im Konsolenbereich **SQL Server-Dienste**aus.  
  
6.  Klicken Sie im Detailbereich mit der rechten Maustaste auf **SQL Server-Agent***(Servername)*, wobei *Servername* der Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Instanz ist, für die Sie das Dienststartkonto ändern möchten. Klicken Sie anschließend auf **Eigenschaften**.  
  
7.  Wählen Sie im Dialogfeld **SQL Server-Agent***(Servername)* **Eigenschaften** auf der Registerkarte **Anmelden** eine der folgenden Optionen unter **Anmelden als** aus:  
  
    -   **Integriertes Konto**: Wählen Sie diese Option aus, wenn die Aufträge nur Ressourcen vom lokalen Server benötigen. Informationen zum Auswählen eines integrierten Kontotyps finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](http://msdn.microsoft.com/library/ms191543.aspx).  
  
        > [!IMPORTANT]  
        > Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] lokale Dienstkonto **in** wird nicht für den [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]-Agentdienst unterstützt.  
  
    -   **Dieses Konto**: Wählen Sie diese Option aus, wenn die Aufträge Ressourcen aus dem gesamten Netzwerk benötigen, einschließlich Anwendungsressourcen, wenn Sie Ereignisse an andere Windows-Anwendungsprotokolle weiterleiten möchten oder wenn Sie Operatoren per E-Mail oder Pager benachrichtigen möchten.  
  
        Bei Auswahl dieser Option:  
  
        1.  Geben Sie das Konto, das verwendet wird, um den SQL Server-Agent auszuführen, in das Feld **Kontoname** ein. Klicken Sie alternativ auf **Durchsuchen** , um das Dialogfeld **Benutzer oder Gruppe auswählen** zu öffnen, und wählen Sie das zu verwendende Konto aus.  
  
        2.  Geben Sie im Feld **Kennwort** das Kennwort für das Konto ein. Geben Sie im Feld **Kennwort bestätigen** das Kennwort erneut ein.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Konfigurations-Manager auf die Schaltfläche **Schließen** .  
  
