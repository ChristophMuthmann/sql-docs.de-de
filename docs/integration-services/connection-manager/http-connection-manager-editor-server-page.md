---
title: "HTTP-Verbindungs-Manager-Editor (Seite Server) | Microsoft Docs"
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
  - "sql13.dts.designer.httpconnection.server.f1"
helpviewer_keywords: 
  - "HTTP-Verbindungs-Manager-Editor"
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# HTTP-Verbindungs-Manager-Editor (Seite Server)
  Mithilfe der Registerkarte **Server** des Dialogfelds **HTTP-Verbindungs-Manager-Editor** können Sie den HTTP-Verbindungs-Manager konfigurieren, indem Sie Eigenschaften, z. B. URL und Sicherheitseinstellungen, angeben. Eine HTTP-Verbindung ermöglicht Paketen den Zugriff auf einen Webserver, indem zum Senden und Empfangen von Dateien HTTP verwendet wird. Nach der Konfiguration des HTTP-Verbindungs-Managers können Sie die Verbindung testen.  
  
> [!IMPORTANT]  
>  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Weitere Informationen zum HTTP-Verbindungs-Manager finden Sie unter [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Weitere Informationen zu einem allgemeinen Verwendungsszenario für den HTTP-Verbindungs-Manager finden Sie unter [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
## enthalten  
 **Server-URL**  
 Geben Sie die URL für den Server ein.  
  
 Wenn Sie die Schaltfläche **WSDL herunterladen** auf der Seite **Allgemein** im **Editor für den Task 'Webdienst'** verwenden möchten, um eine WSDL-Datei herunterzuladen, geben Sie die URL für die WSDL-Datei ein. Diese URL endet mit "? wsdl".  
  
 **Anmeldeinformationen verwenden**  
 Geben Sie an, ob der HTTP-Verbindungs-Manager zur Authentifizierung die Sicherheitsanmeldeinformationen des Benutzers verwenden soll.  
  
 **Benutzername**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Kennwort**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Domäne**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Clientzertifikat verwenden**  
 Geben Sie an, ob der HTTP-Verbindungs-Manager zur Authentifizierung ein Clientzertifikat verwenden soll.  
  
 **Zertifikat**  
 Wählen Sie mithilfe des Dialogfelds **Zertifikat auswählen** ein Zertifikat aus der Liste aus. Im Textfeld wird der dem Zertifikat zugeordnete Name angezeigt.  
  
 **Timeout (in Sekunden)**  
 Geben Sie ein Timeout für Verbindungen mit dem Webserver an. Der Standardwert dieser Eigenschaft beträgt 30 Sekunden.  
  
 **Segmentgröße (in KB)**  
 Geben Sie eine Segmentgröße zum Schreiben von Daten an.  
  
 **Verbindung testen**  
 Nachdem die Konfiguration des HTTP-Verbindungs-Managers abgeschlossen ist, bestätigen Sie die Gültigkeit der Verbindung, indem Sie auf **Verbindung testen** klicken.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [HTTP-Verbindungs-Manager-Editor &#40;Seite „Proxy“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
  