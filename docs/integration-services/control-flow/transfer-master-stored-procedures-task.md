---
title: "In master gespeicherte Prozeduren &#252;bertragen (Task) | Microsoft Docs"
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
  - "sql13.dts.designer.transfermasterspstask.f1"
helpviewer_keywords: 
  - "In master gespeicherte Prozeduren übertragen (Task) [Integration Services]"
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# In master gespeicherte Prozeduren &#252;bertragen (Task)
  Der Task „In 'master' gespeicherte Prozeduren übertragen“ überträgt mindestens eine benutzerdefinierte gespeicherte Prozedur zwischen den **master**-Datenbanken der Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um eine gespeicherte Prozedur von der **master**-Datenbank zu übertragen, muss dbo der Besitzer der gespeicherten Prozedur sein.  
  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" kann zum Übertragen aller gespeicherten Prozeduren oder nur bestimmter gespeicherter Prozeduren konfiguriert werden. Dieser Task kopiert keine gespeicherten Systemprozeduren.  
  
 Die zu übertragenden gespeicherten 'master'-Prozeduren sind eventuell bereits am Ziel vorhanden. Der Task "In 'master' gespeicherte Prozeduren übertragen" kann zur Verarbeitung bereits vorhandener gespeicherter Prozeduren auf folgende Art und Weise konfiguriert werden:  
  
-   Überschreiben bereits vorhandener gespeicherter Prozeduren.  
  
-   Fehlschlagen des Tasks, wenn doppelte gespeicherte Prozeduren vorhanden sind.  
  
-   Überspringen von doppelten gespeicherten Prozeduren.  
  
 Zur Laufzeit stellt der Task "In 'master' gespeicherte Prozeduren übertragen" eine Verbindung mit den Quell- und Zielservern her. Dazu werden die SMO-Verbindungs-Manager verwendet. Die SMO-Verbindungs-Manager werden getrennt vom Task "In 'master' gespeicherte Prozeduren übertragen" konfiguriert. Es wird darauf dann im Task "In 'master' gespeicherte Prozeduren übertragen" verwiesen. Die SMO-Verbindungs-Manager geben den Server- und Authentifizierungsmodus an, der beim Zugriff auf den Server verwendet werden soll. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## Übertragen von gespeicherten Prozeduren zwischen den Instanzen von SQL Server  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" unterstützt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quelle und ein -Ziel.  
  
## Ereignisse  
 Der Task löst ein Informationsereignis aus, das die Anzahl der übertragenen gespeicherten Prozeduren meldet, sowie ein Warnungsereignis, wenn eine gespeicherte Prozedur überschrieben wird.  
  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" meldet keinen schrittweisen Fortschritt der Anmeldeübertragung; er meldet nur 0 % und 100 % der Ausführung.  
  
## Ausführungswert  
 Der Ausführungswert, definiert in der **ExecutionValue** -Eigenschaft des Tasks, gibt die Anzahl der übertragenen gespeicherten Prozeduren zurück. Wenn der **ExecValueVariable**-Eigenschaft des Tasks „In 'master' gespeicherte Prozeduren übertragen“ eine benutzerdefinierte Variable zugewiesen wird, können Informationen über die gespeicherten Prozeduren anderen Objekten im Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md).  
  
## Protokolleinträge  
 Der Task "In 'master' gespeicherte Prozeduren übertragen" enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   TransferStoredProceduresTaskStartTransferringObjects  Dieser Protokolleintrag meldet, dass die Übertragung begonnen hat. Der Protokolleintrag enthält die Startzeit.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  Dieser Protokolleintrag meldet, dass die Übertragung abgeschlossen ist. Der Protokolleintrag enthält die Beendigungszeit.  
  
 Außerdem meldet ein Protokolleintrag für das **OnInformation** -Ereignis die Anzahl der übertragenen gespeicherten Prozeduren, und für das **OnWarning** -Ereignis wird ein Protokolleintrag für jede gespeicherte Prozedur am Ziel geschrieben, der überschrieben wird.  
  
## Sicherheit und Berechtigungen  
 Der Benutzer muss über die Berechtigung zum Anzeigen der Liste mit gespeicherten Prozeduren in der **master**-Datenbank der Quelle verfügen und Mitglied der sysadmin-Serverrolle sein oder über Berechtigungen zum Erstellen von gespeicherten Prozeduren in der **master**-Datenbank auf dem Zielserver verfügen.  
  
## Konfiguration der Tasks "In 'master' gespeicherte Prozeduren übertragen"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „In 'master' gespeicherte Prozeduren übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)  
  
-   [Editor für den Task „In master gespeicherte Prozeduren übertragen“ &#40;Seite „Gespeicherte Prozeduren“&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### Programmgesteuertes Konfigurieren des Tasks "In 'master' gespeicherte Prozeduren übertragen"  
  
## Verwandte Aufgaben  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Siehe auch  
 [SQL Server-Objekte kopieren (Task)](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  