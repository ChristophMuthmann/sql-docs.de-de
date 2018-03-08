---
title: "Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.availabilitygroup.removeprimarydb.f1
helpviewer_keywords:
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], databases
ms.assetid: 6d4ca31e-ddf0-44bf-be5e-a5da060bf096
caps.latest.revision: "28"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 112f97a9a2c9d9052e5b3808c5cae7900b15763c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="remove-a-primary-database-from-an-availability-group-sql-server"></a>Entfernen einer primären Datenbank aus einer Verfügbarkeitsgruppe (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird erläutert, wie sowohl die primäre Datenbank als auch die entsprechenden sekundären Datenbanken aus einer AlwaysOn-Verfügbarkeitsgruppe mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] entfernt werden.  
  
-   **Vorbereitungen:**  
  
     [Voraussetzungen und Einschränkungen](#Prerequisites)  
  
     [Security](#Security)  
  
-   **Entfernen einer Verfügbarkeitsdatenbank mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Entfernen einer Verfügbarkeitsdatenbank aus einer Verfügbarkeitsgruppe](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Voraussetzungen und Einschränkungen  
  
-   Dieser Task wird nur für primäre Replikate unterstützt. Sie müssen mit der Serverinstanz verbunden sein, die das primäre Replikat hostet.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So entfernen Sie eine Verfügbarkeitsdatenbank**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Replikat der zu entfernenden Datenbanken hostet, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie den Knoten **Hohe Verfügbarkeit (immer aktiviert)** und den Knoten **Verfügbarkeitsgruppen** .  
  
3.  Wählen Sie die Verfügbarkeitsgruppe aus, und erweitern Sie den Knoten **Verfügbarkeitsdatenbanken** .  
  
4.  Dieser Schritt hängt davon ab, ob Sie mehrere Datenbankgruppen oder nur eine Datenbank entfernen möchten:  
  
    -   Verwenden Sie zum Entfernen mehrerer Datenbanken den Bereich **Details zum Objekt-Explorer** , um alle zu entfernenden Datenbanken anzuzeigen und auszuwählen. Weitere Informationen finden Sie unter [Verwenden der Details zum Objekt-Explorer zum Überwachen von Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Wählen Sie zum Entfernen einer einzelnen Datenbank diese im Bereich **Objekt-Explorer** oder **Details zum Objekt-Explorer** aus.  
  
5.  Klicken Sie mit der rechten Maustaste auf die ausgewählten Datenbanken, und wählen Sie im Kontextmenü den Befehl **Datenbank aus Verfügbarkeitsgruppe entfernen** aus.  
  
6.  Klicken Sie zum Entfernen aller aufgelisteten Datenbanken im Dialogfeld **Datenbanken aus Verfügbarkeitsgruppe entfernen** auf **OK**. Wenn Sie nicht alle Datenbanken entfernen wollen, klicken Sie auf **Abbrechen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So entfernen Sie eine Verfügbarkeitsdatenbank**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet.  
  
2.  Verwenden Sie die [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) -Anweisung wie folgt:  
  
     ALTER AVAILABILITY GROUP *Gruppenname* REMOVE DATABASE *Verfügbarkeitsdatenbankname*  
  
     Dabei ist *Gruppenname* der Name der Verfügbarkeitsgruppe und *Verfügbarkeitsdatenbankname* der Name der zu entfernenden Datenbank.  
  
     Im folgenden Beispiel wird eine Datenbank namens `Db6` aus der `MyAG` -Verfügbarkeitsgruppe entfernt.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE DATABASE Db6;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So entfernen Sie eine Verfügbarkeitsdatenbank**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das primäre Replikat hostet.  
  
2.  Verwenden Sie das **Remove-SqlAvailabilityDatabase** -Cmdlet, und geben Sie dabei den Namen der Verfügbarkeitsdatenbank an, die aus der Verfügbarkeitsgruppe entfernt werden soll. Wenn Sie mit der Serverinstanz verbunden sind, die das primäre Replikat hostet, werden die primäre Datenbank und ihre entsprechenden sekundären Datenbanken aus der Verfügbarkeitsgruppe entfernt.  
  
     Beispielsweise wird durch den folgenden Befehl das Verfügbarkeitsdatenbank `MyDb9` von der Verfügbarkeitsgruppe namens `MyAg`entfernt. Da der Befehl auf der Serverinstanz ausgeführt wird, von der das primäre Replikat gehostet wird, werden die primäre Datenbank und alle entsprechenden sekundären Datenbanken aus der Verfügbarkeitsgruppe entfernt. Für diese Datenbank wird auf allen sekundären Replikaten keine Datensynchronisierung mehr ausgeführt.  
  
    ```  
    Remove-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\PrimaryComputer\InstanceName\AvailabilityGroups\MyAg\AvailabilityDatabases\MyDb9
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] -PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Entfernen einer Verfügbarkeitsdatenbank aus einer Verfügbarkeitsgruppe  
 Durch das Entfernen einer Verfügbarkeitsdatenbank aus ihrer Verfügbarkeitsgruppe wird die Datensynchronisierung zwischen der früheren primären Datenbank und den entsprechenden sekundären Datenbanken beendet. Die frühere primäre Datenbank bleibt online. Alle entsprechenden sekundären Datenbanken wechseln in den Status RESTORING.  
  
 Zu diesem Zeitpunkt stehen alternative Methoden zum Umgang mit einer entfernten sekundären Datenbank zur Verfügung:  
  
-   Wenn eine bestimmte sekundäre Datenbank nicht mehr benötigt wird, können Sie sie löschen.  
  
     Weitere Informationen finden Sie unter [Löschen einer Datenbank](../../../relational-databases/databases/delete-a-database.md).  
  
-   Wenn Sie auf eine entfernte sekundäre Datenbank zugreifen möchten, nachdem sie aus der Verfügbarkeitsgruppe entfernt wurde, können Sie die Datenbank wiederherstellen. Wenn Sie jedoch eine entfernte sekundäre Datenbank wiederherstellen, sind zwei voneinander abweichende, unabhängige Datenbanken mit demselben Namen online. Sie müssen sicherstellen, dass Clients nur auf eine von beiden zugreifen können (in der Regel die aktuelle primäre Datenbank).  
  
     Weitere Informationen finden Sie unter [Wiederherstellen einer Datenbank ohne Wiederherstellung von Daten &#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
  
