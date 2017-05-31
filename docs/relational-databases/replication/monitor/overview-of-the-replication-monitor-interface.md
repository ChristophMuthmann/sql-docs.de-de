---
title: "Übersicht über die Benutzeroberfläche des Replikationsmonitors | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 078f0e34-7153-45c4-8725-778b5bef88da
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85b3b97fa9dc219012727b01a0d8013e0481a85c
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="overview-of-the-replication-monitor-interface"></a>Übersicht über die Benutzeroberfläche des Replikationsmonitors
  Der Replikationsmonitor in[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bietet eine Sicht aller Replikationsaktivitäten, bei der der Verleger oder der Verteiler im Vordergrund steht, in einem Format mit zwei Bereichen an. Im linken Bereich fügen Sie dem Monitor einen Verleger hinzu, und im rechten Bereich zeigt der Monitor die Informationen zum Verleger, dessen Veröffentlichungen, Abonnements für diese Veröffentlichungen und die verschiedenen Replikations-Agents an. Neben der Darstellung der Informationen zur Replikationstopologie ermöglicht der Replikationsmonitor die Ausführung zahlreicher Aufgaben, wie beispielsweise des Startens und Anhaltens von Agents und des Überprüfens von Daten.  
  
## <a name="viewing-information-for-the-entire-topology"></a>Anzeigen von Informationen zur ganzen Topologie  
 Anzeige im linken Bereich des Replikationsmonitors  
  
-   Verlegergruppen, Verleger und Veröffentlichungen.  
  
-   Verteiler, Verleger und Veröffentlichungen.  
  
 Um Informationen im Replikationsmonitor anzeigen zu können, müssen Sie zunächst einen Verleger hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen und Entfernen von Verlegern vom Replikationsmonitor aus](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
 Mithilfe des linken Bereichs lassen sich Antworten auf folgende Fragen finden:  
  
-   Arbeitet das System fehlerfrei?  
  
     Das Replikationssystem ist relativ fehlerfrei, wenn im linken Bereich keine Fehlersymbole für Knoten angezeigt werden. Um einen vollständigeren Überblick über die Systemintegrität zu erhalten, sollten Sie zusätzlich die Registerkarte **Überwachungsliste für Abonnements** überprüfen, auf der Informationen zu Abonnements angezeigt werden, die möglicherweise ein Eingreifen erfordern.  
  
-   Warum wird ein Agent nicht ausgeführt?  
  
     Ein Agent wird zu einem bestimmten Zeitpunkt nicht ausgeführt, weil entweder die Ausführung nicht geplant ist oder weil ein Fehler aufgetreten ist. Wenn ein Fehler aufgetreten ist, wird für die entsprechenden Knoten im linken Bereich ein Fehlersymbol angezeigt. Wenn der Momentaufnahme-Agent für eine Veröffentlichung beispielsweise aufgrund eines Fehlers angehalten wird, wird für die Verlegergruppe, den Verleger und die Veröffentlichungsknoten ein Fehlersymbol angezeigt wird. Die Zusammenfassungsinformationen für den Momentaufnahme-Agent werden für die Veröffentlichung auf der Registerkarte **Agents** angezeigt. Doppelklicken Sie auf dieser Registerkarte auf den Momentaufnahme-Agent, um detaillierte Fehlerinformationen anzuzeigen.  
  
## <a name="viewing-information-and-performing-tasks-related-to-distributors"></a>Anzeigen von Informationen und Ausführen von veröffentlichungsbezogenen Aufgaben für Verteiler  
 Im Replikationsmonitor werden auf drei Registerkarten Informationen zu Verteilern angezeigt:  
  
-   Registerkarte**Veröffentlichungen**   
  
     Diese Registerkarte enthält Zusammenfassungsinformationen für alle Veröffentlichungen eines Verteilers.  
  
-   Registerkarte**Überwachungsliste für Abonnements**   
  
     Diese Registerkarte stellt Informationen zu Abonnements für den ausgewählten Verteiler bereit. Sie können die Liste der Abonnements filtern, um Fehler, Warnungen und Abonnements mit schlechter Leistung anzuzeigen. Zudem können Sie auf der Registerkarte auf Abonnementeigenschaften zugreifen, auf detaillierte Informationen zum Agent oder Agents, die mit einem Abonnement in Zusammenhang stehen, zugreifen, Abonnements erneut initialisieren und Abonnements überprüfen.  
  
     Mithilfe der Registerkarte **Überwachungsliste für Abonnements** lassen sich die folgenden Fragen beantworten:  
  
    -   Welche Abonnements sind langsam?  
  
         Legen Sie die Optionen auf dieser Registerkarte so fest, dass die Abonnements im Raster nach relativer Leistung sortiert angezeigt werden.  
  
    -   Arbeitet das System fehlerfrei?  
  
         Im Raster der Registerkarte werden Fehler- und Warnungssymbole für alle Abonnements angezeigt, die ein Eingreifen erfordern.  
  
     Diese Registerkarte ist nicht verfügbar für Verteiler mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] oder einer früheren Version.  
  
-   Registerkarte**Agents**   
  
     Diese Registerkarte zeigt ausführliche Informationen zu den Agents und Aufträgen an, die von allen Replikationstypen verwendet werden. Über diese Registerkarte können Sie zudem alle Agents und Aufträge starten und beenden.  
  
 Der Replikationsmonitor enthält zudem ein Kontextmenü für den Verteilerknoten. Klicken Sie mit der rechten Maustaste im linken Bereich auf einen Verteiler, um die folgenden Tasks auszuführen:  
  
-   Fügen Sie dem Replikationsmonitor einen Verleger hinzu.  
  
-   Bearbeiten Sie die Replikationsmonitor-Einstellungen für den Verleger.  
  
-   Wechseln Sie zur Sicht für die Verlegergruppe.  
  
## <a name="viewing-information-and-performing-tasks-related-to-publishers"></a>Anzeigen von Informationen und Ausführen von verlegerbezogenen Aufgaben  
 Im Replikationsmonitor werden auf drei Registerkarten Informationen zu Verlegern angezeigt:  
  
-   Registerkarte**Veröffentlichungen**   
  
     Diese Registerkarte enthält Zusammenfassungsinformationen für alle Veröffentlichungen auf einem Verleger.  
  
-   Registerkarte**Überwachungsliste für Abonnements**   
  
     Diese Registerkarte dient der Anzeige von Informationen zu Abonnements für alle verfügbaren Veröffentlichungen auf dem ausgewählten Verleger. Sie können die Liste der Abonnements filtern, um Fehler, Warnungen und Abonnements mit schlechter Leistung anzuzeigen. Zudem können Sie auf der Registerkarte auf Abonnementeigenschaften zugreifen, auf detaillierte Informationen zum Agent oder Agents, die mit einem Abonnement in Zusammenhang stehen, zugreifen, Abonnements erneut initialisieren und Abonnements überprüfen.  
  
     Mithilfe der Registerkarte **Überwachungsliste für Abonnements** lassen sich die folgenden Fragen beantworten:  
  
    -   Welche Abonnements sind langsam?  
  
         Legen Sie die Optionen auf dieser Registerkarte so fest, dass die Abonnements im Raster nach relativer Leistung sortiert angezeigt werden.  
  
    -   Arbeitet das System fehlerfrei?  
  
         Im Raster der Registerkarte werden Fehler- und Warnungssymbole für alle Abonnements angezeigt, die ein Eingreifen erfordern.  
  
     Diese Registerkarte wird nicht für Verteiler angezeigt, auf denen niedrigere Versionen als [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]ausgeführt werden.  
  
-   Registerkarte**Agents**   
  
     Diese Registerkarte zeigt ausführliche Informationen zu den Agents und Aufträgen an, die von allen Replikationstypen verwendet werden. Über diese Registerkarte können Sie zudem alle Agents und Aufträge starten und beenden.  
  
 Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für einen Verleger &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
 Der Replikationsmonitor enthält zudem ein Kontextmenü für den Verlegerknoten. Klicken Sie im linken Bereich mit der rechten Maustaste auf einen Verleger, um Folgendes auszuführen:  
  
-   Hinzufügen von Replikationsmonitor-Einstellungen für den Verleger  
  
-   Entfernen des Verlegers aus dem Replikationsmonitor  
  
-   Anzeigen und Bearbeiten von Agentprofilen  
  
-   Verbinden oder Trennen der Verbindung mit dem Verteiler, auf dem die Informationen zum Verleger gespeichert sind  
  
## <a name="viewing-information-and-performing-tasks-related-to-publications"></a>Anzeigen von Informationen und Ausführen von veröffentlichungsbezogenen Aufgaben  
 Im Replikationsmonitor werden auf drei Registerkarten und in mehreren Detailfenstern Informationen zu Veröffentlichungen angezeigt:  
  
-   Registerkarte**Alle Abonnements**   
  
     Auf dieser Registerkarte werden Informationen zu allen Abonnements für die ausgewählte Veröffentlichung angezeigt. Diese Registerkarte wird standardmäßig nach Priorität sortiert: Zuerst werden Fehler, dann Warnungen und anschließend aufsteigend nach Leistung Abonnements mit schlechter Leistung angezeigt.  
  
     Mithilfe der Registerkarte **Alle Abonnements** lassen sich die folgenden Fragen beantworten:  
  
    -   Welche Abonnements sind langsam?  
  
         Legen Sie die Optionen auf dieser Registerkarte so fest, dass die Abonnements im Raster nach relativer Leistung sortiert angezeigt werden.  
  
    -   Arbeitet das System fehlerfrei?  
  
         Im Raster der Registerkarte werden Fehler- und Warnungssymbole für alle Abonnements angezeigt, die ein Eingreifen erfordern.  
  
-   Registerkarte**Agents**   
  
     Diese Registerkarte zeigt Informationen zu den Agents an, die von der Replikation verwendet werden. Diese Registerkarte enthält Informationen zu folgenden Agents:  
  
    -   Momentaufnahme-Agent, der von allen Veröffentlichungen verwendet wird.  
  
    -   Protokolllese-Agent, der von allen Transaktionsveröffentlichungen verwendet wird.  
  
    -   Warteschlangenlese-Agent, der von Transaktionsveröffentlichungen verwendet wird, die für Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurden.  
  
     Darüber hinaus können Sie auf der Registerkarte die folgenden Aufgaben ausführen: auf detaillierte Informationen zu den Agents zugreifen und die einzelnen Agents starten und anhalten. Informationen zu den Agents, die den Abonnements zugeordnet sind (Verteilungs-Agent und Merge-Agent), finden Sie in diesem Thema im Abschnitt zum Anzeigen von Informationen und zum Ausführen von veröffentlichungsbezogenen Aufgaben.  
  
-   Registerkarte**Warnungen**   
  
     Auf dieser Registerkarte können Sie Warnungen für Agents angeben. Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
-   Registerkarte**Überwachungstoken** (nur für Transaktionsreplikationen)  
  
     Über diese Registerkarte können Sie die Latenzzeit messen, d. h. die Zeitspanne zwischen dem Ausführen des Commit für eine Transaktion auf dem Verleger und dem Ausführen des Commit für die entsprechende Aktion auf dem Abonnenten.  
  
     Mithilfe dieser Registerkarte können Sie folgende Frage beantworten:  
  
    -   Wie lange dauert es bei der Transaktionsreplikation, bis eine Transaktion, für die ein Commit ausgeführt wurde, den Abonnenten erreicht?  
  
         Zeigen Sie die Gesamtzeit an, die benötigt wird, um eine Transaktion über das System zu übertragen, und vergleichen Sie sie mit älteren Zeiten.  
  
     Diese Registerkarte wird nicht für Verteiler mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] oder einer früheren Version angezeigt. Weitere Informationen zu Überwachungstoken finden Sie unter [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
-   Detailfenster für die Agents, die einer Veröffentlichung zugeordnet sind. Folgende Agents sind Veröffentlichungen zugeordnet:  
  
    -   Momentaufnahme-Agent, der von allen Veröffentlichungen verwendet wird.  
  
    -   Protokolllese-Agent, der von allen Transaktionsveröffentlichungen verwendet wird.  
  
    -   Warteschlangenlese-Agent, der von Transaktionsveröffentlichungen verwendet wird, die für Abonnements mit verzögertem Update über eine Warteschlange aktiviert wurden.  
  
     Doppelklicken Sie im Replikationsmonitor auf einen Agent, um auf die entsprechenden Informationen in einem Detailfenster zuzugreifen. Neben den oben aufgeführten Agents sind folgende Agents Abonnements zugeordnet: Der Verteilungs-Agent für Abonnements ist Momentaufnahme- und Transaktionsveröffentlichungen zu geordnet, und der Merge-Agent ist Abonnements für Mergeveröffentlichungen zugeordnet. Weitere Informationen hierzu finden Sie in diesem Thema im Abschnitt zum Anzeigen von Informationen und zum Ausführen von veröffentlichungsbezogenen Aufgaben.  
  
     Die Detailfenster des Agents enthalten Informationen zu Agentsitzungen angezeigt, einschließlich Startzeit, Beendigungszeit, Dauer und während einer Sitzung ausgeführter Aktionen. Sie sind hilfreich zum Beantworten der folgenden Frage:  
  
    -   Warum wird ein Agent nicht ausgeführt?  
  
         In den verfügbaren Fehlermeldungen werden detaillierte Informationen dazu angegeben, warum ein Agent nicht ausgeführt wird. Sie bilden einen Ausgangspunkt für die Behebung von Problemen in Agents, die einer Veröffentlichung zugeordnet sind.  
  
 Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für eine Veröffentlichung &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md) und [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents, die mit einer Veröffentlichung verknüpft sind &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
 Der Replikationsmonitor enthält zudem ein Kontextmenü für den Veröffentlichungsknoten. Klicken Sie im linken Bereich mit der rechten Maustaste auf eine Veröffentlichung, um Folgendes auszuführen:  
  
-   Erneutes Initialisieren aller Abonnements für eine Veröffentlichung  
  
-   Überprüfen aller Abonnements für eine Veröffentlichung  
  
-   Generieren einer Momentaufnahme für eine Veröffentlichung  
  
-   Anzeigen und Bearbeiten von Veröffentlichungseigenschaften  
  
## <a name="viewing-information-and-performing-tasks-related-to-subscriptions"></a>Anzeigen von Informationen und Ausführen von abonnementbezogenen Aufgaben  
 Im Replikationsmonitor werden auf mehreren verschiedenen Registerkarten Informationen zu Abonnements angezeigt. Doppelklicken Sie im Replikationsmonitor auf ein Abonnement, um auf die entsprechenden Registerkarten in einem Detailfenster zuzugreifen. Alle Registerkarte sind hilfreich, um die Frage "Warum wird ein Agent nicht ausgeführt?" zu beantworten. In den verfügbaren Fehlermeldungen werden detaillierte Informationen dazu angegeben, warum ein Agent nicht ausgeführt wird. Sie bilden einen Ausgangspunkt für die Behebung von Problemen in Agents, die einem Abonnement zugeordnet sind.  
  
-   Registerkarten**Alle Abonnements** und **Überwachungsliste für Abonnements**.  
  
     Diese Registerkarten werden weiter oben in diesem Thema beschrieben.  
  
-   Registerkarte**Verlauf Verleger zu Verteiler** (nur für Transaktionsreplikationen)  
  
     Auf dieser Registerkarte werden Informationen zum Protokolllese-Agent für eine Veröffentlichung angezeigt (diese Registerkarte entspricht dem Detailfenster Protokolllese-Agent).  
  
-   Registerkarte**Verlauf Verteiler zu Abonnent** (Momentaufnahmereplikation und Transaktionsreplikation)  
  
     Auf dieser Registerkarte werden Informationen zum Verteilungs-Agent für ein Abonnement angezeigt.  
  
-   Registerkarte**Nicht verteilte Befehle** (nur für Transaktionsreplikationen)  
  
     Auf diese Registerkarte werden Informationen zur Anzahl der Befehle in der Verteilungsdatenbank angezeigt, die nicht an den ausgewählten Abonnenten übermittelt wurden. Zudem wird die geschätzte Zeit angegeben, die die Übermittlung dieser Befehle in Anspruch nimmt. Mithilfe dieser Registerkarte kann die Frage "Wie weit ist mein Abonnement in Verzug?" beantwortet werden. Diese Registerkarte wird nicht für Verteiler angezeigt, auf denen niedrigere Versionen als SQL Server 2005 ausgeführt werden.  
  
-   Registerkarte**Synchronisierungsverlauf** (nur für Mergereplikationen)  
  
     Auf dieser Registerkarte werden Informationen zum Merge-Agent für ein Abonnement angezeigt. Mithilfe dieser Registerkarte können Sie folgende Frage beantworten:  
  
    -   Warum ist das Mergeabonnement langsam?  
  
         Diese Registerkarte zeigt detaillierte Statistiken für jeden während der Synchronisierung verarbeiteten Artikel an, einschließlich der aufgewendeten Zeit in jeder Verarbeitungsphase (Hochladen von Änderungen, Herunterladen von Änderungen usw.) Dadurch kann genau festgestellt werden, welche Tabellen zu einer Verlangsamung führen. Darüber hinaus bieten diese Statistiken eine optimale Plattform, Leistungsprobleme bei Mergeabonnements zu beheben.  
  
 Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md) und [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents, die einem Abonnement zugeordnet sind &#40;Replikationsmonitor&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="viewing-information-and-performing-tasks-related-to-agent-profiles"></a>Anzeigen von Informationen und Ausführen von Aufgaben, die sich auf Agentprofile beziehen  
 Der Replikationsmonitor enthält mehrere Dialogfelder zum Verwalten von Agentprofilen. Bei Agentprofilen handelt es sich um Parametersätze für einen Agent, mit denen das Verhalten des Agents festgelegt wird. Weitere Informationen finden Sie unter [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md). Die Dialogfelder lauten wie folgt:  
  
-   **Agentprofile**  
  
     In diesem Dialogfeld können Sie die Eigenschaften von Profilen ändern, Profile erstellen und löschen, ein Standardprofil angeben und angeben, dass alle Agents eines bestimmten Typs (beispielsweise Momentaufnahme-Agents) ein bestimmtes Profil verwenden sollen.  
  
-   **\<AgentProfileName> Eigenschaften**  
  
     In diesem Dialogfeld können Sie die Parametereinstellungen in einem Profil anzeigen und bearbeiten.  
  
-   **Neues Agentprofil**  
  
     In diesem Dialogfeld können Sie ein neues Profil erstellen und dabei optional die Werte eines vorhandenen Profils aufnehmen.  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
