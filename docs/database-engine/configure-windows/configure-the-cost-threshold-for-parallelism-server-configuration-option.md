---
title: "Konfigurieren der Serverkonfigurationsoption Kostenschwellenwert f&#252;r Parallelit&#228;t | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Kostenschwellenwert für Parallelität (Option)"
ms.assetid: dad21bee-fe28-41f6-9d2f-e6ababfaf9db
caps.latest.revision: 31
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 31
---
# Konfigurieren der Serverkonfigurationsoption Kostenschwellenwert f&#252;r Parallelit&#228;t
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Kostenschwellenwert für Parallelität** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Mit der Option **Kostenschwellenwert für Parallelität** geben Sie den Schwellenwert an, bei dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parallele Pläne für Abfragen erstellt und ausführt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt und führt einen parallelen Plan für eine Abfrage nur dann aus, wenn die geschätzten Kosten für das Ausführen eines seriellen Plans für dieselbe Abfrage höher liegen als der Wert, der in **Kostenschwellenwert für Parallelität**festgelegt wurde. Die Kosten beziehen sich auf die geschätzten Kosten, die für das Ausführen des seriellen Plans bei einer bestimmten Hardwarekonfiguration anfallen, und sie stellen keine Einheit der Zeit dar. Die Option **Kostenschwellenwert für Parallelität** kann auf einen beliebigen Wert zwischen 0 und 32767 festgelegt werden. Der Standardwert ist 5.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Option Kostenschwelle für Parallelität mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachverfolgung:** [Nach dem Konfigurieren der Option Kostenschwellenwert für Parallelität](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Die Kosten beziehen sich auf eine abstrakte Kosteneinheit und nicht auf eine Einheit der geschätzten Zeit. Legen Sie die Option **cost threshold for parallelism** nur auf SMP-Systemen (Symmetric Multiprocessor) fest.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignoriert den Wert von **Kostenschwellenwert für Parallelität** unter den folgenden Bedingungen:  
  
    -   Ihr Computer verfügt nur über einen logischen Prozessor.  
  
    -   Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] steht wegen der Konfigurationsoption **Affinitätsmaske** nur ein logischer Prozessor zur Verfügung.  
  
    -   Die Option **Max. Grad an Parallelität** ist auf den Wert 1 festgelegt.  
  
 Ein logischer Prozessor ist die grundlegende Einheit von Prozessorhardware, die dem Betriebssystem ermöglicht, einen Task weiterzuleiten oder einen Threadkontext auszuführen. Jeder logische Prozessor kann an einem bestimmten Zeitpunkt nur einen Threadkontext ausführen. Der Prozessorkern ist die Schaltungstechnik, mit der Anweisungen decodiert und ausgeführt werden können. Ein Prozessorkern enthält möglicherweise einen oder mehrere logische Prozessoren. Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage kann zum Abrufen von CPU-Informationen für das System verwendet werden.  
  
```  
SELECT (cpu_count / hyperthread_ratio) AS PhysicalCPUs,   
cpu_count AS logicalCPUs   
FROM sys.dm_os_sys_info  
```  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Diese Option ist eine erweiterte Option und sollte ausschließlich von einem erfahrenen Datenbankadministrator oder einem zertifizierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Techniker geändert werden.  
  
-   In bestimmten Fällen kann ein paralleler Plan ausgewählt werden, obwohl der Kostenplan der Abfrage unter dem aktuellen Wert der Option **Kostenschwellenwert für Parallelität** liegt. Dieser Fall kann eintreten, wenn die Entscheidung zum Verwenden eines parallelen oder seriellen Plans auf einer Kostenabschätzung basiert, die vor dem Abschluss der vollständigen Optimierung zur Verfügung gestellt wurde.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So konfigurieren Sie die Option Kostenschwelle für Parallelität  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften** aus.  
  
2.  Klicken Sie auf den **Erweitert** -Knoten.  
  
3.  Legen Sie unter **Parallelität**für die Option **CostThresholdForParallelism** den gewünschten Wert fest. Geben Sie einen Wert zwischen 0 und 32767 ein bzw. wählen Sie diesen aus.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### So konfigurieren Sie die Option Kostenschwelle für Parallelität  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) verwendet wird, um den Wert der Option `cost threshold for parallelism` auf `10` festzulegen.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cost threshold for parallelism', 10 ;  
GO  
RECONFIGURE  
GO  
```  
  
 Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Option Kostenschwellenwert für Parallelität  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## Siehe auch  
 [Konfigurieren von Parallelindexvorgängen](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Abfragehinweise &#40;Transact-SQL&#41;](../Topic/Query%20Hints%20\(Transact-SQL\).md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [Affinitätsmaske (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  