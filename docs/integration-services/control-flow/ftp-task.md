---
title: "FTP-Task | Microsoft Docs"
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
  - "sql13.dts.designer.ftptask.f1"
helpviewer_keywords: 
  - "FTP-Task [Integration Services]"
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 52
---
# FTP-Task
  Mit dem FTP-Task werden Datendateien heruntergeladen und hochgeladen sowie Verzeichnisse auf Servern verwaltet. Beispielsweise kann ein Paket Datendateien von einem Remoteserver oder einem Internetstandort als Teil eines Paket-Workflows von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] herunterladen. Der FTP-Task kann für folgende Zwecke verwendet werden:  
  
-   Kopieren von Verzeichnissen und Datendateien zwischen Verzeichnissen, vor oder nach dem Verschieben von Daten, sowie Anwenden von Transformationen auf die Daten.  
  
-   Anmelden bei einer FTP-Quelladresse und Kopieren von Dateien oder Paketen in ein Zielverzeichnis.  
  
-   Das Herunterladen von Dateien von einer FTP-Adresse und Anwenden von Transformationen auf Spaltendaten, bevor die Daten in eine Datenbank geladen werden.  
  
 Zur Laufzeit stellt der FTP-Task mithilfe eines FTP-Verbindungs-Managers eine Verbindung mit einem Server her. Der FTP-Verbindungs-Manager wird separat vom FTP-Task konfiguriert, und im FTP-Task wird dann darauf verwiesen. Der FTP-Verbindungs-Manager schließt die Servereinstellungen, die Anmeldeinformationen für den Zugriff auf den FTP-Server ein sowie Optionen wie z. B. das Timeout und die Anzahl von Verbindungsversuchen mit dem Server. Weitere Informationen finden Sie unter [FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
> [!IMPORTANT]  
>  Der FTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Für den Zugriff auf eine lokale Datei oder ein lokales Verzeichnis verwendet der FTP-Task einen Dateiverbindungs-Manager oder Pfadinformationen, die in einer Variablen gespeichert sind. Dagegen verwendet der FTP-Task für den Zugriff auf eine Remotedatei oder ein Remoteverzeichnis einen direkt eingegebenen Pfad auf dem Remoteserver, der im FTP-Verbindungs-Manager angegeben ist, oder in einer Variablen gespeicherte Pfadinformationen. Weitere Informationen finden Sie unter [Dateiverbindungs-Manager](../../integration-services/connection-manager/file-connection-manager.md) und [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
 Dies bedeutet, dass mit dem FTP-Task mehrere Dateien empfangen und mehrere Remotedateien gelöscht werden können. Mit diesem Task kann jedoch nur eine Datei gesendet und eine lokale Datei gelöscht werden, falls ein Verbindungs-Manager verwendet wird. Ein Dateiverbindungs-Manager kann nämlich nur auf eine Datei zugreifen. Für den Zugriff auf mehrere lokale Dateien muss der FTP-Task eine Variable zum Bereitstellen der Pfadinformationen verwenden. Beispielsweise stellt eine Variable, die „C:\Test\\*.txt“ enthält, einen Pfad bereit, der das Löschen oder Senden aller Dateien mit der Erweiterung TXT im Verzeichnis „Test“ unterstützt.  
  
 Um mehrere Dateien zu senden und auf mehrere lokale Dateien und Verzeichnisse zuzugreifen, können Sie den FTP-Task auch mehrmals ausführen, indem Sie den Task in eine Foreach-Schleife einschließen. Mit der Foreach-Schleife ist die Enumeration von Dateien in einem Verzeichnis mithilfe des Foreach-Dateienumerators möglich. Weitere Informationen finden Sie unter [Foreach Loop Container](../../integration-services/control-flow/foreach-loop-container.md).  
  
 Der FTP-Task unterstützt die Platzhalterzeichen *?* und *\** in Pfaden. Auf diese Weise kann mit dem Task auf mehrere Dateien zugegriffen werden. Platzhalterzeichen können jedoch nur in dem Teil des Pfades verwendet werden, in dem der Dateiname angegeben ist. Beispielsweise ist „C:\MyDirectory\\*.txt“ ein gültiger Pfad, „C:\\\*\MyText.txt“ hingegen nicht.  
  
 Die FTP-Vorgänge können so konfiguriert werden, dass der Task Dateisystem beendet wird, wenn der Vorgang einen Fehler erzeugt, oder dass Dateien im ASCII-Modus übertragen werden. Die Vorgänge, mit denen Dateien gesendet und empfangen werden, können so konfiguriert werden, dass Zieldateien und -verzeichnisse überschrieben werden.  
  
## Vordefinierte FTP-Vorgänge  
 Der FTP-Task schließt vordefinierte Vorgänge ein. In der folgenden Tabelle werden diese Vorgänge beschrieben.  
  
|Vorgang|Description|  
|---------------|-----------------|  
|Dateien senden|Sendet eine Datei vom lokalen Computer an den FTP-Server.|  
|Dateien empfangen|Speichert eine Datei vom FTP-Server auf dem lokalen Computer.|  
|Lokales Verzeichnis erstellen|Erstellt einen Ordner auf dem lokalen Computer.|  
|Remoteverzeichnis erstellen|Erstellt einen Ordner auf dem FTP-Server.|  
|Lokales Verzeichnis entfernen|Löscht einen Ordner auf dem lokalen Computer.|  
|Remoteverzeichnis entfernen|Löscht einen Ordner auf dem FTP-Server.|  
|Lokale Dateien löschen|Löscht eine Datei auf dem lokalen Computer.|  
|Remotedateien löschen|Löscht eine Datei auf dem FTP-Server.|  
  
## Verfügbare benutzerdefinierte Protokolleinträge für den FTP-Task  
 In der folgenden Tabelle werden die benutzerdefinierten Protokolleinträge für den FTP-Task aufgelistet. Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) und [Benutzerdefinierte Meldungen für die Protokollierung](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Protokolleintrag|Description|  
|---------------|-----------------|  
|**FTPConnectingToServer**|Zeigt an, dass mit dem Task eine Verbindung zum FTP-Server initiiert wurde.|  
|**FTPOperation**|Berichtet den Beginn und Typ des vom Task ausgeführten FTP-Vorgangs.|  
  
## Verwandte Aufgaben  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Informationen zum Anzeigen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer finden Sie unter [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
 Weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften finden Sie unter <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>.  
  
## Siehe auch  
 [Editor für den FTP-Task &#40;Seite Allgemein&#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [Editor für den FTP-Task &#40;Seite Dateiübertragung&#41;](../../integration-services/control-flow/ftp-task-editor-file-transfer-page.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)  
  
  