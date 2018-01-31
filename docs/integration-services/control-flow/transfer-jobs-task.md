---
title: "Aufträge übertragen (Task) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b14cdb7e26c103104e0e98725f00905f75630af
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="transfer-jobs-task"></a>Aufträge übertragen (Task)
  Durch die Task "Aufträge übertragen" werden ein oder mehrere Aufträge des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents zwischen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übertragen.  
  
 Der Task Aufträge übertragen kann so konfiguriert werden, dass alle Aufträge oder nur bestimmte Aufträge übertragen werden. Sie können auch angeben, ob die übertragenen Aufträge auf dem Ziel aktiviert werden sollen.  
  
 Die zu übertragenden Aufträge sind auf dem Ziel möglicherweise schon vorhanden. Es gibt folgende Möglichkeiten, um den Task Aufträge übertragen so zu konfigurieren, dass bereits vorhandene Aufträge behandelt werden:  
  
-   Vorhandene Aufträge werden überschrieben.  
  
-   Der Auftrag erzeugt einen Fehler, wenn doppelte Aufträge vorhanden sind.  
  
-   Doppelte Aufträge werden ausgelassen.  
  
 Zur Laufzeit stellt der Task Aufträge übertragen mithilfe eines oder zweier SMO-Verbindungs-Manager eine Verbindung mit dem Quell- und Zielserver her. Der SMO-Verbindungs-Manager wird unabhängig vom Task Aufträge übertragen konfiguriert, und im Task Aufträge übertragen wird dann darauf verwiesen. Im SMO-Verbindungs-Manager wird der Server sowie der für den Zugriff auf den Server zu verwendende Authentifizierungsmodus angegeben. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Übertragen von Aufträgen zwischen Instanzen von SQL Server  
 Die Task "Aufträge übertragen" unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quellen und -Ziele. Es gibt keinerlei Beschränkungen, welche Version Sie als Quelle oder Ziel verwenden.  
  
## <a name="events"></a>Ereignisse  
 Der Task Aufträge übertragen löst ein Informationsereignis aus, in dem die Anzahl der übertragenen Aufträge angegeben ist, und ein Warnungsereignis, wenn ein Auftrag überschrieben wird. Während der Auftrag übertragen wird, werden keine Angaben zum Fortschritt des Vorgangs gemacht – es wird lediglich 0 % und bei Abschluss 100 % angezeigt.  
  
## <a name="execution-value"></a>Ausführungswert  
 Der in der **ExecutionValue** -Eigenschaft des Tasks definierte Ausführungswert gibt die Anzahl der zu übertragenden Aufträge zurück. Mithilfe einer benutzerdefinierten Variable, die der **ExecValueVariable**-Eigenschaft des Tasks Aufträge übertragen zugewiesen wird, können Informationen zur Auftragsübertragung für andere Objekte des Pakets verfügbar gemacht werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Protokolleinträge  
 Der Task Aufträge übertragen enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   TransferJobsTaskStarTransferringObjects   Dieser Protokolleintrag gibt an, dass die Übertragung gestartet wurde. Der Protokolleintrag enthält die Startzeit.  
  
-   TransferJobsTaskFinishedTransferringObjects    Dieser Protokolleintrag gibt an, dass die Übertragung abgeschlossen wurde. Der Protokolleintrag enthält die Beendigungszeit.  
  
 Außerdem gibt ein Protokolleintrag für das **OnInformation** -Ereignis die Anzahl der übertragenen Aufträge an. Schließlich wird ein Protokolleintrag für das **OnWarning** -Ereignis für jeden auf dem Ziel überschriebenen Auftrag erstellt.  
  
## <a name="security-and-permissions"></a>Sicherheit und Berechtigungen  
 Zum Übertragen von Aufträgen muss der Benutzer sowohl in der Quell- als auch in der Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Mitglied der festen Serverrolle sysadmin oder einer der festen Datenbankrollen für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent der msdb-Datenbank sein.  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Konfiguration des Tasks "Aufträge übertragen"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf folgendes Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften zu erhalten:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>Editor für den Task Aufträge übertragen (Seite Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Editor für den Task Aufträge übertragen** können Sie den Task Aufträge übertragen benennen und beschreiben.  
  
> [!NOTE]  
>  Nur Mitglieder der festen Serverrolle **sysadmin** oder einer der festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents auf dem Zielserver können dort erfolgreich Aufträge erstellen. Um auf dem Quellserver auf Aufträge zuzugreifen, müssen Benutzer auf dem Server Mitglied mindestens einer festen Datenbankrolle **SQLAgentUserRole** sein. Weitere Informationen zu festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
### <a name="options"></a>Tastatur  
 **Name**  
 Geben Sie für den Task Aufträge übertragen einen eindeutigen Namen ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung des Tasks Aufträge übertragen ein.  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>Editor für den Task Aufträge übertragen (Seite Aufträge)
  Auf der Seite **Aufträge** des Dialogfelds **Editor für den Task "Aufträge übertragen"** können Sie die Eigenschaften für das Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentaufträgen von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere angeben.  
  
> [!NOTE]  
>  Um auf dem Quellserver auf Aufträge zuzugreifen, müssen Benutzer auf dem Server Mitglied mindestens einer festen Serverrolle **SQLAgentUserRole** sein. Um auf dem Zielserver Aufträge erfolgreich zu erstellen, muss der Benutzer Mitglied der festen Datenbankrolle **sysadmin** oder einer der festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents sein. Weitere Informationen zu den festen Datenbankrollen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents und zu deren Berechtigungen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
### <a name="options"></a>Tastatur  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver herzustellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver herzustellen.  
  
 **TransferAllJobs**  
 Wählen Sie aus, ob der Task alle oder nur angegebene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agentaufträge vom Quell- auf den Zielserver kopieren soll.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Wahr**|Kopiert alle Aufträge.|  
|**False**|Kopiert nur angegebene Aufträge.|  
  
 **JobsList**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(...)** , um die zu kopierenden Aufträge auszuwählen. Es muss mindestens ein Auftrag ausgewählt werden.  
  
> [!NOTE]  
>  Geben Sie vor der Auswahl der zu kopierenden Aufträge **SourceConnection** an.  
  
 Die Option **JobsList** ist nicht verfügbar, wenn **TransferAllJobs** auf **True**festgelegt ist.  
  
 **IfObjectExists**  
 Wählen Sie aus, wie der Task Aufträge behandeln soll, die auf dem Zielserver bereits mit demselben Namen vorhanden sind.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**FailTask**|Der Task schlägt fehl, wenn auf dem Zielserver bereits Aufträge mit demselben Namen vorhanden sind.|  
|**Overwrite**|Der Task überschreibt auf dem Zielserver Aufträge mit demselben Namen.|  
|**Skip**|Der Task lässt Aufträge aus, die auf dem Zielserver mit demselben Namen vorhanden sind.|  
  
 **EnableJobsAtDestination**  
 Wählen Sie aus, ob die auf den Zielserver kopierten Aufträge aktiviert werden sollen.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Wahr**|Aktiviert Jobs auf dem Zielserver.|  
|**False**|Deaktiviert Jobs auf dem Zielserver.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
