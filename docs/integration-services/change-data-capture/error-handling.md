---
title: Fehlerbehandlung | Microsoft-Dokumentation
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
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 95594b1b733db7c1bf96fa9e803ee11b00f1cbb7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="error-handling"></a>Fehlerbehandlung
  Eine Oracle CDC-Instanz führt das Mining für Änderungen einer einzelnen Oracle-Quelldatenbank durch (ein Oracle RAC-Cluster wird als einzelne Datenbank angesehen) und schreibt die Änderungen mit ausgeführtem Commit in Änderungstabellen in einer CDC-Datenbank auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz.  
  
 Eine CDC-Instanz verwaltet ihren Status in einer Systemtabelle mit dem Namen **cdc.xdbcdc_state**. Diese Tabelle kann jederzeit abgefragt werden, um den Status der CDC-Instanz zu ermitteln. Weitere Informationen zur Tabelle „cdc.xdbcdc_state“ finden Sie unter [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state).  
  
 In der Tabelle unten werden die Status der CDC-Instanz in der Tabelle xdbcdc_state beschrieben.  
  
 Für jeden Status werden für die entsprechenden Spalten in der Tabelle cdc.xdbcdc_state die folgenden beiden Angaben gemacht:  
  
-   Instanz ist nicht aktiv (momentan ist kein Windows-Prozess für die Verarbeitung vorhanden). Wenn der Wert der **aktiven Spalte** 1 beträgt, wird ein Unterprozess des Oracle CDC Service ausgeführt, der diese Oracle CDC-Instanz verarbeitet.  
  
-   Wenn der Wert der Spalte **Fehler** 0 beträgt, befindet sich die Oracle CDC-Instanz nicht in einem Fehlerzustand. Wenn der Wert der Spalte **Fehler** 1 beträgt, liegt ein Fehler vor, der die Oracle CDC-Instanz an der Verarbeitung von Änderungen hindert.  
  
     Wenn die Spalte **Fehler** den Wert 1 und die **aktive** Spalte den Wert 1 aufweist, liegt für die Oracle CDC-Instanz ein behebbarer Fehler vor, der automatisch behoben werden kann. Wenn die Spalte Fehler den Wert 1 und die Spalte Aktiv den Wert 0 aufweist, ist in den meisten Fällen eine manuelle Problemumgehung erforderlich, um das Problem vor dem Fortsetzen der Verarbeitung zu beheben.  
  
 In der folgenden Tabelle werden die verschiedenen Statuscodes beschrieben, die von der Oracle CDC-Instanz in ihrer Statustabelle gemeldet werden können.  
  
|Status|Code für Status Aktiv|Code für Status Fehler|Description|Unterstatus|  
|------------|------------------------|-----------------------|-----------------|---------------|  
|ABORTED|0|1|Die Oracle CDC-Instanz wird nicht ausgeführt. Der Unterstatus ABORTED gibt an, dass die Oracle CDC-Instanz ACTIVE war und dann unerwartet beendet wurde.|Der Unterstatus ABORTED wird von der Hauptinstanz des Oracle CDC Service festgelegt, wenn erkannt wird, dass die Oracle CDC-Instanz während des Status ACTIVE nicht ausgeführt wird.|  
|Fehler|0|1|Die Oracle CDC-Instanz wird nicht ausgeführt. Der Status ERROR gibt an, dass die CDC-Instanz ACTIVE war und dann ein Fehler aufgetreten ist, der nicht behebbar ist, sodass die Instanz sich selbst deaktiviert hat.|MISCONFIGURED: Ein nicht behebbarer Konfigurationsfehler wurde erkannt.<br /><br /> PASSWORD-REQUIRED: Für den Change Data Capture Designer für Oracle von Attunity ist kein Kennwort festgelegt, oder das konfigurierte Kennwort ist nicht gültig. Der Grund kann eine Änderung des Kennworts für den asymmetrischen Schlüssel des Diensts sein.|  
|RUNNING|1|0|Die CDC-Instanz wird ausgeführt und verarbeitet Änderungsdatensätze.|IDLE: Alle Änderungsdatensätze wurden verarbeitet und in den Zielsteuertabellen (**_CT**) gespeichert. Es ist keine aktive Transaktion in Verbindung mit den Steuertabellen vorhanden.<br /><br /> PROCESSING: Es werden Änderungsdatensätze verarbeitet, die noch nicht in die Steuertabellen (**_CT**) geschrieben wurden.|  
|STOPPED|0|0|Die CDC-Instanz wird nicht ausgeführt.|Der Unterstatus STOP gibt an, dass die CDC-Instanz ACTIVE war und dann ordnungsgemäß beendet wurde.|  
|SUSPENDED|1|1|Die CDC-Instanz wird ausgeführt, aber die Verarbeitung wurde aufgrund eines behebbaren Fehlers angehalten.|DISCONNECTED: Die Verbindung zur Oracle-Quelldatenbank kann nicht hergestellt werden. Die Verarbeitung wird fortgesetzt, nachdem die Verbindung wiederhergestellt wurde.<br /><br /> STORAGE: Der Speicher ist voll. Die Verarbeitung wird fortgesetzt, wenn Speicher verfügbar wird. In einigen Fällen wird dieser Status möglicherweise nicht angezeigt, weil die Statustabelle nicht aktualisiert werden kann.<br /><br /> LOGGER: Die Protokollierung verfügt über eine Verbindung mit Oracle, kann aber aufgrund eines vorübergehenden Problems die Oracle-Transaktionsprotokolle nicht lesen.|  
|DATAERROR|x|x|Dieser Statuscode wird nur für die Tabelle **xdbcdc_trace** verwendet. Er wird nicht in der Tabelle **xdbcdc_state** angezeigt. Ablaufverfolgungsdatensätze mit diesem Status weisen auf ein Problem mit einem Oracle-Protokolldatensatz hin. Der fehlerhafte Protokolldatensatz wird in der Spalte **data** als BLOB gespeichert.|BADRECORD: Der angefügte Protokolldatensatz konnte nicht analysiert werden.<br /><br /> CONVERT-ERROR: Die Daten in einigen Spalten konnten nicht in die Zielspalten in der Aufzeichnungstabelle konvertiert werden. Dieser Status wird nur angezeigt, wenn in der Konfiguration angegeben ist, dass Konvertierungsfehler zu Ablaufverfolgungsdatensätzen führen sollen.|  
  
 Da der Status des Oracle CDC Service in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert wird, kann es vorkommen, dass der Statuswert in der Datenbank nicht den tatsächlichen Status des Diensts widerspiegelt. Am häufigsten tritt der Fall auf, bei dem der Dienst seine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verliert und diese nicht wiederherstellen kann (aus einem beliebigen Grund). In diesem Fall ist der in **cdc.xdbcdc_state** gespeicherte Status veraltet. Wenn der Zeitstempel der letzten Aktualisierung (UTC) mehr als eine Minute alt ist, ist der Status wahrscheinlich veraltet. Verwenden Sie in diesem Fall die Windows-Ereignisanzeige, um nach weiteren Informationen zum Status des Diensts zu suchen.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 In diesem Abschnitt wird beschrieben, wie der Oracle CDC Service Fehler behandelt.  
  
### <a name="logging"></a>Protokollierung  
 Der Oracle CDC Service erstellt an einem der folgenden Orte Fehlerinformationen.  
  
-   Im Windows-Ereignisprotokoll, das für die Protokollierung von Fehlern und zum Angeben der Lebenszyklusereignisse für den Oracle CDC Service verwendet wird (Starten, Beenden, Herstellen der Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz).  
  
-   In der Tabelle MSXDBCDC.dbo.xdbcdc_trace, die vom Hauptprozess des Oracle CDC Service für die allgemeine Protokollierung und die Ablaufverfolgung verwendet wird.  
  
-   In der Tabelle „\<cdc-database>.cdc.xdbcdc_trace“, die von Oracle CDC-Instanzen für die allgemeine Protokollierung und die Ablaufverfolgung verwendet wird. Dies bedeutet, dass auf eine bestimmte Oracle CDC-Instanz bezogene Fehler in der Ablaufverfolgungstabelle dieser Instanz protokolliert werden.  
  
 Die Informationen werden vom Oracle CDC Service protokolliert, wenn für den Dienst Folgendes gilt:  
  
-   Wird vom Dienstkontroll-Manager gestartet und beendet.  
  
-   Es kann keine Verbindung mit der zugeordneten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz hergestellt werden (und nach dem erfolgreichen Herstellen einer Verbindung nach einem Fehler).  
  
-   Beim Starten von Oracle CDC Service-Instanzen tritt ein Fehler auf.  
  
-   Es wird erkannt, dass eine Oracle CDC-Instanz abgebrochen wurde.  
  
-   Es tritt ein unerwarteter Fehler auf.  
  
 Die Informationen werden von der CDC-Instanz protokolliert, wenn für die Instanz Folgendes gilt:  
  
-   Sie ist aktiviert oder deaktiviert.  
  
-   Es tritt ein Fehler auf.  
  
-   Ein behebbarer Fehler wird behoben.  
  
 Die Ablaufverfolgungstabelle wird auch zum Aufzeichnen von detaillierten Ablaufverfolgungsinformationen für die Problembehandlung verwendet.  
  
### <a name="handling-source-oracle-connection-errors"></a>Behandeln von Fehlern der Oracle-Quellverbindung  
 Der Oracle CDC Service benötigt eine persistente Verbindung mit der Oracle-Quelldatenbank. Viele Verbindungsfehler, die nicht mit der Dienstkonfiguration zusammenhängen (z. B. Netzwerkfehler), werden als vorübergehend angesehen. Wenn der Oracle CDC Service keine Verbindung mit der Oracle-Datenbank herstellen kann (entweder beim Starten oder während der Arbeitsschritte nach einer Trennung der Verbindung), ändert der Dienst seinen Status in SUSPENDED/DISCONNECTED und begibt sich in eine Wiederholungsschleife, in der in regelmäßigen Abständen versucht wird, die Verbindung wiederherzustellen. Nachdem die Verbindung hergestellt wurde, wird die Verarbeitung fortgesetzt.  
  
 Andere Arten von Verbindungsfehlern sind nicht vorübergehend (z. B. ungültige Anmeldeinformationen, unzureichende Berechtigungen und eine ungültige Datenbankadresse). Wenn diese Fehler auftreten, wird der Status des Oracle CDC Service auf ERROR/MISCONFIGURED oder ERROR/PASSWORD-REQUIRED festgelegt, und der Dienst wird deaktiviert. Falls der Benutzer den zugrunde liegenden Fehler behebt, sollte die Oracle CDC-Instanz manuell aktiviert werden, damit die Verarbeitung fortgesetzt werden kann.  
  
 Wenn nicht eindeutig erkennbar ist, ob der Fehler vorübergehend ist, sollte davon ausgegangen werden, dass der vorübergehend ist.  
  
### <a name="handling-target-sql-server-connection-errors"></a>Behandeln von Verbindungsfehlern des SQL Server-Ziels  
 Der Oracle CDC Service benötigt eine persistente Verbindung zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz. Diese Verbindung wird für Folgendes verwendet:  
  
-   Sicherstellen, dass keine anderen Dienste mit dem gleichen Namen diese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz momentan verwenden.  
  
-   Überprüfen, welche Oracle CDC-Instanz aktiviert oder deaktiviert ist, und Starten (oder Beenden) ihres Unterprozesses.  
  
 Wenn der Dienst eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz herstellt und bestätigt, dass dies der einzige Oracle CDC Service mit diesem Namen ist, der aktiv ist, kann er überprüfen, welche Oracle CDC-Instanzen aktiviert sind, und ihre Behandlungsprozesse starten (anschließend beendet der Dienst diese Prozesse, nachdem sie deaktiviert wurden). Die Oracle CDC-Instanzen verwenden ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindungen für die Arbeit mit der CDC-Datenbank der Oracle CDC-Instanz.  
  
 Die Behandlung der Fehler, die für die Verbindung zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ziel auftreten, hängt davon ab, ob die Fehler vorübergehend sind.  
  
 Für bekannte nicht vorübergehende Fehler (z. B. ungültige Anmeldeinformationen, unzureichende Berechtigungen, ungültige Verbindungsinformationen) protokolliert der Dienst einen Fehler im Windows-Ereignisprotokoll und beendet die Ausführung (das Schreiben in die Ablaufverfolgungstabelle ist nicht möglich, weil keine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt werden kann). In diesem Fall muss der Benutzer den Fehler beheben und den Oracle CDC-Windows-Dienst neu starten.  
  
 Für vorübergehende und unerwartete Fehler wird der Vorgang mehrere Male wiederholt, und wenn der Fehler über einen längeren Zeitraum hinweg bestehen bleibt, beendet der CDC Service die Unterprozesse der CDC-Instanzen und kehrt zum ursprünglichen Verbindungsversuch zurück (es kann sein, dass zu diesem Zeitpunkt bereits ein Oracle CDC Service auf einem anderen Computer die Kontrolle über den benannten CDC-Dienst übernommen hat).  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>Behandeln von vollständigen Fehlern des SQL Server-Zielspeichers  
 Wenn der Oracle CDC Service erkennt, dass er keine neuen Änderungsdaten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC-Zieldatenbank einfügen kann, schreibt er eine Warnung in das Ereignisprotokoll und versucht, einen Ablaufverfolgungsdatensatz einzufügen (obwohl dieser möglicherweise aus dem gleichen Grund scheitert). Anschließend wiederholt er den Vorgang in regelmäßigen Abständen, bis dieser erfolgreich ist.  
  
### <a name="handling-oracle-cdc-errors"></a>Behandeln von Oracle CDC-Fehlern  
 Die Oracle CDC-Instanz liest das Oracle-Transaktionsprotokoll und verarbeitet es. Wenn bei der CDC-Verarbeitung ein Fehler auftritt, wird er in der Tabelle **cdc.xdbcdc_state** gemeldet. Der Benutzer muss basierend auf dem gemeldeten Fehler manuell eingreifen.  
  
 Die Oracle CDC-Instanz ist z. B. nicht über einen längeren Zeitraum aktiv, und die erforderlichen Oracle-Transaktionsprotokolldateien sind dann ggf. nicht mehr verfügbar. In diesem Fall muss der Oracle-Datenbankadministrator die erforderlichen Protokolle für die Oracle CDC-Instanz wiederherstellen, damit die Verarbeitung fortgesetzt werden kann.  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>Behandeln von unerwarteten Oracle CDC-Instanzfehlern  
 Der Oracle CDC Service überwacht seine Unterprozesse der CDC-Instanz. Wenn ein Unterprozess der CDC-Instanz abgebrochen wird, deaktiviert der CDC Service diesen in der Tabelle MSXDBCDC.dbo.xdbcdc_databases und aktualisiert seinen cdc.xdbcdc_state-Status auf ABORTED. In diesem Fall wird das standardmäßige Dialogfeld Windows-Fehlerberichterstattung verwendet, um diesen Fehler zur weiteren Analyse zu melden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Change Data Capture Designer für Oracle von Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC-Instanz](../../integration-services/change-data-capture/the-oracle-cdc-instance.md)  
  
  
