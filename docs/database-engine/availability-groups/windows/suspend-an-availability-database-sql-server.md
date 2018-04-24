---
title: Anhalten einer Verfügbarkeitsdatenbank (SQL Server) | Microsoft-Dokumentation
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
- sql13.swb.availabilitygroup.suspenddatamove.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], suspending a database
- Availability Groups [SQL Server], databases
ms.assetid: 86858982-6af1-4e80-9a93-87451f0d7ee9
caps.latest.revision: 51
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 22eb081d662868e26cd28b7b6ea0af483f7cb04d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="suspend-an-availability-database-sql-server"></a>Anhalten einer Verfügbarkeitsdatenbank (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Eine Verfügbarkeitsdatenbank können Sie in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]anhalten. Beachten Sie, dass der Befehl zum Anhalten auf der Serverinstanz ausgegeben werden muss, die die anzuhaltende oder fortzusetzende Datenbank hostet.  
  
 Die Auswirkung eines Anhaltebefehls ist davon abhängig, ob Sie eine sekundäre Datenbank oder eine primäre Datenbank anhalten:  
  
|Angehaltene Datenbank|Auswirkung des Anhaltebefehls|  
|------------------------|-------------------------------|  
|Sekundäre Datenbank|Nur die lokale sekundäre Datenbank wird angehalten, und ihr Synchronisierungsstatus wird NOT SYNCHRONIZING. Andere sekundäre Datenbanken sind nicht betroffen. Die angehaltene Datenbank empfängt keine Daten (Protokolldatensätze) mehr und wendet keine Daten mehr an und beginnt, hinter die primäre Datenbank zu fallen. Vorhandene Verbindungen mit dem lesbaren sekundären Replikat können weiter verwendet werden. Neue Verbindungen mit der angehaltenen Datenbank auf dem lesbaren sekundären Replikat werden erst zugelassen, wenn Datenverschiebung fortgesetzt wird.<br /><br /> Die primäre Datenbank bleibt verfügbar. Wenn Sie jede der entsprechenden sekundären Datenbanken anhalten, wird die primären Datenbank ungeschützt ausgeführt.<br /><br /> **\*\* Wichtig \*\*** Während eine sekundäre Datenbank angehalten ist, sammelt die Sendewarteschlange der entsprechenden primären Datenbank nicht gesendete Transaktionsprotokoll-Datensätze. Verbindungen mit dem sekundären Replikat geben Daten zurück, die verfügbar waren, als die Datenverschiebung angehalten wurde.|  
|Primäre Datenbank|Die primäre Datenbank beendet die Datenverschiebung zu jeder verbundenen sekundären Datenbank. Die primäre Datenbank wird weiterhin in einem ungeschützten Modus ausgeführt. Die primäre Datenbank bleibt für Clients verfügbar, und vorhandene Verbindungen in einer lesbaren sekundären Datenbank bleiben verwendbar, und neue Verbindungen können hergestellt werden.|  
  
> [!NOTE]  
>  Ein Anhalten einer sekundären AlwaysOn-Datenbank wirkt sich nicht direkt auf die Verfügbarkeit der primären Datenbank aus. Das Anhalten einer sekundären Datenbank kann jedoch sich auf Redundanz- und Failoverfunktionen für die primäre Datenbank auswirken. Dies steht im Gegensatz zur Datenbankspiegelung, bei der der Spiegelungsstatus sowohl in der Spiegeldatenbank als auch in der Prinzipaldatenbank angehalten wird. Durch Anhalten einer primären AlwaysOn-Datenbank wird die Datenverschiebung auf allen entsprechenden sekundären Datenbanken angehalten, und Redundanz- und Failoverfunktionen für diese Datenbank werden deaktiviert, bis die primäre Datenbank fortgesetzt wird.  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Empfehlungen](#Recommendations)  
  
     [Security](#Security)  
  
-   **Anhalten einer Datenbank mit:**  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Nachverfolgung:** [Vermeiden eines vollen Transaktionsprotokolls](#FollowUp)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Restrictions"></a> Einschränkungen  
 Ein SUSPEND-Befehl gibt einen Wert zurück, sobald es vom Replikat akzeptiert wurde, das die Zieldatenbank hostet. Das Anhalten der Datenbank ist jedoch dadurch asynchron.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Sie müssen mit der Serverinstanz verbunden sein, die die Datenbank hostet, die angehalten werden soll. Um eine primäre Datenbank und die entsprechenden sekundären Datenbanken anzuhalten, stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet. Um eine sekundäre Datenbank anzuhalten und die primäre Datenbank verfügbar zu lassen, stellen Sie eine Verbindung mit dem sekundären Replikat her.  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Bei Engpässen ist das Anhalten einer oder mehrerer sekundärer Datenbanken möglicherweise kurz nützlich, um die Leistung auf dem primären Replikat vorübergehend zu verbessern. Solange eine sekundäre Datenbank angehalten bleibt, kann das Transaktionsprotokoll der entsprechenden primären Datenbank nicht abgeschnitten werden. Dies führt dazu, dass sich Protokolldatensätze auf der primären Datenbank ansammeln. Daher wird empfohlen, dass Sie eine angehaltene sekundäre Datenbank schnell fortsetzen oder entfernen. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Nachverfolgung: Vermeiden eines vollen Transaktionsprotokolls](#FollowUp).  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER-Berechtigung für die Datenbank.  
  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So halten Sie eine Datenbank an**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz mit dem Verfügbarkeitsreplikat her, auf der eine Datenbank angehalten werden soll, und erweitern Sie die Serverstruktur. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Voraussetzungen](#Prerequisites).  
  
2.  Erweitern Sie den Knoten **Hohe Verfügbarkeit (immer aktiviert)** und den Knoten **Verfügbarkeitsgruppen** .  
  
3.  Erweitern Sie die Verfügbarkeitsgruppe.  
  
4.  Erweitern Sie den Knoten **Verfügbarkeitsdatenbanken** , klicken Sie mit der rechten Maustaste auf die Datenbank, und klicken Sie auf **Datenverschiebung anhalten**.  
  
5.  Klicken Sie im Dialogfeld **Datenverschiebung anhalten** auf **OK**.  
  
     Im Objekt-Explorer wird angegeben, dass die Datenbank angehalten wird, indem das Datenbanksymbol einen Pausenindikator anzeigt.  
  
> [!NOTE]  
>  Wiederholen Sie zum Anhalten weiterer Datenbanken in diesem Replikatspeicherort Schritt 4 und 5 für jede Datenbank.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So halten Sie eine Datenbank an**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das Replikat hostet, dessen Datenbank Sie anhalten möchten. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Voraussetzungen](#Prerequisites).  
  
2.  Halten Sie die Datenbank mithilfe der folgenden [ALTER DATABASE](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md)-Anweisung an:  
  
     ALTER DATABASE *database_name* SET HADR SUSPEND  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So halten Sie eine Datenbank an**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das Replikat hostet, dessen Datenbank Sie anhalten möchten. Weitere Informationen finden Sie weiter oben in diesem Thema unter [Voraussetzungen](#Prerequisites).  
  
2.  Verwenden Sie das Cmdlet **Suspend-SqlAvailabilityDatabase** , um die Verfügbarkeitsgruppe anzuhalten.  
  
     Durch den folgenden Befehl wird beispielsweise die Datensynchronisierung für die Verfügbarkeitsdatenbank `MyDb3` in der Verfügbarkeitsgruppe `MyAg` auf der Serverinstanz `Computer\Instance`angehalten.  
  
    ```  
    Suspend-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Follow Up: Avoiding a Full Transaction Log  
 Wenn ein automatischer Prüfpunkt für eine Datenbank ausgeführt wird, wird normalerweise das zugehörige Transaktionsprotokoll nach der nächsten Protokollsicherung auf diesen Prüfpunkt gekürzt. Wenn jedoch eine sekundäre Datenbank angehalten wird, bleiben alle aktuellen Protokolldatensätze auf der primären Datenbank aktiv. Wenn das Transaktionsprotokoll voll ist (weil die maximale Größe erreicht wurde oder weil für die Serverinstanz der Speicherplatz nicht ausreicht), kann die Datenbank keine Updates mehr ausführen.  
  
 Führen Sie eine der folgenden Aktionen aus, um dieses Problem zu umgehen:  
  
-   Fügen Sie mehr Protokollspeicherplatz für die primäre Datenbank hinzu.  
  
-   Setzen Sie die sekundäre Datenbank fort, bevor das Protokoll voll ist. Weitere Informationen finden Sie weiter unten in diesem Thema unter [Fortsetzen einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)anhalten.  
  
-   Entfernen Sie die sekundäre Datenbank. Weitere Informationen finden Sie unter [Entfernen einer sekundären Datenbank aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md).  
  
 **So beheben Sie die Fehler eines vollständigen Transaktionsprotokolls**  
  
-   [Problembehandlung bei vollen Transaktionsprotokollen &#40;SQL Server-Fehler 9002&#41;](../../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Fortsetzen einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Fortsetzen einer Verfügbarkeitsdatenbank &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/resume-an-availability-database-sql-server.md)  
  
  
