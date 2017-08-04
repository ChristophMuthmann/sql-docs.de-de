---
title: "FTP-Task-Editor (Seite Dateiübertragung) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca75f79962fcf7b7cae067a7d841f80f9c4c2032
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="ftp-task-editor-file-transfer-page"></a>Editor für den FTP-Task (Seite Dateiübertragung)
  Mithilfe der Seite **Dateiübertragung** des Dialogfelds **Editor für den FTP-Task** können Sie den FTP-Vorgang konfigurieren, der durch den Task ausgeführt wird.  
  
 Informationen zu diesem Task finden Sie unter [FTP-Task](../../integration-services/control-flow/ftp-task.md).  
  
## <a name="options"></a>enthalten  
 **IsRemotePathVariable**  
 Geben Sie an, ob der Remotepfad in einer Variablen gespeichert ist. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**True**|Der Zielpfad ist in einer Variablen gespeichert. Wenn Sie diesen Wert auswählen, wird die dynamische Option **RemoteVariable**angezeigt.|  
|**False**|Der Zielpfad wird in einem Dateiverbindungs-Manager angegeben. Wenn Sie diesen Wert auswählen, wird die dynamische Option **RemotePath**angezeigt.|  
  
 **OverwriteFileAtDestination**  
 Geben Sie an, ob eine Datei am Ziel überschrieben werden kann.  
  
 **IsLocalPathVariable**  
 Geben Sie an, ob der lokale Pfad in einer Variablen gespeichert ist. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**True**|Der Zielpfad ist in einer Variablen gespeichert. Wenn Sie diesen Wert auswählen, wird die dynamische Option **LocalVariable**angezeigt.|  
|**False**|Der Zielpfad wird in einem Dateiverbindungs-Manager angegeben. Wenn Sie diesen Wert auswählen, wird die dynamische Option **LocalPath**angezeigt.|  
  
 **Vorgang**  
 Wählen Sie den auszuführenden FTP-Vorgang aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Dateien senden**|Senden Sie Dateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable**, **LocalPathRemoteVariable** und **RemotePath**angezeigt.|  
|**Dateien empfangen**|Empfangen Sie Dateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable**, **LocalPathRemoteVariable** und **RemotePath**angezeigt.|  
|**Lokales Verzeichnis erstellen**|Erstellen Sie ein lokales Verzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable** und **LocalPath**angezeigt.|  
|**Remoteverzeichnis erstellen**|Erstellen Sie ein Remoteverzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **RemoteVariable** und **RemotePath**angezeigt.|  
|**Lokales Verzeichnis entfernen**|Entfernen Sie ein lokales Verzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable** und **LocalPath**angezeigt.|  
|**Remoteverzeichnis entfernen**|Entfernen Sie ein Remoteverzeichnis. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **RemoteVariable** und **RemotePath**angezeigt.|  
|**Lokale Dateien löschen**|Löschen Sie lokale Dateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **LocalVariable** und **LocalPath**angezeigt.|  
|**Remotedateien löschen**|Löschen Sie Remotedateien. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen **RemoteVariable** und **RemotePath**angezeigt.|  
  
 **IsTransferASCII**  
 Geben Sie an, ob die auf und von einem Remote-FTP-Server übertragenen Dateien im ASCII-Modus übertragen werden sollen.  
  
## <a name="isremotepathvariable-dynamic-options"></a>IsRemotePathVariable (dynamische Optionen)  
  
### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **RemoteVariable**  
 Wählen Sie eine vorhandene benutzerdefinierte Variable aus, oder klicken Sie auf \< **neue Variable...** > um eine benutzerdefinierte Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Hinzufügen von Variablen  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 Wählen Sie einen vorhandenen FTP-Verbindungs-Manager, oder klicken Sie auf \< **neue Verbindung...** > um einen Verbindungs-Manager erstellen.  
  
 **Verwandte Themen:** [FTP-Verbindungs-Manager](../../integration-services/connection-manager/ftp-connection-manager.md), [FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>IsLocalPathVariable (dynamische Optionen)  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 Wählen Sie eine vorhandene benutzerdefinierte Variable aus, oder klicken Sie auf \< **neue Variable...** > um eine Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Hinzufügen von Variablen  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 Wählen Sie einen vorhandenen Dateiverbindungs-Manager, oder klicken Sie auf \< **neue Verbindung...** > um einen Verbindungs-Manager erstellen.  
  
 **Verwandte Themen:** [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [FTP-Task-Editor &#40; Seite "Allgemein" &#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  
