---
title: Erstellen eines Operators | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 192d0a6c93a19c86d853492624a8fda40378be90
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-an-operator"></a>Create an Operator
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie Sie in der Konfiguration festlegen können, dass ein Benutzer Benachrichtigungen über [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]empfängt.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So erstellen Sie einen Operator mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   Die Pager- und **net send** -Optionen werden in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nicht mehr im [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden.  
  
-   Beachten Sie, dass E-Mail- und Pagerbenachrichtigungen an Operatoren nur versendet werden können, wenn der SQL Server-Agent für die Verwendung von Datenbank-E-Mail konfiguriert ist. Weitere Informationen finden Sie unter [Zuweisen von Warnungen zu einem Operator](http://msdn.microsoft.com/library/ms190038.aspx).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Nur Mitglieder der festen Serverrolle **sysadmin** können Operatoren erstellen.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>So erstellen Sie einen Operator  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, auf dem Sie den SQL Server-Agent-Operator erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Operatoren** , und wählen Sie dann **Neuer Operator**aus.  
  
    Die folgenden Optionen befinden sich im Dialogfeld **Neuer Operator** auf der Seite **Allgemein** :  
  
    **Name**  
    Ändern Sie den Namen des Operators.  
  
    **Enabled**  
    Aktiviert den Operator. Bei fehlender Aktivierung werden keine Benachrichtigungen an den Operator gesendet.  
  
    **E-Mail-Name**  
    Gibt die E-Mail-Adresse des Operators an.  
  
    **NET SEND-Adresse**  
    Gibt die für **NET SEND**zu verwendende Adresse an.  
  
    **Pager-E-Mail-Name**  
    Gibt die E-Mail-Adresse für den Pager des Operators an.  
  
    **Pager empfangsbereit am**  
    Legt fest, zu welchen Zeiten der Pager aktiv ist.  
  
    **Montag - Sonntag**  
    Wählen Sie die Tage aus, an denen der Pager aktiv ist.  
  
    **Arbeitstag - Beginn**  
    Wählen Sie die Tageszeit aus, nach deren Eintreten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent Meldungen an den Pager sendet.  
  
    **Arbeitstag - Ende**  
    Wählen Sie die Tageszeit aus, nach deren Eintreten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent keine weiteren Meldungen an den Pager sendet.  
  
    Die folgenden Optionen befinden sich im Dialogfeld **Neuer Operator** auf der Seite **Benachrichtigungen** :  
  
    **Warnungen**  
    Zeigt die Warnungen in der Instanz an.  
  
    **Jobs**  
    Zeigt die Aufträge in der Instanz an.  
  
    **Warnungsliste**  
    Listet die Warnungen in der Instanz auf.  
  
    **Auftragsliste**  
    Listet die Aufträge in der Instanz auf.  
  
    **E-Mail**  
    Benachrichtigt den Operator per E-Mail.  
  
    **Pager**  
    Benachrichtigt den Operator, indem eine E-Mail-Nachricht an die Pageradresse gesendet wird.  
  
    **Net send**  
    Benachrichtigt diesen Operator per **net send**.  
  
4.  Klicken Sie auf **OK**, wenn Sie das Erstellen des neuen Operators abgeschlossen haben.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-create-an-operator"></a>So erstellen Sie einen Operator  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- sets up the operator information for user 'danwi.'
    -- The operator is enabled.   
    -- SQL Server Agent sends notifications by pager 
    -- from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_add_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/817cd98a-4dff-4ed8-a546-f336c144d1e0).  
  
