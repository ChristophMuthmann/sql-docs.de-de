---
title: "&#220;berwachen der Leistung mit dem Replikationsmonitor | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachen der Leistung [SQL Server-Replikation], Replikationsmonitor"
  - "Protokolllese-Agent, Überwachung"
  - "Replikationsmonitor, Leistung"
  - "Merge-Agent, Überwachung"
  - "Warteschlangenlese-Agent, Überwachung"
  - "Momentaufnahme-Agent, Überwachung"
  - "Verteilungs-Agent, Überwachung"
  - "Überwachen der Leistung [SQL Server-Replikation]"
ms.assetid: f212397d-1bfd-496b-a246-668952891d09
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# &#220;berwachen der Leistung mit dem Replikationsmonitor
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Replikationsmonitor ermöglicht es Ihnen, die Leistung bei Transaktions- und Mergereplikationen zu überwachen. Zu diesem Zweck können die folgenden Aktionen ausgeführt werden:  
  
-   Festlegen von Warnungen und Schwellenwerten  
  
-   Anzeigen von Leistungsindikatoren  
  
-   Ermitteln der Latenzzeit mit Überwachungstokens (Transaktionsreplikation)  
  
-   Anzeigen detaillierter Synchronisierungsstatistiken (Mergereplikation)  
  
-   Anzeigen von Transaktionen und Bereitstellungszeiten (Transaktionsreplikation)  
  
## Festlegen von Schwellenwerten und Warnungen  
 Im Replikationsmonitor können Sie Warnungen für eine Reihe von Leistungszuständen aktivieren. Beim Aktivieren einer Warnung geben Sie einen Schwellenwert an. Wenn dieser Schwellenwert erreicht oder überschritten wird, wird eine Warnung angezeigt, dem **Status** Spalte für das Abonnement und die Veröffentlichung mit dem synchronisiert wird (es sei denn, ein Problem mit einer höheren Priorität angezeigt werden muss). Neben der Warnung im Replikationsmonitor kann bei Erreichen eines Schwellenwerts auch ein Warnhinweis ausgelöst werden. Warnungen können für die folgenden Leistungszustände aktiviert werden:  
  
-   Die angegebene Latenzzeit (Zeit, die zwischen dem Start einer Transaktion auf dem Verleger und dem Start der entsprechenden Transaktion auf dem Abonnenten vergeht) wird überschritten.  
  
     Betrifft nur Transaktionsreplikationen. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird als Status **Leistungskritisch**angezeigt.  
  
-   Die angegebene Synchronisierungszeit wird überschritten.  
  
     Betrifft nur Mergereplikationen. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird der Status angezeigt, als **langer Mergevorgang**. Sie können für DFÜ- und LAN-Verbindungen (Local Area Network, lokales Netzwerk) unterschiedliche Schwellenwerte angeben.  
  
-   Die angegebene Zahl von Zeilen konnte nicht innerhalb der festgelegten Zeit verarbeitet werden.  
  
     Betrifft nur Mergereplikationen. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird als Status **Leistungskritisch**angezeigt. Sie können für DFÜ- und LAN-Verbindungen unterschiedliche Schwellenwerte angeben.  
  
 Weitere Informationen finden Sie unter [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
## Anzeigen von Leistungsindikatoren  
 Der Replikationsmonitor zeigt bei Transaktions- und Mergereplikationen in den Spalten **Aktuelle Durchschnittsleistung** und **Die derzeit schlechteste Leistung** (für Veröffentlichungen) und in der **Leistung** -Spalte (für Abonnements) Leistungswerte an. Folgende Werte sind möglich:  
  
-   Hervorragend  
  
-   Gut  
  
-   Durchschnittlich  
  
-   Schlecht  
  
-   Kritisch (nur bei Transaktionsreplikation)  
  
 Welcher Wert angezeigt wird, hängt von Folgendem ab:  
  
-   Bei der Transaktionsreplikation richtet sich die Angabe zur Leistungsqualität nach dem Schwellenwert für die Latenzzeit. Wenn dieser Schwellenwert nicht festgelegt ist, wird auch kein Leistungswert angezeigt. Aus der folgenden Tabelle geht der Zusammenhang zwischen dem Schwellenwert und dem Wert für die Leistungsqualität hervor. Wenn für den Schwellenwert z. B. 60 Sekunden festgelegt ist und die tatsächliche Latenzzeit 30 Sekunden beträgt, entspricht diese Latenzzeit 50 % des Schwellenwerts, woraus sich der Wert "Gut" ergibt.  
  
    |Hervorragend|Gut|Durchschnittlich|Schlecht|Kritisch|  
    |---------------|----------|----------|----------|--------------|  
    |0 – 34%|35 – 59%|60 – 84%|85 – 99%|100% +|  
  
-   Bei der Mergereplikation ist Leistungsqualität unabhängig von den beiden Schwellenwerten (der Schwellenwert für die wird bestimmt, ob der Wert **Leistung ist kritisch** wird angezeigt, dem **Status** Spalte). Die Leistungsqualität wird ermittelt, indem die Leistung der einzelnen Abonnements mit der durchschnittlichen bisherigen Leistung der Veröffentlichungsabonnements mit dem gleichen Verbindungstyp (DFÜ oder LAN) verglichen wird. Der Replikationsmonitor zeigt einen Wert an, nachdem fünf Synchronisierungen mit jeweils mindestens 50 Änderungen über denselben Verbindungstyp stattgefunden haben. Wenn weniger als fünf Synchronisierungen mit 50 oder mehr Änderungen ausgeführt wurden oder wenn die letzte Synchronisierung weniger als 50 Änderungen aufweist, zeigt der Replikationsmonitor keinen Wert an.  
  
     Aus der folgenden Tabelle geht der Zusammenhang zwischen der durchschnittlichen Leistung und dem Wert für die Leistungsqualität hervor. Wenn z. B. zehn Abonnenten über eine LAN-Verbindung mit einer Durchschnittsrate von 100 Zeilen pro Sekunde synchronisiert werden und eines der Abonnements dann mit einer Rate von 125 Zeilen pro Sekunde synchronisiert wird, beläuft sich die Leistung für diese Abonnentensynchronisierung auf 125 % des Durchschnitts, was einer guten Leistung entspricht.  
  
    |Hervorragend|Gut|Durchschnittlich|Schlecht|  
    |---------------|----------|----------|----------|  
    |151+%|76 – 150%|26 – 75%|0 – 25%|  
  
 Weitere Informationen zum Anzeigen von Abonnementinformationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für ein Abonnement & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md).  
  
## Ermitteln der Latenzzeit mit Überwachungstokens  
 Mithilfe der Transaktionsreplikation können Sie die Latenzzeit (Latenz) in einem System messen, indem Sie ein Token (kleine Menge von Daten) in das Transaktionsprotokoll der Veröffentlichungsdatenbank einfügen und aufzeichnen, wie lange dieses Token benötigt, bis es beim Verteiler und den Abonnenten ankommt. Mithilfe des Tokens können Sie auch feststellen, ob Daten den Verteiler oder die Abonnenten gar nicht erreichen. Weitere Informationen finden Sie unter [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## Anzeigen von Details zur Synchronisierungsleistung bei der Mergereplikation  
 Bei Mergereplikationen zeigt der Replikationsmonitor detaillierte Statistiken für alle Artikel an, die während einer Synchronisierung verarbeitet werden. So lässt sich diesen Statistiken z. B. die Länge der einzelnen Verarbeitungsphasen (Hochladen von Änderungen, Herunterladen von Änderungen usw.) entnehmen. Auf diese Weise können Sie besser die Tabellen identifizieren, die zu einer Verlangsamung führen, und Sie können hier auch hervorragend Leistungsprobleme im Zusammenhang mit Mergeabonnements diagnostizieren. Weitere Informationen zum Anzeigen detaillierter Statistiken finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Anzeigen von Transaktions- und Bereitstellungszeiten bei der Transaktionsreplikation  
 Bei Transaktionsreplikationen zeigt der Replikationsmonitor Informationen zur Anzahl der Transaktionen in der Verteilungsdatenbank an, die noch nicht an einen Abonnenten verteilt wurden, und er gibt an, wie lange die Verteilung dieser Transaktionen schätzungsweise dauert. Weitere Informationen finden Sie unter [Anzeigen von Informationen und Ausführen von Aufgaben für die Agents einem Abonnement zugeordneten & #40; Der Replikationsmonitor & #41;](../../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
## Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)  
  
  