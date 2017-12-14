---
title: "In master gespeicherte Prozeduren übertragen (Task) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfermasterspstask.f1
- sql13.dts.designer.transferstoredprocedurestask.general.f1
- sql13.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords: Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3028cc454a6957672a0c0fd9f34ce5582849dd1f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="transfer-master-stored-procedures-task"></a>In master gespeicherte Prozeduren übertragen (Task)
  Der Task „In 'master' gespeicherte Prozeduren übertragen“ überträgt mindestens eine benutzerdefinierte gespeicherte Prozedur zwischen den **master** -Datenbanken der Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um eine gespeicherte Prozedur von der **master** -Datenbank zu übertragen, muss dbo der Besitzer der gespeicherten Prozedur sein.  
  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" kann zum Übertragen aller gespeicherten Prozeduren oder nur bestimmter gespeicherter Prozeduren konfiguriert werden. Dieser Task kopiert keine gespeicherten Systemprozeduren.  
  
 Die zu übertragenden gespeicherten 'master'-Prozeduren sind eventuell bereits am Ziel vorhanden. Der Task "In 'master' gespeicherte Prozeduren übertragen" kann zur Verarbeitung bereits vorhandener gespeicherter Prozeduren auf folgende Art und Weise konfiguriert werden:  
  
-   Überschreiben bereits vorhandener gespeicherter Prozeduren.  
  
-   Fehlschlagen des Tasks, wenn doppelte gespeicherte Prozeduren vorhanden sind.  
  
-   Überspringen von doppelten gespeicherten Prozeduren.  
  
 Zur Laufzeit stellt der Task "In 'master' gespeicherte Prozeduren übertragen" eine Verbindung mit den Quell- und Zielservern her. Dazu werden die SMO-Verbindungs-Manager verwendet. Die SMO-Verbindungs-Manager werden getrennt vom Task "In 'master' gespeicherte Prozeduren übertragen" konfiguriert. Es wird darauf dann im Task "In 'master' gespeicherte Prozeduren übertragen" verwiesen. Die SMO-Verbindungs-Manager geben den Server- und Authentifizierungsmodus an, der beim Zugriff auf den Server verwendet werden soll. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>Übertragen von gespeicherten Prozeduren zwischen den Instanzen von SQL Server  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" unterstützt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quelle und ein -Ziel.  
  
## <a name="events"></a>Ereignisse  
 Der Task löst ein Informationsereignis aus, das die Anzahl der übertragenen gespeicherten Prozeduren meldet, sowie ein Warnungsereignis, wenn eine gespeicherte Prozedur überschrieben wird.  
  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" meldet keinen schrittweisen Fortschritt der Anmeldeübertragung; er meldet nur 0 % und 100 % der Ausführung.  
  
## <a name="execution-value"></a>Ausführungswert  
 Der Ausführungswert, definiert in der **ExecutionValue** -Eigenschaft des Tasks, gibt die Anzahl der übertragenen gespeicherten Prozeduren zurück. Wenn der **ExecValueVariable**-Eigenschaft des Tasks „In 'master' gespeicherte Prozeduren übertragen“ eine benutzerdefinierte Variable zugewiesen wird, können Informationen über die gespeicherten Prozeduren anderen Objekten im Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Protokolleinträge  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   TransferStoredProceduresTaskStartTransferringObjects  Dieser Protokolleintrag meldet, dass die Übertragung begonnen hat. Der Protokolleintrag enthält die Startzeit.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  Dieser Protokolleintrag meldet, dass die Übertragung abgeschlossen ist. Der Protokolleintrag enthält die Beendigungszeit.  
  
 Außerdem meldet ein Protokolleintrag für das **OnInformation** -Ereignis die Anzahl der übertragenen gespeicherten Prozeduren, und für das **OnWarning** -Ereignis wird ein Protokolleintrag für jede gespeicherte Prozedur am Ziel geschrieben, der überschrieben wird.  
  
## <a name="security-and-permissions"></a>Sicherheit und Berechtigungen  
 Der Benutzer muss über die Berechtigung zum Anzeigen der Liste mit gespeicherten Prozeduren in der **master** -Datenbank der Quelle verfügen und Mitglied der sysadmin-Serverrolle sein oder über Berechtigungen zum Erstellen von gespeicherten Prozeduren in der **master** -Datenbank auf dem Zielserver verfügen.  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Konfiguration der Tasks "In 'master' gespeicherte Prozeduren übertragen"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>Programmgesteuertes Konfigurieren des Tasks "In 'master' gespeicherte Prozeduren übertragen"  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-master-stored-procedures-task-editor-general-page"></a>Editor für den Task 'In 'master' gespeicherte Prozeduren übertragen' (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Editor für den Task "In 'master' gespeicherte Prozeduren übertragen"** können Sie einen Namen und eine Beschreibung für den Task angeben.  
  
> [!NOTE]  
>  Dieser Task überträgt lediglich die benutzerdefinierten gespeicherten Prozeduren des **dbo** -Besitzers aus einer **master** -Datenbank auf dem Quellserver in eine **master** -Datenbank auf dem Zielserver. Benutzer müssen die CREATE PROCEDURE-Berechtigung für die **master** -Datenbank des Zielservers besitzen oder Mitglieder der festen Serverrolle **sysadmin** auf dem Zielserver sein, um dort gespeicherte Prozeduren erstellen zu können.  
  
### <a name="options"></a>enthalten  
 **Name**  
 Geben Sie für den Task 'In 'master' gespeicherte Prozeduren übertragen einen eindeutigen Namen ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung für den Task 'In 'master' gespeicherte Prozeduren übertragen ein.  
  
## <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor für den Task 'In 'master' gespeicherte Prozeduren übertragen' (Seite Gespeicherte Prozeduren)
  Verwenden Sie die Seite **Gespeicherte Prozeduren** im Dialogfeld **Editor für den Task „In 'master' gespeicherte Prozeduren übertragen“** , um die Eigenschaften für das Kopieren einer oder mehrerer benutzerdefinierter gespeicherter Prozeduren aus der **master** -Datenbank einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in die **master** -Datenbank einer anderen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu kopieren.  
  
> [!NOTE]  
>  Dieser Task überträgt lediglich die benutzerdefinierten gespeicherten Prozeduren des **dbo** -Besitzers aus einer **master** -Datenbank auf dem Quellserver in eine **master** -Datenbank auf dem Zielserver. Benutzer müssen die CREATE PROCEDURE-Berechtigung für die **master** -Datenbank des Zielservers besitzen oder Mitglieder der festen Serverrolle **sysadmin** auf dem Zielserver sein, um dort gespeicherte Prozeduren erstellen zu können.  
  
### <a name="options"></a>enthalten  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver herzustellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver herzustellen.  
  
 **IfObjectExists**  
 Wählen Sie aus, wie der Task benutzerdefinierte gespeicherte Prozeduren behandeln soll, die in der **master** -Datenbank auf dem Zielserver bereits mit demselben Namen vorhanden sind.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**FailTask**|Der Task schlägt fehl, wenn in der **master** -Datenbank auf dem Zielserver bereits gespeicherte Prozeduren mit demselben Namen vorhanden sind.|  
|**Overwrite**|Der Task überschreibt bereits vorhandene gespeicherte Prozeduren mit demselben Namen in der **master** -Datenbank auf dem Zielserver.|  
|**Skip**|Der Task lässt bereits vorhandene gespeicherte Prozeduren mit demselben Namen in der **master** -Datenbank auf dem Zielserver aus.|  
  
 **TransferAllStoredProcedures**  
 Wählen Sie aus, ob alle benutzerdefinierten gespeicherten Prozeduren in der **master** -Datenbank auf dem Quellserver auf den Zielserver kopiert werden sollen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Kopiert alle benutzerdefinierten gespeicherten Prozeduren in der **master** -Datenbank.|  
|**False**|Kopiert nur die angegebenen gespeicherten Prozeduren.|  
  
 **StoredProceduresList**  
 Wählen Sie aus, welche benutzerdefinierten gespeicherten Prozeduren in der **master** -Datenbank auf dem Quellserver in die **master** -Datenbank auf dem Zielserver kopiert werden sollen. Diese Option ist nur verfügbar, wenn **TransferAllStoredProcedures** auf **FALSE**festgelegt ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Objekte kopieren (Task)](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
