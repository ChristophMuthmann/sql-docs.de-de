---
title: Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor | Microsoft-Dokumentation
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
- alerts [SQL Server replication]
- Merge Agent, thresholds and warnings
- Distribution Agent, thresholds and warnings
- thresholds [SQL Server replication]
- Replication Monitor, thresholds and warnings
- monitoring performance [SQL Server replication], thresholds and warnings
ms.assetid: 3a409c2c-b77e-4001-b81a-1dcd918618ec
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b47d0b4565cc187ae0746fa7a6c9b5b1f864c3e7
ms.lasthandoff: 04/11/2017

---
# <a name="set-thresholds-and-warnings-in-replication-monitor"></a>Festlegen von Schwellenwerten und Warnungen im Replikationsmonitor
  Im Replikationsmonitor von[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] werden Statusinformationen für Veröffentlichungen und Abonnements angezeigt. Standardmäßig zeigt der Replikationsmonitor Warnungen nur für nicht initialisierte Abonnements an. Sie können Warnungen jedoch auch für andere Bedingungen aktivieren. Sie sollten Warnungen für Ihre Topologie aktivieren, damit Sie rechtzeitig über Status und Leistung informiert werden.  
  
 Beim Aktivieren einer Warnung geben Sie einen Schwellenwert an. Wenn dieser Schwellenwert erreicht oder überschritten wird, wird eine Warnung angezeigt (außer es muss ein Problem mit höherer Priorität angezeigt werden). Neben der Warnung im Replikationsmonitor kann bei Erreichen eines Schwellenwerts auch ein Warnhinweis ausgelöst werden. Sie können Warnungen für folgende Bedingungen aktivieren:  
  
-   Bevorstehender Abonnementablauf  
  
     Dieser Statuswert gilt für alle Arten der Replikation. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird der Abonnementstatus als **Läuft demnächst ab/Abgelaufen**angezeigt.  
  
-   Die angegebene Latenzzeit (Zeit, die zwischen dem Start einer Transaktion auf dem Verleger und dem Start der entsprechenden Transaktion auf dem Abonnenten vergeht) wird überschritten.  
  
     Betrifft nur Transaktionsreplikationen. Falls der angegebene Schwellenwert erreicht oder überschritten wird, wird der Abonnementstatus als **Leistungskritisch**angezeigt.  
  
-   Die angegebene Synchronisierungszeit wird überschritten.  
  
     Betrifft nur Mergereplikationen. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird als Status **Langer Mergevorgang**angezeigt. Sie können verschiedene Schwellenwerte für DFÜ- und Local Area Network-(LAN-)Verbindungen angeben.  
  
-   Die angegebene Zahl von Zeilen konnte nicht innerhalb der festgelegten Zeit verarbeitet werden.  
  
     Betrifft nur Mergereplikationen. Wenn der angegebene Schwellenwert erreicht oder überschritten wird, wird als Status **Leistungskritisch**angezeigt. Sie können verschiedene Schwellenwerte für DFÜ- und LAN-Verbindungen angeben.  
  
 Weitere Informationen zu den Warnungen **Leistungskritisch** und **langer Mergevorgang**, finden Sie unter [Überwachen der Leistung mit dem Replikationsmonitor](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **In diesem Thema**  
  
-   [Festlegen der Schwellenwerte und Warnungen für eine Transaktionsveröffentlichung](#Transactional)  
  
-   [Festlegen der Schwellenwerte und Warnungen für eine Mergeveröffentlichung](#Merge)  
  
-   [Festlegen der Schwellenwerte und Warnungen für eine Momentaufnahmeveröffentlichung](#Snapshot)  
  
##  <a name="Transactional"></a> So legen Sie die Schwellenwerte und Warnungen für eine Transaktionsveröffentlichung fest  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Warnungen** . Wenn Sie weitere Informationen zu den Optionen auf dieser Registerkarte benötigen, klicken Sie auf der Menüleiste auf **Hilfe** .  
  
3.  Aktivieren Sie eine Warnung, indem Sie das entsprechende Kontrollkästchen aktivieren: **Warnung, wenn ein Abonnement innerhalb des Schwellenwerts abläuft** oder **Warnung, wenn die Latenzzeit den Schwellenwert überschreitet**.  
  
4.  Legen Sie in der **Schwellenwert** -Spalte einen Schwellenwert für die Warnungen fest. Wenn Sie z. B. unter Schritt 3 die Option **Warnung, wenn die Latenzzeit den Schwellenwert überschreitet** ausgewählt haben, können Sie in der **Schwellenwert** -Spalte eine Latenzzeit von **60 Sekunden** angeben.  
  
5.  Klicken Sie auf **Änderungen speichern**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>So konfigurieren Sie eine Warnung für einen Schwellenwert  
  
1.  Klicken Sie auf **Warnungen konfigurieren**.  
  
2.  Wählen Sie im Dialogfeld **Replikationswarnungen konfigurieren** eine Warnung aus, und klicken Sie dann auf **Konfigurieren**.  
  
     In diesem Dialogfeld werden Warnungen für alle Veröffentlichungstypen angezeigt – auch für Warnungen, die nichts mit den Überwachungsschwellenwerten zu tun haben. Weitere Informationen finden Sie unter [Verwenden von Warnungen für Replikations-Agentereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Legen Sie im Dialogfeld **\<Eigenschaften von Warnung AlertName>** die gewünschten Optionen fest:  
  
    -   Klicken Sie auf der Seite **Allgemein** auf **Aktivieren**, und geben Sie an, für welche Datenbank die Warnung gelten soll.  
  
    -   Geben Sie auf der Seite **Antwort** an, ob eine E-Mail gesendet und/oder ein Auftrag ausgeführt werden soll.  
  
    -   Passen Sie auf der Seite **Optionen** den Text der Antwort an.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf **Schließen**.  
  
##  <a name="Merge"></a> Festlegen der Schwellenwerte und Warnungen für eine Mergeveröffentlichung  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Warnungen** . Wenn Sie weitere Informationen zu den Optionen dieser Registerkarte erhalten möchten, klicken Sie auf der Menüleiste auf **Hilfe** .  
  
3.  Aktivieren Sie eine Warnung, indem Sie das entsprechende Kontrollkästchen aktivieren:  
  
    -   **Warnung, wenn ein Abonnement innerhalb des Schwellenwerts abläuft**  
  
    -   **Warnung, wenn eine Zusammenführungslänge für DFÜ-Verbindungen den Schwellenwert überschreitet**  
  
    -   **Warnung, wenn eine Zusammenführungslänge für LAN-Verbindungen den Schwellenwert überschreitet**  
  
    -   **Warnung, wenn der Wert für zusammengeführte Zeilen pro Sekunde für LAN-Verbindungen kleiner ist als der Schwellenwert**  
  
    -   **Warnung, wenn der Wert für zusammengeführte Zeilen pro Sekunde für DFÜ-Verbindungen kleiner ist als der Schwellenwert**  
  
4.  Legen Sie in der **Schwellenwert** -Spalte Schwellenwerte für die Warnungen fest Wenn Sie beispielsweise unter Schritt 3 die Option **Warnung, wenn eine Zusammenführungslänge für DFÜ-Verbindungen den Schwellenwert überschreitet** ausgewählt haben, könnten Sie in der **Schwellenwert** -Spalte beispielsweise **10 Minuten** angeben.  
  
5.  Klicken Sie auf **Änderungen speichern**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>So konfigurieren Sie eine Warnung für einen Schwellenwert  
  
1.  Klicken Sie auf **Warnungen konfigurieren**.  
  
2.  Wählen Sie im Dialogfeld **Replikationswarnungen konfigurieren** eine Warnung aus, und klicken Sie dann auf **Konfigurieren**.  
  
     In diesem Dialogfeld werden Warnungen für alle Veröffentlichungstypen angezeigt – auch für Warnungen, die nichts mit den Überwachungsschwellenwerten zu tun haben.  
  
3.  Legen Sie im Dialogfeld **\<Eigenschaften von Warnung AlertName>** die gewünschten Optionen fest:  
  
    -   Klicken Sie auf der Seite **Allgemein** auf **Aktivieren**, und geben Sie an, für welche Datenbank die Warnung gelten soll.  
  
    -   Geben Sie auf der Seite **Antwort** an, ob eine E-Mail gesendet und/oder ein Auftrag ausgeführt werden soll.  
  
    -   Passen Sie auf der Seite **Optionen** den Text der Antwort an.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf **Schließen**.  
  
##  <a name="Snapshot"></a> Festlegen der Schwellenwerte und Warnungen für eine Momentaufnahmeveröffentlichung  
  
1.  Erweitern Sie im linken Bereich eine Verlegergruppe, erweitern Sie einen Verleger, und klicken Sie dann auf eine Veröffentlichung.  
  
2.  Klicken Sie auf die Registerkarte **Warnungen** . Wenn Sie weitere Informationen zu den Optionen auf dieser Registerkarte benötigen, klicken Sie im Menü am oberen Rand auf **Hilfe** .  
  
3.  Aktivieren Sie die Warnung, indem Sie das Kontrollkästchen **Warnung, wenn ein Abonnement innerhalb des Schwellenwerts abläuft**aktivieren.  
  
4.  Legen Sie in der **Schwellenwert** -Spalte einen Schwellenwert für die Warnung fest Sie können z.B. einen Wert von **70%** in der **Schwellenwert**-Spalte auswählen.  
  
5.  Klicken Sie auf **Änderungen speichern**.  
  
#### <a name="to-configure-an-alert-for-a-threshold"></a>So konfigurieren Sie eine Warnung für einen Schwellenwert  
  
1.  Klicken Sie auf **Warnungen konfigurieren**.  
  
2.  Wählen Sie im Dialogfeld **Replikationswarnungen konfigurieren** eine Warnung aus, und klicken Sie dann auf **Konfigurieren**.  
  
     In diesem Dialogfeld werden Warnungen für alle Veröffentlichungstypen angezeigt – auch für Warnungen, die nichts mit den Überwachungsschwellenwerten zu tun haben. Weitere Informationen finden Sie unter [Verwenden von Warnungen für Replikations-Agentereignisse](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md).  
  
3.  Legen Sie im Dialogfeld **\<Eigenschaften von Warnung AlertName>** die gewünschten Optionen fest:  
  
    -   Klicken Sie auf der Seite **Allgemein** auf **Aktivieren**, und geben Sie an, für welche Datenbank die Warnung gelten soll.  
  
    -   Geben Sie auf der Seite **Antwort** an, ob eine E-Mail gesendet und/oder ein Auftrag ausgeführt werden soll.  
  
    -   Passen Sie auf der Seite **Optionen** den Text der Antwort an.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf **Schließen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Replikation](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
