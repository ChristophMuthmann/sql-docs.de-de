---
title: "CDC-Steuerungstask | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.cdccontroltask.f1"
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# CDC-Steuerungstask
  Der CDC-Steuerungstask wird verwendet, um den Lebenszyklus von Change Data Capture-Paketen (CDC) zu steuern. Er behandelt die CDC-Paketsynchronisierung mit dem Paket des erstmaligen Ladens, also die Verwaltung der Bereiche von Protokollfolgenummern (LSNs), die bei einer Ausführung eines CDC-Pakets verarbeitet werden. Außerdem wird der CDC-Steuerungstask für Fehlerszenarien und für die Wiederherstellung verwendet.  
  
 Der CDC-Steuerungstask verwaltet den Status des CDC-Pakets in einer SSIS-Paketvariablen und kann diesen auch in einer Datenbanktabelle dauerhaft speichern, damit der Status über Paketaktivierungen hinweg und zwischen mehreren Paketen beibehalten werden kann, die zusammen einen allgemeinen CDC-Prozess durchführen (ein Task kann z. B. für das erstmalige Laden und ein anderer Task für Trickle-Feed-Updates zuständig sein).  
  
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
  
## Behandeln von CDC-Statuspersistenz  
 Der CDC-Steuerungstask behält zwischen Aktivierungen einen persistenten Status bei. Die im CDC-Status gespeicherten Informationen werden verwendet, um den Verarbeitungsbereich für das CDC-Paket zu bestimmen und zu verwalten und Fehlerzustände zu erkennen. Der persistente Status wird als Zeichenfolge gespeichert. Weitere Informationen finden Sie unter [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md).  
  
 Der CDC-Steuerungstask unterstützt zwei Typen der Statuspersistenz:  
  
-   Manuelle Statuspersistenz: In diesem Fall verwaltet der CDC-Steuerungstask den in einer Paketvariablen gespeicherten Status. Der Paketentwickler muss die Variable vor dem Aufrufen der CDC-Steuerung jedoch aus einem persistenten Speicher lesen und dann in diesen persistenten Speicher zurückschreiben, nachdem die CDC-Steuerung zuletzt aufgerufen und die CDC-Ausführung abgeschlossen wurde.  
  
-   Automatische Statuspersistenz: Der CDC-Status wird in einer Tabelle in einer Datenbank gespeichert. Der Status wird unter einem in der **StateName** -Eigenschaft angegebenen Namen in einer Tabelle gespeichert, die in der **Tabelle für Speicherstatus** -Eigenschaft angegeben ist. Sie befindet sich in einem ausgewählten Verbindungs-Manager zum Speichern des Status. Die Standardeinstellung ist der Quellverbindungs-Manager, aber häufig wird der Zielverbindungs-Manager verwendet. Der CDC-Steuerungstask aktualisiert den Statuswert in der Statustabelle, und dafür wird als Teil der Ambient-Transaktion ein Commit ausgeführt.  
  
## Fehlerbehandlung  
 Der CDC-Steuerungstask meldet möglicherweise in folgenden Fällen einen Fehler:  
  
-   Beim Lesen des persistenten CDC-Status oder beim Aktualisieren des persistenten Status tritt ein Fehler auf.  
  
-   Beim Lesen der aktuellen LSN-Informationen aus der Quelldatenbank tritt ein Fehler auf.  
  
-   Der gelesene CDC-Status ist nicht konsistent.  
  
 In all diesen Fällen meldet der CDC-Steuerungstask einen Fehler, der mithilfe der Standardmethode behandelt werden kann, die SSIS auch für Befehlsflussfehler verwendet.  
  
 Der CDC-Steuerungstask zeigt möglicherweise auch eine Warnung an, wenn der Get Processing Range-Vorgang direkt nach einem anderen Get Processing Range-Vorgang aufgerufen wird, ohne dass Mark Processed Range aufgerufen wird. Dies ist ein Anzeichen dafür, dass bei der vorherigen Ausführung ein Fehler aufgetreten ist oder dass möglicherweise ein anderes CDC-Paket ausgeführt wird und den gleichen CDC-Statusnamen verwendet.  
  
## Konfigurieren des CDC-Steuerungstasks  
 Sie können Eigenschaften programmgesteuert oder mit dem SSIS-Designer festlegen.  
  
## In diesem Abschnitt  
  
-   [Task-Editor für CDC-Steuerelement](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
-   [Benutzerdefinierte Eigenschaften des CDC-Steuerungstasks](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
## Verwandte Aufgaben  
 [Definieren einer Statusvariablen](../../integration-services/data-flow/define-a-state-variable.md)  
  
## Verwandte Inhalte  
  
-   Technischer Artikel [Installieren von Microsoft SQL Server 2012 Change Data Capture für Oracle von Attunity](http://go.microsoft.com/fwlink/?LinkId=252958)auf social.technet.microsoft.com.  
  
-   Technischer Artikel [Troubleshoot Configuration Issues in Microsoft Change Data Capture for Oracle by Attunity](http://go.microsoft.com/fwlink/?LinkId=252960) (Behandeln von Konfigurationsproblemen in Microsoft Change Data Capture für Oracle von Attunity) auf social.technet.microsoft.com.  
  
-   Technischer Artikel [Behandeln von Fehlern bei CDC-Instanzen in Microsoft Change Data Capture für Oracle von Attunity](http://go.microsoft.com/fwlink/?LinkId=252961)auf social.technet.microsoft.com.  
  
  