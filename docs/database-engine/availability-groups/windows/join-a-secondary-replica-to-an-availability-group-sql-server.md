---
title: Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c40410f42d499f31a33225a80182bfe4e30cdcb8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="join-a-secondary-replica-to-an-availability-group-sql-server"></a>Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie ein sekundäres Replikat in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]mit [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]oder PowerShell mit einer Always On-Verfügbarkeitsgruppe verknüpft wird. Nachdem ein sekundäres Replikat einer Always On-Verfügbarkeitsgruppe hinzugefügt wurde, muss das sekundäre Replikat mit der Verfügbarkeitsgruppe verknüpft werden. Der Joinvorgang für das Replikat muss auf der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz ausgeführt werden, die das sekundäre Replikat hostet.  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Security](#Security)  
  
-   **So bereiten Sie eine sekundäre Datenbank vor mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Nachverfolgung:** [Konfigurieren von sekundären Datenbanken](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Das primäre Replikat der Verfügbarkeitsgruppe muss derzeit online sein.  
  
-   Sie müssen mit der Serverinstanz verbunden sein, die ein sekundäres Replikat hostet, das noch nicht mit der Verfügbarkeitsgruppe verknüpft wurde.  
  
-   Die lokale Serverinstanz muss in der Lage sein, eine Verbindung mit dem Datenbankspiegelungs-Endpunkt der Serverinstanz herzustellen, die das primäre Replikat hostet.  
  
> [!IMPORTANT]  
>  Sobald eine Voraussetzung nicht erfüllt ist, tritt bei dem Joinvorgang ein Fehler auf. Nach einem fehlerhaften Joinversuch müssen Sie möglicherweise eine Verbindung mit der Serverinstanz herstellen, die das primäre Replikat hostet, um das sekundäre Replikat zu entfernen und erneut hinzuzufügen, bevor Sie es mit der Verfügbarkeitsgruppe verknüpfen können. Weitere Informationen finden Sie unter [Entfernen eines sekundären Replikats aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md) und [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So verknüpfen Sie ein Verfügbarkeitsreplikat mit einer Verfügbarkeitsgruppe**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das sekundäre Replikat hostet, und klicken Sie auf den Servernamen, um die Serverstruktur zu erweitern.  
  
2.  Erweitern Sie den Knoten **Hohe Verfügbarkeit (immer aktiviert)** und den Knoten **Verfügbarkeitsgruppen** .  
  
3.  Wählen Sie die Verfügbarkeitsgruppe des sekundären Replikats aus, zu dem eine Verbindung besteht.  
  
4.  Klicken Sie mit der rechten Maustaste auf das sekundäre Replikat, und klicken Sie auf **Verfügbarkeitsgruppe beitreten**.  
  
5.  Das Dialogfeld **Replikat mit Verfügbarkeitsgruppe verknüpfen** wird geöffnet.  
  
6.  Klicken Sie auf **OK**, um das sekundäre Replikat mit der Verfügbarkeitsgruppe zu verknüpfen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So verknüpfen Sie ein Verfügbarkeitsreplikat mit einer Verfügbarkeitsgruppe**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das sekundäre Replikat hostet.  
  
2.  Verwenden Sie die [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) -Anweisung wie folgt:  
  
     ALTER AVAILABILITY GROUP *Gruppenname* JOIN  
  
     Dabei ist *Gruppenname* der Name der Verfügbarkeitsgruppe.  
  
     Im folgenden Codebeispiel wird das sekundäre Replikat mit der `MyAG`-Verfügbarkeitsgruppe verknüpft.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  Unter [Erstellen einer Verfügbarkeitsgruppe &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md) können Sie die Verwendung dieser [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung im Kontext sehen.  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So verknüpfen Sie ein Verfügbarkeitsreplikat mit einer Verfügbarkeitsgruppe**  
  
 Im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Anbieter:  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das sekundäre Replikat hostet.  
  
2.  Verknüpfen Sie das sekundäre Replikat mit der Verfügbarkeitsgruppe, indem Sie das Cmdlet **Join-SqlAvailabilityGroup** mit dem Namen der Verfügbarkeitsgruppe ausführen.  
  
     Beispielsweise wird ein sekundäres Replikat, das von der Serverinstanz unter dem angegebenen Pfad gehostet wird, mithilfe des folgenden Befehls mit der Verfügbarkeitsgruppe `MyAg`verknüpft.  Von dieser Serverinstanz muss ein sekundäres Replikat in dieser Verfügbarkeitsgruppe gehostet werden.  
  
    ```  
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Nachverfolgung: Konfigurieren von sekundären Datenbanken  
 Für jede Datenbank in der Verfügbarkeitsgruppe benötigen Sie eine sekundäre Datenbank auf der Serverinstanz, die das sekundäre Replikat hostet. Sie können sekundäre Datenbanken entweder vor oder nach dem Verknüpfen eines sekundären Replikats mit einer Verfügbarkeitsgruppe konfigurieren. Gehen Sie wie folgt vor:  
  
1.  Stellen Sie mit RESTORE WITH NORECOVERY für jeden Wiederherstellungsvorgang die neuesten Datenbank- und Protokollsicherungen für jede primäre Datenbank auf der Serverinstanz wieder her, die das sekundäre Replikat hostet. Weitere Informationen finden Sie unter [Manuelles Vorbereiten einer sekundären Datenbank auf eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)erstellt und konfiguriert wird.  
  
2.  Verknüpfen Sie jede sekundäre Datenbank mit der Verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [Verknüpfen einer sekundären Datenbank mit einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)aktiviert sind, eine Always On-Verfügbarkeitsgruppe zu erstellen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellung und Konfiguration von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)   
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Problembehandlung für die AlwaysOn-Verfügbarkeitsgruppenkonfiguration &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
