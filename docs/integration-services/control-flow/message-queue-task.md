---
title: "Nachrichtenwarteschlange (Task) | Microsoft Docs"
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
  - "sql13.dts.designer.messagequeuetask.f1"
helpviewer_keywords: 
  - "Nachrichtenwarteschlange (Task) [Integration Services]"
  - "Empfangen von Nachrichten"
  - "Nachrichten [Integration Services]"
  - "Senden von Nachrichten"
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
caps.latest.revision: 68
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 68
---
# Nachrichtenwarteschlange (Task)
  Mit dem Task „Nachrichtenwarteschlange“ können Sie Message Queuing (MSMQ) verwenden, um Nachrichten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen zu senden und zu empfangen oder um Nachrichten an eine Anwendungswarteschlange zu senden, die von einer benutzerdefinierten Anwendung verarbeitet wird. Bei diesen Nachrichten kann es sich um einfachen Text, Dateien oder Variablen und deren Werte handeln.  
  
 Mit dem Task Nachrichtenwarteschlange können Sie Vorgänge im gesamten Unternehmen koordinieren. Nachrichten können in eine Warteschlange eingereiht und später übermittelt werden, falls das Ziel nicht verfügbar oder ausgelastet ist. Beispielsweise können mit diesem Task Nachrichten für den Offlinelaptopcomputer von Vertriebsmitarbeitern, die ihre Nachrichten beim Herstellen einer Verbindung mit dem Netzwerk erhalten, einer Warteschlange hinzugefügt werden. Der Task Nachrichtenwarteschlange kann für folgende Zwecke verwendet werden:  
  
-   Verzögern der Taskausführung bis zum Einchecken anderer Pakete. Beispielsweise sendet an jedem Einzelhandelsstandort ein Task Nachrichtenwarteschlange nach der nächtlichen Wartung eine Nachricht an Ihren Firmencomputer. Ein Paket, das auf dem Firmencomputer ausgeführt wird, enthält Tasks Nachrichtenwarteschlange, die auf die Nachricht von einem bestimmten Einzelhandelsstandort warten. Beim Eintreffen einer Nachricht werden von einem Task Daten von diesem Standort hochgeladen. Nach dem Einchecken aller Standorte berechnet das Paket die Gesamtbeträge.  
  
-   Senden von Datendateien an den Computer, der diese verarbeitet. Beispielsweise kann der Kassenstand eines Restaurants in einer Datendateinachricht an das Buchhaltungssystem des Unternehmens gesendet werden, um Daten zum Trinkgeld jedes Kellners zu extrahieren.  
  
-   Verteilen von Dateien im gesamten Unternehmen. Beispielsweise kann ein Paket einen Task Nachrichtenwarteschlange verwenden, um eine Paketdatei an einen anderen Computer zu senden. Ein Paket, das auf dem Zielcomputer ausgeführt wird, kann mit einem Task Nachrichtenwarteschlange das Paket lokal abrufen und speichern.  
  
 Beim Senden oder Empfangen von Nachrichten verwendet der Task Nachrichtenwarteschlange einen von vier Nachrichtentypen: Datendatei, Zeichenfolge, Zeichenfolgennachricht an Variable oder Variable. Der Nachrichtentyp Zeichenfolgennachricht an Variable kann nur zum Empfangen von Nachrichten verwendet werden.  
  
 Dieser Task verwendet einen MSMQ-Verbindungs-Manager, um eine Verbindung mit einer Nachrichtenwarteschlange herzustellen. Weitere Informationen finden Sie unter [MSMQ-Verbindungs-Manager](../../integration-services/connection-manager/msmq-connection-manager.md). Weitere Informationen zu Message Queuing finden Sie in der [MSDN Library](http://go.microsoft.com/fwlink/?LinkId=7022).  
  
 Für den Task Nachrichtenwarteschlange muss der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst installiert sein. Manche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponenten, die Sie für die Installation auf der Seite **Zu installierende Komponenten** oder der Seite **Funktionsauswahl** des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auswählen können, installieren eine Teilmenge der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten. Diese Komponenten sind für bestimmte Tasks hilfreich, aber die Funktionalität von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ist begrenzt. Beispielsweise installiert die [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] -Option [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponenten, die zum Entwerfen eines Pakets erforderlich sind, aber der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Dienst wird nicht installiert. Deshalb kann der Task Nachrichtenwarteschlange nicht ausgeführt werden. Um eine vollständige Installation von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]sicherzustellen, müssen Sie [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] auf der Seite **Zu installierende Komponenten** auswählen. Weitere Informationen zum Installieren und Ausführen des Tasks „Nachrichtenwarteschlange“ finden Sie unter [Installieren von Integration Services](../../integration-services/install-windows/install-integration-services.md).  
  
> [!NOTE]  
>  Der Task Nachrichtenwarteschlange entspricht nicht dem Federal Information Processing Standard (FIPS) 140-2, wenn das Betriebssystem des Computers im FIPS-Modus konfiguriert ist und der Task die Verschlüsselung verwendet. Wenn der Task Nachrichtenwarteschlange keine Verschlüsselung verwendet, kann der Task erfolgreich ausgeführt werden.  
  
## Nachrichtentypen  
 Es gibt folgende Möglichkeiten, um die Nachrichtentypen zu konfigurieren, die der Task Nachrichtenwarteschlange bereitstellt:  
  
-   **Data file** gibt an, dass eine Datei die Nachricht enthält. Wenn Sie Nachrichten empfangen, können Sie den Task so konfigurieren, dass die Datei gespeichert wird und eine vorhandene Datei überschreiben wird, und das Paket angeben, von dem der Task Nachrichten empfangen kann.  
  
-   **String** definiert die Nachricht als Zeichenfolge. Wenn Sie Nachrichten empfangen, können Sie den Task so konfigurieren, dass die empfangene Zeichenfolge mit einer benutzerdefinierten Zeichenfolge verglichen und abhängig vom Vergleich die entsprechende Maßnahme ergriffen wird. Ein Zeichenfolgenvergleich kann genau sein, die Groß-/Kleinschreibung beachten oder die Groß-/Kleinschreibung ignorieren sowie eine Teilzeichenfolge verwenden.  
  
-   **String message to variable** gibt die Quellnachricht als Zeichenfolge an, die an eine Zielvariable gesendet wird. Sie können den Task so konfigurieren, dass die empfangene Zeichenfolge mit einer benutzerdefinierten Zeichenfolge mithilfe eines genauen Vergleichs, eines Vergleichs mit Beachtung der Groß-/Kleinschreibung oder eines Teilzeichenfolge-Vergleichs verglichen wird. Dieser Nachrichtentyp ist nur verfügbar, wenn der Task Nachrichten empfängt.  
  
-   **Variable** gibt an, dass die Nachricht mindestens eine Variable enthält. Sie können den Task so konfigurieren, dass die in der Nachricht enthaltenen Namen der Variablen angegeben werden. Wenn Sie Nachrichten empfangen, können Sie den Task so konfigurieren, dass sowohl das Paket, von dem Nachrichten empfangen werden können, als auch die Variable, die das Ziel der Nachricht ist, angegeben werden.  
  
## Senden von Nachrichten  
 Beim Konfigurieren des Tasks Nachrichtenwarteschlange zum Senden von Nachrichten können Sie einen der zurzeit von der Message Queuing-Technologie unterstützten Verschlüsselungsalgorithmen, RC2 und RC4, zum Verschlüsseln der Nachricht verwenden. Diese Verschlüsselungsalgorithmen werden inzwischen im Vergleich zu neueren Algorithmen, die von der Message Queuing-Technologie noch nicht unterstützt werden, beide als kryptografisch schwach betrachtet. Daher sollten Sie Ihren Kryptografiebedarf sorgfältig überdenken, wenn Sie Nachrichten mithilfe des Tasks Nachrichtenwarteschlange senden.  
  
## Empfangen von Nachrichten  
 Beim Empfangen von Nachrichten kann der Task Nachrichtenwarteschlange wie folgt konfiguriert werden.  
  
-   Umgehen der Nachricht oder Entfernen der Nachricht aus der Warteschlange.  
  
-   Angeben eines Timeouts.  
  
-   Fehler bei einem Timeout.  
  
-   Überschreiben einer vorhandenen Datei, falls die Nachricht in einer **Data file**gespeichert ist.  
  
-   Speichern der Nachrichtendatei unter einem anderen Dateinamen, falls die Nachricht den Typ **Data file message** verwendet.  
  
## Verfügbare benutzerdefinierte Meldungen für die Protokollierung für den Task 'Nachrichtenwarteschlange'  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den Task Nachrichtenwarteschlange aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**MSMQAfterOpen**|Zeigt an, dass das Öffnen der Warteschlange beendet wurde.|  
|**MSMQBeforeOpen**|Zeigt an, dass das Öffnen der Warteschlange begonnen wurde.|  
|**MSMQBeginReceive**|Zeigt an, dass das Empfangen einer Meldung begonnen wurde.|  
|**MSMQBeginSend**|Zeigt an, dass das Senden einer Meldung begonnen wurde.|  
|**MSMQEndReceive**|Zeigt an, dass das Empfangen einer Meldung beendet wurde.|  
|**MSMQEndSend**|Zeigt an, dass das Senden einer Meldung beendet wurde.|  
|**MSMQTaskInfo**|Enthält beschreibende Informationen zum Task.|  
|**MSMQTaskTimeOut**|Zeigt an, dass beim Task ein Timeout eingetreten ist.|  
  
## Konfiguration des Tasks "Nachrichtenwarteschlange"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen. Klicken Sie auf eines der folgenden Themen, um Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/message-queue-task-editor-general-page.md)  
  
-   [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Empfangen“&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)  
  
-   [Editor für den Task „Nachrichtenwarteschlange“ &#40;Seite „Senden“&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften finden Sie in der Dokumentation zur **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** -Klasse im Entwicklerhandbuch.  
  
## Verwandte Aufgaben  
 Weitere Informationen zum Anzeigen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer finden Sie unter [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
## Siehe auch  
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  