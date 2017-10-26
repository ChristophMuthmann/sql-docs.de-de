---
title: "Entfernen einer Verfügbarkeitsgruppe (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.deleteag.f1
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], dropping
ms.assetid: 4b7f7f62-43a3-49db-a72e-22d4d7c2ddbb
caps.latest.revision: 48
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 393f088ea977236aa7feba6107828eb64e646b64
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="remove-an-availability-group-sql-server"></a>Entfernen einer Verfügbarkeitsgruppe (SQL Server)
  In diesem Thema wird beschrieben, wie eine Always On-Verfügbarkeitsgruppe mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]gelöscht wird. Wenn eine Serverinstanz, auf der eines der Verfügbarkeitsreplikate gehostet wird, offline ist, wenn Sie eine Verfügbarkeitsgruppe löschen, so wird das lokale Verfügbarkeitsreplikat von der Serverinstanz gelöscht, nachdem diese online geschaltet wurde. Beim Löschen einer Verfügbarkeitsgruppe werden sämtliche zugeordneten Verfügbarkeitsgruppenlistener gelöscht.  
  
 Beachten Sie, dass eine Verfügbarkeitsgruppe ggf. aus einem WSFC (Windows Server Failover Clustering)-Knoten gelöscht werden kann, der über die richtigen Sicherheitsanmeldeinformationen für die Verfügbarkeitsgruppe verfügt. Auf diese Weise können Sie eine Verfügbarkeitsgruppe löschen, wenn keine ihrer Verfügbarkeitsreplikate mehr vorhanden ist.  
  
> [!IMPORTANT]  
>  Entfernen Sie die Verfügbarkeitsgruppe wenn möglich nur, während eine Verbindung mit der Serverinstanz besteht, die das primäre Replikat hostet. Wenn die Verfügbarkeitsgruppe aus dem primären Replikat gelöscht wird, sind Änderungen in den früheren primären Datenbanken (ohne hohen Verfügbarkeitsschutz) zulässig. Durch Löschen einer Verfügbarkeitsgruppe aus einem sekundären Replikat erhält das primäre Replikat den Status RESTORING und Änderungen an den Datenbanken sind nicht zulässig.  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen und Empfehlungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **So löschen Sie eine Verfügbarkeitsgruppe mithilfe von:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen und Empfehlungen  
  
-   Wenn die Verfügbarkeitsgruppe online ist, bewirkt das Löschen aus einem sekundären Replikat den Übergang des primären Replikats in den Status RESTORING. Daher sollten Sie die Verfügbarkeitsgruppe möglichst nur aus der Serverinstanz entfernen, die das primäre Replikat hostet.  
  
-   Wenn Sie eine Verfügbarkeitsgruppe von einem Computer löschen, der aus dem WSFC-Failovercluster entfernt wurde, wird die Verfügbarkeitsgruppe nur lokal gelöscht.  
  
-   Löschen Sie eine Verfügbarkeitsgruppe nicht, wenn der WSFC-Cluster (Windows Server Failover Clustering) kein Quorum hat. Wenn Sie eine Verfügbarkeitsgruppe löschen müssen, solange der Cluster über kein Quorum verfügt, wird die Metadaten-Verfügbarkeitsgruppe, die im Cluster gespeichert ist, nicht entfernt. Nachdem der Cluster das Quorum wiedererlangt hat, müssen Sie die Verfügbarkeitsgruppe erneut löschen, um diese aus dem WSFC-Cluster zu entfernen.  
  
-   Auf einem sekundären Replikat sollte DROP AVAILABILITY GROUP nur im Notfall verwendet werden. Das liegt daran, dass durch Löschen einer Verfügbarkeitsgruppe die Verfügbarkeitsgruppe offline geschaltet wird. Wenn Sie die Verfügbarkeitsgruppe aus einem sekundären Replikat löschen, kann das primäre Replikat nicht bestimmen, ob der OFFLINE-Status aufgrund des Quorumverlusts, eines erzwungenen Failovers oder eines DROP AVAILABILITY GROUP-Befehls aufgetreten ist. Das primäre Replikat geht in den Status RESTORING über, um eine mögliche Split Brain-Situation zu verhindern. Weitere Informationen finden Sie unter [Funktionsweise: DROP AVAILABILITY GROUP-Verhaltensweisen](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Blog von CSS SQL Server-Ingenieuren).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung. Um eine Verfügbarkeitsgruppe zu löschen, die nicht von der lokalen Serverinstanz gehostet wird, benötigen Sie die CONTROL SERVER-Berechtigung oder die CONTROL-Berechtigung für diese Verfügbarkeitsgruppe.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So löschen Sie eine Verfügbarkeitsgruppe**  
  
1.  Wenn möglich, stellen Sie in Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet, oder stellen Sie eine Verbindung zu einer anderen Serverinstanz her, die für Always On-Verfügbarkeitsgruppen in einem WSFC-Knoten aktiviert ist, der die richtigen Sicherheitsanmeldeinformationen für die Verfügbarkeitsgruppe besitzt. Erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie die Knoten **Always On High Availability** (Always On Hochverfügbarkeit) und **Verfügbarkeitsgruppen** .  
  
3.  Dieser Schritt hängt davon ab, ob Sie mehrere Verfügbarkeitsgruppen oder nur eine Verfügbarkeitsgruppe löschen möchten:  
  
    -   Zum Löschen mehrerer Verfügbarkeitsgruppen, deren primären Replikate sich auf der verbundenen Serverinstanz befinden, verwenden Sie den Bereich **Details zum Objekt-Explorer**, um alle Verfügbarkeitsgruppen, die Sie löschen möchten, anzuzeigen und auszuwählen. Weitere Informationen finden Sie unter [Verwenden der Details zum Objekt-Explorer zum Überwachen von Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Zum Löschen einer einzelnen Verfügbarkeitsgruppe wählen Sie sie entweder im Bereich **Objekt-Explorer** oder im Bereich **Details zum Objekt-Explorer** aus.  
  
4.  Klicken Sie mit der rechten Maustaste auf die ausgewählte Verfügbarkeitsgruppe oder die Gruppen, und wählen Sie den Befehl **Löschen** aus.  
  
5.  Um im Dialogfeld **Verfügbarkeitsgruppe entfernen** alle aufgelisteten Verfügbarkeitsgruppen zu löschen, klicken Sie auf **OK**. Wenn Sie nicht alle aufgelisteten Verfügbarkeitsgruppen entfernen möchten, klicken Sie auf **Abbrechen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So löschen Sie eine Verfügbarkeitsgruppe**  
  
1.  Wenn möglich, stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet, oder stellen Sie eine Verbindung zu einer anderen Serverinstanz her, die für Always On-Verfügbarkeitsgruppen in einem WSFC-Knoten aktiviert ist, der die richtigen Sicherheitsanmeldeinformationen für die Verfügbarkeitsgruppe besitzt.  
  
2.  Verwenden Sie die [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md) -Anweisung wie folgt:  
  
     DROP AVAILABILITY GROUP *group_name*  
  
     Dabei ist *group_name* der Name der Verfügbarkeitsgruppe die gelöscht werden soll.  
  
     Im folgenden Beispiel wird die `MyAG` -Verfügbarkeitsgruppe gelöscht.  
  
    ```  
    DROP AVAILABILITY GROUP MyAG;  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So löschen Sie eine Verfügbarkeitsgruppe**  
  
 Im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Anbieter:  
  
1.  Wechseln Sie, falls möglich, mit in**cd**in das Verzeichnis der Serverinstanz, die das primäre Replikat hostet, oder stellen Sie eine Verbindung zu einer anderen Serverinstanz her, die für Always On-Verfügbarkeitsgruppen in einem WSFC-Knoten aktiviert ist, der die richtigen Sicherheitsanmeldeinformationen für die Verfügbarkeitsgruppe besitzt.  
  
2.  Verwenden Sie das **Remove-SqlAvailabilityGroup** -Cmdlet.  
  
     Beispielsweise wird die Verfügbarkeitsgruppe namens `MyAg`mit dem folgenden Befehl entfernt. Dieser Befehl kann auf jeder Serverinstanz ausgeführt werden, von der ein Verfügbarkeitsreplikat für die Verfügbarkeitsgruppe gehostet wird.  
  
    ```  
    Remove-SqlAvailabilityGroup `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
    ```  
  
    > [!NOTE]  
    >  Verwenden Sie das Cmdlet **Get-Help** in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -PowerShell-Umgebung, um die Syntax eines Cmdlets anzuzeigen. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Funktionsweise: DROP AVAILABILITY GROUP-Verhaltensweisen](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Blog von CSS SQL Server-Ingenieuren)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)  
  
  

