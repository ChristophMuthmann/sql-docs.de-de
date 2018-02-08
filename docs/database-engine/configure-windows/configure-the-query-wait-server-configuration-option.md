---
title: "Konfigurieren der Serverkonfigurationsoption „Abfragewartezeit“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [SQL Server], timing out
- time [SQL Server], query wait time
- query wait option [SQL Server]
ms.assetid: 0fc4aa01-65a3-4a33-9ef4-caca41add238
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3851530283ba7b2f25984bb7dca73fb562b3151
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="configure-the-query-wait-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Abfragewartezeit
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Abfragewartezeit** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Arbeitsspeicherintensive Abfragen, wie Abfragen mit Sortier- und Hashvorgängen, werden in Warteschlangen eingereiht, wenn nicht ausreichend Arbeitsspeicher zum Ausführen der Abfrage zur Verfügung steht. Die Option **Abfragewartezeit** gibt die Zeit in Sekunden (von 0 bis 2147483647) an, die eine Abfrage vor dem Timeout auf Ressourcen warten soll. Der Standardwert für diese Option ist -1. Das bedeutet, der Timeout wird als das 25-fache der geschätzten Abfragekosten berechnet.  
  
> [!IMPORTANT]  
>  Eine Transaktion, die die wartende Abfrage enthält, kann Sperren aufrechterhalten, während die Abfrage auf freien Arbeitsspeicher wartet. In seltenen Situationen kann ein nicht zu erkennender Deadlock auftreten. Das Reduzieren der Abfragewartezeit verringert die Wahrscheinlichkeit solcher Deadlocks. Schließlich wird die wartende Abfrage beendet, und die Transaktionssperren werden aufgehoben. Durch das Erhöhen der maximalen Wartezeit kann jedoch auch der Zeitaufwand bis zum Beenden der Abfrage erhöht werden. Änderungen an dieser Option werden nicht empfohlen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **So konfigurieren Sie die Option "Abfragewartezeit" mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option „Abfragewartezeit“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Experten geändert werden.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-configure-the-query-wait-option"></a>So konfigurieren Sie die Option Abfragewartezeit  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den **Erweitert** -Knoten.  
  
3.  Geben Sie unter **Parallelität**den gewünschten Wert für die Option **Abfragewartezeit** ein.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-query-wait-option"></a>So konfigurieren Sie die Option Abfragewartezeit  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `query wait` auf `7500` Sekunden festzulegen.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'query wait', 7500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option "Abfragewartezeit"  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
