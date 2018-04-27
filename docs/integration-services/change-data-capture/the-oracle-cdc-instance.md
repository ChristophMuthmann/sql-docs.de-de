---
title: Oracle CDC-Instanz | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03de4078f3ede60ef20e9a8d77b035decd3a4491
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="the-oracle-cdc-instance"></a>Oracle CDC-Instanz
  Die Oracle CDC-Instanz ist ein vom Oracle CDC Service erstellter Prozess zur Verarbeitung der Änderungen, die aus einer einzelnen Oracle-Quelldatenbank aufgezeichnet wurden. Die Oracle CDC-Instanz ruft ihre Konfiguration aus der Tabelle **cdc.xdbcdc_config** ab und verwaltet ihren Status in der Tabelle **cdc.xdbcdc_state** . Diese Tabellen sind Teil der CDC-Datenbank, über die die Oracle CDC-Instanz definiert wird. Weitere Informationen zur Datenbank xdbcdc und zu Tabellen finden Sie unter [The CDC Databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase).  
  
 Im Folgenden werden die Tasks beschrieben, die von der Oracle CDC-Instanz ausgeführt werden:  
  
-   **Durchführen der Startüberprüfung für den Dienst:** Nach dem Starten lädt die CDC-Instanz ihre Konfiguration aus der Tabelle **xdbcdc_config** und führt eine Reihe von Statusüberprüfungen aus. So wird sichergestellt, dass der permanente Status der CDC-Instanz einheitlich ist und dass mit der Verarbeitung der Änderungen begonnen werden kann.  
  
-   **Vorbereiten auf die Änderungsaufzeichnung**: Wenn die Überprüfung erfolgreich ist, scannt die Oracle CDC-Instanz alle momentan definierten Aufzeichnungsinstanzen und bereitet die Oracle LogMiner-Abfragen und andere Unterstützungsstrukturen vor, die für die Änderungsaufzeichnung erforderlich sind. Außerdem lädt die Oracle-Instanz den internen Aufzeichnungsstatus neu, der bei der letzten Ausführung der Oracle CDC-Instanz gespeichert wurde.  
  
-   **Aufzeichnen von Änderungen aus Oracle**: Die Oracle CDC-Instanz fasst Änderungen aus Oracle mithilfe der Oracle LogMiner-Funktion in einem Pool zusammen, sortiert diese nach Transaktionscommit und ändert dann die Uhrzeit in einer Transaktion und schreibt sie in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Änderungstabellen in der CDC-Datenbank.  
  
-   **Herunterfahren des Diensts**: Der Lebenszyklus der Oracle CDC-Instanz wird vom Oracle CDC Service verwaltet. Wenn für die Oracle CDC-Instanz das Herunterfahren angefordert wird, werden die folgenden Tasks ausgeführt:  
  
    -   Das Lesen von Daten aus dem Oracle-Transaktionsprotokoll wird beendet.  
  
    -   Das Schreiben abgeschlossener Oracle-Transaktionen in die CDC-Datenbank wird beendet.  
  
    -   Es wird (falls erforderlich) bis zu 30 Sekunden gewartet, bis die aktuelle Transaktion in die CDC-Datenbank geschrieben wurde. Wenn mehr als 30 Sekunden vergehen, wird der Schreibvorgang abgebrochen und für die Transaktion ein Rollback ausgeführt (um den Vorgang nach dem Neustart der CDC-Instanz wiederholen zu können).  
  
    -   In einem separaten Thread werden so viele im Arbeitsspeicher zwischengespeicherte Datensätze wie möglich für bis zu 30 Sekunden in die Tabelle mit den bereitgestellten Transaktionen geschrieben (von der ältesten bis zur neuesten Transaktion). Anschließend wird die Tabelle **xdbcdc_state** aktualisiert und für alle Änderungen ein Commit ausgeführt.  
  
-   **Durchführen von Konfigurationsänderungen:** Die Oracle CDC-Instanz wird entweder vom CDC Service oder bei Erkennung einer neuen Version in der Tabelle **cdc.xdbcdc_config** über Konfigurationsänderungen benachrichtigt. Für die meisten Änderungen ist kein Neustart der Oracle CDC-Instanz erforderlich (z. B. beim Hinzufügen oder Entfernen von Aufzeichnungsinstanzen). Bei einigen anderen Änderungen, z. B. beim Ändern der Oracle-Verbindungszeichenfolge oder der Anmeldeinformationen, muss jedoch ein Neustart der CDC-Instanz ausgeführt werden.  
  
-   **Durchführen der Wiederherstellung:** Beim Starten einer Oracle CDC-Instanz wird ihr interner Status aus den Tabellen **xdbcdc_state** und **xdbcdc_staged_transactions** wiederhergestellt. Nachdem der Status wiederhergestellt wurde, fährt die CDC-Instanz normal fort.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fehlerbehandlung](../../integration-services/change-data-capture/error-handling.md)  
  
  
