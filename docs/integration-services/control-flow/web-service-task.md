---
title: Webdienst (Task) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: d8ebe6e3486cb13440a66383c518c9d306f2984f
ms.contentlocale: de-de
ms.lasthandoff: 08/11/2017

---
# <a name="web-service-task"></a>Webdienst (Task)
  Der Task "Webdienst" führt eine Webdienstmethode aus. Der Task "Webdienst" kann für folgende Zwecke verwendet werden:  
  
-   Schreiben der von einer Webdienstmethode zurückgegebenen Werte in eine Variable. Beispielsweise können Sie die Tageshöchsttemperatur von einer Webdienstmethode abrufen und dann mit diesem Wert eine Variable aktualisieren, die in einem Ausdruck zum Festlegen eines Spaltenwertes verwendet wird.  
  
-   Schreiben der von einer Webdienstmethode zurückgegebenen Werte in eine Datei. Beispielsweise kann eine Liste potenzieller Kunden in eine Datei geschrieben werden. Diese Datei kann dann in einem Paket als Datenquelle verwendet werden, mit dem die Daten vor dem Schreiben in eine Datenbank bereinigt werden.  
  
## <a name="wsdl-file"></a>WSDL-Datei  
 Der Task "Webdienst" verwendet einen HTTP-Verbindungs-Manager, um eine Verbindung mit dem Webdienst herzustellen. Der HTTP-Verbindungs-Manager wird separat vom Task Webdienst konfiguriert, und im Task wird dann darauf verwiesen. Der HTTP-Verbindungs-Manager gibt die Serverproxyeinstellungen an, wie z. B. die Server-URL, Anmeldeinformationen für den Zugriff auf den Webdiensteserver und die Timeoutlänge. Weitere Informationen finden Sie unter [HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Der HTTP-Verbindungs-Manager kann auf eine Website oder eine WSDL-Datei (Web Service Description Language) zeigen. Die URL des HTTP-Verbindungs-Managers, die auf eine WSDL-Datei zeigt, enthält den `?WSDL` -Parameter: beispielsweise `http://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 Die WSDL-Datei muss lokal verfügbar sein, um den Task Webdienst mithilfe des Dialogfelds **Editor für den Task Webdienst** des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers zu konfigurieren.  
  
-   Falls der HTTP-Verbindungs-Manager auf eine Website zeigt, muss die WSDL-Datei manuell auf einen lokalen Computer kopiert werden.  
  
-   Falls der HTTP-Verbindungs-Manager auf eine WSDL-Datei zeigt, kann mit dem Task Webdienst die Datei von der Website in eine lokale Datei heruntergeladen werden.  
  
 In der WSDL-Datei sind die Methoden des Webdienstes, die für die Methoden erforderlichen Eingabeparameter, die von den Methoden zurückgegebenen Antworten und die Kommunikationsmethode mit dem Webdienst aufgelistet.  
  
 Falls die Methode Eingabeparameter verwendet, erfordert der Task Webdienst Parameterwerte. Beispielsweise muss für eine Webdienstmethode, die anhand Ihrer Größe die zu kaufende Skilänge empfiehlt, Ihre Größe mithilfe eines Eingabeparameters übergeben werden. Die Parameterwerte können entweder über im Task definierte Zeichenfolgen oder über im Bereich des Tasks bzw. im übergeordneten Container definierte Variablen übergeben werden. Die Verwendung von Variablen bietet den Vorteil, dass die Parameterwerte über Paketkonfigurationen oder Skripts dynamisch aktualisiert werden können. Weitere Informationen finden Sie unter [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) und [Paketkonfigurationen](../../integration-services/packages/package-configurations.md).  
  
 Viele Webdienstmethoden verwenden keine Eingabeparameter. Beispielsweise ist für eine Webdienstmethode, die die Namen der im aktuellen Monat geborenen Präsidenten abruft, kein Eingabeparameter notwendig, weil der Webdienst den aktuellen Monat lokal bestimmen kann.  
  
 Die Ergebnisse der Webdienstmethode können in eine Variable oder eine Datei geschrieben werden. Mit dem Dateiverbindungs-Manager geben Sie entweder die Datei an oder stellen den Namen der Variablen bereit, in die die Ergebnisse geschrieben werden sollen. Weitere Informationen finden Sie unter [Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md) und [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Verfügbare benutzerdefinierte Meldungen für die Protokollierung für den Task 'Webdienst'  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge aufgelistet, die für den Task 'Webdienst' aktiviert werden können. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**WSTaskBegin**|Der Zugriff auf einen Webdienst wurde begonnen.|  
|**WSTaskEnd**|Eine Webdienstmethode wurde beendet.|  
|**WSTaskInfo**|Beschreibende Informationen zum Task.|  
  
## <a name="configuration-of-the-web-service-task"></a>Konfiguration der Task "Webdienst"  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Programmgesteuerte Konfiguration des Task "Webdienst"  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften zu erhalten:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>Editor für den Task 'Webdienst' (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Editor für den Task 'Webdienst'** können Sie einen HTTP-Verbindungs-Manager und den Speicherort der WSDL-Datei (Web Services Description Language) angeben, die der Task „Webdienst“ verwendet, den Task „Webdienst“ beschreiben und die WSDL-Datei herunterladen.  
  
### <a name="options"></a>enthalten  
 **HTTPConnection**  
 Wählen Sie einen Verbindungs-Manager in der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > um einen neuen Verbindungs-Manager zu erstellen.  
  
> [!IMPORTANT]  
>  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 **Verwandte Themen:** [HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md), [HTTP-Verbindungs-Manager-Editor &#40;Seite Server&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Geben Sie den vollqualifizierten Pfad der auf dem Computer lokalen WSDL-Datei an, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , um nach dieser Datei zu suchen.  
  
 Wenn Sie die WSDL-Datei bereits manuell auf den Computer heruntergeladen haben, wählen Sie diese Datei aus. Wenn die WSDL-Datei jedoch noch nicht heruntergeladen wurde, führen Sie folgende Schritte aus:  
  
-   Erstellen Sie eine leere Datei mit der Dateinamenerweiterung WSDL.  
  
-   Wählen Sie diese leere Datei für die Option **WSDLFile** aus.  
  
-   Legen Sie den Wert von **OverwriteWSDLFile** auf **True** fest, damit die leere Datei mit der tatsächlichen WSDL-Datei überschrieben werden kann.  
  
-   Klicken Sie auf **WSDL herunterladen** , um die tatsächliche WSDL-Datei herunterzuladen und die leere Datei zu überschreiben.  
  
    > [!NOTE]  
    >  Die Option **WSDL herunterladen** wird erst aktiviert, wenn Sie den Namen einer vorhandenen lokalen Datei im Feld **WSDLFile** angeben.  
  
 **OverwriteWSDLFile**  
 Geben Sie an, ob die WSDL-Datei für den Task Webdienst überschrieben werden kann.  
  
 Wenn Sie die WSDL-Datei mithilfe der Schaltfläche **WSDL herunterladen** herunterladen möchten, legen Sie diesen Wert auf **True**fest.  
  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task Webdienst an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks Webdienst ein.  
  
 **WSDL herunterladen**  
 Lädt die WSDL-Datei herunter.  
  
 Diese Schaltfläche wird erst aktiviert, wenn Sie den Namen einer vorhandenen lokalen Datei im Feld **WSDLFile** angeben.  
  
## <a name="web-service-task-editor-input-page"></a>Editor für den Task 'Webdienst' (Seite Eingabe)
  Mithilfe der Seite **Eingabe** des Dialogfelds **Editor für den Task 'Webdienst'** können Sie den Webdienst, die Webmethode sowie die Werte angeben, die der Webmethode als Eingabe zur Verfügung gestellt werden sollen. Die Werte können entweder durch Eingeben von Zeichenfolgen direkt in die Wert-Spalte oder durch Auswählen von Variablen in der Wert-Spalte bereitgestellt werden.  
  
### <a name="options"></a>enthalten  
 **Dienst**  
 Wählen Sie aus der Liste einen Webdienst aus, der zum Ausführen der Webmethode verwendet werden soll.  
  
 **Methode**  
 Wählen Sie für den auszuführenden Task eine Webmethode aus der Liste aus.  
  
 **WebMethodDocumentation**  
 Geben Sie eine Beschreibung der Webmethode ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , und geben Sie anschließend im Dialogfeld **Dokumentation der Webmethode** die Beschreibung ein.  
  
 **Name**  
 Führt die Namen der Eingaben in die Webmethode in einer Liste auf.  
  
 **Typ**  
 Führt die Datentypen der Eingaben in einer Liste auf.  
  
> [!NOTE]  
>  Der Webdiensttask unterstützt nur Parameter der folgenden Datentypen: Grundtypen, wie ganze Zahlen und Zeichenfolgen, Arrays und Sequenzen von Grundtypen sowie Enumerationen.  
  
 **Variable**  
 Aktivieren Sie die Kontrollkästchen, um Variablen für das Bereitstellen von Eingaben zu verwenden.  
  
 **Wert**  
 Wenn die Kontrollkästchen für die Variablen aktiviert sind, wählen Sie die Variablen in der Liste aus, um die Eingaben bereitzustellen. Andernfalls geben Sie die Werte ein, die in den Eingaben verwendet werden sollen.  
  
## <a name="web-service-task-editor-output-page"></a>Editor für den Task 'Webdienst' (Seite Ausgabe)
  Verwenden Sie die Seite **Ausgabe** des Dialogfelds **Editor für den Task 'Webdienst'** , um anzugeben, wo das durch die Webmethode zurückgegebene Ergebnis gespeichert werden soll.  
  
### <a name="static-options"></a>Statische Optionen  
 **OutputType**  
 Wählt den Speichertyp, der beim Speichern der Ergebnisse verwendet werden soll. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**File Connection**|Speichert die Ergebnisse in einer Datei. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Datei**angezeigt.|  
|**Variable**|Speichert die Ergebnisse in einer Variablen. Wenn Sie diesen Wert auswählen, wird die dynamische Option **Variable**angezeigt.|  
  
### <a name="outputtype-dynamic-options"></a>OutputType (dynamische Optionen)  
  
#### <a name="outputtype--file-connection"></a>OutputType = File Connection  
 **File**  
 Wählen Sie einen Dateiverbindungs-Manager in der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>OutputType = Variable  
 **Variable**  
 Wählen Sie eine Variable in der Liste aus, oder klicken Sie auf \< **neue Variable...** > um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Video [Vorgehensweise: Aufrufen eines Webdiensts mit dem Task 'Webdienst' (SQL Server-Video)](http://go.microsoft.com/fwlink/?LinkId=259642)auf technet.microsoft.com.  

