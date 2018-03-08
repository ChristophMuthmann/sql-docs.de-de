---
title: "Ändern des Sitzungstimeouts für ein Verfügbarkeitsreplikat (SQL Server) | Microsoft-Dokumentation"
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
helpviewer_keywords:
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], session timeout
- session timeout [SQL Server]
ms.assetid: e23c6e06-1cd1-4d4a-9bc2-e3e06ab2933d
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33df21b45637b206eac86dc895534a2afb70e1ed
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="change-the-session-timeout-period-for-an-availability-replica-sql-server"></a>Ändern des Sitzungstimeouts für ein Verfügbarkeitsreplikat (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie das Sitzungstimeout eines Always On-Verfügbarkeitsreplikats mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] konfiguriert wird. Das Sitzungstimeout ist eine Replikateigenschaft, die steuert, wie lange (in Sekunden) ein Verfügbarkeitsreplikat auf eine Pingantwort von einem verbundenen Replikat wartet, bevor die Verbindung als fehlgeschlagen betrachtet wird. Standardmäßig wartet ein Replikat 10 Sekunden auf eine Pingantwort. Diese Replikateigenschaft wendet nur die Verbindung zwischen einem angegebenen sekundären Replikat und dem primären Replikat der Verfügbarkeitsgruppe an. Weitere Informationen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **Ändern des Sitzungstimeouts mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen mit der Serverinstanz verbunden sein, die das primäre Replikat hostet.  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Es wird empfohlen, einen Timeoutzeitraum von 10 Sekunden oder mehr zu wählen. Wenn Sie diesen Wert auf weniger als 10 Sekunden festlegen, verpasst ein stark ausgelastetes System möglicherweise PINGs und meldet einen falschen Fehler.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So ändern Sie das Sitzungstimeout für ein Verfügbarkeitsreplikat**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Verfügbarkeitsreplikat hostet, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie die Knoten **Hohe Verfügbarkeit mit Always On** und **Verfügbarkeitsgruppen** .  
  
3.  Klicken Sie auf die Verfügbarkeitsgruppe, deren Verfügbarkeitsreplikat konfiguriert werden soll.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Replikat, das konfiguriert werden soll, und klicken Sie auf **Eigenschaften**.  
  
5.  Verwenden Sie im Dialogfeld **Eigenschaften des Verfügbarkeitsreplikats** das Feld **Sitzungstimeout (Sekunden)** , um die Anzahl der Sekunden für das Sitzungstimeout für dieses Replikat zu ändern.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie das Sitzungstimeout für ein Verfügbarkeitsreplikat**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet.  
  
2.  Verwenden Sie die [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) -Anweisung wie folgt:  
  
     ALTER AVAILABILITY GROUP *Gruppenname*  
  
     MODIFY REPLICA ON '*Instanzname*' WITH ( SESSION_TIMEOUT =*Sekunden* )  
  
     Dabei ist *Gruppenname* der Name der Verfügbarkeitsgruppe, *Instanzname* der Name der Serverinstanz, die das zu ändernde Verfügbarkeitsreplikat hostet, und *Sekunden* gibt die Mindestanzahl von Sekunden an, die das Replikat als sekundäres Replikat vor dem Anwenden des Protokolls auf Datenbanken warten muss. Der Standard von 0 Sekunden gibt an, dass es keine Verzögerung gibt.  
  
     Im folgenden Beispiel, eingegeben für das primäre Replikat der `AccountsAG` -Verfügbarkeitsgruppe, wird der Sitzungstimeoutwert in `15` Sekunden für das Replikat geändert, das sich auf der Serverinstanz `INSTANCE09` befindet.  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG   
       MODIFY REPLICA ON 'INSTANCE09' WITH (SESSION_TIMEOUT = 15);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So ändern Sie das Sitzungstimeout für ein Verfügbarkeitsreplikat**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das primäre Replikat hostet.  
  
2.  Verwenden Sie das Cmdlet **Set-SqlAvailabilityReplica** mit dem **SessionTimeout** -Parameter, um die Anzahl der Sekunden für das Sitzungstimeout für ein angegebenes Verfügbarkeitsreplikat zu ändern.  
  
     Mit dem folgenden Befehl wird der Zeitraum für das Sitzungstimeout z. B. auf 15 Sekunden festgelegt.  
  
    ```  
    Set-SqlAvailabilityReplica –SessionTimeout 15 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
