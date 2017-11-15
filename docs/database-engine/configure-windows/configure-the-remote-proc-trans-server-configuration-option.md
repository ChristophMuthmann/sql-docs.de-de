---
title: "Konfigurieren der Serverkonfigurationsoption „remote proc trans“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote proc trans option
- distributed transactions [SQL Server], enforcing
ms.assetid: cfbc6158-ab96-44b4-87eb-ea278c1b0c6b
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 870769ef0c99cd35dcafdab83a09c7e2c050a097
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-remote-proc-trans-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption „remote proc trans“
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **remote proc trans** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mit der Option **remote proc trans** können Sie die Aktionen einer Server-zu-Server-Prozedur über eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator-Transaktion (MS DTC) schützen.  
  
 Legen Sie den Wert von **remote proc trans** auf 1 fest, um eine von MS DTC koordinierte verteilte Transaktion zum Schutz der ACID-Eigenschaften (atomar, konsistent, isoliert und beständig) von Transaktionen bereitzustellen. Sitzungen, die nach dem Festlegen dieser Option auf 1 beginnen, erben die Konfigurationseinstellung als Standardeinstellung.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option „remote proc trans“ mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachbereitung:**  [Nach dem Konfigurieren der Option „remote proc trans“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Um diesen Wert festlegen zu können, müssen Remoteserververbindungen zulässig sein.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option wird aus Gründen der Kompatibilität mit früheren Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Anwendungen bereitgestellt, die remote gespeicherte Prozeduren verwenden. Anstatt remote gespeicherte Prozeduren aufzurufen, sollten Sie verteilte Abfragen verwenden, die auf Verbindungsserver verweisen. Diese werden mithilfe von [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)definiert.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-proc-trans-option"></a>So konfigurieren Sie die Option „remote proc trans“  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den Knoten **Verbindungen** .  
  
3.  Aktivieren Sie unter **Remoteserververbindungen**das Kontrollkästchen **Verteilte Transaktionen für die Kommunikation zwischen Servern verlangen** .  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-remote-proc-trans-option"></a>So konfigurieren Sie die Option „remote proc trans“  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `remote proc trans` auf `1`festzulegen.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote proc trans', 1 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachbereitung: Nach dem Konfigurieren der Option „remote proc trans“  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
