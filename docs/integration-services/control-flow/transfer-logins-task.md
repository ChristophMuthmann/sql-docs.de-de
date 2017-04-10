---
title: "Task &quot;Anmeldungen &#252;bertragen&quot; | Microsoft Docs"
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
  - "sql13.dts.designer.transferloginstask.f1"
helpviewer_keywords: 
  - "Anmeldungen übertragen (Task) [Integration Services]"
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Task &quot;Anmeldungen &#252;bertragen&quot;
  Mit dem Task "Anmeldungen übertragen" wird mindestens eine Anmeldung zwischen den Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übertragen.  
  
## Übertragen von Anmeldungen zwischen den Instanzen von SQL Server  
 Der Task "Anmeldungen übertragen" unterstützt eine Quelle und ein Ziel in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Ereignisse  
 Die Task löst ein Informationsereignis aus, das die Anzahl der übertragenen Anmeldungen meldet, sowie ein Warnungsereignis, wenn eine Anmeldung überschrieben wird.  
  
 Die Task "Anmeldungen übertragen" meldet keinen schrittweisen Fortschritt der Anmeldeübertragung; sie meldet nur 0 % und 100 % der Ausführung.  
  
## Ausführungswert  
 Der Ausführungswert, definiert in der **ExecutionValue** -Eigenschaft der Task, gibt die Anzahl der übertragenen Anmeldungen zurück. Indem der **ExecValueVariable**-Eigenschaft des Tasks „Anmeldungen übertragen“ eine benutzerdefinierte Variable zugewiesen wird, können Informationen über die Anmeldeübertragung anderen Objekten im Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](../Topic/Use%20Variables%20in%20Packages.md).  
  
## Protokolleinträge  
 Die Task "Anmeldungen übertragen" enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   TransferLoginsTaskStarTransferringObjects    Dieser Protokolleintrag meldet, dass die Übertragung begonnen hat. Der Protokolleintrag enthält die Startzeit.  
  
-   TransferLoginsTaskFinishedTransferringObjects   Dieser Protokolleintrag meldet, dass die Übertragung abgeschlossen ist. Der Protokolleintrag enthält die Beendigungszeit.  
  
 Außerdem meldet ein Protokolleintrag für das **OnInformation** -Ereignis die Anzahl der übertragenen Anmeldungen, und für das **OnWarning** -Ereignis wird ein Protokolleintrag für jede Anmeldung im Ziel geschrieben, die überschrieben wird.  
  
## Sicherheit und Berechtigungen  
 Um nach Anmeldungen auf dem Quellserver zu suchen und Anmeldungen auf dem Zielserver zu erstellen, muss der Benutzer Mitglied der sysadmin-Serverrolle auf beiden Servern sein.  
  
## Konfiguration des Tasks "Anmeldungen übertragen"  
 Die Task "Anmeldungen übertragen" kann so konfiguriert werden, dass alle Anmeldungen, nur die angegebenen Anmeldungen oder alle Anmeldungen, die Zugriff auf bestimmte Datenbanken haben, übertragen werden. Die Anmeldung sa kann nicht übertragen werden. Die Anmeldung „sa“ kann umbenannt werden. Die umbenannte Anmeldung „sa“ kann jedoch ebenfalls nicht übertragen werden.  
  
 Sie können auch angeben, ob der Task die mit den Anmeldungen verknüpften Sicherheits-IDs (Security Identification Numbers, SIDs) kopieren soll. Wenn die Task "Anmeldungen übertragen" zusammen mit der Task "Datenbanken übertragen" verwendet wird, müssen die SIDs in das Ziel kopiert werden. Anderenfalls werden die übertragenen Anmeldungen nicht von der Zieldatenbank erkannt.  
  
 Am Ziel werden die übertragenen Anmeldungen deaktiviert, und ihnen werden zufällige Kennwörter zugewiesen. Ein Mitglied der Rolle sysadmin am Zielserver muss die Kennwörter ändern und die Anmeldungen aktivieren, bevor die Anmeldungen verwendet werden können.  
  
 Die zu übertragenden Anmeldungen sind eventuell bereits am Ziel vorhanden. Die Task "Anmeldungen übertragen" kann zur Verarbeitung bereits vorhandener Anmeldungen auf folgende Art und Weise konfiguriert werden:  
  
-   Bereits vorhandene Anmeldungen werden überschrieben.  
  
-   Task schlägt fehl, wenn doppelte Anmeldungen vorhanden sind.  
  
-   Doppelte Anmeldungen werden übersprungen.  
  
 Zur Laufzeit stellt die Task "Anmeldungen übertragen" eine Verbindung mit den Quell- und Zielservern her. Dazu werden die SMO-Verbindungs-Manager verwendet. Die SMO-Verbindungs-Manager werden getrennt von der Task "Anmeldungen übertragen" konfiguriert. Darauf wird dann in der Task "Anmeldungen übertragen" verwiesen. Die SMO-Verbindungs-Manager geben den Server- und Authentifizierungsmodus an, der beim Zugriff auf den Server verwendet werden soll. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task Anmeldungen übertragen &#40;Seite Allgemein&#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)  
  
-   [Editor für den Task Anmeldungen übertragen &#40;Seite Anmeldungen&#41;](../../integration-services/control-flow/transfer-logins-task-editor-logins-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Programmgesteuerte Konfiguration des Tasks "Anmeldungen übertragen"  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  