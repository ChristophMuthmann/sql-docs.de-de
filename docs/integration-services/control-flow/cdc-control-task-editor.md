---
title: "Task-Editor f&#252;r CDC-Steuerelement | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.cdccontroltask.config.f1"
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Task-Editor f&#252;r CDC-Steuerelement
  Im Dialogfeld **Task-Editor für CDC-Steuerelement** können Sie den CDC-Steuerungstask konfigurieren. Die Konfiguration des CDC-Steuerungstasks beinhaltet das Definieren einer Verbindung mit der CDC-Datenbank, des CDC-Taskvorgangs und der Zustandsverwaltungsinformationen.  
  
 Weitere Informationen zum CDC-Steuerungstask finden Sie unter [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 **So öffnen Sie den Task-Editor für CDC-Steuerelement**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]das [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] -Paket, das den CDC-Steuerungstask enthält.  
  
2.  Doppelklicken Sie auf der Registerkarte **Ablaufsteuerung** auf den CDC-Steuerungstask.  
  
## enthalten  
 **ADO.NET-Verbindungs-Manager für die SQL Server-CDC-Datenbank**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder klicken Sie auf **Neu**, um eine neue Verbindung zu erstellen. Die Verbindung muss zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank hergestellt werden, die für CDC aktiviert ist und in der sich die ausgewählte Änderungstabelle befindet.  
  
 **CDC-Steuerungsvorgang**  
 Wählen Sie den Vorgang aus, der für diesen Task ausgeführt werden soll. Für alle Vorgänge wird die Statusvariable verwendet, die in einer SSIS-Paketvariable gespeichert wird, die den Status speichert und zwischen verschiedenen Komponenten im Paket übergibt.  
  
-   **Beginn des anfänglichen Ladevorgangs kennzeichnen**: Dieser Vorgang wird verwendet, wenn der anfängliche Ladevorgang aus einer aktiven Datenbank ohne Momentaufnahme erfolgt. Er wird zu Beginn eines Pakets für das anfängliche Laden verwendet, um die aktuelle LSN in der Quelldatenbank aufzuzeichnen, bevor das Paket für das anfängliche Laden mit dem Lesen der Quelltabellen beginnt. Für diesen Vorgang ist eine Verbindung mit der Quelldatenbank erforderlich.  
  
     Wenn Sie bei Verwendung von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (nicht Oracle) die Option **Beginn des anfänglichen Ladevorgangs kennzeichnen** auswählen, muss als Benutzer im Verbindungs-Manager entweder **db_owner** oder **sysadmin** angegeben sein.  
  
-   **Ende des anfänglichen Ladevorgangs kennzeichnen**: Dieser Vorgang wird verwendet, wenn der anfängliche Ladevorgang aus einer aktiven Datenbank ohne Momentaufnahme erfolgt. Er wird am Ende eines Pakets zum anfänglichen Laden verwendet, um die aktuelle LSN in der Quelldatenbank aufzuzeichnen, nachdem das Paket für das anfängliche Laden das Lesen der Quelltabellen beendet hat. Diese LSN wird durch das Aufzeichnen der aktuellen Zeit, zu der dieser Vorgang aufgetreten ist, und das anschließende Abfragen der `cdc.lsn_time_`-Zuordnungstabelle in der CDC-Datenbank ermittelt. Dabei wird nach einer Änderung gesucht, die nach diesem Zeitpunkt aufgetreten ist.  
  
     Wenn Sie bei Verwendung von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (nicht Oracle) die Option **Ende des anfänglichen Ladevorgangs kennzeichnen** auswählen, muss als Benutzer im Verbindungs-Manager entweder **db_owner** oder **sysadmin** angegeben sein.  
  
-   **CDC-Start kennzeichnen**: Dieser Vorgang wird verwendet, wenn der anfängliche Ladevorgang aus einer Momentaufnahmedatenbank oder einer inaktiven Datenbank erfolgt. Er wird an einem beliebigem Punkt im anfänglich geladenen Paket aufgerufen. Der Vorgang akzeptiert einen Parameter, bei dem es sich um eine Momentaufnahme-LSN oder den Namen einer Momentaufnahmedatenbank (von dem die Momentaufnahme-LSN automatisch abgeleitet wird) handeln kann. Der Parameter kann auch leer gelassen werden. In diesem Fall wird die aktuelle Datenbank-LSN als Start-LSN für das Änderungsverarbeitungspaket verwendet.  
  
     Dieser Vorgang wird anstelle der Vorgänge "Beginn/Ende des anfänglichen Ladevorgangs kennzeichnen" verwendet.  
  
     Wenn Sie bei Verwendung von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC (nicht Oracle) die Option **CDC-Start kennzeichnen** auswählen, muss als Benutzer im Verbindungs-Manager entweder **db_owner** oder **sysadmin** angegeben sein.  
  
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
 Geben Sie den Namen der Statustabelle ein, die zum Speichern des CDC-Status verwendet werden soll. Die angegebene Tabelle muss zwei Spalten mit den Namen **name** und **state** enthalten, und beide Spalten müssen vom Datentyp **varchar (256)** sein.  
  
 Sie können optional auf **Neu** klicken, um ein SQL-Skript abzurufen, das eine neue Statustabelle mit den erforderlichen Spalten erstellt. Bei Auswahl von **Automatische Statuspersistenz** muss der Entwickler eine den obigen Anforderungen entsprechende Statustabelle erstellen.  
  
 Dieses Option ist nur verfügbar, wenn **Automatische Statuspersistenz** ausgewählt ist, und ist ein erforderlicher Parameter.  
  
 **Statusname**  
 Geben Sie einen Namen ein, der dem beständigen CDC-Status zugeordnet werden soll. In den Paketen für das vollständige Laden und den CDC-Paketen, die denselben CDC-Kontext verwenden, wird ein gemeinsamer Statusname angegeben. Dieser Name wird verwendet, um in der Statustabelle nach der Statuszeile zu suchen.  
  
## Siehe auch  
 [Benutzerdefinierte Eigenschaften des CDC-Steuerungstasks](../../integration-services/control-flow/cdc-control-task-custom-properties.md)  
  
  