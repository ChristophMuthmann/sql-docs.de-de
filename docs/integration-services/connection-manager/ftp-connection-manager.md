---
title: "FTP-Verbindungs-Manager | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FTP-Verbindungs-Manager"
  - "Verbindungen [Integration Services], FTP"
  - "Verbindungs-Manager [Integration Services], FTP"
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 41
---
# FTP-Verbindungs-Manager
  Mit einem FTP-Verbindungs-Manager kann ein Paket eine Verbindung mit einem FTP-Server (File Transfer Protocol) herstellen. Der FTP-Task von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet diesen Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen FTP-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit als FTP-Verbindung aufgelöst werden kann, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections**-Sammlung im Paket den Verbindungs-Manager hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **FTP**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um den FTP-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie einen Servernamen und einen Serverport an.  
  
-   Geben Sie den anonymen Zugriff an, oder stellen Sie einen Benutzernamen und ein Kennwort für die Standardauthentifizierung bereit.  
  
    > [!IMPORTANT]  
    >  Der FTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
-   Legen Sie das Timeout, die Wiederholungsversuche und die jeweils zu kopierende Datenmenge fest.  
  
-   Geben Sie an, ob der FTP-Verbindungs-Manager den passiven oder aktiven Modus verwendet.  
  
 Sie müssen u. U. die folgenden Standardwerte des Verbindungs-Managers ändern, je nach Konfiguration der FTP-Site, zu der der FTP-Verbindungs-Manager eine Verbindung herstellt:  
  
-   Der Serverport wird auf 21 festgelegt. Sie sollten den Port angeben, an dem von der FTP-Site gelauscht wird.  
  
-   Der Benutzername ist auf "anonym" festgelegt. Sie sollten die für die FTP-Site erforderlichen Anmeldeinformationen bereitstellen.  
  
## Aktiver/passiver Modus  
 Ein FTP-Verbindungs-Manager kann Dateien mithilfe des aktiven oder passiven Modus senden und empfangen. Im aktiven Modus wird die Datenverbindung vom Server initiiert, im passiven Modus wird sie vom Client initiiert.  
  
## Konfiguration des FTP-Verbindungs-Managers  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer festlegen können, finden Sie unter [FTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/ftp-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Siehe auch  
 [FTP-Task](../../integration-services/control-flow/ftp-task.md)   
 [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  