---
title: "Flexible Failoverrichtlinie f&#252;r automatisches Failover einer Verf&#252;gbarkeitsgruppe (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verfügbarkeitsgruppen [SQL Server], flexible Failoverrichtlinie"
  - "Verfügbarkeitsgruppen [SQL Server], Failover"
  - "flexible Failoverrichtlinie"
  - "Failover [SQL Server], AlwaysOn-Verfügbarkeitsgruppen"
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
caps.latest.revision: 29
ms.author: "mikeray"
manager: "jhubbard"
---
# Flexible Failoverrichtlinie f&#252;r automatisches Failover einer Verf&#252;gbarkeitsgruppe (SQL Server)
  Eine flexible Failoverrichtlinie ermöglicht eine präzise Kontrolle über die Bedingungen, die ein [automatisches Failover](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) für eine Verfügbarkeitsgruppe verursachen. Durch eine Änderung der Fehlerbedingungen, die ein automatisches Failover und die Häufigkeit von Integritätsprüfungen auslösen, können Sie die Wahrscheinlichkeit für ein automatisches Failover erhöhen oder verringern, um das SLA für hohe Verfügbarkeit zu unterstützen.  
  
 Die flexible Failoverrichtlinie für eine Verfügbarkeitsgruppe wird durch die Fehlerbedingungsebene und einen Schwellenwert für das Integritätsprüfungstimeout definiert. Sobald erkannt wird, dass eine Verfügbarkeitsgruppe ihre Fehlerbedingungsebene oder ihren Schwellenwert für das Integritätsprüfungstimeout überschritten hat, meldet die Ressourcen-DLL der Verfügbarkeitsgruppe dies dem WSFC-Cluster (Windows Server Failover Clustering). Der WSFC-Cluster initiiert dann ein automatisches Failover zum sekundären Replikat.  
  
> [!IMPORTANT]  
>  Wenn eine Verfügbarkeitsgruppe den Schwellenwert für WSFC-Fehler überschreitet, versucht der WSFC-Cluster nicht, ein automatisches Failover für die Verfügbarkeitsgruppe auszuführen. Außerdem verbleibt die WSFC-Ressourcengruppe der Verfügbarkeitsgruppe so lange in einem fehlerhaften Zustand, bis der Clusteradministrator die fehlerhafte Gruppe manuell online schaltet oder bis der Datenbankadministrator ein manuelles Failover der Verfügbarkeitsgruppe ausführt. Der *WSFC-Fehlerschwellenwert* ist als maximale Anzahl von Fehlern definiert, die während eines bestimmten Zeitraums für die Verfügbarkeitsgruppe unterstützt werden. Der Standardzeitraum beträgt sechs Stunden, und der Standardwert für die maximale Anzahl von Fehlern während dieses Zeitraums entspricht *n*-1, wobei *n* für die Anzahl der WSFC-Knoten steht. Um den Fehlerschwellenwert für eine angegebene Verfügbarkeitsgruppe zu ändern, verwenden Sie die WSFC Failover Manager Console.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Schwellenwert für das Integritätsprüfungstimeout](#HCtimeout)  
  
-   [Fehlerbedingungsebene](#FClevel)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
-   [Verwandte Inhalte](#RelatedContent)  
  
##  <a name="HCtimeout"></a> Schwellenwert für das Integritätsprüfungstimeout  
 Die WSFC-Ressourcen-DLL der Verfügbarkeitsgruppe führt eine *Integritätsprüfung* am primären Replikat aus, indem sie die gespeicherte Prozedur [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) auf der SQL Server-Instanz aufruft, die das primäre Replikat hostet. **sp_server_diagnostics** gibt Ergebnisse in einem Intervall zurück, das 1/3 des Schwellenwerts für das Integritätsprüfungstimeout für die Verfügbarkeitsgruppe entspricht. Der Standardschwellenwert für das Integritätsprüfungstimeout ist 30 Sekunden, und dies bedeutet, dass **sp_server_diagnostics** in einem Intervall von 10 Sekunden Ergebnisse zurückgibt. Wenn **sp_server_diagnostics** langsam ist oder keine Informationen zurückgibt, wartet die Ressourcen-DLL das gesamte Intervall des durch den Schwellenwert definierten Integritätsprüfungstimeouts ab, bevor festgestellt wird, dass das primäre Replikat nicht reagiert. Wenn das primäre Replikat nicht reagiert, wird ein automatisches Failover initiiert, sofern dies aktuell unterstützt wird.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** führt keine Integritätsprüfungen auf Datenbankebene aus.  
  
##  <a name="FClevel"></a> Fehlerbedingungsebene  
 Ob die Diagnosedaten und Zustandsinformationen, die von **sp_server_diagnostics** zurückgegeben wurden, ein automatisches Failover garantieren, hängt von der Fehlerbedingungsebene der Verfügbarkeitsgruppe ab. Die *Fehlerbedingungsebene* gibt an, welche Fehlerbedingungen ein automatisches Failover auslösen. Es gibt fünf Fehlerbedingungsebenen, die von der Ebene mit den wenigsten Einschränkungen (Ebene 1) bis zur Ebene mit den meisten Einschränkungen (Ebene 5) reichen. Jede Bedingungsebene umfasst stets auch die weniger restriktiven Ebenen. Daher schließt die strengste Ebene 5 die vier Bedingungsebenen mit weniger Einschränkungen ein usw.  
  
> [!IMPORTANT]  
>  Beschädigte und fehlerverdächtige Datenbanken werden von keiner Fehlerbedingungsebene erkannt. Deshalb werden automatische Failover niemals von Datenbanken ausgelöst, die beschädigt oder fehlerverdächtig sind (entweder aufgrund von Hardwarefehlern, Datenkorruption oder anderen Fehlern).  
  
 In der folgenden Tabelle werden die Fehlerbedingungen beschrieben, die der jeweiligen Ebene entspricht.  
  
|Ebene|Fehlerbedingung|[!INCLUDE[tsql](../../../includes/tsql-md.md)] Wert|PowerShell-Wert|  
|-----------|-----------------------|------------------------------|----------------------|  
|1 (eins)|der Server ausfällt. Gibt an, dass ein automatisches Failover in den folgenden Fällen initiiert wird:<br /><br /> Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Dienst ist ausgefallen.<br /><br /> Das Leasing der Verfügbarkeitsgruppe für die Verbindung mit dem WSFC-Cluster läuft ab, da keine ACK-Meldung von der Serverinstanz empfangen wird. Weitere Informationen finden Sie unter [How It Works: SQL Server AlwaysOn Lease Timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> <br /><br /> Dies ist die am wenigsten restriktive Ebene.|1|**OnServerDown**|  
|2 (zwei)|der Server nicht reagiert. Gibt an, dass ein automatisches Failover in den folgenden Fällen initiiert wird:<br /><br /> Die Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt keine Verbindung mit dem Cluster her, und der vom Benutzer angegebene Schwellenwert für das Integritätsprüfungstimeout der Verfügbarkeitsgruppe wurde überschritten.<br /><br /> Das Verfügbarkeitsreplikat weist einen fehlerhaften Status auf.|2|**OnServerUnresponsive**|  
|3 (drei)|ein kritischer Serverfehler auftritt. Gibt an, dass ein automatisches Failover bei kritischen internen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlern initiiert wird, z. B. verwaisten Spinlocks, ernsten Schreibzugriffsverletzungen oder zu vielen Sicherungen.<br /><br /> Dies ist der Standardebene.|3|**OnCriticalServerError**|  
|4 (vier)|ein mittelschwerer Serverfehler auftritt. Gibt an, dass ein automatisches Failover bei mittelschweren internen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Fehlern initiiert wird, z. B. bei dauerhaft unzureichendem Arbeitsspeicher im internen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Ressourcenpool.|4|**OnModerateServerError**|  
|5 (fünf)|eine qualifizierte Fehlerbedingung auftritt. Gibt an, dass ein automatisches Failover bei sämtlichen qualifizierten Fehlerbedingungen initiiert wird, einschließlich:<br /><br /> Erschöpfung der SQL Engine-Arbeitsthreads.<br /><br /> Erkennung eines unlösbaren Deadlocks.<br /><br /> <br /><br /> Dies ist die restriktivste Ebene.|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  Das Fehlen einer Reaktion auf Clientanforderungen durch eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz ist für Verfügbarkeitsgruppen nicht relevant.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So konfigurieren Sie ein automatisches Failover**  
  
-   [Ändern des Verfügbarkeitsmodus eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md) (automatisches Failover erfordert den Verfügbarkeitsmodus für synchrone Commits)  
  
-   [Ändern des Failovermodus eines Verfügbarkeitsreplikats &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Konfigurieren der flexiblen Failoverrichtlinie zum Steuern der Bedingungen für ein automatisches Failover &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/configure flexible automatic failover policy.md)  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Funktionsweise: SQL Server AlwaysOn-Leasetimeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)  
  
## Siehe auch  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verfügbarkeitsmodi &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover und Failovermodi &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Windows Server-Failoverclustering &#40;WSFC&#41; mit SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Failoverrichtlinie für Failoverclusterinstanzen](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  