---
title: "Konfigurieren der Serverkonfigurationsoption „Wiederherstellungsintervall“ | Microsoft-Dokumentation"
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
- restoring recovery interval [SQL Server]
- checkpoints [SQL Server]
- recovery interval option [SQL Server]
- default recovery interval option
- time [SQL Server], recovery interval
- interval for recovery [SQL Server]
- maximum number of minutes per database recovery
- recovery [SQL Server], recovery interval option
ms.assetid: e4734b3b-8fbe-4b65-9c48-91b5a3dd18e1
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: c945263cf63d626798c0d94aa35b9113f78eaaa4
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-recovery-interval-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Wiederherstellungsintervall
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Wiederherstellungsintervall** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mit der Option **Wiederherstellungsintervall** wird eine Obergrenze für die Zeitdauer festgelegt, wie lange das Wiederherstellen einer Datenbank dauern darf. Das [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verwendet den für diese Option angegebenen Wert, um annäherungsweise zu ermitteln, wie häufig [automatische Prüfpunkte](../../relational-databases/logs/database-checkpoints-sql-server.md) für die jeweilige Datenbank ausgegeben werden sollen.  
  
 Der Standardwert für das Wiederherstellungsintervall ist 0, was es dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] ermöglicht, das Wiederherstellungsintervall automatisch zu konfigurieren. In der Regel geht mit dem standardmäßigen Wiederherstellungsintervall etwa ein automatischer Prüfpunkt pro Minute für aktive Datenbanken einher, was zu Wiederherstellungszeiten von unter einer Minute führt. Höhere Werte geben die ungefähre maximale Wiederherstellungszeit in Minuten an. Wenn Sie beispielsweise das Wiederherstellungsintervall auf 3 festlegen, bedeutet dies eine maximale Wiederherstellungszeit von ungefähr drei Minuten.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Wiederherstellungsintervall-Serverkonfigurationsoption mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option Wiederherstellungsintervall](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Das Wiederherstellungsintervall wirkt sich nur auf Datenbanken aus, die die standardmäßige Zielwiederherstellungszeit (0) verwenden. Um das Serverwiederherstellungsintervall für eine Datenbank zu überschreiben, konfigurieren Sie für die Datenbank eine nicht standardmäßige Zielwiederherstellungszeit. Weitere Informationen finden Sie unter [Ändern der Zielwiederherstellungszeit einer Datenbank &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)konfiguriert wird.  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Techniker geändert werden.  
  
-   In der Regel empfiehlt es sich, das Wiederherstellungsintervall bei 0 zu belassen, falls keine Leistungsprobleme auftreten. Wenn Sie die Einstellung für das Wiederherstellungsintervall erhöhen möchten, empfehlen wir eine schrittweise Erhöhung des entsprechenden Werts. Werten Sie zudem die Auswirkungen der jeweiligen stufenweisen Erhöhung auf die Wiederherstellungsleistung aus.  
  
-   Wenn Sie **sp_configure** zum Ändern des Werts der Option **Wiederherstellungsintervall** auf mehr als 60 (Minuten) verwenden, sollten Sie RECONFIGURE WITH OVERRIDE angeben. Mit WITH OVERRIDE wird die Überprüfung des Konfigurationswerts deaktiviert (für Werte, die nicht gültig sind oder die keine empfohlenen Werte sind).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So legen Sie das Wiederherstellungsintervall fest**  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf eine Serverinstanz, und wählen Sie **Eigenschaften**.  
  
2.  Klicken Sie auf den Knoten **Datenbankeinstellungen** .  
  
3.  Geben Sie unter **Wiederherstellung**im Feld **Wiederherstellungsintervall (Minuten)** einen Wert zwischen 0 und 32767 ein, oder wählen Sie einen Wert aus, um die maximale Zeitdauer in Minuten festzulegen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Starten zum Wiederherstellen jeder Datenbank verwenden soll. Die Standardeinstellung ist 0; bei dieser Einstellung wird die Option automatisch von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfiguriert. In der Praxis bedeutet dies eine Wiederherstellungszeit von weniger als einer Minute und das Auftreten eines Prüfpunktes in Abständen von ungefähr einer Minute bei aktiven Datenbanken.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-set-the-recovery-interval"></a>So legen Sie das Wiederherstellungsintervall fest  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `recovery interval` auf `3` Minuten festzulegen.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'recovery interval', 3 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Wiederherstellungsintervall  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Siehe auch  
 [Ändern der Zielwiederherstellungszeit einer Datenbank &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)   
 [Datenbankprüfpunkte &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Erweiterte Optionen anzeigen (Serverkonfigurationsoption)](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  

