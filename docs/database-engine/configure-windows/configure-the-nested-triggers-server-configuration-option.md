---
title: "Konfigurieren der Serverkonfigurationsoption „Geschachtelte Trigger“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- nested triggers option
ms.assetid: 29d7372b-d406-4a5b-80c6-a2d231d25211
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 28dc19f9d28cc2556ac948c857298dfc29eebb1b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-nested-triggers-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Geschachtelte Trigger
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Geschachtelte Trigger** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mit der Option **Geschachtelte Trigger** wird gesteuert, ob ein AFTER-Trigger kaskadiert werden kann. Das heißt, ob eine Aktion ausgeführt werden kann, die einen anderen Trigger initiiert, der wiederum einen anderen Trigger initiiert usw. Wenn die Option **Geschachtelte Trigger** auf 0 festgelegt ist, können AFTER-Trigger nicht kaskadiert werden. Wenn die Option **Geschachtelte Trigger** auf 1 festgelegt ist (Standardeinstellung), können AFTER-Trigger auf bis zu 32 Ebenen kaskadiert werden. INSTEAD OF-Trigger können unabhängig von der festgelegten Option geschachtelt werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option Geschachtelte Trigger mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option Geschachtelte Trigger](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-configure-the-nested-triggers-option"></a>So konfigurieren Sie die Option Geschachtelte Trigger  
  
1.  Klicken Sie im **Objekt-Explorer**mit der rechten Maustaste auf einen Server, und wählen Sie dann **Eigenschaften**aus.  
  
2.  Legen Sie auf der Seite **Erweitert** die Option **Triggern ermöglichen, weitere Trigger auszulösen** auf **True** (Standardeinstellung) oder **False**fest.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-nested-triggers-option"></a>So konfigurieren Sie die Option Geschachtelte Trigger  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `nested triggers` auf `0`festzulegen.  
  
```wmimof  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'nested triggers', 0 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Geschachtelte Trigger  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von geschachtelten Triggern](../../relational-databases/triggers/create-nested-triggers.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

