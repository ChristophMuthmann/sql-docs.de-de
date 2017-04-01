---
title: "Konfigurieren der Serverkonfigurationsoption Timeout f&#252;r Remoteabfragen | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Zeitlimit für Remoteabfragen [SQL Server]"
  - "Timeout für Remoteabfragen (Option)"
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Konfigurieren der Serverkonfigurationsoption Timeout f&#252;r Remoteabfragen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Timeout für Remoteabfragen** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mithilfe der Option **Timeout für Remoteabfragen** können Sie angeben, wie viel Zeit (in Sekunden) ein Remotevorgang in Anspruch nehmen kann, bevor in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Timeout auftritt. Der Standardwert für diese Option beträgt 600, was einer Wartezeit von 10 Minuten entspricht. Dieser Wert gilt für eine von [!INCLUDE[ssDE](../../includes/ssde-md.md)] als Remoteabfrage initiierte ausgehende Verbindung. Der Wert hat keine Auswirkungen auf von [!INCLUDE[ssDE](../../includes/ssde-md.md)] empfangene Abfragen. Wenn Sie das Timeout deaktivieren möchten, setzen Sie den Wert auf 0. Bei einer Abfrage wird dann bis zum Abbruch gewartet.  
  
 Bei heterogenen Abfragen wird durch **Timeout für Remoteabfragen** die Anzahl der Sekunden angegeben (initialisiert im Befehlsobjekt mithilfe der DBPROP_COMMANDTIMEOUT-Rowseteigenschaft), die ein Remoteanbieter auf Resultsets warten sollte, bevor für die Abfrage ein Timeout eintritt. Dieser Wert wird, soweit dies vom Remoteanbieter unterstützt wird, auch zum Festlegen von DBPROP_GENERALTIMEOUT verwendet. Dadurch tritt für alle anderen Vorgänge nach Ablauf der angegebenen Anzahl von Sekunden ein Timeout ein.  
  
 Bei remote gespeicherten Prozeduren wird durch **Timeout für Remoteabfragen** die Anzahl der Sekunden angegeben, die nach dem Senden einer `EXEC` -Anweisung vergehen müssen, bevor für die remote gespeicherte Prozedur ein Timeout eintritt.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option Timeout für Remoteabfragen mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren der Option Timeout für Remoteabfragen](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Um diesen Wert festlegen zu können, müssen Remoteserververbindungen zulässig sein.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Um **sp_configure** mit beiden Parametern auszuführen, um eine Konfigurationsoption zu ändern oder die RECONFIGURE-Anweisung auszuführen, muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So konfigurieren Sie die Option Timeout für Remoteabfragen  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften** aus.  
  
2.  Klicken Sie auf den Knoten **Verbindungen** .  
  
3.  Unter **Remoteserververbindungen**im Feld **Timeout für Remoteabfragen** können Sie einen Wert zwischen 0 und 2.147.483.647 eingeben oder auswählen, um die maximale Anzahl von Sekunden festzulegen, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wartet, bevor ein Timeout auftritt.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So konfigurieren Sie die Option Timeout für Remoteabfragen  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie Sie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) zum Festlegen des Werts der Option `remote query timeout` auf `0` verwenden, um das Timeout zu deaktivieren.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Timeout für Remoteabfragen  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Eigenschaften und Verhaltensweisen von Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  