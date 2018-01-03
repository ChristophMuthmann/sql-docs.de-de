---
title: "Konfigurieren der Serverkonfigurationsoption „Startprozeduren suchen“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: scan for startup procs option
ms.assetid: 6bf9d252-e766-458d-9dcd-23d895f032a2
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5da0fb043922a9771ff50bc1aa951b31d00c568c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="configure-the-scan-for-startup-procs-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Startprozeduren suchen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Startprozeduren suchen** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Sie können mithilfe der Option **Startprozeduren suchen** nach der automatischen Ausführung gespeicherter Prozeduren zum Startzeitpunkt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suchen. Wenn diese Option auf 1 festgelegt ist, sucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nach allen automatisch ausgeführten gespeicherten Prozeduren, die auf dem Server definiert sind, und führt diese aus. Der Standardwert für **Startprozeduren suchen** ist „0“ (kein Scannen).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **So konfigurieren Sie die Option Startprozeduren suchen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option „Startprozeduren suchen“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Techniker geändert werden.  
  
-   Der Wert für diese Option kann mithilfe von **sp_configure**festgelegt werden. Er wird jedoch automatisch festgelegt, wenn Sie die gespeicherte Systemprozedur **sp_procoption**verwenden. Diese Prozedur wird verwendet, um gespeicherte Prozeduren als automatisch ausgeführte Prozeduren zu kennzeichnen oder die Kennzeichnung aufzuheben. Wird **sp_procoption** zum Kennzeichnen der ersten gespeicherten Prozedur als autoproc verwendet, wird für diese Option automatisch der Wert „1“ festgelegt. Wenn **sp_procoption** verwendet wird, um die Kennzeichnung der letzten gespeicherten Prozedur als autoproc aufzuheben, wird der Wert für diese Option automatisch auf „0“ festgelegt. Wenn Sie **sp_procoption** zum Kennzeichnen bzw. zum Aufheben von Kennzeichnungen verwenden und die Kennzeichnungen von autoprocs vor dem Löschen immer aufheben, ist es nicht notwendig, diese Option manuell festzulegen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>So konfigurieren Sie die Option "Startprozeduren suchen"  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den **Erweitert** -Knoten.  
  
3.  Ändern Sie unter **Sonstiges**die Option **Startprozeduren suchen** in TRUE oder FALSE, indem Sie im Dropdown-Listenfeld den gewünschten Wert auswählen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>So konfigurieren Sie die Option "Startprozeduren suchen"  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `scan for startup procs` auf `1`festzulegen.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'scan for startup procs', 1 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Startprozeduren suchen  
 Der Server muss neu gestartet werden, bevor die Einstellung wirksam werden kann.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_procoption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)  
  
  
