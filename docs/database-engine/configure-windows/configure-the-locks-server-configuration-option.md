---
title: "Konfigurieren der Serverkonfigurationsoption „Sperren“ | Microsoft-Dokumentation"
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
- locks option [SQL Server]
ms.assetid: b0cf0f86-7652-4574-a9fb-908e10d03973
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cdafcdcd8fbabebfc55c285b46ea4ee1534ec43
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="configure-the-locks-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Sperren
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Sperren** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mithilfe der Option **Sperren** können Sie die maximale Anzahl verfügbarer Sperren festlegen und so die Menge an Arbeitsspeicher begrenzen, die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] für Sperren verwendet. Die Standardeinstellung ist 0. Dadurch kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] Sperrstrukturen je nach Systemanforderungen dynamisch zuordnen oder die Zuordnung von Sperrstrukturen aufheben.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **So konfigurieren Sie die Option Sperren mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung**  [Nach dem Konfigurieren der Option „Sperren“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Experten geändert werden.  
  
-   Wenn der Server gestartet wird, während die Option **Sperren** auf 0 festgelegt ist, richtet der Sperren-Manager ausreichend Arbeitsspeicher von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für einen ersten Pool von 2.500 Sperrstrukturen ein. Wenn der Sperrenpool verbraucht ist, wird zusätzlicher Arbeitsspeicher für den Pool eingerichtet.  
  
     Wenn für den Sperrenpool mehr Arbeitsspeicher benötigt wird als im [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Speicherpool verfügbar ist und auf dem Computer weiterer Speicher zur Verfügung steht (wenn also der Schwellenwert **Max. Serverarbeitsspeicher** noch nicht erreicht ist), weist [!INCLUDE[ssDE](../../includes/ssde-md.md)] in der Regel dynamisch Speicher zu, um die Sperrenanforderung zu erfüllen. Wenn durch das Zuweisen dieses Speichers jedoch eine Auslagerung auf Betriebssystemebene ausgelöst würde (wenn beispielsweise eine weitere Anwendung auf dem gleichen Computer als Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird und diesen Arbeitsspeicher verwendet), wird kein weiterer Speicherplatz für Sperren zugewiesen. Der dynamische Sperrenpool ruft nicht mehr als 60 Prozent des Speichers ab, der dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]zugewiesen ist. Wenn der Sperrenpool 60 Prozent des von einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]angeforderten Speichers erreicht hat oder wenn auf dem Computer kein weiterer Speicher verfügbar ist, wird bei weiteren Sperrenanforderungen ein Fehler generiert.  
  
     Wenn Sperren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dynamisch verwendet werden dürfen, entspricht dies der empfohlenen Konfiguration. Sie können **Sperren** jedoch festlegen und die Möglichkeit der dynamischen Zuweisung von Sperrenressourcen durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] außer Kraft setzen. Wenn **Sperren** auf einen anderen Wert als 0 festgelegt wird, kann [!INCLUDE[ssDE](../../includes/ssde-md.md)] dem unter **Sperren**angegebenen Wert keine weiteren Sperren zuweisen. Erhöhen Sie diesen Wert, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Meldung anzeigt, dass die Anzahl der verfügbaren Sperren überschritten wurde. Da jede Sperre Arbeitsspeicher verbraucht (96 Bytes pro Sperre), kann es bei Erhöhung dieses Werts erforderlich werden, dem Server mehr Speicher zuzuweisen.  
  
-   Die Option **Sperren** wirkt sich auch darauf aus, wann eine Sperrenausweitung stattfindet. Wenn **Sperren** auf 0 festgelegt ist, findet eine Sperrenausweitung statt, sobald der von den aktuellen Sperrenstrukturen verwendete Speicher 40 Prozent des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Speicherpools erreicht hat. Wenn **Sperren** nicht auf 0 festgelegt ist, findet eine Sperrenausweitung statt, sobald die Anzahl der Sperren 40 Prozent des für **Sperren**festgelegten Werts erreicht.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-configure-the-locks-option"></a>So konfigurieren Sie die Option locks  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den **Erweitert** -Knoten.  
  
3.  Geben Sie unter **Parallelität**den gewünschten Wert für die Option **Sperren** ein.  
  
     Mithilfe der Option **Sperren** können Sie die maximale Anzahl verfügbarer Sperren festlegen und so die Menge an Arbeitsspeicher begrenzen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für Sperren verwendet.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-locks-option"></a>So konfigurieren Sie die Option locks  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) zum Festlegen des Werts der Option `locks` verwendet wird, um die Anzahl der für alle Benutzer verfügbaren Sperren auf `20000`zu setzen.  
  
```sql  
Use AdventureWorks2012 ;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'locks', 20000;  
GO  
RECONFIGURE;  
GO  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)angezeigt oder konfiguriert wird.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Sperren  
 Der Server muss neu gestartet werden, bevor die Einstellung wirksam werden kann.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
