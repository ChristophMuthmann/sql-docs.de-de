---
title: Task „Fehlermeldungen übertragen“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.f1
- sql13.dts.designer.transfererrormessagestask.general.f1
- sql13.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f1e505b971f709124635cb9aa2ecd5bcbaf4f4af
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="transfer-error-messages-task"></a>Fehlermeldungen übertragen (Task)
  Der Task „Fehlermeldungen übertragen“ überträgt eine oder mehrere benutzerdefinierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlermeldungen zwischen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Benutzerdefinierte Meldungen sind Meldungen mit einem Bezeichner gleich oder größer als 50000. Meldungen mit einem Bezeichner kleiner als 50000 sind Systemfehlermeldungen und können nicht mithilfe des Tasks "Fehlermeldungen übertragen" übertragen werden.  
  
 Der Task Fehlermeldungen übertragen kann so konfiguriert werden, dass alle Fehlermeldungen oder nur die angegebenen Fehlermeldungen übertragen werden. Benutzerdefinierte Fehlermeldungen stehen möglicherweise in einer Vielzahl von verschiedenen Sprachen zur Verfügung, und der Task kann so konfiguriert werden, dass nur Meldungen in ausgewählten Sprachen zur Verfügung stehen. Auf dem Zielserver muss eine Version der Meldung in us_english vorhanden sein, die Codepage 1033 verwendet, bevor Sie andere Sprachversionen auf diesen Server übertragen können.  
  
 Die sysmessages-Tabelle in der master-Datenbank enthält alle Fehlermeldungen, sowohl Systemfehlermeldungen als auch benutzerdefinierte Fehlermeldungen, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden.  
  
 Die zu übertragenden benutzerdefinierten Meldungen sind auf dem Ziel möglicherweise schon vorhanden. Eine Fehlermeldung wird als doppelte Fehlermeldung definiert, wenn der Bezeichner und die Sprache identisch sind. Es gibt folgende Möglichkeiten, um den Task "Fehlermeldungen übertragen" zur Verarbeitung bereits vorhandener Fehlermeldungen zu konfigurieren:  
  
-   Vorhandene Fehlermeldungen überschreiben.  
  
-   Der Task erzeugt einen Fehler, wenn doppelte Meldungen vorhanden sind.  
  
-   Doppelte Fehlermeldungen auslassen.  
  
 Zur Laufzeit stellt der Task "Fehlermeldungen übertragen" mithilfe eines oder zweier SMO-Verbindungs-Manager eine Verbindung mit dem Quell- und Zielserver her. Der SMO-Verbindungs-Manager wird unabhängig vom Task "Fehlermeldungen übertragen" konfiguriert, und im Task "Fehlermeldungen übertragen" wird dann darauf verwiesen. Im SMO-Verbindungs-Manager wird der Server sowie der für den Zugriff auf den Server zu verwendende Authentifizierungsmodus angegeben. Weitere Informationen finden Sie unter [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
 Der Task "Fehlermeldungen übertragen" unterstützt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quelle und ein Ziel. Es gibt keinerlei Beschränkungen, welche Version Sie als Quelle oder Ziel verwenden.  
  
## <a name="events"></a>Ereignisse  
 Der Task löst ein Informationsereignis aus, das die Anzahl der übertragenen Fehlermeldungen meldet.  
  
 Der Task "Fehlermeldungen übertragen" meldet keinen schrittweisen Fortschritt der Fehlermeldungsübertragung; er meldet nur 0 % und 100 % der Ausführung.  
  
## <a name="execution-value"></a>Ausführungswert  
 Der in der **ExecutionValue** -Eigenschaft des Tasks definierte Ausführungswert gibt die Anzahl der zu übertragenden Fehlermeldungen zurück. Indem der **ExecValueVariable**-Eigenschaft des Tasks „Fehlermeldung übertragen“ eine benutzerdefinierte Variable zugewiesen wird, können Informationen über die Fehlermeldungsübertragung anderen Objekten im Paket zur Verfügung gestellt werden. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Verwenden von Variablen in Paketen](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Protokolleinträge  
 Der Task "Fehlermeldungen übertragen" enthält die folgenden benutzerdefinierten Protokolleinträge:  
  
-   TransferErrorMessagesTaskStartTransferringObjects   Dieser Protokolleintrag meldet, dass die Übertragung begonnen hat. Der Protokolleintrag enthält die Startzeit.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   Dieser Protokolleintrag meldet das Beenden der Übertragung. Der Protokolleintrag enthält die Beendigungszeit.  
  
 Zusätzlich meldet ein Protokolleintrag für das **OnInformation** -Ereignis die Anzahl der übertragenen Fehlermeldungen. Für jede Fehlermeldung auf dem Ziel, die überschrieben wird, wird außerdem ein Protokolleintrag für das **OnWarning event** geschrieben.  
  
## <a name="security-and-permissions"></a>Sicherheit und Berechtigungen  
 Um neue Fehlermeldungen zu erstellen, muss der Benutzer, von dem das Paket ausgeführt wird, auf dem Zielserver Mitglied der sysadmin- oder serveradmin-Serverrolle sein.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>Konfiguration des Tasks "Fehlermeldungen übertragen"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-error-messages-task-editor-general-page"></a>Editor für den Task Fehlermeldungen übertragen (Seite Allgemein)
  Mithilfe der Seite **Allgemein** des Dialogfelds **Editor für den Task Fehlermeldungen übertragen** können Sie den Task Fehlermeldungen übertragen benennen und beschreiben. Der Task „Fehlermeldungen übertragen“ überträgt eine oder mehrere benutzerdefinierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlermeldungen zwischen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].   
  
### <a name="options"></a>Tastatur  
 **Name**  
 Geben Sie für den Task Fehlermeldungen übertragen einen eindeutigen Namen ein. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung für den Task Fehlermeldungen übertragen ein.  
  
## <a name="transfer-error-messages-task-editor-messages-page"></a>Editor für den Task Fehlermeldungen übertragen (Seite Meldungen)
  Verwenden Sie die Seite **Meldungen** im Dialogfeld **Editor für den Task „Fehlermeldungen übertragen“** , um die Eigenschaften für das Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlermeldungen von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere anzugeben. 
  
### <a name="options"></a>Tastatur  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver herzustellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver herzustellen.  
  
 **IfObjectExists**  
 Wählen Sie aus, ob der Task vorhandene benutzerdefinierte Fehlermeldungen überschreiben, vorhandene Meldungen auslassen oder einen Fehler erzeugen soll, wenn auf dem Zielserver bereits Meldungen desselben Namens vorhanden sind.  
  
 **TransferAllErrorMessages**  
 Wählen Sie aus, ob der Task alle oder nur die angegebenen benutzerdefinierten Meldungen vom Quell- auf den Zielserver kopieren soll.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Wahr**|Alle benutzerdefinierten Meldungen kopieren.|  
|**False**|Nur die angegebenen benutzerdefinierten Meldungen kopieren.|  
  
 **ErrorMessagesList**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , um die zu kopierenden Fehlermeldungen auszuwählen.  
  
> [!NOTE]  
>  Sie müssen **SourceConnection** angeben, bevor Sie eine zu kopierende Fehlermeldung auswählen können.  
  
 **ErrorMessageLanguagesList**  
 Klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , um die Sprachen auszuwählen, für die benutzerdefinierte Fehlermeldungen auf den Zielserver kopiert werden. Auf dem Zielserver muss eine Version der Meldung in us_english (Codepage 1033) vorhanden sein, bevor Sie andere Sprachversionen auf den Server übertragen können.  
  
> [!NOTE]  
>  Sie müssen **SourceConnection** angeben, bevor Sie eine zu kopierende Fehlermeldung auswählen können.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  
