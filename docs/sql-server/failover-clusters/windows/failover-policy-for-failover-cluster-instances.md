---
title: "Failoverrichtlinie für Failoverclusterinstanzen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: failover-clusters
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: flexible failover policy
ms.assetid: 39ceaac5-42fa-4b5d-bfb6-54403d7f0dc9
caps.latest.revision: "45"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 70117aaa0f1e936fff8c8d78f82636d4e77c460b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="failover-policy-for-failover-cluster-instances"></a>Failoverrichtlinie für Failoverclusterinstanzen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Failoverclusterinstanz (FCI) kann jeweils nur ein Knoten Besitzer der WSFC-Clusterressourcengruppe (Windows Server Failover Cluster) sein. Die Clientanforderungen werden durch diesen Knoten in der FCI behandelt. Falls ein Fehler auftritt und kein erfolgreicher Neustart möglich ist, geht die Gruppe in den Besitz eines anderen WSFC-Knotens in der FCI über. Dieser Prozess wird als Failover bezeichnet. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] erhöht die Zuverlässigkeit der Fehlererkennung und bietet eine flexible Failoverrichtlinie.  
  
 Eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -FCI ist im Hinblick auf die Failovererkennung vom zugrunde liegenden WSFC-Dienst abhängig. Daher wird das Failoververhalten für die FCI durch zwei Mechanismen bestimmt: Der erste Mechanismus wird durch die systemeigenen WSFC-Funktionen und der zweite durch die Funktionen bereitgestellt, die vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Setup hinzugefügt werden.  
  
-   Da die Quorumkonfiguration vom WSFC-Cluster verwaltet wird, ist sichergestellt, dass bei einem automatischen Failover ein eindeutiges Failoverziel vorhanden ist. Der WSFC-Dienst ermittelt kontinuierlich, ob der Cluster einen optimalem Quorumzustand aufweist und schaltet die Ressourcengruppe entsprechend online und offline.  
  
-   Von der aktiven [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz werden regelmäßig Komponentendiagnosen über eine dedizierte Verbindung an die WSFC-Ressourcengruppe übermittelt. Die Failoverrichtlinie, in der die Fehlerbedingungen definiert sind, durch die Neustarts und Failover ausgelöst werden, wird von der WSFC-Ressourcengruppe verwaltet.  
  
 In diesem Thema wird der zweite oben genannte Mechanismus erörtert. Weitere Informationen zum WSFC-Verhalten bei der Quorumkonfiguration und Integritätserkennung finden Sie unter [WSFC-Quorummodi und Abstimmungskonfiguration &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
> [!IMPORTANT]  
>  Automatische Failover auf und von einer FCI sind in einer Always On-Verfügbarkeitsgruppe nicht zulässig. Ein manuelles Failover auf eine FCI bzw. von einer FCI ist in einer Always On-Verfügbarkeitsgruppe jedoch zulässig.  
  
##  <a name="Concepts"></a> Übersicht über die Failoverrichtlinie  
 Der Failoverprozess lässt sich in folgende Schritte gliedern:  
  
1.  [Überwachen des Integritätsstatus](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#monitor)  
  
2.  [Bestimmen von Fehlern](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#determine)  
  
3.  [Reagieren auf Fehler](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#respond)  
  
###  <a name="monitor"></a> Überwachen des Integritätsstatus  
 Es gibt drei Arten von Integritätsstatus, die für die FCI überwacht werden:  
  
-   [Status des SQL Server-Diensts](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#service)  
  
-   [Reaktionsfähigkeit der SQL Server-Instanz](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#instance)  
  
-   [SQL Server-Komponentendiagnose](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#component)  
  
####  <a name="service"></a> Status des SQL Server-Diensts  
 Der WSFC-Dienst überwacht den Startstatus des SQL Server-Diensts auf dem aktiven FCI-Knoten, um die Beendigung des SQL Server-Diensts zu erkennen.  
  
####  <a name="instance"></a> Reaktionsfähigkeit der SQL Server-Instanz  
 Während des Starts von SQL Server verwendet der WSFC-Dienst die Ressourcen-DLL des SQL Server-Datenbankmoduls, um eine neue Verbindung auf einem separaten Thread zu erstellen, die ausschließlich zum Überwachen des Integritätsstatus verwendet wird. Dadurch wird sichergestellt, dass die SQL-Instanz auch unter höherer Auslastung über die erforderlichen Ressourcen zum Übermitteln ihres Integritätsstatus verfügt. Unter Verwendung dieser dedizierten Verbindung führt SQL Server die gespeicherte Systemprozedur [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) im Wiederholungsmodus aus, um regelmäßig den Integritätsstatus der SQL Server-Komponenten an die Ressourcen-DLL zu übermitteln.  
  
 Die Ressourcen-DLL bestimmt die Reaktionsfähigkeit der SQL-Instanz mithilfe eines Timeouts für die Zustandsüberprüfung. Die HealthCheckTimeout-Eigenschaft definiert, wie lange die Ressourcen-DLL auf eine Antwort von der gespeicherten Prozedur sp_server_diagnostics wartet, bevor der WSFC-Dienst die Meldung erhält, dass die SQL-Instanz nicht reagiert. Diese Eigenschaft kann sowohl mit T-SQL als auch im Failovercluster-Manager-Snap-In konfiguriert werden. Weitere Informationen finden Sie unter [Configure HealthCheckTimeout Property Settings](../../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md). Nachfolgend wird beschrieben, wie sich diese Eigenschaft auf die Einstellungen bezüglich Timeout und Wiederholungsintervall auswirken:  
  
-   Die gespeicherte Prozedur sp_server_diagnostics wird von der Ressourcen-DLL aufgerufen, und das Wiederholungsintervall wird auf ein Drittel des Werts der HealthCheckTimeout-Einstellung festgelegt.  
  
-   Wenn die gespeicherte Prozedur sp_server_diagnostics langsam ist oder keine Informationen zurückgibt, wartet die Ressourcen-DLL, bis das durch HealthCheckTimeout angegebene Intervall abgelaufen ist, bevor an den WSFC-Dienst gemeldet wird, dass die SQL-Instanz nicht reagiert.  
  
-   Wenn die dedizierte Verbindung unterbrochen wird, versucht die Ressourcen-DLL für die durch HealthCheckTimeout angegebene Dauer, eine neue Verbindung mit der SQL-Instanz herzustellen, bevor an den WSFC-Dienst gemeldet wird, dass die SQL-Instanz nicht reagiert.  
  
####  <a name="component"></a> SQL Server-Komponentendiagnose  
 Die gespeicherte Systemprozedur sp_server_diagnostics sammelt in regelmäßigen Abständen Diagnoseinformationen zu den Komponenten der SQL-Instanz. Die gesammelten Diagnoseinformationen werden als Zeile für die folgenden Komponenten angegeben und an den aufrufenden Thread übergeben.  
  
1.  System  
  
2.  resource  
  
3.  query process  
  
4.  io_subsystem  
  
5.  Ereignisse  
  
 Das System, die Ressource und der Abfrageprozess werden für die Fehlererkennung verwendet. Die io_subsytem und die Ereignisse werden nur zu Diagnosezwecken verwendet.  
  
 Jedes Rowset der Informationen wird auch in das SQL Server-Clusterdiagnoseprotokoll geschrieben. Weitere Informationen finden Sie unter [Anzeigen und Lesen des Failoverclusterinstanz-Diagnoseprotokolls](../../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md).  
  
> [!TIP]  
>  Die gespeicherte Prozedur sp_server_diagnostic wird von der SQL Server Always On-Technologie genutzt und kann in jeder SQL Server-Instanz zur einfacheren Problemerkennung und -behandlung verwendet werden.  
  
####  <a name="determine"></a> Bestimmen von Fehlern  
 Die Ressourcen-DLL des SQL Server-Datenbankmoduls bestimmt anhand der FailureConditionLevel-Eigenschaft, ob der erkannte Integritätsstatus eine Fehlerbedingung darstellt. Durch die FailureConditionLevel-Eigenschaft wird definiert, welcher erkannte Integritätsstatus zu einem Neustart oder Failover führt. Die unterschiedlichsten Optionen sind verfügbar: So kann beispielsweise nie ein automatischer Neustart oder ein automatisches Failover ausgelöst werden, oder bei jeder möglichen Fehlerbedingung wird immer ein automatischer Neustart bzw. ein automatisches Failover ausgeführt. Weitere Informationen zum Konfigurieren dieser Eigenschaft finden Sie unter [Configure FailureConditionLevel Property Settings](../../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).  
  
 Die Fehlerbedingungen werden auf einer ansteigenden Skala festgelegt. Auf der Ebene 1-5 enthält jede Ebene die Bedingungen der vorherigen Ebenen sowie die eigenen Bedingungen. Dies bedeutet, dass die Wahrscheinlichkeit eines Failovers oder Neustarts mit jeder Ebene zunimmt. Die Fehlerbedingungsebenen werden in der folgenden Tabelle beschrieben.  
  
 Informieren Sie sich unter [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md), da diese gespeicherte Systemprozedur eine wichtige Funktion im Hinblick auf Fehlerbedingungsebenen erfüllt.  
  
|Ebene|Bedingung|Beschreibung|  
|-----------|---------------|-----------------|  
|0|Kein automatischer Failover oder Neustart|Gibt an, dass bei einer Fehlerbedingung nicht automatisch ein Failover oder Neustart ausgelöst wird. Diese Ebene ist nur für die Systemwartung vorgesehen.|  
|1|Failover oder Neustart bei Serverausfall|Gibt an, dass ein Neustart oder ein Failover des Server ausgelöst wird, wenn die folgende Bedingung zutrifft:<br /><br /> SQL Server-Dienst ist ausgefallen.|  
|2|Failover oder Neustart bei nicht reagierendem Server|Gibt an, dass ein Neustart oder ein Failover des Server ausgelöst wird, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> SQL Server-Dienst ist ausgefallen.<br /><br /> SQL Server-Instanz reagiert nicht (die Ressourcen-DLL kann von sp_server_diagnostics keine Daten innerhalb der durch die HealthCheckTimeout-Einstellungen vorgegebenen Zeit empfangen).|  
|3*|Failover oder Neustart bei wichtigen Serverfehlern|Gibt an, dass ein Neustart oder ein Failover des Server ausgelöst wird, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> SQL Server-Dienst ist ausgefallen.<br /><br /> SQL Server-Instanz reagiert nicht (die Ressourcen-DLL kann von sp_server_diagnostics keine Daten innerhalb der durch die HealthCheckTimeout-Einstellungen vorgegebenen Zeit empfangen).<br /><br /> Gespeicherte Systemprozedur sp_server_diagnostics gibt einen Systemfehler zurück.|  
|4|Failover oder Neustart auf mittelschweren Serverfehlern|Gibt an, dass ein Neustart oder ein Failover des Server ausgelöst wird, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> SQL Server-Dienst ist ausgefallen.<br /><br /> SQL Server-Instanz reagiert nicht (die Ressourcen-DLL kann von sp_server_diagnostics keine Daten innerhalb der durch die HealthCheckTimeout-Einstellungen vorgegebenen Zeit empfangen).<br /><br /> Gespeicherte Systemprozedur sp_server_diagnostics gibt einen Systemfehler zurück.<br /><br /> Gespeicherte Systemprozedur sp_server_diagnostics gibt einen Ressourcenfehler zurück.|  
|5|Failover oder Neustart bei qualifizierten Fehlerbedingungen|Gibt an, dass ein Neustart oder ein Failover des Server ausgelöst wird, wenn eine der folgenden Bedingungen zutrifft:<br /><br /> SQL Server-Dienst ist ausgefallen.<br /><br /> SQL Server-Instanz reagiert nicht (die Ressourcen-DLL kann von sp_server_diagnostics keine Daten innerhalb der durch die HealthCheckTimeout-Einstellungen vorgegebenen Zeit empfangen).<br /><br /> Gespeicherte Systemprozedur sp_server_diagnostics gibt einen Systemfehler zurück.<br /><br /> Gespeicherte Systemprozedur sp_server_diagnostics gibt einen Ressourcenfehler zurück.<br /><br /> Gespeicherte Systemprozedur sp_server_diagnostics gibt Fehler bei der Abfrageverarbeitung zurück.|  
  
 *Standardwert  
  
####  <a name="respond"></a> Reagieren auf Fehler  
 Wie der WSFC-Dienst auf die erkannten Fehlerbedingungen reagiert, hängt vom WSFC-Quorumstatus sowie von den Neustart- und Failovereinstellungen der FCI-Ressourcengruppe ab. Wenn die FCI das WSFC-Quorum verloren hat, wird die gesamte FCI offline geschaltet und weist keine Hochverfügbarkeit mehr auf. Wenn die FCI noch über das WSFC-Quorum verfügt, reagiert der WSFC-Dienst u. U. wie folgt: Zunächst wird versucht, den fehlerhaften Knoten neu zu starten, und dann ein Failover ausgeführt, falls die Neustarts nicht erfolgreich sind. Die Neustart- und Failovereinstellungen werden im Failovercluster-Manager-Snap-In konfiguriert. Weitere Informationen zu diesen Einstellungen finden Sie unter [\<Eigenschaften von <Ressource>: Richtlinien (Registerkarte)](http://technet.microsoft.com/library/cc725685.aspx).  
  
 Informationen zum Verwalten der Quorumintegrität finden Sie unter [WSFC-Quorummodi und Abstimmungskonfiguration &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
