---
title: CDC-Steuerungstask | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.cdccontroltask.f1
- sql13.ssis.designer.cdccontroltask.config.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 99a864cf9f2e8708fa4e605dacaa7ecaf170ef79
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

---
# <a name="cdc-control-task"></a>CDC-Steuerungstask
  Der CDC-Steuerungstask wird verwendet, um den Lebenszyklus von Change Data Capture-Paketen (CDC) zu steuern. Er behandelt die CDC-Paketsynchronisierung mit dem Paket des erstmaligen Ladens, also die Verwaltung der Bereiche von Protokollfolgenummern (LSNs), die bei einer Ausführung eines CDC-Pakets verarbeitet werden. Außerdem wird der CDC-Steuerungstask für Fehlerszenarien und für die Wiederherstellung verwendet.  
  
 Der CDC-Steuerungstask verwaltet den Status des CDC-Pakets in einer SSIS-Paketvariablen und kann diesen auch in einer Datenbanktabelle dauerhaft speichern, damit der Status über Paketaktivierungen hinweg und zwischen mehreren Paketen beibehalten werden kann, die zusammen einen allgemeinen CDC-Prozess durchführen (ein Task kann z. B. für das erstmalige Laden und ein anderer Task für Trickle-Feed-Updates zuständig sein).  
  
 Der CDC-Steuerungstask unterstützt zwei Gruppen von Vorgängen. Eine Gruppe behandelt die Synchronisierung von erstmaligem Laden und Änderungsverarbeitung, und die andere Gruppe verwaltet den LSN-Bereich für die Änderungsverarbeitung zur Ausführung eines CDC-Pakets und verfolgt, welche Daten erfolgreich verarbeitet wurden.  
  
 Die folgenden Vorgänge behandeln die Synchronisierung von erstmaligem Laden und Änderungsverarbeitung:  
  
|Vorgang|Description|  
|---------------|-----------------|  
|ResetCdcState|Dieser Vorgang wird verwendet, um den persistenten CDC-Status zurückzusetzen, der dem aktuellen CDC-Kontext zugeordnet ist. Nachdem dieser Vorgang ausgeführt wurde, wird die aktuelle höchste LSN aus der LSN-Zeitstempeltabelle `sys.fn_cdc_get_max_lsn` zum Startpunkt für den nächsten Verarbeitungsbereich. Für diesen Vorgang ist eine Verbindung zur Quelldatenbank erforderlich.|  
|MarkInitialLoadStart|Dieser Vorgang wird zu Beginn eines Pakets für das erstmalige Laden verwendet, um die aktuelle LSN in der Quelldatenbank aufzuzeichnen, bevor das Paket für das erstmalige Laden mit dem Lesen der Quelltabellen beginnt. Dies erfordert eine Verbindung zur Quelldatenbank, damit `sys.fn_cdc_get_max_lsn`aufgerufen werden kann.<br /><br /> Wenn Sie bei der Verwendung von CDC in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (d.h. nicht in Oracle) die Option MarkInitialLoadStart auswählen, muss der im Verbindungs-Manager angegebene Benutzer über die Rolle db_owner oder sysadmin verfügen.|  
|MarkInitialLoadEnd|Dieser Vorgang wird am Ende eines Pakets zum erstmaligen Laden verwendet, um die aktuelle LSN in der Quelldatenbank aufzuzeichnen, nachdem das Paket für das erstmalige Laden das Lesen der Quelltabellen beendet hat. Diese LSN wird durch das Aufzeichnen des aktuellen Zeitpunkts, zu dem dieser Vorgang aufgetreten ist, und das anschließende Abfragen der Zuordnungstabelle `cdc.lsn_time_`in der CDC-Datenbank ermittelt. Dabei wird nach einer Änderung gesucht, die nach diesem Zeitpunkt aufgetreten ist.<br /><br /> Wenn Sie bei der Verwendung von CDC in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (d.h. nicht in Oracle) die Option MarkInitialLoadEnd auswählen, muss der im Verbindungs-Manager angegebene Benutzer über die Berechtigung db_owner oder sysadmin verfügen.|  
|MarkCdcStart|Dieser Vorgang wird verwendet, wenn das erstmalige Laden basierend auf einer Momentaufnahmen-Datenbank erfolgt. In diesem Fall sollte die Änderungsverarbeitung unmittelbar nach der Momentaufnahme-LSN starten. Sie können den Namen der zu verwendenden Momentaufnahmen-Datenbank angeben. Der CDC-Steuerungstask fragt [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dann nach der Momentaufnahme-LSN ab. Sie können die Momentaufnahme-LSN auch direkt angeben.<br /><br /> Wenn Sie bei der Verwendung von CDC in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (d.h. nicht in Oracle) die Option MarkCdcStart auswählen, muss der im Verbindungs-Manager angegebene Benutzer über die Berechtigung db_owner oder sysadmin verfügen.|  
  
 Die folgenden Vorgänge werden verwendet, um den Verarbeitungsbereich zu verwalten:  
  
|Vorgang|Description|  
|---------------|-----------------|  
|GetProcessingRange|Dieser Vorgang wird vor dem Aufrufen des Datenflusses verwendet, der den CDC-Quelldatenfluss nutzt. Dabei wird ein Bereich von LSNs eingerichtet, der vom CDC-Quelldatenfluss nach dem Aufrufen gelesen wird. Der Bereich wird in einer SSIS-Paketvariablen gespeichert, die von der CDC-Quelle während der Datenflussverarbeitung verwendet wird.<br /><br /> Weitere Informationen zu den gespeicherten Status finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).|  
|MarkProcessedRange|Dieser Vorgang wird nach jeder CDC-Ausführung ausgeführt (nachdem der CDC-Datenfluss erfolgreich abgeschlossen wurde), um die letzte LSN aufzuzeichnen, die bei der CDC-Ausführung vollständig verarbeitet wurde. Bei der nächsten Ausführung von GetProcessingRange dient diese Position als Startpunkt für den Verarbeitungsbereich.|  
  
## <a name="handling-cdc-state-persistency"></a>Behandeln von CDC-Statuspersistenz  
 Der CDC-Steuerungstask behält zwischen Aktivierungen einen persistenten Status bei. Die im CDC-Status gespeicherten Informationen werden verwendet, um den Verarbeitungsbereich für das CDC-Paket zu bestimmen und zu verwalten und Fehlerzustände zu erkennen. Der persistente Status wird als Zeichenfolge gespeichert. Weitere Informationen finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).  
  
 Der CDC-Steuerungstask unterstützt zwei Typen der Statuspersistenz:  
  
-   Manuelle Statuspersistenz: In diesem Fall verwaltet der CDC-Steuerungstask den in einer Paketvariablen gespeicherten Status. Der Paketentwickler muss die Variable vor dem Aufrufen der CDC-Steuerung jedoch aus einem persistenten Speicher lesen und dann in diesen persistenten Speicher zurückschreiben, nachdem die CDC-Steuerung zuletzt aufgerufen und die CDC-Ausführung abgeschlossen wurde.  
  
-   Automatische Statuspersistenz: Der CDC-Status wird in einer Tabelle in einer Datenbank gespeichert. Der Status wird unter einem in der **StateName** -Eigenschaft angegebenen Namen in einer Tabelle gespeichert, die in der **Tabelle für Speicherstatus** -Eigenschaft angegeben ist. Sie befindet sich in einem ausgewählten Verbindungs-Manager zum Speichern des Status. Die Standardeinstellung ist der Quellverbindungs-Manager, aber häufig wird der Zielverbindungs-Manager verwendet. Der CDC-Steuerungstask aktualisiert den Statuswert in der Statustabelle, und dafür wird als Teil der Ambient-Transaktion ein Commit ausgeführt.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Der CDC-Steuerungstask meldet möglicherweise in folgenden Fällen einen Fehler:  
  
-   Beim Lesen des persistenten CDC-Status oder beim Aktualisieren des persistenten Status tritt ein Fehler auf.  
  
-   Beim Lesen der aktuellen LSN-Informationen aus der Quelldatenbank tritt ein Fehler auf.  
  
-   Der gelesene CDC-Status ist nicht konsistent.  
  
 In all diesen Fällen meldet der CDC-Steuerungstask einen Fehler, der mithilfe der Standardmethode behandelt werden kann, die SSIS auch für Befehlsflussfehler verwendet.  
  
 Der CDC-Steuerungstask zeigt möglicherweise auch eine Warnung an, wenn der Get Processing Range-Vorgang direkt nach einem anderen Get Processing Range-Vorgang aufgerufen wird, ohne dass Mark Processed Range aufgerufen wird. Dies ist ein Anzeichen dafür, dass bei der vorherigen Ausführung ein Fehler aufgetreten ist oder dass möglicherweise ein anderes CDC-Paket ausgeführt wird und den gleichen CDC-Statusnamen verwendet.  
  
## <a name="configuring-the-cdc-control-task"></a>Konfigurieren des CDC-Steuerungstasks  
 Sie können Eigenschaften programmgesteuert oder mit dem SSIS-Designer festlegen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Benutzerdefinierte Eigenschaften CDC-Steuerungstasks](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   Technischer Artikel [Installieren von Microsoft SQL Server 2012 Change Data Capture für Oracle von Attunity](http://go.microsoft.com/fwlink/?LinkId=252958)auf social.technet.microsoft.com.  
  
-   Technischer Artikel [Troubleshoot Configuration Issues in Microsoft Change Data Capture for Oracle by Attunity](http://go.microsoft.com/fwlink/?LinkId=252960)(Behandeln von Konfigurationsproblemen in Microsoft Change Data Capture für Oracle von Attunity) auf social.technet.microsoft.com.  
  
-   Technischer Artikel [Behandeln von Fehlern bei CDC-Instanzen in Microsoft Change Data Capture für Oracle von Attunity](http://go.microsoft.com/fwlink/?LinkId=252961)auf social.technet.microsoft.com.  
  
## <a name="cdc-control-task-editor"></a>Task-Editor für CDC-Steuerelement
  Im Dialogfeld **Task-Editor für CDC-Steuerelement** können Sie den CDC-Steuerungstask konfigurieren. Die Konfiguration des CDC-Steuerungstasks beinhaltet das Definieren einer Verbindung mit der CDC-Datenbank, des CDC-Taskvorgangs und der Zustandsverwaltungsinformationen.  
  
 Weitere Informationen zum CDC-Steuerungstask finden Sie unter [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 **So öffnen Sie den Task-Editor für CDC-Steuerelement**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das den CDC-Steuerungstask enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Ablaufsteuerung** auf den CDC-Steuerungstask.  
  
### <a name="options"></a>enthalten  
 **ADO.NET-Verbindungs-Manager für die SQL Server-CDC-Datenbank**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um eine neue Verbindung zu erstellen. Die Verbindung muss zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank hergestellt werden, die für CDC aktiviert ist und in der sich die ausgewählte Änderungstabelle befindet.  
  
 **CDC-Steuerungsvorgang**  
 Wählen Sie den Vorgang aus, der für diesen Task ausgeführt werden soll. Für alle Vorgänge wird die Statusvariable verwendet, die in einer SSIS-Paketvariable gespeichert wird, die den Status speichert und zwischen verschiedenen Komponenten im Paket übergibt.  
  
-   **Beginn des anfänglichen Ladevorgangs kennzeichnen**: Dieser Vorgang wird verwendet, wenn der anfängliche Ladevorgang aus einer aktiven Datenbank ohne Momentaufnahme erfolgt. Er wird zu Beginn eines Pakets für das anfängliche Laden verwendet, um die aktuelle LSN in der Quelldatenbank aufzuzeichnen, bevor das Paket für das anfängliche Laden mit dem Lesen der Quelltabellen beginnt. Für diesen Vorgang ist eine Verbindung mit der Quelldatenbank erforderlich.  
  
     Wenn Sie bei Verwendung von **CDC (nicht Oracle) die Option** Beginn des anfänglichen Ladevorgangs kennzeichnen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auswählen, muss als Benutzer im Verbindungs-Manager entweder  **db_owner** oder **sysadmin**angegeben sein.  
  
-   **Ende des anfänglichen Ladevorgangs kennzeichnen**: Dieser Vorgang wird verwendet, wenn der anfängliche Ladevorgang aus einer aktiven Datenbank ohne Momentaufnahme erfolgt. Er wird am Ende eines Pakets zum anfänglichen Laden verwendet, um die aktuelle LSN in der Quelldatenbank aufzuzeichnen, nachdem das Paket für das anfängliche Laden das Lesen der Quelltabellen beendet hat. Diese LSN wird durch das Aufzeichnen der aktuellen Zeit, zu der dieser Vorgang aufgetreten ist, und das anschließende Abfragen der `cdc.lsn_time_`-Zuordnungstabelle in der CDC-Datenbank ermittelt. Dabei wird nach einer Änderung gesucht, die nach diesem Zeitpunkt aufgetreten ist.  
  
     Wenn Sie bei Verwendung von **CDC (nicht Oracle) die Option** Ende des anfänglichen Ladevorgangs kennzeichnen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auswählen, muss als Benutzer im Verbindungs-Manager entweder  **db_owner** oder **sysadmin**angegeben sein.  
  
-   **CDC-Start kennzeichnen**: Dieser Vorgang wird verwendet, wenn der anfängliche Ladevorgang aus einer Momentaufnahmedatenbank oder einer inaktiven Datenbank erfolgt. Er wird an einem beliebigem Punkt im anfänglich geladenen Paket aufgerufen. Der Vorgang akzeptiert einen Parameter, bei dem es sich um eine Momentaufnahme-LSN oder den Namen einer Momentaufnahmedatenbank (von dem die Momentaufnahme-LSN automatisch abgeleitet wird) handeln kann. Der Parameter kann auch leer gelassen werden. In diesem Fall wird die aktuelle Datenbank-LSN als Start-LSN für das Änderungsverarbeitungspaket verwendet.  
  
     Dieser Vorgang wird anstelle der Vorgänge "Beginn/Ende des anfänglichen Ladevorgangs kennzeichnen" verwendet.  
  
     Wenn Sie bei Verwendung von **CDC (nicht Oracle) die Option** CDC-Start kennzeichnen [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] auswählen, muss als Benutzer im Verbindungs-Manager entweder  **db_owner** oder **sysadmin**angegeben sein.  
  
-   **Verarbeitungsbereich abrufen**: Dieser Vorgang wird in einem Änderungsverarbeitungspaket vor dem Aufrufen des Datenflusses verwendet, der den CDC-Quelldatenfluss verwendet. Dabei wird ein Bereich von LSNs eingerichtet, der vom CDC-Quelldatenfluss nach dem Aufrufen gelesen wird. Der Bereich wird in einer SSIS-Paketvariablen gespeichert, die von der CDC-Quelle während der Datenflussverarbeitung verwendet wird.  
  
     Weitere Informationen zu den möglichen CDC-Status finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).  
  
-   **Verarbeiteten Bereich kennzeichnen**: Dieser Vorgang wird in einem Änderungsverarbeitungspaket am Ende einer CDC-Ausführung (nachdem der CDC-Datenfluss erfolgreich abgeschlossen wurde) verwendet, um die letzte LSN aufzuzeichnen, die vollständig in der CDC-Ausführung verarbeitet wurde. Bei der nächsten Ausführung von `GetProcessingRange` bestimmt diese Position den Startpunkt für den nächsten Verarbeitungsbereich.  
  
-   **CDC-Status zurücksetzen**: Dieser Vorgang wird verwendet, um den beständigen CDC-Status zurückzusetzen, der dem aktuellen CDC-Kontext zugeordnet ist. Nachdem dieser Vorgang ausgeführt wurde, wird die aktuelle höchste LSN aus der LSN-Zeitstempeltabelle `sys.fn_cdc_get_max_lsn` zum Startpunkt für den nächsten Verarbeitungsbereich. Für diesen Vorgang ist eine Verbindung zur Quelldatenbank erforderlich.  
  
     Dieser Vorgang wird z. B. verwendet, wenn Sie nur die neu erstellten Änderungsdatensätze verarbeiten und alle alten Änderungsdatensätze ignorieren möchten.  
  
 **Variable, die den CDC-Status enthält**  
 Wählen Sie die SSIS-Paketvariable aus, die die Statusinformationen für den Taskvorgang speichert. Sie sollten vor Beginn eine Variable definieren. Wenn Sie **Automatische Statuspersistenz**auswählen, wird die Statusvariable automatisch geladen und gespeichert.  
  
 Weitere Informationen zum Definieren der Statusvariable finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).  
  
 **SQL Server LSN, um CDC zu starten/Name der Momentaufnahme**  
 Geben Sie die aktuelle Quelldatenbank-LSN oder den Namen der Momentaufnahmedatenbank ein, aus der der anfängliche Ladevorgang ausgeführt wird, um die Startposition für CDC zu bestimmen. Diese Option ist nur verfügbar, wenn **CDC-Steuerungsvorgang** auf **CDC-Start kennzeichnen**festgelegt ist.  
  
 Weitere Informationen zu diesen Vorgängen finden Sie unter [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 **Status automatisch in Datenbanktabelle speichern**  
 Aktivieren Sie dieses Kontrollkästchen, damit der CDC-Steuerungstask das Laden und Speichern des CDC-Status in einer in der angegebenen Datenbank enthaltenen Statustabelle automatisch behandelt. Wird dieses Kontrollkästchen nicht aktiviert, muss der Entwickler den CDC-Status beim Start des Pakets laden und bei jeder Änderung des CDC-Status speichern.  
  
 **Verbindungs-Manager für die Datenbank, in der der Status gespeichert wird**  
 Wählen Sie in der Liste einen vorhandenen ADO.NET-Verbindungs-Manager aus, oder klicken Sie auf Neu, um eine neue Verbindung zu erstellen. Es handelt sich hierbei um eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, die die Statustabelle enthält. Die Statustabelle enthält die Statusinformationen.  
  
 Dieses Option ist nur verfügbar, wenn **Automatische Statuspersistenz** ausgewählt ist, und ist ein erforderlicher Parameter.  
  
 **Tabelle zum Speichern des Status**  
 Geben Sie den Namen der Statustabelle ein, die zum Speichern des CDC-Status verwendet werden soll. Die angegebene Tabelle muss zwei Spalten mit den Namen **name** und **state** enthalten, und beide Spalten müssen vom Datentyp **varchar (256)**sein.  
  
 Sie können optional auf **Neu** klicken, um ein SQL-Skript abzurufen, das eine neue Statustabelle mit den erforderlichen Spalten erstellt. Bei Auswahl von **Automatische Statuspersistenz** muss der Entwickler eine den obigen Anforderungen entsprechende Statustabelle erstellen.  
  
 Dieses Option ist nur verfügbar, wenn **Automatische Statuspersistenz** ausgewählt ist, und ist ein erforderlicher Parameter.  
  
 **Statusname**  
 Geben Sie einen Namen ein, der dem beständigen CDC-Status zugeordnet werden soll. In den Paketen für das vollständige Laden und den CDC-Paketen, die denselben CDC-Kontext verwenden, wird ein gemeinsamer Statusname angegeben. Dieser Name wird verwendet, um in der Statustabelle nach der Statuszeile zu suchen.  
  

