---
title: "Entfernen einer sekund&#228;ren Replikats aus einer Verf&#252;gbarkeitsgruppe (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.availabilitygroup.removesecondaryar.f1"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server], Verfügbarkeitsreplikate"
  - "Verfügbarkeitsgruppen [SQL Server], Konfigurieren"
ms.assetid: 35ddc8b6-3e7c-4417-9a0a-d4987a09ddf7
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# Entfernen einer sekund&#228;ren Replikats aus einer Verf&#252;gbarkeitsgruppe (SQL Server)
  In diesem Thema wird beschrieben, wie ein sekundäres Replikat aus einer Always On-Verfügbarkeitsgruppe mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] entfernt wird.  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **So entfernen Sie ein sekundäres Replikat mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Entfernen eines sekundären Replikats](#PostBestPractices)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Dieser Task wird nur für das primäre Replikat unterstützt.  
  
-   Nur ein sekundäres Replikat kann aus einer Verfügbarkeitsgruppe entfernt werden.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie benötigen eine Verbindung zur Serverinstanz, die das primäre Replikat der Verfügbarkeitsgruppe hostet.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So entfernen Sie ein sekundäres Replikat**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Verfügbarkeitsreplikat hostet, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie die Knoten **Always On High Availability** (Always On Hochverfügbarkeit) und **Verfügbarkeitsgruppen**.  
  
3.  Wählen Sie die Verfügbarkeitsgruppe aus, und erweitern Sie den Knoten **Verfügbarkeitsreplikate** .  
  
4.  Dieser Schritt hängt davon ab, ob Sie mehrere Replikate oder nur ein Replikat entfernen möchten:  
  
    -   Verwenden Sie zum Entfernen mehrerer Replikate den Bereich **Details zum Objekt-Explorer** , um alle zu entfernenden Replikate anzuzeigen und auszuwählen. Weitere Informationen finden Sie unter [Verwenden der Details zum Objekt-Explorer zum Überwachen von Verfügbarkeitsgruppen &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use object explorer details to monitor availability groups.md).  
  
    -   Wählen Sie zum Entfernen eines einzelnen Replikats dieses im Bereich **Objekt-Explorer** oder **Details zum Objekt-Explorer** aus.  
  
5.  Klicken Sie mit der rechten Maustaste auf die ausgewählten sekundären Replikate, und wählen Sie im Befehlsmenü **Aus Verfügbarkeitsgruppe entfernen** aus.  
  
6.  Klicken Sie zum Entfernen aller aufgeführten sekundären Replikate im Dialogfeld **Sekundäre Replikate aus Verfügbarkeitsgruppe entfernen** auf **OK**. Wenn Sie nicht alle aufgelisteten Replikate entfernen wollen, klicken Sie auf **Abbrechen**.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So entfernen Sie ein sekundäres Replikat**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet.  
  
2.  Verwenden Sie die [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) -Anweisung wie folgt:  
  
     ALTER AVAILABILITY GROUP *Gruppenname* REMOVE REPLICA ON '*Instanzname*' [,...*n*]  
  
     Dabei ist *Gruppenname* der Name der Verfügbarkeitsgruppe und *Instanzname* die Serverinstanz, auf der sich das sekundäre Replikat befindet.  
  
     Im folgenden Codebeispiel wird ein sekundäres Replikat aus der *MyAG* -Verfügbarkeitsgruppe entfernt. Das sekundäre Zielreplikat befindet sich auf der Serverinstanz *HADR_INSTANCE* auf dem Computer *COMPUTER02*.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG REMOVE REPLICA ON 'COMPUTER02\HADR_INSTANCE';  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So entfernen Sie ein sekundäres Replikat**  
  
1.  Wechseln Sie mit **cd** in das Verzeichnis der Serverinstanz, auf der das primäre Replikat gehostet wird.  
  
2.  Verwenden Sie das Cmdlet **Remove-SqlAvailabilityReplica**.  
  
     Beispielsweise wird durch den folgenden Befehl das Verfügbarkeitsreplikat auf dem `MyReplica`-Server von der Verfügbarkeitsgruppe namens `MyAg` entfernt.  Dieser Befehl muss auf der Serverinstanz ausgeführt werden, von der das primäre Replikat der Verfügbarkeitsgruppe gehostet wird.  
  
    ```  
    Remove-SqlAvailabilityReplica `   
    -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Verwenden Sie das Cmdlet **Get-Help** in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-PowerShell-Umgebung, um die Syntax eines Cmdlets anzuzeigen. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="PostBestPractices"></a> Nachverfolgung: Nach dem Entfernen eines sekundären Replikats  
 Wenn Sie ein Replikat angeben, das derzeit nicht verfügbar ist, wird beim Onlineschalten des Replikats festgestellt, dass es entfernt wurde.  
  
 Wird ein Replikat entfernt, empfängt es keine Daten mehr. Nachdem für ein sekundäres Replikat bestätigt wurde, dass es aus dem globalen Speicher entfernt wurde, entfernt das Replikat die Verfügbarkeitsgruppeneinstellungen aus seinen Datenbanken, die auf der lokalen Serverinstanz im Status RECOVERING verbleiben.  
  
## Siehe auch  
 [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)   
 [Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  