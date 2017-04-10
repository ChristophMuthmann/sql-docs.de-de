---
title: "Editor f&#252;r den FTP-Task (Seite Datei&#252;bertragung) | Microsoft Docs"
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
  - "sql13.dts.designer.ftptask.filetransfer.f1"
helpviewer_keywords: 
  - "Editor für den FTP-Task"
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor f&#252;r den FTP-Task (Seite Datei&#252;bertragung)
  Mithilfe der Seite **Dateiübertragung** des Dialogfelds **Editor für den FTP-Task** können Sie den FTP-Vorgang konfigurieren, der durch den Task ausgeführt wird.  
  
 Informationen zu diesem Task finden Sie unter [FTP-Task](../../integration-services/control-flow/ftp-task.md).  
  
## enthalten  
 **IsRemotePathVariable**  
 Geben Sie an, ob der Remotepfad in einer Variablen gespeichert ist. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Der Zielpfad ist in einer Variablen gespeichert. Wenn Sie diesen Wert auswählen, wird die dynamische Option **RemoteVariable**angezeigt.|  
|**False**|Der Zielpfad wird in einem Dateiverbindungs-Manager angegeben. Wenn Sie diesen Wert auswählen, wird die dynamische Option **RemotePath**angezeigt.|  
  
 **OverwriteFileAtDestination**  
 Geben Sie an, ob eine Datei am Ziel überschrieben werden kann.  
  
 **IsLocalPathVariable**  
 Geben Sie an, ob der lokale Pfad in einer Variablen gespeichert ist. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Wahr**|Der Zielpfad ist in einer Variablen gespeichert. Wenn Sie diesen Wert auswählen, wird die dynamische Option **LocalVariable**angezeigt.|  
|**False**|Der Zielpfad wird in einem Dateiverbindungs-Manager angegeben. Wenn Sie diesen Wert auswählen, wird die dynamische Option **LocalPath**angezeigt.|  
  
 **Vorgang**  
 Wählen Sie den auszuführenden FTP-Vorgang aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Dateien senden**|Senden Sie Dateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable**, **LocalPathRemoteVariable** und **RemotePath** angezeigt.|  
|**Dateien empfangen**|Empfangen Sie Dateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable**, **LocalPathRemoteVariable** und **RemotePath** angezeigt.|  
|**Lokales Verzeichnis erstellen**|Erstellen Sie ein lokales Verzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable** und **LocalPath**angezeigt.|  
|**Remoteverzeichnis erstellen**|Erstellen Sie ein Remoteverzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **RemoteVariable** und **RemotePath**angezeigt.|  
|**Lokales Verzeichnis entfernen**|Entfernen Sie ein lokales Verzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable** und **LocalPath**angezeigt.|  
|**Remoteverzeichnis entfernen**|Entfernen Sie ein Remoteverzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **RemoteVariable** und **RemotePath**angezeigt.|  
|**Lokale Dateien löschen**|Löschen Sie lokale Dateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable** und **LocalPath**angezeigt.|  
|**Remotedateien löschen**|Löschen Sie Remotedateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **RemoteVariable** und **RemotePath**angezeigt.|  
  
 **IsTransferASCII**  
 Geben Sie an, ob die auf und von einem Remote-FTP-Server übertragenen Dateien im ASCII-Modus übertragen werden sollen.  
  
## IsRemotePathVariable (dynamische Optionen)  
  
### IsRemotePathVariable = True  
 **RemoteVariable**  
 Wählen Sie eine vorhandene benutzerdefinierte Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um eine benutzerdefinierte Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Hinzufügen von Variablen  
  
### IsRemotePathVariable = False  
 **RemotePath**  
 Wählen Sie einen vorhandenen FTP-Verbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung…**>, um einen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md), [FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
## IsLocalPathVariable (dynamische Optionen)  
  
### IsLocalPathVariable = True  
 **LocalVariable**  
 Wählen Sie eine vorhandene benutzerdefinierte Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um eine Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Hinzufügen von Variablen  
  
### IsLocalPathVariable = False  
 **LocalPath**  
 Wählen Sie einen vorhandenen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung…**>, um einen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den FTP-Task &#40;Seite Allgemein&#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  