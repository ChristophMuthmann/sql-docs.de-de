---
title: "Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ad04708d680bc716c971fa5e24c304b5516d56a8
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-read-only-access-on-an-availability-replica-sql-server"></a>Konfigurieren des schreibgeschützten Zugriffs auf ein Verfügbarkeitsreplikat (SQL Server)
  Standardmäßig sind sowohl der Lese-/Schreibzugriff als auch der Zugriff für beabsichtigte Lesevorgänge für das primäre Replikat zulässig, während für sekundäre Replikate einer AlwaysOn-Verfügbarkeitsgruppe keine Verbindungen zulässig sind. In diesem Thema wird beschrieben, wie der Verbindungszugriff für ein Verfügbarkeitsreplikat einer AlwaysOn-Verfügbarkeitsgruppe in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] unter Verwendung von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell konfiguriert wird.  
  
 Informationen dazu, welche Auswirkungen die Aktivierung des schreibgeschützten Zugriffs für ein sekundäres Replikat hat, und eine Einführung in den Verbindungszugriff finden Sie unter [Informationen zum Clientverbindungszugriff auf Verfügbarkeitsreplikate &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md) und [Aktive sekundäre Replikate: Lesbare sekundäre Replikate &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
-   **Vorbereitungen:**  
  
     [Voraussetzungen und Einschränkungen](#Prerequisites)  
  
     [Sicherheit](#Security)  
  
-   **Konfigurieren des Zugriffs auf ein Verfügbarkeitsreplikat mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Nachverfolgung:**  [Nach dem Konfigurieren des schreibgeschützten Zugriffs für ein Verfügbarkeitsreplikat](#FollowUp)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Voraussetzungen und Einschränkungen  
  
-   Um einen anderen Verbindungszugriff zu konfigurieren, benötigen Sie eine Verbindung zur Serverinstanz, die das primäre Replikat hostet.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
  
|Task|Berechtigungen|  
|----------|-----------------|  
|So konfigurieren Sie Replikate beim Erstellen einer Verfügbarkeitsgruppe|Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** und die CREATE AVAILABILITY GROUP-Serverberechtigung, ALTER ANY AVAILABILITY GROUP-Berechtigung oder CONTROL SERVER-Berechtigung.|  
|So ändern Sie ein Verfügbarkeitsreplikat|Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.|  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 **So konfigurieren Sie den Zugriff auf einem Verfügbarkeitsreplikat**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Verfügbarkeitsreplikat hostet, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie die Knoten **Hohe Verfügbarkeit mit AlwaysOn** und **Verfügbarkeitsgruppen** .  
  
3.  Klicken Sie auf die Verfügbarkeitsgruppe, deren Replikat geändert werden soll.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Verfügbarkeitsreplikat, und klicken Sie auf **Eigenschaften**.  
  
5.  Im Dialogfeld **Eigenschaften des Verfügbarkeitsreplikats** können Sie den Verbindungszugriff für die primäre Rolle und die sekundäre Rolle wie folgt ändern:  
  
    -   Wählen Sie für die sekundäre Rolle aus der Dropdownliste für die lesbare sekundäre Rolle ****  wie folgt einen neuen Wert aus:  
  
         **Nein**  
         Es werden keine Verbindungen mit sekundären Datenbanken dieses Replikats zugelassen. Sie sind für den Lesezugriff nicht verfügbar. Dies ist die Standardeinstellung.  
  
         **Nur beabsichtigte Lesevorgänge**  
         Es sind nur schreibgeschützte Verbindungen zu sekundären Datenbanken dieses Replikats zulässig. Die sekundären Datenbanken sind alle für Lesezugriff verfügbar.  
  
         **ja**  
         Alle Verbindungen zu sekundären Datenbanken dieses Replikats sind zugelassen, aber nur für Lesezugriff. Die sekundären Datenbanken sind alle für Lesezugriff verfügbar.  
  
    -   Wählen Sie für die primäre Rolle aus der Dropdownliste für Verbindungen in der primären Rolle ****  einen neuen Wert wie folgt aus:  
  
         **Alle Verbindungen zulassen**  
         Für die Datenbanken im primären Replikat sind alle Verbindungen zugelassen. Dies ist die Standardeinstellung.  
  
         **Verbindungen mit Lese-/Schreibzugriff zulassen**  
         Wenn die Eigenschaft für die Anwendungsabsicht auf **ReadWrite** festgelegt ist oder keine Verbindungseigenschaft für die Anwendungsabsicht festgelegt wurde, wird die Verbindung zugelassen. Verbindungen, bei denen die Verbindungseigenschaft für die Anwendungsabsicht auf **ReadOnly** festgelegt ist, werden zugelassen. Dies kann verhindern, dass Kunden mit dem primären Replikat versehentlich eine leseintensive Arbeitsauslastung verbinden. Weitere Informationen zur Verbindungseigenschaft für die Anwendungsabsicht finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So konfigurieren Sie den Zugriff auf einem Verfügbarkeitsreplikat**  
  
> [!NOTE]  
>  Ein Beispiel für diese Prozedur finden Sie weiter unten in diesem Abschnitt unter [Beispiel (Transact-SQL)](#TsqlExample).  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet.  
  
2.  Wenn Sie ein Replikat für eine neue Verfügbarkeitsgruppe angeben, verwenden Sie die [-Anweisung](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Verwenden Sie zum Hinzufügen oder Ändern eines Replikats für eine vorhandene Verfügbarkeitsgruppe die [-Anweisung](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Geben Sie zum Konfigurieren des Verbindungszugriffs für die sekundäre Rolle in der ADD REPLICA- bzw. MODIFY REPLICA WITH-Klausel die SECONDARY_ROLE-Option wie folgt an:  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         Erläuterungen:  
  
         Nein  
         Es werden keine direkten Verbindungen mit sekundären Datenbanken dieses Replikats zugelassen. Sie sind für den Lesezugriff nicht verfügbar. Dies ist die Standardeinstellung.  
  
         READ_ONLY  
         Es sind nur schreibgeschützte Verbindungen zu sekundären Datenbanken dieses Replikats zulässig. Die sekundären Datenbanken sind alle für Lesezugriff verfügbar.  
  
         ALL  
         Alle Verbindungen zu sekundären Datenbanken dieses Replikats sind zugelassen, aber nur für Lesezugriff. Die sekundären Datenbanken sind alle für Lesezugriff verfügbar.  
  
3.  Geben Sie zum Konfigurieren des Verbindungszugriffs für die primäre Rolle in der ADD REPLICA- bzw. MODIFY REPLICA WITH-Klausel die PRIMARY_ROLE-Option wie folgt an:  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     Erläuterungen:  
  
     READ_WRITE  
     Verbindungen, bei denen die Verbindungseigenschaft für die Anwendungsabsicht auf **ReadOnly** festgelegt ist, werden nicht zugelassen.  Wenn die Eigenschaft für die Anwendungsabsicht auf **ReadWrite** festgelegt ist oder keine Verbindungseigenschaft für die Anwendungsabsicht festgelegt wurde, wird die Verbindung zugelassen. Weitere Informationen zur Verbindungseigenschaft für die Anwendungsabsicht finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
     ALL  
     Für die Datenbanken im primären Replikat sind alle Verbindungen zugelassen. Dies ist die Standardeinstellung.  
  
###  <a name="TsqlExample"></a> Beispiel (Transact-SQL)  
 Im folgenden Beispiel wird einer Verfügbarkeitsgruppe namens *AG2*ein sekundäres Replikat hinzugefügt. Zum Hosten des neuen Verfügbarkeitsreplikats wurde die eigenständige Serverinstanz *COMPUTER03\HADR_INSTANCE*angegeben. Dieses Replikat ist zum ausschließlichen Zulassen von Verbindungen mit Lese-/Schreibzugriff für die primäre Rolle sowie zum ausschließlichen Zulassen von Verbindungen mit beabsichtigten Lesevorgängen konfiguriert.  
  
```  
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So konfigurieren Sie den Zugriff auf einem Verfügbarkeitsreplikat**  
  
> [!NOTE]  
>  Ein Codebeispiel finden Sie weiter unten in diesem Abschnitt unter [Beispiel (PowerShell)](#PSExample).  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, auf der das primäre Replikat gehostet wird.  
  
2.  Verwenden Sie zum Hinzufügen eines Verfügbarkeitsreplikats zu einer Verfügbarkeitsgruppe das Cmdlet **New-SqlAvailabilityReplica** . Verwenden Sie zum Ändern eines vorhandenen Verfügbarkeitsreplikats das Cmdlet **Set-SqlAvailabilityReplica** . Die relevanten Parameter lauten wie folgt:  
  
    -   Um den Verbindungszugriff für die sekundäre Rolle zu konfigurieren, geben Sie den Parameter **ConnectionModeInSecondaryRole** *secondary_role_keyword* an, wobei *secondary_role_keyword* einem der folgenden Werte entspricht:  
  
         **AllowNoConnections**  
         Für die Datenbanken im sekundären Replikat sind keine direkten Verbindungen zugelassen, und die Datenbanken sind für den Lesezugriff nicht verfügbar. Dies ist die Standardeinstellung.  
  
         **AllowReadIntentConnectionsOnly**  
         Verbindungen mit den Datenbanken im sekundären Replikat sind nur zulässig, wenn die Eigenschaft für die Anwendungsabsicht auf **ReadOnly**festgelegt ist. Weitere Informationen zu dieser Eigenschaft finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Für alle Verbindungen mit den Datenbanken im sekundären Replikat ist der schreibgeschützte Zugriff zugelassen.  
  
    -   Um den Verbindungszugriff für die primäre Rolle zu konfigurieren, geben Sie **ConnectionModeInPrimaryRole** *primary_role_keyword* an, wobei *primary_role_keyword* einem der folgenden Werte entspricht:  
  
         **AllowReadWriteConnections**  
         Verbindungen, bei denen die Verbindungseigenschaft für die Anwendungsabsicht auf ReadOnly festgelegt ist, werden nicht zugelassen. Wenn die Eigenschaft für die Anwendungsabsicht auf ReadWrite festgelegt ist oder keine Verbindungseigenschaft für die Anwendungsabsicht festgelegt wurde, wird die Verbindung zugelassen. Weitere Informationen zur Verbindungseigenschaft für die Anwendungsabsicht finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
         **AllowAllConnections**  
         Für die Datenbanken im primären Replikat sind alle Verbindungen zugelassen. Dies ist die Standardeinstellung.  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das Cmdlet **Get-Help** in der [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] -PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="PSExample"></a> Beispiel (PowerShell)  
 Im folgenden Beispiel wird sowohl der **ConnectionModeInSecondaryRole** -Parameter als auch der **ConnectionModeInPrimaryRole** -Parameter auf **AllowAllConnections**festgelegt.  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach der Konfiguration des schreibgeschützten Zugriffs für ein Verfügbarkeitsreplikat  
 **Schreibgeschützter Zugriff auf ein lesbares sekundäres Replikat**  
  
-   Bei Verwendung der Hilfsprogramme [bcp](../../../tools/bcp-utility.md) oder [sqlcmd](../../../tools/sqlcmd-utility.md)können Sie den schreibgeschützten Zugriff für jedes sekundäre Replikat angeben, das den schreibgeschützten Zugriff unterstützt, indem Sie den Switch **-K ReadOnly** angeben.  
  
-   So ermöglichen Sie, dass Clientanwendungen eine Verbindung mit lesbaren sekundären Replikaten herstellen können  
  
    ||Voraussetzung|Link|  
    |-|------------------|----------|  
    |![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Stellen Sie sicher, dass die Verfügbarkeitsgruppe über einen Listener verfügt.|[Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Kontrollkästchen](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|Konfigurieren Sie das schreibgeschützte Routing für eine Verfügbarkeitsgruppe.|[Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **Faktoren, die sich auf Trigger und Aufträge nach einem Failover auswirken können**  
  
 Wenn Sie Trigger und Aufträge haben, die beim Ausführen auf einer nicht lesbaren sekundären Datenbank oder einer lesbaren sekundären Datenbank fehlschlagen, müssen Sie ein Skript für die Trigger und Aufträge erstellen, die auf einem angegebenen Replikat kontrolliert werden sollen, um zu bestimmen, ob die Datenbank eine primäre Datenbank oder eine lesbare sekundäre Datenbank ist. Um diese Informationen abzurufen, verwenden Sie die [DATABASEPROPERTYEX](../../../t-sql/functions/databasepropertyex-transact-sql.md) -Funktion, um die **Updatability** -Eigenschaft der Datenbank zurückzugeben. Um eine schreibgeschützte Datenbank zu identifizieren, geben Sie READ_ONLY wie folgt als Wert an:  
  
```  
DATABASEPROPERTYEX([db name],’Updatability’) = N’READ_ONLY’  
```  
  
 Um eine Datenbank mit Lese-/Schreibzugriff zu identifizieren, geben Sie READ_WRITE als Wert an.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Konfigurieren des schreibgeschützten Routing für eine Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Erstellen oder Konfigurieren eines Verfügbarkeitsgruppenlisteners &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [AlwaysOn: Leistungsversprechen lesbarer sekundärer Replikate](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-value-proposition-of-readable-secondary.aspx)  
  
-   [AlwaysOn: Warum gibt es zwei Optionen, um ein sekundäres Replikat für die Lesearbeitslast zu aktivieren?](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [AlwaysOn: Einrichten eines lesbaren sekundären Replikats](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-setting-up-readable-seconary-replica.aspx)  
  
-   [AlwaysOn: Ich habe gerade lesbare sekundäre Replikate aktiviert, meine Abfrage wird jedoch blockiert.](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [AlwaysOn: Verfügbarmachen aktueller Statistiken auf lesbaren sekundären Replikaten, schreibgeschützten Datenbanken und Datenbank-Momentaufnahmen](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [AlwaysOn: Herausforderungen bei Statistiken auf schreibgeschützten Datenbanken, Datenbank-Momentaufnahmen und sekundären Replikaten](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [AlwaysOn: Auswirkungen auf die primäre Arbeitslast, wenn die Berichterstellungsarbeitslast auf dem sekundären Replikat ausgeführt wird](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [AlwaysOn: Auswirkungen der Zuordnung der Berichterstellungsarbeitslast vom lesbaren sekundären Replikat zur Momentaufnahmeisolation](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [AlwaysOn: Minimieren der Blockierung von REDO-Threads beim Ausführen der Berichterstellungsarbeitslast auf sekundären Replikaten](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [AlwaysOn: Lesbares sekundäres Replikat und Datenlatenz](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On.aspx)  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Aktive sekundäre Replikate: Lesbare sekundäre Replikate (Always On-Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Informationen zum Clientverbindungszugriff auf Verfügbarkeitsreplikate (SQL Server)](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  

