---
title: Verwenden des Verfügbarkeitsgruppen-Dashboards von Always On (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/30/2017
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
- sql13.swb.agdashboard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
- Availability Groups [SQL Server], dashboard
ms.assetid: c9ba2589-139e-42bc-99e1-94546717c64d
caps.latest.revision: 30
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4645d6deeb80cc8c7bceeff685598cdfcff3841f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-the-always-on-availability-group-dashboard-sql-server-management-studio"></a>Verwenden des Verfügbarkeitsgruppen-Dashboards von Always On (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Datenbankadministratoren verwenden das Verfügbarkeitsgruppen-Dashboard von Always On, um die Integrität einer Verfügbarkeitsgruppe und deren Verfügbarkeitsreplikate und -datenbanken in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] in einer übersichtlichen Ansicht darzustellen. Einige der typischen Verwendungen für das Verfügbarkeitsgruppen-Dashboard von Always On sind:  
  
-   Auswählen eines Replikats für ein manuelles Failover.  
  
-   Abschätzen von Datenverlust beim Erzwingen eines Failovers.  
  
-   Auswerten der Datensynchronisierungsleistung.  
  
-   Auswerten der Auswirkungen auf die Leistung eines sekundären Replikats mit synchronem Commit  
  
 Das Dashboard bietet wichtige Statusangaben und Leistungsindikatoren zu Verfügbarkeitsgruppen, die Ihnen Entscheidungen zu Vorgängen mit hoher Verfügbarkeit anhand folgender Informationen ermöglichen.  
  
-   Replikat-Rollupstatus  
  
-   Synchronisierungsmodus und -status  
  
-   Geschätzter Datenverlust  
  
-   Geschätzte Wiederherstellungszeit (Aufholen wiederholen)  
  
-   Datenbankreplikatdetails  
  
-   Synchronisierungsmodus und -status  
  
-   Zeit zum Wiederherstellen des Protokolls  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Sie müssen mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Serverinstanz) verbunden sein, die entweder das primäre Verfügbarkeitsreplikat oder ein sekundäres Replikat einer Verfügbarkeitsgruppe hostet.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert CONNECT-, VIEW SERVER STATE- und VIEW ANY DEFINITION-Berechtigungen.  
  
##  <a name="SSMSProcedure"></a> So starten Sie das Always On-Dashboard  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] her, auf der das Always On-Dashboard ausgeführt werden soll.  
  
2.  Erweitern Sie den Knoten **Hohe Verfügbarkeit (immer aktiviert)** , klicken Sie mit der rechten Maustaste auf den Knoten **Verfügbarkeitsgruppen** , und klicken Sie dann auf **Dashboard anzeigen**.  
  
###  <a name="DashboardOptions"></a> So ändern Sie Always On-Dashboard-Optionen  
 Sie können das [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]-Dialogfeld **Optionen** verwenden, um das Verhalten des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Always On-Dashboards für das automatische Aktualisieren und Aktivieren einer automatisch definierten Always On-Richtlinie zu konfigurieren.  
  
1.  Klicken Sie im Menü **Extras** auf **Optionen**.  
  
2.  Um das Dashboard automatisch zu aktualisieren, wählen Sie im Dialogfeld **Optionen** den Befehl **Automatische Aktualisierung aktivieren**aus, geben Sie das Aktualisierungsintervall in Sekunden ein, und geben Sie dann die Häufigkeit ein, mit der der Verbindungsversuch wiederholt werden soll.  
  
3.  Zum Aktivieren einer benutzerdefinierten Richtlinie wählen Sie **Benutzerdefinierte Always On-Richtlinie aktivieren**aus.  
  
##  <a name="AvGroupsView"></a> Zusammenfassung zu Verfügbarkeitsgruppen  
 Im Verfügbarkeitsgruppen-Bildschirm wird eine Zusammenfassungszeile für jede Verfügbarkeitsgruppe angezeigt, für die die verbundene Serverinstanz ein Replikat hostet. In diesem Bereich werden die folgenden Spalten angezeigt.  
  
 **Name der Verfügbarkeitsgruppe**  
 Der Name einer Verfügbarkeitsgruppe, für die die verbundene Serverinstanz ein Replikat hostet.  
  
 **Primäre Instanz**  
 Der Name der Serverinstanz, die das primäre Replikat der Verfügbarkeitsgruppe hostet.  
  
 **Failovermodus**  
 Zeigt den Failovermodus an, für den das Replikat konfiguriert ist. Die folgenden Werte für den Failovermodus sind möglich:  
  
-   **Automatisch**. Gibt an, dass ein oder mehrere Replikate im automatischen Failovermodus sind.  
  
-   **Manuell**. Gibt an, dass kein Replikat im automatischen Failovermodus ist.  
  
 **Probleme**  
 Klicken Sie auf den Link **Probleme** , um die Problembehandlungsdokumentation für ein angegebenes Problem zu öffnen. Eine Liste aller Always On-Richtlinienprobleme finden sie unter [Always On-Richtlinien für Betriebsprobleme mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
> [!TIP]  
>  Klicken Sie auf die Spaltenüberschriften, um die Verfügbarkeitsgruppeninformationen nach dem Namen der Verfügbarkeitsgruppe, primärer Instanz, Failovermodus oder Problem zu sortieren.  
  
##  <a name="AvGroupDetails"></a> Verfügbarkeitsgruppendetails  
 Die folgenden Detailinformationen werden für die Verfügbarkeitsgruppe angezeigt, die Sie im Zusammenfassungsbildschirm auswählen:  
  
 **Status der Verfügbarkeitsgruppe**  
 Zeigt den Zustand für die Verfügbarkeitsgruppe an.  
  
 **Primary instance**  
 Der Name der Serverinstanz, die das primäre Replikat der Verfügbarkeitsgruppe hostet.  
  
 **Failover mode**  
 Zeigt den Failovermodus an, für den das Replikat konfiguriert ist. Die folgenden Werte für den Failovermodus sind möglich:  
  
-   **Automatisch**. Gibt an, dass ein oder mehrere Replikate im automatischen Failovermodus sind.  
  
-   **Manuell**. Gibt an, dass kein Replikat im automatischen Failovermodus ist.  
  
 **Clusterstatus**  
 Name und Zustand des Clusters, auf dem die Instanz des verbundenen Servers und die Verfügbarkeitsgruppe ein Elementknoten ist.  
  
##  <a name="AvReplicaDetails"></a> Verfügbarkeitsreplikatdetails  

Beim Verbinden mit dem primären Replikat **Verfügbarkeitsreplikatdetails** werden Informationen von allen Replikaten in der Verfügbarkeitsgruppe angezeigt. Beim Verbinden mit einem sekundären Replikat werden in der Anzeige nur Informationen vom verbundenen Replikat dargestellt.  

Im Bereich **Verfügbarkeitsreplikat** werden die folgenden Spalten angezeigt:  
  
 **Name**  
 Der Namen der Serverinstanz, die das Verfügbarkeitsreplikat hostet. Diese Spalte wird standardmäßig angezeigt.  
  
 **Rolle**  
 Gibt die aktuelle Rolle des Verfügbarkeitsreplikats an, entweder **Primär** oder **Sekundär**. Informationen über [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]-Rollen finden Sie unter [Übersicht über Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md). Diese Spalte wird standardmäßig angezeigt.  
  
 **Failovermodus**  
 Zeigt den Failovermodus an, für den das Replikat konfiguriert ist. Die folgenden Werte für den Failovermodus sind möglich:  
  
-   **Automatisch**. Gibt an, dass ein oder mehrere Replikate im automatischen Failovermodus sind.  
  
-   **Manuell**. Gibt an, dass kein Replikat im automatischen Failovermodus ist.  
  
 **Synchronisierungsstatus**  
 Gibt an, ob ein sekundäres Replikat gerade mit dem primärem Replikat synchronisiert wird. Diese Spalte wird standardmäßig angezeigt. Die folgenden Werte sind möglich:  
  
-   **Nicht synchronisiert**. Mindestens eine Datenbank im Replikat ist nicht synchronisiert oder wurde noch nicht mit der Verfügbarkeitsgruppe verknüpft.  
  
-   **Wird synchronisiert**. Mindestens eine Datenbank im Replikat wird synchronisiert.  
  
-   **Synchronisiert**. Alle Datenbanken im sekundären Replikat werden mit den entsprechenden primären Datenbanken auf dem aktuellen primären Replikat (falls vorhanden) oder auf dem letzten primären Replikat synchronisiert.  
  
    > [!NOTE]  
    >  Im Leistungsmodus befindet sich die Datenbank nie im Status "Synchronisiert".  
  
-   **NULL**. Unbekannter Status. Dieser Wert tritt auf, wenn die lokale Serverinstanz nicht mit dem WSFC-Failovercluster kommunizieren kann (d. h., der lokale Knoten ist nicht Teil des WSFC-Quorums).  
  
 **Probleme**  
 Listet den Namen des Problems auf. Dieser Wert wird standardmäßig angezeigt. Eine Liste aller Always On-Richtlinienprobleme finden sie unter [Always On-Richtlinien für Betriebsprobleme mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
 **Verfügbarkeitsmodus**  
 Gibt die Replikateigenschaft an, die Sie für jedes Verfügbarkeitsreplikat einzeln festgelegt haben. Dieser Wert wird standardmäßig ausgeblendet. Die folgenden Werte sind möglich:  
  
-   **Asynchron**. Das sekundäre Replikat wird nie mit dem primären Replikat synchronisiert.  
  
-   **Synchronous**. Beim Aufholen zur primären Datenbank geht eine sekundäre Datenbank in diesen Status über und bleibt aufgeholt, solange die Datensynchronisierung für die Datenbank ausgeführt wird.  
  
 **Primärer Verbindungsmodus**  
 Gibt den Modus an, der zum Herstellen einer Verbindung mit dem primären Replikat verwendet wird.  Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Sekundärer Verbindungsmodus**  
 Gibt den Modus an, der zum Herstellen einer Verbindung mit dem sekundären Replikat verwendet wird.  Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Verbindungsstatus**  
 Gibt an, ob ein sekundäres Replikat derzeit mit dem primären Replikat verbunden ist. Diese Spalte wird standardmäßig ausgeblendet. Die folgenden Werte sind möglich:  
  
-   **Getrennt**. Gibt bei einem Remoteverfügbarkeitsreplikat an, dass es vom lokalen Verfügbarkeitsreplikat getrennt ist. Die Antwort des lokalen Replikats auf den Status "Getrennt" hängt wie folgt von dessen Rolle ab:  
  
    -   Wenn auf dem primären Replikat ein sekundäres Replikat getrennt ist, werden die sekundären Datenbanken auf dem primären Replikat als **Nicht synchronisiert** gekennzeichnet, und das primäre Replikat wartet, bis das sekundäre Replikat wieder verbunden ist.  
  
    -   Wird erkannt, dass das sekundäre Replikat getrennt ist, wird versucht, die Verbindung des sekundären Replikats mit dem primären Replikat wiederherzustellen.  
  
-   **Verbunden**. Ein Remoteverfügbarkeitsreplikat, das derzeit mit dem lokalen Replikat verbunden ist.  
  
 **Betriebszustand**  
 Gibt den aktuellen Betriebszustand des sekundären Replikats an. Dieser Wert wird standardmäßig ausgeblendet. Die folgenden Werte sind möglich:  
  
 **0**. Ausstehendes Failover  
  
 **1**. Ausstehend  
  
 **2**. Online  
  
 **3**. Offline  
  
 **4**. Fehler  
  
 **5**. Fehler, kein Quorum  
  
 **NULL**. Das Replikat ist nicht lokal  
  
 **Nummer des letzten Verbindungsfehlers**  
 Die Nummer des letzten Verbindungsfehlers.  Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Beschreibung des letzten Verbindungsfehlers**  
 Die Beschreibung des letzten Verbindungsfehlers.  Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Timestamp des letzten Verbindungsfehlers**  
 Der Timestamp des letzten Verbindungsfehlers. Dieser Wert wird standardmäßig ausgeblendet.  
  
> [!NOTE]  
>  Informationen zu Leistungsindikatoren für Verfügbarkeitsreplikate finden Sie unter [SQL Server, Verfügbarkeitsreplikat](../../../relational-databases/performance-monitor/sql-server-availability-replica.md).  
  
##  <a name="AvDbDetails"></a> So gruppieren Sie Verfügbarkeitsgruppeninformationen  
 Klicken Sie zum Gruppieren der Informationen auf **Gruppieren nach**, und wählen Sie eine der folgenden Möglichkeiten aus:  
  
-   **Verfügbarkeitsreplikate**  
  
-   **Verfügbarkeitsdatenbanken**  
  
-   **Synchronization state**  
  
-   **Failoverbereitschaft**  
  
-   **Probleme**  
  
 Im Bereich, der die gruppierten Informationen anzeigt, werden die folgenden Spalten angezeigt:  
  
 **Name**  
 Der Name der Verfügbarkeitsdatenbank. Dieser Wert wird standardmäßig angezeigt.  
  
 **Replikat**  
 Der Name der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die das Verfügbarkeitsreplikat hostet. Dieser Wert wird standardmäßig angezeigt.  
  
 **Synchronisierungsstatus**  
 Gibt an, ob die Verfügbarkeitsdatenbank gerade mit dem primärem Replikat synchronisiert wird. Dieser Wert wird standardmäßig angezeigt. Folgende Synchronisierungsstatus sind möglich:  
  
-   **Synchronisierung wird nicht ausgeführt**.  
  
    -   Gibt bei der primären Rolle an, dass die Datenbank nicht bereit ist, das Transaktionsprotokoll mit den entsprechenden sekundären Datenbanken zu synchronisieren.  
  
    -   Gibt bei einer sekundären Datenbank an, dass die Protokollsynchronisierung für die Datenbank aufgrund eines Verbindungsproblems nicht gestartet wurde oder beim Start oder einem Rollenwechsel verschiedene Übergangsstatuswerte durchläuft.  
  
-   **Wird synchronisiert**.  
  
     Auf einem primären Replikat:  
  
    -   Gibt bei einer primären Datenbank an, dass diese Datenbank bereit ist, eine Scananforderung von einer sekundären Datenbank zu akzeptieren.  
  
    -   Gibt auf einem sekundären Replikat an, dass derzeit eine aktive Datenverschiebung für diese sekundäre Datenbank stattfindet.  
  
     Gibt auf einem sekundären Replikat an, dass derzeit eine aktive Datenverschiebung für dieses Replikat stattfindet.  
  
-   **Synchronisiert**.  
  
     Gibt bei einer primären Datenbank an, dass mindestens eine sekundäre Datenbank synchronisiert ist.  
  
     Gibt bei einer sekundären Datenbank an, dass die Datenbank mit der entsprechenden primären Datenbank synchronisiert ist.  
  
-   **Wiederherstellen**.  
  
     Gibt die Rollbackphase an, wenn eine sekundäre Datenbank aktiv Seiten von der primären Datenbank abruft.  
  
    > [!CAUTION]  
    >  Wenn eine Datenbank sich im Status REVERTING befindet, kann die Datenbank sich nach einem erzwungenen Failover zum sekundären Replikat in einem Status befinden, in dem sie nicht gestartet werden kann.  
  
-   **Wird initialisiert**.  
  
     Gibt die Rollbackphase an, wenn das Transaktionsprotokoll (erforderlich, um eine sekundäre Datenbank auf den gleichen Stand wie die Rückgängig-LSN zu bringen) übermittelt und auf einem sekundären Replikat festgeschrieben wird.  
  
    > [!CAUTION]  
    >  Wenn eine Datenbank den Status INITIALIZING aufweist, befindet sich die Datenbank nach einem erzwungenen Failover zum sekundären Replikat immer in einem Status, in dem sie nicht gestartet werden kann.  
  
 **Failover Readiness**  
 Gibt an, für welches Verfügbarkeitsreplikat ein Failover mit oder ohne potenziellen Datenverlust ausgeführt werden kann. Diese Spalte wird standardmäßig angezeigt. Die folgenden Werte sind möglich:  
  
-   **Datenverlust**  
  
-   **Kein Datenverlust**  
  
 **Probleme**  
 Listet den Namen des Problems auf. Diese Spalte wird standardmäßig angezeigt. Die folgenden Werte sind möglich:  
  
-   **Warnungen**. Klicken Sie, um die Schwellenwerte und Warnungen anzuzeigen.  
  
-   **Kritisch**. Klicken Sie, um die kritischen Probleme anzuzeigen.  
  
 Eine Liste aller Always On-Richtlinienprobleme finden sie unter [Always On-Richtlinien für Betriebsprobleme mit Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md).  
  
 **Angehalten**  
 Gibt an, ob der Status der Datenbank **Angehalten** oder **Fortgesetzt**lautet. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Ursache für das Anhalten**  
 Gibt die Ursache für den Status "Angehalten" an. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Geschätzter Datenverlust (Sekunden)**  
 Zeigt den Zeitunterschied des letzten Transaktionsprotokolleintrags im primären und sekundären Replikat an. Bei einem Fehler auf dem primären Replikat gehen alle Transaktionsprotokolleinträge innerhalb des Zeitfensters verloren. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Geschätzte Wiederherstellungszeit (Sekunden)**  
 Gibt die Zeit in Sekunden an, die das Wiederholen der Aufholzeit dauert. Die *Aufholzeit* ist die Zeit, die das sekundäre Replikat zum Aufholen des primären Replikats benötigt. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Synchronisierungsleistung (Sekunden)**  
 Gibt die Zeit in Sekunden an, die die Synchronisierung zwischen dem primären und sekundären Replikat dauert. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Größe der Protokoll-Sendewarteschlange (KB)**  
 Gibt die Menge an Protokolldatensätzen in den Protokolldateien der primären Datenbank an, die noch nicht an das sekundäre Replikat gesendet wurden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Protokoll-Senderate (KB/s)**  
 Gibt die Rate in KB pro Sekunde an, mit der Protokolldatensätze an das sekundäre Replikat gesendet werden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Größe der Wiederholungswarteschlange (KB)**  
 Gibt die Menge an Protokolldatensätzen in den Protokolldateien des sekundären Replikats an, die noch nicht wiederhergestellt wurden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Rollforwardrate (KB/s)**  
 Gibt die Rate in KB pro Sekunde an, mit der die Protokolldatensätze wiederhergestellt werden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Dateidatenstrom-Senderate (KB/s)**  
 Gibt die Rate des Dateidatenstroms in KB pro Sekunde an, mit der Transaktionen an das Replikat gesendet werden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Protokollende-LSN**  
 Gibt die tatsächliche Protokollfolgenummer (LSN) an, die dem letzten Protokolldatensatz im Protokollcache auf den primären und sekundären Replikaten entspricht. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Wiederherstellungs-LSN**  
 Gibt bei einem primären Replikat das Ende des Transaktionsprotokolls an, bevor das Replikat nach einer Wiederherstellung oder einem Failover neue Protokolldatensätze schreibt. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Kürzungs-LSN**  
 Gibt den minimalen Protokollkürzungswert für das primäre Replikat an. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **LSN des letzten Commits**  
 Gibt die tatsächliche LSN an, die dem letzten Commitdatensatz im Transaktionsprotokoll entspricht. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Letzte Commitzeit**  
 Gibt die Zeit an, die dem letzten Commitdatensatz entspricht. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **LSN des letzten Sendevorgangs**  
 Gibt den Punkt an, bis zu dem alle Protokollblöcke vom primären Replikat gesendet wurden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Letzte Sendezeit**  
 Gibt die Zeit an, zu der der letzte Protokollblock gesendet wurde. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **LSN des letzten Empfangsvorgangs**  
 Gibt den Punkt an, bis zu dem alle Protokollblöcke vom sekundären Replikat empfangen wurden, das die sekundäre Datenbank hostet. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Letzte Empfangszeit**  
 Gibt die Zeit an, zu der der in der letzten Meldung empfangene Protokollblockbezeichner auf dem sekundären Replikat gelesen wurde. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **LSN der letzten Festschreibung**  
 Gibt den Punkt an, bis zu dem alle Protokolldatensätze auf dem sekundären Replikat auf den Datenträger geleert wurden. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Uhrzeit der letzten Festschreibung**  
 Gibt die Zeit an, zu der der Protokollblockbezeichner für die letzte festgeschriebene LSN auf dem sekundären Replikat empfangen wurde. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **LSN der letzten Wiederholung**  
 Gibt die tatsächliche LSN des Protokolldatensatzes an, der zuletzt auf dem sekundären Replikat wiederholt wurde. Dieser Wert wird standardmäßig ausgeblendet.  
  
 **Letzte Wiederholungszeit**  
 Gibt die Zeit an, zu der der letzte Protokolldatensatz in der sekundären Datenbank wiederhergestellt wurde. Dieser Wert wird standardmäßig ausgeblendet.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Verwenden von Always On-Richtlinien zum Anzeigen des Zustands einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
