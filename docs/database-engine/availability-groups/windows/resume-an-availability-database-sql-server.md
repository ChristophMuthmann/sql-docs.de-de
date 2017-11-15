---
title: "Fortsetzen einer Verfügbarkeitsdatenbank (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b7a4af01a6b999655a038f02375b7bb0b8bc8a19
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="resume-an-availability-database-sql-server"></a>Fortsetzen einer Verfügbarkeitsdatenbank (SQL Server)
  Eine angehaltene Verfügbarkeitsdatenbank können Sie in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]fortsetzen. Beim Fortsetzen einer angehaltenen Datenbank wechselt die Datenbank in den Status SYNCHRONIZING. Beim Fortsetzen der primären Datenbank werden auch ihre sekundären Datenbanken fortgesetzt, die beim Anhalten der primären Datenbank angehalten wurden. Wenn eine sekundäre Datenbank lokal von der Serverinstanz, die das sekundäre Replikat hostet, angehalten wurde, muss diese sekundäre Datenbank lokal fortgesetzt werden. Sobald sich eine bestimmte sekundäre Datenbank und die entsprechende primäre Datenbank im Status SYNCHRONIZING befinden, wird die Datensynchronisierung auf der sekundären Datenbank fortgesetzt.  
  
> [!NOTE]  
>  Das Anhalten und Fortsetzen einer sekundären AlwaysOn-Datenbank wirkt sich nicht direkt auf die Verfügbarkeit der primären Datenbank aus. Das Anhalten einer sekundären Datenbank kann jedoch sich auf Redundanz- und Failoverfunktionen für die primäre Datenbank auswirken, bis die angehaltene sekundäre Datenbank fortgesetzt wird. Dies steht im Gegensatz zur Datenbankspiegelung, bei der der Spiegelungsstatus sowohl in der Spiegeldatenbank als auch in der Prinzipaldatenbank angehalten wird, bis die Spiegelung fortgesetzt wird. Durch Anhalten einer primären AlwaysOn-Datenbank wird die Datenverschiebung auf allen entsprechenden sekundären Datenbanken angehalten, und Redundanz- und Failoverfunktionen für diese Datenbank werden deaktiviert, bis die primäre Datenbank fortgesetzt wird.  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **So setzen Sie eine sekundäre Datenbank fort mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
### <a name="limitations-and-restrictions"></a>Einschränkungen  
 Ein RESUME-Befehl gibt einen Wert zurück, sobald es vom Replikat akzeptiert wurde, das die Zieldatenbank hostet. Das Fortsetzen der Datenbank ist jedoch dadurch asynchron.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Sie müssen mit der Serverinstanz verbunden sein, auf der die fortzusetzende Datenbank gehostet wird.  
  
-   Die Verfügbarkeitsgruppe muss online sein.  
  
-   Die primäre Datenbank muss online und verfügbar sein.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So setzen Sie eine sekundäre Datenbank fort**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz mit dem Verfügbarkeitsreplikat her, auf der eine Datenbank fortgesetzt werden soll, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie die Knoten **Hohe Verfügbarkeit (immer aktiviert)** und **Verfügbarkeitsgruppen** .  
  
3.  Erweitern Sie die Verfügbarkeitsgruppe.  
  
4.  Erweitern Sie den Knoten **Verfügbarkeitsdatenbanken** , klicken Sie mit der rechten Maustaste auf die Datenbank, und klicken Sie auf **Datenverschiebung fortsetzen**.  
  
5.  Klicken Sie im Dialogfeld **Datenverschiebung fortsetzen** auf **OK**.  
  
> [!NOTE]  
>  Wiederholen Sie zum Fortsetzen weiterer Datenbanken in diesem Replikatspeicherort Schritt 4 und 5 für jede Datenbank.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So setzen Sie eine sekundäre Datenbank fort, die lokal angehalten wurde**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das sekundäre Replikat hostet, dessen Datenbank Sie fortsetzen möchten.  
  
2.  Setzen Sie die sekundäre Datenbank mithilfe der folgenden [ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md)-Anweisung fort:  
  
     ALTER DATABASE *database_name* SET HADR RESUME  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So setzen Sie eine sekundäre Datenbank fort**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das Replikat hostet, dessen Datenbank Sie fortsetzen möchten. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Voraussetzungen](#Prerequisites).  
  
2.  Verwenden Sie das Cmdlet **Resume-SqlAvailabilityDatabase** , um die Verfügbarkeitsgruppe fortzusetzen.  
  
     Beispielsweise wird durch den folgenden Befehl die Datensynchronisierung für die Verfügbarkeitsdatenbank `MyDb3` in der Verfügbarkeitsgruppe `MyAg`fortgesetzt.  
  
    ```  
    Resume-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das Cmdlet **Get-Help** in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Anhalten einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
