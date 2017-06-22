---
title: SQL Server-Agent|Microsoft-Dokumente
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
ms.assetid: 8d1dc600-aabb-416f-b3af-fbc9fccfd0ec
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0c9be76ca64a4df24cca399308244c5bc4c28e0d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-agent"></a>SQL Server-Agent
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ist eAufträge Microsoft WAufträgedows-Dienst, der geplante admAufträgeistrative Tasks Aufträge *ausführt, die als* Aufträge [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)].  
  
**In diesem Thema**  
  
-   [Vorteile des SQL Server-Agents](#Benefits)  
  
-   [Komponenten des SQL Server-Agents](#Components)  
  
-   [Sicherheit für die Administration mit dem SQL Server-Agent](#Security)  
  
## <a name="Benefits"></a>Vorteile des SQL Server-Agents  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , um Auftragsinformationen zu speichern. Aufträge enthalten einen oder mehrere Auftragsschritte. Jeder Schritt enthält einen eigenen Task, z. B. das Sichern einer Datenbank.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent kann einen Auftrag anhand eines Zeitplans, als Reaktion auf ein bestimmtes Ereignis oder bei Bedarf ausführen. Wenn Sie z. B. am Ende jedes Arbeitstages alle Server des Unternehmens sichern möchten, können Sie diesen Task automatisieren. Planen Sie die Sicherung so, dass sie montags bis freitags nach 22:00 Uhr ausgeführt wird. Falls bei der Sicherung ein Problem auftritt, kann der SQL Server-Agent das Ereignis aufzeichnen und Sie benachrichtigen.  
  
> [!NOTE]  
> Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst ist standardmäßig deaktiviert, wenn [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] installiert ist, es sei denn, der Benutzer legt explizit fest, dass der Dienst automatisch gestartet werden soll.  
  
## <a name="Components"></a>Komponenten des SQL Server-Agents  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwendet die folgenden Komponenten, um die auszuführenden Aufgaben, den Zeitpunkt der Ausführung und die Meldung erfolgreicher bzw. fehlgeschlagener Aufgaben zu definieren.  
  
### <a name="jobs"></a>ausführt, die als  
Ein *Auftrag* umfasst eine angegebene Reihe von Aktionen, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ausführt. Durch die Verwendung von Aufträgen können Sie eine Verwaltungsaufgabe so definieren, dass diese ein- oder mehrmals ausgeführt und der erfolgreiche oder fehlgeschlagene Abschluss der Ausführung überwacht werden kann. Aufträge können auf einem lokalen oder mehreren Remoteservern ausgeführt werden.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agentaufträge, die zu der Zeit eines Failoverereignisses auf einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Failoverclusterinstanz ausgeführt werden, werden nach dem Failover nicht zu einem anderen Failoverclusterknoten fortgesetzt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agentaufträge, die ausgeführt werden, wenn ein Hyper-V-Knoten angehalten wird, werden nicht fortgesetzt, wenn die Pause ein Failover zu einem anderen Knoten verursacht. Aufträge, die begonnen, aber wegen eines Failoverereignisses nicht abgeschlossen werden, werden als gestartet protokolliert, zeigen jedoch keine weiteren Protokolleinträge für Abschluss oder Fehler an. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agentaufträge in diesen Szenarien wurden scheinbar nie beendet.  
  
Für die Ausführung von Aufträgen gibt es mehrere Möglichkeiten:  
  
-   Ausführung gemäß einem Zeitplan oder mehreren Zeitplänen.  
  
-   Ausführung als Reaktion auf eine oder mehrere Warnungen.  
  
-   Ausführung im Rahmen der gespeicherten Prozedur sp_start_job.  
  
Die einzelnen Aktionen im Rahmen eines Auftrags werden als *Auftragsschritte*bezeichnet. Ein Auftragsschritt kann beispielsweise in der Ausführung einer [!INCLUDE[tsql](../../includes/tsql_md.md)] -Anweisung, der Ausführung eines [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Pakets oder der Ausgabe eines Befehls an einen Analysis Services-Server bestehen. Auftragsschritte werden als Teil des Auftrags verwaltet.  
  
Jeder Auftragsschritt wird in einem bestimmten Sicherheitskontext ausgeführt. Bei Auftragsschritten, die [!INCLUDE[tsql](../../includes/tsql_md.md)]verwenden, nutzen Sie zum Festlegen des Sicherheitskontexts für den Auftragsschritt die EXECUTE AS-Anweisung. Bei anderen Arten von Auftragsschritten verwenden Sie ein Proxykonto, um den Sicherheitskontext für den Auftragsschritt festzulegen.  
  
### <a name="schedules"></a>Zeitpläne  
Durch einen *Zeitplan* wird angegeben, wann ein Auftrag ausgeführt wird. Im Rahmen eines Zeitplans können auch mehrere Aufträge ausgeführt werden, und für einen Auftrag können mehrere Zeitpläne gelten. Ein Zeitplan kann bezüglich des Ausführungszeitpunktes für einen Auftrag folgende Bedingungen definieren:  
  
-   Ausführung sobald der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent startet.  
  
-   Ausführung, wenn sich die CPU-Auslastung des Computers in einem Bereich befindet, den Sie als Leerlauf definiert haben.  
  
-   Einmalige Ausführung zu einem angegebenen Zeitpunkt und Datum.  
  
-   Ausführung auf wiederkehrender Basis.  
  
Weitere Informationen finden Sie unter [Anlegen und Zuweisen von Zeitplänen zu Aufträgen](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### <a name="alerts"></a>Warnungen  
Eine *Warnung* ist eine automatische Reaktion auf ein bestimmtes Ereignis. Bei einem Ereignis kann es sich z. B. um das Starten eines Auftrags oder um das Erreichen eines bestimmten Schwellenwertes im Hinblick auf die Systemressourcen handeln. Sie definieren die Bedingungen, unter denen eine Warnung auftritt.  
  
Eine Warnung kann als Reaktion auf eine der folgenden Bedingungen ausgegeben werden:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Ereignisse  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Leistungsbedingungen  
  
-   Ereignisse in der Microsoft Windows-Verwaltungsinstrumentation (WMI) auf dem Computer, auf dem der SQL Server-Agent ausgeführt wird.  
  
Eine Warnung kann die folgenden Aktionen ausführen:  
  
-   Benachrichtigen eines oder mehrerer Operatoren.  
  
-   Ausführen eines Auftrags.  
  
Weitere Informationen finden Sie unter [Warnungen](../../ssms/agent/alerts.md).  
  
### <a name="operators"></a>Operatoren  
Ein *Operator* definiert die Kontaktinformationen einer Person, die für die Verwaltung einer oder mehrerer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Instanzen zuständig ist. In einigen Unternehmen werden die Aufgaben eines Operators einer einzelnen Person zugewiesen. In größeren Unternehmen mit mehreren Servern teilen sich mehrere Personen die Aufgaben des Operators. Der Operator enthält keine Sicherheitsinformationen und definiert auch nicht den Sicherheitsprinzipal.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] kann Operatoren bei Warnungen folgendermaßen benachrichtigen:  
  
-   E-Mail  
  
-   Pager (per E-Mail)  
  
-   **net send**  
  
> [!NOTE]  
> Um Benachrichtigungen mit **NET SEND**zu senden, muss der Windows Messenger-Dienst auf dem Computer mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent gestartet sein.  
  
> [!IMPORTANT]  
> Die Pager- und **NET SEND** -Optionen werden in zukünftigen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nicht mehr im [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent vorhanden sein. Vermeiden Sie die Verwendung dieser Funktionen bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, die diese Funktionen zurzeit verwenden.  
  
Um Operatoren Benachrichtigungen per E-Mail oder Pager zu senden, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent so konfigurieren, dass Datenbank-E-Mail verwendet wird. Weitere Informationen finden Sie unter [Database Mail](http://msdn.microsoft.com/en-us/9e4563dd-4799-4b32-a78a-048ea44a44c1).  
  
Ein Operator kann auch als Alias für eine Gruppe von Personen definiert werden. Auf diese Weise werden alle Mitglieder dieses Alias zur selben Zeit benachrichtigt. Weitere Informationen finden Sie unter [Operatoren](../../ssms/agent/operators.md).  
  
## <a name="Security"></a>Sicherheit für die Administration mit dem SQL Server-Agent  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwendet die festen Datenbankrollen **SQLAgentUserRole**, **SQLAgentReaderRole**und **SQLAgentOperatorRole** in der **msdb** -Datenbank, um den Zugriff auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent für Benutzer zu steuern, die keine Mitglieder der festen Serverrolle **sysadmin** sind. Neben diesen festen Datenbankrollen können Datenbankadministratoren mithilfe von Subsystemen und Proxys sicherstellen, dass jeder Auftragsschritt mit den mindestens erforderlichen Berechtigungen ausgeführt wird.  
  
### <a name="roles"></a>Rollen  
Mitglieder der festen Datenbankrollen **SQLAgentUserRole**, **SQLAgentReaderRole**und **SQLAgentOperatorRole** in **msdb**und Mitglieder der festen Serverrolle **sysadmin** haben Zugriff auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent. Ein Benutzer, der keiner dieser Rollen angehört, kann den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent nicht verwenden. Weitere Informationen zu den Rollen, die vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwendet werden, finden Sie unter [Implementieren der SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md).  
  
### <a name="subsystems"></a>Subsysteme  
Ein Subsystem ist ein vordefiniertes Objekt, das die für einen Auftragsschritt verfügbare Funktionalität darstellt. Jeder Proxy hat Zugriff auf mindestens ein Subsystem. Subsysteme bieten Sicherheit, weil sie den Zugriff auf die für ein Proxykonto verfügbare Funktionalität begrenzen. Jeder Auftragsschritt wird im Kontext eines Proxys ausgeführt, mit Ausnahme von [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritten. [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritten wird der Sicherheitskontext mithilfe des EXECUTE AS-Befehls festgelegt.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definiert die in der folgenden Tabelle aufgeführten Subsysteme:  
  
|Name des Subsystems|Description|  
|--------------|-----------|  
|Microsoft ActiveX-Skript|Ausführen eines ActiveX-Skript-Auftragsschritts.<br /><br />**Warning** Das ActiveX Scripting-Subsystem wird in einer zukünftigen Version von [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent entfernt. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird.|  
|Betriebssystem (**CmdExec**)|Ausführen eines ausführbaren Programms.|  
|PowerShell|Ausführen eines PowerShell-Skripterstellungs-Auftragsschritts.|  
|Replikationsverteiler|Ausführen eines Auftragsschritts, der den Replikationsverteilungs-Agent aktiviert.|  
|Replikationsmerge|Ausführen eines Auftragsschritts, der den Replikationsmerge-Agent aktiviert.|  
|Replikation-Warteschlangenleser|Ausführen eines Auftragsschritts, der den Warteschlangenlese-Agent der Microsoft SQL Server-Replikation aktiviert.|  
|Replikationsmomentaufnahme|Ausführen eines Auftragsschritts, der den Replikationsmomentaufnahme-Agent aktiviert.|  
|Replikationstransaktionsprotokoll-Leser|Ausführen eines Auftragsschritts, der den Protokolllese-Agent aktiviert.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] -Befehl|Ausführen eines [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] -Befehls.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] -Abfrage|Ausführen einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] -Abfrage.|  
|[!INCLUDE[ssIS](../../includes/ssis_md.md)] -Paketausführung|Ausführen eines [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Pakets.|  
  
> [!NOTE]  
> Da [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritte keine Proxys verwenden, gibt es kein Subsystem des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents für [!INCLUDE[tsql](../../includes/tsql_md.md)] -Auftragsschritte.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent erzwingt Subsystemeinschränkungen, selbst wenn der Sicherheitsprinzipal für den Proxy normalerweise die Berechtigung zum Ausführen des Tasks im Auftragsschritt hätte. Beispielsweise kann ein Proxykonto für einen Benutzer, der Mitglied der festen Serverrolle „sysadmin“ ist, nur einen [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Auftragsschritt ausführen, wenn das Proxykonto Zugriff auf das [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Subsystem hat. Der Benutzer kann jedoch [!INCLUDE[ssIS](../../includes/ssis_md.md)] -Pakete ausführen.  
  
### <a name="proxies"></a>Proxys  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent verwendet Proxys zum Verwalten von Sicherheitskontexten. Ein Proxy kann für mehrere Auftragsschritte verwendet werden. Mitglieder der festen Serverrolle **sysadmin** können Proxys erstellen.  
  
Jeder Proxy entspricht Sicherheitsanmeldeinformationen. Jeder Proxy kann einer Gruppe von Subsystemen und Anmeldenamen zugeordnet werden. Der Proxy kann nur für Auftragsschritte benutzt werden, die ein dem Proxy zugeordnetes Subsystem verwenden. Um einen Auftragsschritt zu erstellen, der einen bestimmten Proxy verwendet, muss der Auftragsbesitzer einen Anmeldenamen verwenden, der diesem Proxy zugeordnet ist, oder er muss ein Mitglied einer Rolle mit unbeschränktem Zugriff auf Proxys sein. Mitglieder der festen Serverrolle **sysadmin** haben unbeschränkten Zugriff auf Proxys. Mitglieder von **SQLAgentUserRole**, **SQLAgentReaderRole**oder **SQLAgentOperatorRole** können nur Proxys verwenden, für die Ihnen der Zugriff erteilt wurde. Jedem Benutzer, der Mitglied einer dieser festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agents ist, muss Zugriff auf bestimmte Proxys gewährt werden, damit er Auftragsschritte erstellen kann, bei denen diese Proxys verwendet werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
Konfigurieren Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent anhand der folgenden Schritte zur Automatisierung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Verwaltung:  
  
1.  Überprüfen Sie, welche administrativen Tasks oder Serverereignisse regelmäßig auftreten und ob diese Tasks oder Ereignisse programmgesteuert verwaltet werden können. Ein Task eignet sich für die Automatisierung, wenn er eine festgelegte Reihenfolge von Schritten umfasst und zu einem bestimmten Zeitpunkt oder als Reaktion auf ein bestimmtes Ereignis auftritt.  
  
2.  Definieren Sie die Aufträge, Zeitpläne, Warnungen und Operatoren mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] -Skripts oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Management Objects (SMO). Weitere Informationen finden Sie unter [Erstellen von Aufträgen](../../ssms/agent/create-jobs.md).  
  
3.  Führen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge aus, die Sie definiert haben.  
  
> [!NOTE]  
> Für die Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]erhält der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Dienst den Namen SQLSERVERAGENT. Für benannte Instanzen erhält der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst den Namen SQLAgent$*instancename*.  
  
Falls Sie mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ausführen, können Sie Tasks, die auf allen Instanzen ausgeführt werden müssen, mithilfe der Multiserververwaltung automatisieren. Weitere Informationen finden Sie unter [Automatisierte Verwaltung in einem Unternehmen](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
Verwenden Sie für die ersten Schritte mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent die folgenden Aufgaben:  
  
|Description|Thema|  
|-----------|-----|  
|Beschreibt, wie SQL Server-Agent konfiguriert wird.|[Konfigurieren des SQL Server-Agents](../../ssms/agent/configure-sql-server-agent.md)|  
|Beschreibt, wie der SQL Server-Agent-Dienst gestartet, beendet und angehalten wird.|[Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)|  
|Beschreibt Überlegungen zum Angeben eines Kontos für den SQL Server-Agent-Dienst.|[Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)|  
|Beschreibt, wie das SQL Server-Agent-Fehlerprotokoll verwendet wird.|[SQL Server-Agent-Fehlerprotokoll](../../ssms/agent/sql-server-agent-error-log.md)|  
|Beschreibt, wie Leistungsobjekte verwendet werden.|[Verwenden von Leistungsobjekten](../../ssms/agent/use-performance-objects.md)|  
|Beschreibt den Wartungsplanungs-Assistenten, ein Hilfsprogramm, mit dem Sie Aufträge, Warnungen und Operatoren erstellen können, um die Verwaltung einer Instanz von SQL Server zu automatisieren.|[Verwenden des Wartungsplanungs-Assistenten](http://msdn.microsoft.com/en-us/db65c726-9892-480c-873b-3af29afcee44)|  
|Beschreibt, wie administrative Aufgaben mit dem SQL Server-Agent automatisiert werden.|[Automatisierte Administrationstasks &amp;#40;SQL Server Agent&amp;#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)|  
  
## <a name="see-also"></a>Siehe auch  
[Oberflächenkonfiguration](http://msdn.microsoft.com/en-us/f741169c-1453-4ad2-830b-bf2be27d712f)  
  

