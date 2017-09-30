---
title: "Konfigurieren der Serverkonfigurationsoption „Remotezugriff“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote servers [SQL Server], stored procedure execution
ms.assetid: f5de748d-1c55-4714-9661-38fe62e5095f
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 3fb74c78868691c1a59a132eb637dedbfebec41e
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="configure-the-remote-access-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Remotezugriff
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird das Feature "Remotezugriff" erläutert. Diese Konfigurationsoption ist eine ungünstige und veraltete Kommunikationsfunktion für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die Sie vermutlich nicht verwenden sollten. Wenn Sie zu dieser Seite gelangt, weil Sie Probleme beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]haben, lesen Sie stattdessen eines der folgenden Themen:  
  
-   [Lernprogramm: Erste Schritte mit dem Datenbankmodul](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
-   [Anmelden an SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
-   [Herstellen einer Verbindung mit SQL Server, wenn Systemadministratoren gesperrt sind](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
-   [Herstellen einer Verbindung zu einem registrierten Server &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/connect-to-a-registered-server-sql-server-management-studio.md)  
  
-   [Herstellen einer Verbindung mit einer beliebigen SQL Server-Komponente aus SQL Server Management Studio](http://msdn.microsoft.com/library/5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e)  
  
-   [Herstellen einer Verbindung mit dem Datenbankmodul mithilfe von sqlcmd](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)  
  
-   [So beheben Sie Verbindungsfehler mit dem SQL Server-Datenbankmodul](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
 Programmierer finden möglicherweise die folgenden Themen nützlich:  
  
-   [Vorgehensweise: Verbinden mit SQL Server mithilfe der SQL-Authentifizierung in ASP.NET 2.0](https://msdn.microsoft.com/library/ff648340.aspx)  
  
-   [Herstellen einer Verbindung zu einer Instanz von SQL Server](../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)  
  
-   [Vorgehensweise: Erstellen von Verbindungen zu SQL Server-Datenbanken](https://msdn.microsoft.com/library/s4yys16a.aspx)  
  
 **Der Hauptteil dieses Themas beginnt hier.**  
  
 In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Remotezugriff** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mithilfe der Option **Remotezugriff** können Sie die Ausführung gespeicherter Prozeduren von lokalen Servern oder Remoteservern steuern, auf denen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt werden. Der Standardwert für diese Option ist 1. Damit wird die Berechtigung zum Ausführen lokal gespeicherter Prozeduren von Remoteservern aus oder zum Ausführen remote gespeicherter Prozeduren vom lokalen Server aus erteilt. Legen Sie die Option auf 0 fest, um zu verhindern, dass lokal gespeicherte Prozeduren von einem Remoteserver aus ausgeführt werden oder dass remote gespeicherte Prozeduren auf dem lokalen Server ausgeführt werden können.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Verwenden Sie stattdessen [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). <br />Wenn der Remotezugriff nicht aktiviert ist, schlägt die Ausführung einer gespeicherten Prozedur auf einem Verbindungsserver fehl, wenn ein vierteiliger Name wie die Syntax `EXEC SQL01.TestDB.dbo.proc_test;` verwendet wird. Verwenden Sie stattdessen die `EXECUTE ... AT`-Syntax, z.B. `EXEC(N'TestDB.dbo.proc_test') AT [SQL01];`.
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option Remotezugriff mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option „Remotezugriff“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Option **Remotezugriff** gilt nur für Server, die mithilfe von [sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)hinzugefügt wurden, und wird aus Gründen der Abwärtskompatibilität bereitgestellt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-access-option"></a>So konfigurieren Sie die Option Remotezugriff  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den Knoten **Verbindungen** .  
  
3.  Aktivieren oder deaktivieren Sie unter **Remoteserververbindungen**das Kontrollkästchen **Remoteverbindungen mit diesem Server zulassen** .  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-remote-access-option"></a>So konfigurieren Sie die Option Remotezugriff  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `remote access` auf `0`festzulegen.  
  
```tsql  
EXEC sp_configure 'remote access', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Remotezugriff  
 Diese Einstellung wird erst wirksam, wenn Sie SQL Server neu starten.  
  
## <a name="see-also"></a>Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

