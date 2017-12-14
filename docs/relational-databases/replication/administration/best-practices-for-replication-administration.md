---
title: "Bewährte Methoden für die Replikationsverwaltung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administering replication, best practices
- replication [SQL Server], administering
ms.assetid: 850e8a87-b34c-4934-afb5-a1104f118ba8
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2d98762b93d118bb7b8f03839440ca799500defd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="best-practices-for-replication-administration"></a>Bewährte Methoden für die Replikationsverwaltung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Nachdem Sie die Replikation konfiguriert haben, müssen Sie sich mit der Verwaltung einer Replikationstopologie vertraut machen. Dieses Thema enthält grundlegende Hinweise zur Best Pa in verschiedenen Bereichen sowie Links zu weiteren Informationen zu jedem Bereich. Neben den folgenden Hinweisen zu den bewährten Methoden in diesem Thema sollten Sie das Thema mit den häufig gestellten Fragen lesen, um die häufigen Fragen und Probleme kennen zu lernen: [Häufig gestellte Fragen für Replikationsadministratoren](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md).  
  
 Eine Unterteilung der Hinweise zu den bewährten Methoden in zwei Bereiche bietet sich an:  
  
-   Die folgenden Informationen betreffen bewährte Methoden, die bei allen Replikationstopologien implementiert werden sollten:  
  
    -   Entwickeln und Testen einer Sicherungs- und Wiederherstellungsstrategie  
  
    -   Erstellen von Skripts für die Replikationstopologie  
  
    -   Erstellen von Schwellenwerten und Warnungen  
  
    -   Überwachen der Replikationstopologie  
  
    -   Einrichten von Leistungsgrundlagen und gegebenenfalls Optimierung der Replikation  
  
-   Die folgenden Informationen betreffen bewährte Methoden, die in Betracht gezogen werden sollten, jedoch für Ihre Topologie möglicherweise nicht erforderlich sind:  
  
    -   Regelmäßige Überprüfung der Daten  
  
    -   Anpassen der Agentparameter anhand von Profilen  
  
    -   Anpassen der Beibehaltungsdauer für Veröffentlichungen und die Verteilung  
  
    -   Grundlegendes zum Ändern von Artikel- und Veröffentlichungseigenschaften bei geänderten Anwendungsanforderungen  
  
    -   Grunglegendes zu Schemaänderungen bei geänderten Anwendungsanforderungen  
  
## <a name="develop-and-test-a-backup-and-restore-strategy"></a>Entwickeln und Testen einer Sicherungs- und Wiederherstellungsstrategie  
 Sichern Sie alle Datenbanken in regelmäßigen Abständen, und testen Sie regelmäßig, ob diese Sicherungen wiederhergestellt werden können. Das gilt auch für replizierte Datenbanken. Folgende Datenbanken sollten regelmäßig gesichert werden:  
  
-   Veröffentlichungsdatenbank  
  
-   Verteilungsdatenbank  
  
-   Abonnementdatenbanken  
  
-   Die Datenbanken**msdb** und **master** auf dem Verleger, Verteiler und allen Abonnenten  
  
 Bei replizierten Datenbanken gibt es besondere Aspekte im Hinblick auf das Sichern und Wiederherstellen von Daten. Weitere Informationen finden Sie unter [Sichern und Wiederherstellen von replizierten Datenbanken](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md).  
  
## <a name="script-the-replication-topology"></a>Erstellen von Skripts für die Replikationstopologie  
 Für die Replikationskomponenten in einer Topologie sollten im Rahmen des Plans zur Wiederherstellung im Notfall Skripts erstellt werden; diese können dann auch zur Automatisierung sich wiederholender Tasks verwendet werden. Ein Skript enthält die gespeicherten [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Systemprozeduren zum Implementieren der Replikationskomponenten, für die Skripts erstellt wurden, z. B. einer Veröffentlichung oder eines Abonnements. Skripts können nach dem Erstellen einer Komponente nicht mithilfe eines Assistenten (z. B. dem Assistenten für neue Veröffentlichung) oder in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] erstellt werden. Sie können das Skript mithilfe von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder **sqlcmd**anzeigen, ändern oder ausführen. Skripts können mit Sicherungsdateien gespeichert und dann verwendet werden, wenn eine Replikationstopologie erneut konfiguriert werden muss. Weitere Informationen finden Sie unter [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
 Falls Eigenschaftenänderungen vorgenommen wurden, sollten für eine Komponente neue Skripts erstellt werden. Wenn Sie bei einer Transaktionsreplikation benutzerdefinierte gespeicherte Prozeduren verwenden, sollte zusammen mit den Skripts eine Kopie aller dieser Prozeduren gespeichert werden. Nach Änderungen an der Prozedur sollte die Kopie dann aktualisiert werden (zu Prozedurupdates kommt es in der Regel nach Schemaänderungen oder wenn sich die Anwendungsanforderungen ändern). Weitere Informationen zu benutzerdefinierten Prozeduren finden Sie unter [Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
## <a name="establish-performance-baselines-and-tune-replication-if-necessary"></a>Einrichten von Leistungsgrundlagen und gegebenenfalls Optimierung der Replikation  
 Machen Sie sich vor dem Konfigurieren der Replikation mit den Faktoren vertraut, die sich auf die Replikationsleistung auswirken:  
  
-   Server- und Netzwerkhardware  
  
-   Datenbankentwurf  
  
-   Verteilerkonfiguration  
  
-   Entwurf und Optionen von Veröffentlichungen  
  
-   Entwurf und Verwendung von Filtern  
  
-   Abonnementoptionen  
  
-   Momentaufnahmeoptionen  
  
-   Agentparameter  
  
-   Verwaltung  
  
 Nach dem Konfigurieren der Replikation sollten Sie Leistungsgrundlagen entwickeln, die es Ihnen ermöglichen, das Replikationsverhalten bei einer typischen Auslastung der Anwendungen und Topologie zu ermitteln. Verwenden Sie den Replikationsmonitor und den Systemmonitor, um die typischen Zahlen für die folgenden fünf Dimensionen der Replikationsleistung zu ermitteln:  
  
-   Latenzzeit: die erforderliche Zeit für die Weitergabe einer Datenänderung zwischen den Knoten in einer Replikationstopologie.  
  
-   Durchsatz: der Umfang der Replikationsaktivität, die ein System unterstützt (gemessen in Befehlen, die in einem Zeitraum übermittelt werden).  
  
-   Parallelität: die Anzahl der Replikationsprozesse, die in einem System gleichzeitig aktiv sein können.  
  
-   Dauer der Synchronisierung: der Zeitraum, bis eine bestimmte Synchronisierung abgeschlossen ist.  
  
-   Ressourcenverbrauch: die Hardware- und Netzwerkressourcen, die im Rahmen der Replikationsverarbeitung verwendet werden.  
  
 Latenzzeit und Durchsatz sind für die Transaktionsreplikation am wichtigsten, da Systeme, die auf der Transaktionsreplikation basieren, in der Regel eine geringe Latenzzeit und einen hohen Durchsatz erfordern. Parallelität und Dauer der Synchronisierung sind bei der Mergereplikation am wichtigsten, da Systeme, die auf der Mergereplikation basieren, häufig eine große Zahl Abonnenten aufweisen und bei einem Verleger eine beträchtliche Zahl gleichzeitiger Synchronisierungen mit diesen Abonnenten erfolgen kann.  
  
 Nachdem Sie die Zahlen der Leistungsgrundlagen ermittelt haben, legen Sie im Replikationsmonitor Schwellenwerte fest. Weitere Informationen finden Sie unter [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) und [Verwenden von Warnungen für Replikations-Agentereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md). Sollte ein Leistungsproblem auftreten, lesen Sie die Vorschläge in den oben aufgeführten Themen zur Leistungsverbesserung durch, und ändern Sie die entsprechenden Bereiche, die sich auf die von Ihnen festgestellten Probleme beziehen.  
  
## <a name="create-thresholds-and-alerts"></a>Erstellen von Schwellenwerten und Warnungen  
 Im Replikationsmonitor können Sie eine Reihe von Schwellenwerten festlegen, die sich auf Status und Leistung beziehen. Legen Sie die geeigneten Schwellenwerte für Ihre Topologie fest. Wenn ein Schwellenwert erreicht wird, wird eine Warnung angezeigt, und optional kann eine Warnung an ein E-Mail-Konto, einen Pager oder ein anderes Gerät gesendet werden. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 Neben den Warnungen, die Schwellenwerten zur Überwachung zugeordnet werden können, stellt die Replikation eine Reihe vordefinierter Warnungen bereit, die auf Aktionen des Replikations-Agents reagieren. Diese Warnungen können dazu dienen, einen Administrator über den Status der Replikationstopologie auf dem Laufenden zu halten. Lesen Sie das Thema, das eine Beschreibung der Warnungen enthält, und verwenden Sie diejenigen, die Ihren Verwaltungsanforderungen entsprechen (Sie können gegebenenfalls auch weitere Warnungen erstellen). Weitere Informationen finden Sie unter [Verwenden von Warnungen für Replikations-Agentereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
## <a name="monitor-the-replication-topology"></a>Überwachen der Replikationstopologie  
 Nachdem die Replikationstopologie eingerichtet wurde sowie Schwellenwerte und Warnungen konfiguriert wurden, sollte die Replikation regelmäßig überwacht werden. Die Überwachung einer Replikationstopologie ist ein wichtiger Aspekt bei der Bereitstellung der Replikation. Da die Replikationsaktivität verteilt ist, ist es außerordentlich wichtig, die Aktivität und den Status auf allen an der Replikation beteiligten Computern nachzuverfolgen. Zum Überwachen der Replikation stehen die folgenden Tools zur Verfügung:  
  
-   Der Replikationsmonitor ist das wichtigste Tool bei der Überwachung der Replikation. Er ermöglicht es Ihnen, die allgemeine Integrität der Replikationstopologie zu überwachen. Weitere Informationen finden Sie unter [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] und Replikationsverwaltungsobjekte (RMO) stellen eine Schnittstelle zur Überwachung der Replikation bereit. Weitere Informationen finden Sie unter [Monitoring Replication](../../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
-   Auch der Systemmonitor kann bei der Überwachung der Replikationsleistung hilfreich sein. Weitere Informationen finden Sie unter [Monitoring Replication with System Monitor](../../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md).  
  
## <a name="validate-data-periodically"></a>Regelmäßige Überprüfung der Daten  
 Eine Datenüberprüfung ist bei der Replikation zwar nicht erforderlich, es wird jedoch empfohlen, die Überprüfung regelmäßig für die Transaktions- und die Mergereplikation auszuführen. Mit der Überprüfung stellen Sie sicher, dass die Daten auf dem Abonnenten mit denen auf dem Verleger übereinstimmen. Eine erfolgreiche Überprüfung bedeutet, dass zu diesem Zeitpunkt alle Änderungen vom Verleger auf den Abonnenten repliziert wurden (und vom Abonnenten auf den Verleger, wenn Updates auf dem Abonnenten unterstützt werden) und dass die beiden Datenbanken synchron sind.  
  
 Es wird empfohlen, die Überprüfung in Übereinstimmung mit dem Sicherungszeitplan der Veröffentlichungsdatenbank auszuführen. Wenn beispielsweise einmal wöchentlich eine vollständige Sicherung der Veröffentlichungsdatenbank erfolgt, könnte die Überprüfung einmal wöchentlich nach Abschluss der Sicherung ausgeführt werden. Weitere Informationen zur Überprüfung finden Sie unter [Überprüfen von replizierten Daten](../../../relational-databases/replication/validate-replicated-data.md).  
  
## <a name="use-agent-profiles-to-change-agent-parameters-if-necessary"></a>Verwenden von Agentprofilen zum Ändern von Agentparameter bei Bedarf  
 Agentprofile stellen eine praktische Methode zum Festlegen von Parametern des Replikations-Agents dar. Parameter können auch in der Befehlszeile des Agents angegeben werden. Es ist jedoch in der Regel besser, ein vordefiniertes Agentprofil zu verwenden oder ein neues Profil zu erstellen, wenn Sie den Wert eines Parameters ändern müssen. Wenn Sie z. B. die Mergereplikation verwenden und ein Abonnent von einer Breitbandverbindung auf eine DFÜ-Verbindung wechselt, sollten Sie das **slow link** -Profil für den Merge-Agent verwenden. Dieses Profil verwendet eine Reihe von Parametern, die sich für langsame Datenverbindungen besser eigenen. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="adjust-publication-and-distribution-retention-periods-if-necessary"></a>Anpassen der Beibehaltungsdauer für Veröffentlichungen und die Verteilung bei Bedarf  
 Bei der Transaktions- und der Mergereplikation wird jeweils anhand einer Beibehaltungsdauer ermittelt, wie lange Transaktionen in der Verteilungsdatenbank gespeichert werden und wie häufig ein Abonnement synchronisiert werden muss. Verwenden Sie zunächst die Standardeinstellungen. Überwachen Sie jedoch Ihre Topologie, um zu ermitteln, ob die Einstellungen angepasst werden müssen. Bei der Megereplikation z. B. wird mit der Beibehaltungsdauer für die Veröffentlichung (standardmäßig 14 Tage) festgelegt, wie lange Metadaten in Systemtabellen gespeichert werden. Wenn Abonnements immer innerhalb von fünf Tagen synchronisiert werden, sollten Sie die Einstellung auf eine niedrigere Zahl anpassen. Dadurch werden die Metadaten verringert und gegebenenfalls die Leistung verbessert. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## <a name="understand-how-to-modify-publications-if-application-requirements-change"></a>Grundlegendes zum Ändern von Veröffentlichungen bei geänderten Anwendungsanforderungen  
 Nachdem Sie eine Veröffentlichung erstellt haben, ist es möglicherweise notwendig, Artikel hinzuzufügen oder zu löschen bzw. die Veröffentlichungs- oder Artikeleigenschaften zu ändern. Die meisten Änderungen sind auch nach der Erstellung der Veröffentlichung möglich. In einigen Fällen muss jedoch eine neue Momentaufnahme für die Veröffentlichung generiert werden, und/oder die Abonnements für die Veröffentlichung müssen erneut initialisiert werden. Weitere Informationen finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) und [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
## <a name="understand-how-to-make-schema-changes-if-application-requirements-change"></a>Grunglegendes zu Schemaänderungen bei geänderten Anwendungsanforderungen  
 In vielen Fällen sind jedoch Schemaänderungen erforderlich, sobald eine Anwendung in die Produktionsumgebung gebracht wird. In einer Replikationstopologie müssen diese Änderungen häufig an alle Abonnenten weitergegeben werden. Die Replikation unterstützt eine breite Palette von Schemaänderungen an veröffentlichten Objekten. Wenn Sie eine der folgenden Schemaänderungen am entsprechenden veröffentlichten Objekt auf einem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verleger vornehmen, wird diese Änderung standardmäßig an alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten weitergegeben:  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Weitere Informationen finden Sie unter [Vornehmen von Schemaänderungen in Veröffentlichungsdatenbanken](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwaltung &#40;Replikation&#41;](../../../relational-databases/replication/administration/administration-replication.md)  
  
  
