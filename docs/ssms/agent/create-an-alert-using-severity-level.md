---
title: Erstellen einer Warnung mithilfe von Schweregraden | Microsoft-Dokumentation
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
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 70290c329c16b7718e1add6f733cb0f855d5b2fd
ms.lasthandoff: 04/11/2017

---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
In diesem Thema wird beschrieben, wie eine Warnung des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents in [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder [!INCLUDE[tsql](../../includes/tsql_md.md)]erstellt wird, die beim Auftreten eines Ereignisses mit einem bestimmten Schweregrad ausgelöst wird.  
  
**In diesem Thema**  
  
-   **Vorbereitungen:**  
  
    [Einschränkungen](#Restrictions)  
  
    [Security](#Security)  
  
-   **So erstellen Sie eine Warnung mithilfe von Schweregraden mit**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] lässt sich das gesamte Warnungssystem auf einfache Weise mit einer grafischen Oberfläche verwalten. Dies ist die empfohlene Vorgehensweise, um eine Warnungsinfrastruktur zu konfigurieren.  
  
-   Ereignisse, die mit **xp_logevent** generiert werden, treten in der master-Datenbank auf. Daher wird von **xp_logevent** erst dann eine Warnung ausgegeben, wenn der **@database_name** -Wert für die Warnung den Wert **'master'** oder NULL hat.  
  
-   Bei den Schweregraden 19 bis 25 wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Meldung an das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows gesendet und eine Warnung ausgelöst. Ereignisse mit einem Schweregrad unter 19 lösen nur dann Warnungen aus, wenn Sie **sp_altermessage**, RAISERROR WITH LOG oder **xp_logevent** verwendet haben, um zu erzwingen, dass die Warnungen in das Windows-Anwendungsprotokoll geschrieben werden.  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Berechtigungen  
Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** die Prozedur **sp_add_alert**ausführen.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>So erstellen Sie eine Warnung mithilfe von Schweregraden  
  
1.  Klicken Sie im **** Objekt-Explorer auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Warnung mithilfe des Schweregrads erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Warnungen** , und wählen Sie **Neue Warnung**aus.  
  
4.  Geben Sie im Dialogfeld **Neue Warnung** einen **** Namen für diese Warnung ein.  
  
5.  Klicken Sie in der Liste **Typ** auf **SQL Server-Ereigniswarnung**.  
  
6.  Klicken Sie in der Liste **Datenbankname**auf den **** Datenbanknamen, um die Warnung auf eine bestimmte Datenbank zu beschränken.  
  
7.  Klicken Sie unter **Warnungen werden ausgelöst basierend auf**auf **Schweregrad** , und wählen Sie dann den bestimmten Schweregrad aus, womit die Warnung ausgelöst wird.  
  
8.  Aktivieren Sie das Kontrollkästchen neben **Warnung auslösen, wenn eine Meldung Folgendes enthält** , um die Warnung auf eine bestimmte Zeichenfolge zu beschränken, und geben Sie dann ein Schlüsselwort oder Zeichenfolge für den Meldungstext ****ein. Es können maximal 100 Zeichen eingegeben werden.  
  
9. Klicken Sie auf **OK**.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>So erstellen Sie eine Warnung mithilfe von Schweregraden  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up
    -- the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up
    -- the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The DB will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
Weitere Informationen finden Sie unter [sp_add_alert (Transact-SQL)](http://msdn.microsoft.com/en-us/d9b41853-e22d-4813-a79f-57efb4511f09).  
  

