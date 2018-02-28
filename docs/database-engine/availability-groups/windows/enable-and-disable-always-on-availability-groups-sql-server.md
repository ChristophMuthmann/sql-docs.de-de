---
title: "Aktivieren und Deaktivieren von Always On-Verfügbarkeitsgruppen (SQL Server) | SQL-Server"
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c795cc98d8dffa44d7f9759b8f66e896f75123c4
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/23/2018
---
# <a name="enable-and-disable-always-on-availability-groups-sql-server"></a>Aktivieren und Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] muss aktiviert werden, damit eine Serverinstanz Verfügbarkeitsgruppen verwenden kann. Bevor Sie eine beliebige Verfügbarkeitsgruppe erstellen und konfigurieren können, muss die Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] für jede Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aktiviert worden sein, auf der ein Verfügbarkeitsreplikat für mindestens eine Verfügbarkeitsgruppe gehostet wird.  
  
> [!IMPORTANT]  
>  Wenn Sie einen WSFC-Cluster löschen und neu erstellen, müssen Sie die Funktion [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] für jede Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deaktivieren und erneut aktivieren, auf der auf dem ursprünglichen WSFC-Cluster ein Verfügbarkeitsreplikat gehostet wurde.  
  
-   **Vorbereitungen:**  
  
     [Erforderliche Komponenten](#Prerequisites)  
  
     [Security](#Security)  
  
-   **Vorgehensweise:**  
  
    -   [Bestimmen, ob AlwaysOn-Verfügbarkeitsgruppen aktiviert sind](#IsEnabled)  
  
    -   [Aktivieren von AlwaysOn-Verfügbarkeitsgruppen](#EnableAOAG)  
  
    -   [Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen](#DisableAOAG)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Voraussetzungen zum Aktivieren von AlwaysOn-Verfügbarkeitsgruppen  
  
-   Die Serverinstanz muss sich auf einem WSFC-Knoten (Windows Server Failover Clustering) befinden.  
  
-   Auf der Serverinstanz muss eine Edition von SQL Server ausgeführt werden, die [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]unterstützt. Weitere Informationen finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
-   AlwaysOn-Verfügbarkeitsgruppen sollten jeweils nur für eine Serverinstanz aktiviert werden. Warten Sie nach der Aktivierung von AlwaysOn-Verfügbarkeitsgruppen, bis der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Dienst neu gestartet wurde, bevor Sie mit einer anderen Serverinstanz fortfahren.  
  
 Informationen zu zusätzlichen Voraussetzungen zum Erstellen und Konfigurieren von Verfügbarkeitsgruppen finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen für AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Sicherheit  
 Während AlwaysOn-Verfügbarkeitsgruppen auf einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]aktiviert sind, verfügt die Serverinstanz über Vollzugriff auf den WSFC-Cluster.  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert auf dem lokalen Computer die Mitgliedschaft in der Gruppe **Administrator** und Vollzugriff auf den WSFC-Cluster. Wenn Sie AlwaysOn mit PowerShell aktivieren, öffnen Sie das Eingabeaufforderungsfenster unter Verwendung der Option **Als Administrator ausführen** .  
  
 Erfordert, dass von Active Directory Objekte erstellt und Objektberechtigungen verwaltet werden.  
  
##  <a name="IsEnabled"></a> Bestimmen, ob AlwaysOn-Verfügbarkeitsgruppen aktiviert sind  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="SSMS1Procedure"></a> Verwendung von SQL Server Management Studio  
 **So ermitteln Sie, ob AlwaysOn-Verfügbarkeitsgruppen aktiviert sind**  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Serverinstanz, und klicken Sie auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Servereigenschaften** auf die Seite **Allgemein** . Die Eigenschaft **Ist HADR-aktiviert** zeigt einen der folgenden Werte an:  
  
    -   **True**, wenn AlwaysOn-Verfügbarkeitsgruppen aktiviert sind.  
  
    -   **False**, wenn AlwaysOn-Verfügbarkeitsgruppen deaktiviert sind.  
  
###  <a name="Tsql1Procedure"></a> Verwenden von Transact-SQL  
 **So ermitteln Sie, ob AlwaysOn-Verfügbarkeitsgruppen aktiviert sind**  
  
1.  Verwenden Sie die folgende [SERVERPROPERTY](../../../t-sql/functions/serverproperty-transact-sql.md) -Anweisung:  
  
    ```  
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     Die Einstellung der **IsHadrEnabled** -Servereigenschaft gibt folgendermaßen an, ob eine Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] für AlwaysOn-Verfügbarkeitsgruppen aktiviert ist:  
  
    -   Falls **IsHadrEnabled** = 1, sind AlwaysOn-Verfügbarkeitsgruppen aktiviert.  
  
    -   Falls **IsHadrEnabled** = 0, sind AlwaysOn-Verfügbarkeitsgruppen deaktiviert.  
  
    > [!NOTE]  
    >  Weitere Informationen zur **IsHadrEnabled** -Servereigenschaft finden Sie unter [SERVERPROPERTY &#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)unterstützt.  
  
###  <a name="PowerShell1Procedure"></a> PowerShell  
 **So ermitteln Sie, ob AlwaysOn-Verfügbarkeitsgruppen aktiviert sind**  
  
1.  Legen Sie die Serverinstanz als Standard fest (**cd**), auf der Sie ermitteln möchten, ob [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] aktiviert ist.  
  
2.  Geben Sie den folgenden **Get-Item** -Befehl von PowerShell ein:  
  
    ```  
    PS SQLSERVER:\SQL\NODE1\DEFAULT> get-item . | select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="EnableAOAG"></a> Aktivieren von AlwaysOn-Verfügbarkeitsgruppen  
 **So aktivieren Sie AlwaysOn mit der folgenden Option:**  
  
-   [SQL Server-Konfigurations-Manager](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="SQLCM2Procedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
 **So aktivieren Sie AlwaysOn-Verfügbarkeitsgruppen**  
  
1.  Stellen Sie eine Verbindung mit dem Windows Server Failover Clustering (WSFC)-Knoten her, auf dem die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz gehostet wird, auf der Sie AlwaysOn-Verfügbarkeitsgruppen aktivieren möchten.  
  
2.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server Konfigurations-Manager**.  
  
3.  Klicken Sie im **SQL Server-Konfigurations-Manager** auf **SQL Server-Dienste** und mit der rechten Maustaste auf SQL Server (**\<***Instanzname***>)**, wobei **\<***Instanzname***>** der Name einer lokalen Serverinstanz ist, für die Sie Always On-Verfügbarkeitsgruppen aktivieren sollten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Wählen Sie die Registerkarte **Hohe Verfügbarkeit mit AlwaysOn** aus.  
  
5.  Überprüfen Sie, ob das Feld **Name des Windows-Failoverclusters** den Namen des lokalen Failoverclusters enthält. Wenn dieses Feld leer ist, wird [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]von dieser Serverinstanz derzeit nicht unterstützt. Der lokale Computer ist kein Clusterknoten, der WSFC-Cluster wurde geschlossen oder diese Edition von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] unterstützt [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]nicht.  
  
6.  Aktivieren Sie das Kontrollkästchen **AlwaysOn-Verfügbarkeitsgruppen aktivieren** , und klicken Sie auf **OK**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfigurations-Manager speichert die Änderung. Dann müssen Sie den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst manuell neu starten. Dies ermöglicht die Auswahl einer für die Geschäftsanforderungen optimalen Neustartzeit. Wenn der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst neu gestartet wird, wird AlwaysOn aktiviert, und die **IsHadrEnabled** -Servereigenschaft wird auf 1 festgelegt.  
  
###  <a name="PScmd2Procedure"></a> SQL Server PowerShell  
 **So aktivieren Sie AlwaysOn**  
  
1.  Wechseln Sie in das Verzeichnis einer Serverinstanz (**cd**), die Sie für AlwaysOn-Verfügbarkeitsgruppen aktivieren möchten.  
  
2.  Verwenden Sie das Cmdlet **Enable-SqlAlwaysOn** um Always On-Verfügbarkeitsgruppen zu aktivieren.  
  
     Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
    > [!NOTE]  
    >  Informationen zur Steuerung des Neustarts des **-Diensts durch das** Enable-SqlAlwaysOn [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Cmdlet finden Sie unter [Wann startet ein Cmdlet den SQL Server-Dienst neu?](#WhenCmdletRestartsSQL) weiter unten in diesem Thema.  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
####  <a name="ExmplEnable-SqlHadrServic"></a> Beispiel: Enable-SqlAlwaysOn  
 Durch den folgenden PowerShell-Befehl wird [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] auf einer Instanz von SQL Server (*Computer*\\*Instanz*) aktiviert.  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="DisableAOAG"></a> Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen  
  
-   **Vor dem Deaktivieren von AlwaysOn:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So deaktivieren Sie AlwaysOn mit der folgenden Option**  
  
    -   [SQL Server-Konfigurations-Manager](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **Nachverfolgung:**  [Nach dem Deaktivieren von AlwaysOn](#FollowUp)  
  
> [!IMPORTANT]  
>  Deaktivieren Sie AlwaysOn jeweils nur auf einer Serverinstanz. Warten Sie nach der Deaktivierung von AlwaysOn-Verfügbarkeitsgruppen, bis der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst neu gestartet wurde, bevor Sie mit einer anderen Serverinstanz fortfahren.  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Bevor Sie AlwaysOn auf einer Serverinstanz deaktivieren, sollten Sie wie folgt vorgehen:  
  
1.  Wenn das primäre Replikat einer Verfügbarkeitsgruppe, die beibehalten werden soll, derzeit auf einer Serverinstanz gehostet wird, sollten Sie nach Möglichkeit manuell ein Failover für die Verfügbarkeitsgruppe zum synchronisierten sekundären Replikat ausführen. Weitere Informationen finden Sie unter [Ausführen eines geplanten manuellen Failovers einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
2.  Entfernen Sie alle lokalen sekundären Replikate. Weitere Informationen finden Sie unter [Entfernen eines sekundären Replikats aus einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server.md).  
  
###  <a name="SQLCM3Procedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
 **So deaktivieren Sie AlwaysOn**  
  
1.  Stellen Sie eine Verbindung mit dem Windows Server Failover Clustering (WSFC)-Knoten her, auf dem die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz gehostet wird, auf der Sie AlwaysOn-Verfügbarkeitsgruppen deaktivieren möchten.  
  
2.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
3.  Klicken Sie im **SQL Server-Konfigurations-Manager** auf **SQL Server-Dienste** und mit der rechten Maustaste auf SQL Server (**\<***Instanzname***>)**, wobei **\<***Instanzname***>** der Name einer lokalen Serverinstanz ist, für die Sie Always On-Verfügbarkeitsgruppen deaktivieren sollten, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Deaktivieren Sie auf der Registerkarte**Hohe Verfügbarkeit mit AlwaysOn**das Kontrollkästchen **AlwaysOn-Verfügbarkeitsgruppen aktivieren** , und klicken Sie auf **OK**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Konfigurations-Manager speichert die Änderung und startet den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst neu. Beim Neustart des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Diensts wird AlwaysOn deaktiviert. Zudem wird die **IsHadrEnabled** -Servereigenschaft auf 0 festgelegt, um anzuzeigen, dass AlwaysOn-Verfügbarkeitsgruppen deaktiviert sind.  
  
5.  Es empfiehlt sich, dass Sie die Informationen unter [Nachverfolgung: Nach dem Deaktivieren von AlwaysOn](#FollowUp)später in diesem Thema lesen.  
  
###  <a name="PScmd3Procedure"></a> SQL Server PowerShell  
 **So deaktivieren Sie AlwaysOn**  
  
1.  Wechseln Sie in das Verzeichnis (**cd**) einer derzeit aktivierten Serverinstanz, die Sie für AlwaysOn-Verfügbarkeitsgruppen deaktivieren möchten.  
  
2.  Verwenden Sie das **Disable-SqlAlwaysOn**-Cmdlet, um die Always On-Verfügbarkeitsgruppen zu aktivieren.  
  
     Beispielsweise werden durch den folgenden Befehl AlwaysOn-Verfügbarkeitsgruppen auf der SQL Serverinstanz (*Computer*\\*Instanz*) deaktiviert.  Dieser Befehl erfordert einen Neustart der Instanz, und Sie werden aufgefordert, diesen Neustart zu bestätigen.  
  
    ```  
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  Informationen zur Steuerung, ob das Cmdlet **Disable-SqlAlwaysOn** den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Dienst neu startet, finden Sie unter [Wann startet ein Cmdlet den SQL Server-Dienst neu?](#WhenCmdletRestartsSQL) weiter unten in diesem Thema.  
  
     Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="FollowUp"></a> Nachverfolgung: Nach dem Deaktivieren von AlwaysOn  
 Nachdem Sie AlwaysOn-Verfügbarkeitsgruppen deaktiviert haben, muss die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] neu gestartet werden. Die Serverinstanz wird vom SQL-Konfigurations-Manager automatisch neu gestartet. Wenn Sie jedoch das **Disable-SqlAlwaysOn** -Cmdlet verwendet haben, müssen Sie die Serverinstanz manuell neu starten. Weitere Informationen finden Sie unter [sqlservr Application](../../../tools/sqlservr-application.md).  
  
 Auf der neu gestarteten Serverinstanz:  
  
-   Verfügbarkeitsdatenbanken werden bei SQL Server-Start nicht gestartet. Daher kann nicht auf sie zugegriffen werden.  
  
-   Die einzige unterstützte AlwaysOn- [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Anweisung ist [DROP AVAILABILITY GROUP](../../../t-sql/statements/drop-availability-group-transact-sql.md). Die Optionen CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP und SET HADR von ALTER DATABASE werden nicht unterstützt.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Metadaten und [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] -Konfigurationsdaten in WSFC sind von der Deaktivierung der AlwaysOn-Verfügbarkeitsgruppen nicht betroffen.  
  
 Wenn Sie AlwaysOn-Verfügbarkeitsgruppen dauerhaft auf jeder Serverinstanz deaktivieren, die ein Verfügbarkeitsreplikat für eine oder mehrere Verfügbarkeitsgruppen hostet, empfiehlt es sich, dass Sie die folgenden Schritte ausführen:  
  
1.  Wenn Sie die lokalen Verfügbarkeitsreplikate nicht vor dem Deaktivieren von AlwaysOn entfernt haben, löschen Sie jede Verfügbarkeitsgruppe, für die die Serverinstanz ein Verfügbarkeitsreplikat hostet. Informationen zum Löschen einer Verfügbarkeitsgruppe finden Sie unter [Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
2.  Um die zurückgelassenen Metadaten zu entfernen, löschen Sie jede betroffene Verfügbarkeitsgruppe auf einer Serverinstanz, die Teil des ursprünglichen WSFC-Clusters ist.  
  
3.  Auf die primären Datenbanken kann weiterhin anhand aller Verbindungen außer der Datensynchronisierung zwischen der primären und der sekundären Datenbank zugegriffen werden.  
  
4.  Die sekundären Datenbanken übernehmen den Status RESTORING. Sie können sie entweder löschen oder sie mit RESTORE WITH RECOVERY wiederherstellen. Wiederhergestellte Datenbanken nehmen jedoch nicht mehr an der Datensynchronisierung für Verfügbarkeitsgruppen teil.  
  
##  <a name="WhenCmdletRestartsSQL"></a> Wann startet ein Cmdlet den SQL Server-Dienst neu?  
 Auf einer aktuell ausgeführten Serverinstanz kann die Verwendung von **Enable-SqlAlwaysOn** oder **Disable-SqlAlwaysOn** zum Ändern der aktuellen Always On-Einstellung zu einem Neustart des SQL Server-Diensts führen. Das Neustartverhalten hängt von den folgenden Bedingungen ab:  
  
|-NoServiceRestart-Parameter angegeben|-Force-Parameter angegeben|Wurde der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienst neu gestartet?|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|nein|nein|Standardmäßig. Aber das Cmdlet fordert Sie folgendermaßen auf:<br /><br /> **Um diese Aktion abzuschließen, müssen wir den SQL Server-Dienst für die Serverinstanz "<instance_name>" neu starten. Möchten Sie den Vorgang fortsetzen?**<br /><br /> **[Y] Ja  [N] Nein  [S] Anhalten  [?] Hilfe (Standard ist „Y"):**<br /><br /> Wenn Sie **N** oder **S**angeben, wird der Dienst nicht neu gestartet.|  
|nein|ja|Der Dienst wird neu gestartet.|  
|ja|nein|Der Dienst wird nicht neu gestartet.|  
|ja|ja|Der Dienst wird nicht neu gestartet.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

