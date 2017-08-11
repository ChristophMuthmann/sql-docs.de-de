---
title: HTTP-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.httpconnection.server.f1
- sql13.dts.designer.httpconnection.proxy.f1
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 7dbd165b8d94247365697fe3b9e0cbb372becd8c
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="http-connection-manager"></a>HTTP-Verbindungs-Manager
  Eine HTTP-Verbindung ermöglicht Paketen den Zugriff auf einen Webserver, indem zum Senden und Empfangen von Dateien HTTP verwendet wird. Der Task Webdienst von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet diesen Verbindungs-Manager.  
  
 Wenn Sie einem Paket einen HTTP-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine HTTP-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und der **Connections** -Sammlung im Paket den Verbindungs-Manager hinzufügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist festgelegt auf **HTTP.**  
  
 Es gibt folgende Möglichkeiten, um den HTTP-Verbindungs-Manager zu konfigurieren:  
  
-   Verwenden Sie Anmeldeinformationen. Falls der Verbindungs-Manager Anmeldeinformationen verwendet, enthalten die Eigenschaften den Benutzernamen, ein Kennwort und eine Domäne.  
  
    > [!IMPORTANT]  
    >  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
-   Verwenden Sie ein Clientzertifikat. Falls der Verbindungs-Manager ein Clientzertifikat verwendet, enthalten die Eigenschaften den Zertifikatnamen.  
  
-   Stellen Sie ein Timeout für Verbindungen mit dem Server und eine Segmentgröße zum Schreiben von Daten bereit.  
  
-   Verwenden Sie einen Proxyserver. Für den Proxyserver können Sie auch konfigurieren, dass Anmeldeinformationen verwendet werden und der Proxyserver umgangen wird und stattdessen lokale Adressen verwendet werden.  
  
## <a name="configuration-of-the-http-connection-manager"></a>Konfiguration des HTTP-Verbindungs-Managers  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="http-connection-manager-editor-server-page"></a>HTTP-Verbindungs-Manager-Editor (Seite Server)
  Mithilfe der Registerkarte **Server** des Dialogfelds **HTTP-Verbindungs-Manager-Editor** können Sie den HTTP-Verbindungs-Manager konfigurieren, indem Sie Eigenschaften, z. B. URL und Sicherheitseinstellungen, angeben. Eine HTTP-Verbindung ermöglicht Paketen den Zugriff auf einen Webserver, indem zum Senden und Empfangen von Dateien HTTP verwendet wird. Nach der Konfiguration des HTTP-Verbindungs-Managers können Sie die Verbindung testen.  
  
> [!IMPORTANT]  
>  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Weitere Informationen zum HTTP-Verbindungs-Manager finden Sie unter [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Weitere Informationen zu einem allgemeinen Verwendungsszenario für den HTTP-Verbindungs-Manager finden Sie unter [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>enthalten  
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
 Nachdem die Konfiguration des HTTP-Verbindungs-Managers abgeschlossen ist, bestätigen Sie die Gültigkeit der Verbindung, indem Sie auf **Verbindung testen**klicken.  
  
## <a name="http-connection-manager-editor-proxy-page"></a>HTTP-Verbindungs-Manager-Editor (Seite Proxy)
  Auf der Registerkarte **Proxy** des Dialogfelds **HTTP-Verbindungs-Manager-Editor** können Sie den HTTP-Verbindungs-Manager für die Verwendung eines Proxyservers konfigurieren. Eine HTTP-Verbindung ermöglicht Paketen den Zugriff auf einen Webserver, indem zum Senden und Empfangen von Dateien HTTP verwendet wird.  
  
 Weitere Informationen zum HTTP-Verbindungs-Manager finden Sie unter [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Weitere Informationen zu einem allgemeinen Verwendungsszenario für den HTTP-Verbindungs-Manager finden Sie unter [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
### <a name="options"></a>enthalten  
 **Proxy verwenden**  
 Gibt an, ob der HTTP-Verbindungs-Manager Verbindungen über einen Proxyserver herstellen soll.  
  
 **Proxy-URL**  
 Geben Sie die URL für den Proxy ein.  
  
 **Proxyserver für lokale Adressen umgehen**  
 Gibt an, ob der HTTP-Verbindungs-Manager den Proxyserver für lokale Adressen umgehen soll.  
  
 **Anmeldeinformationen verwenden**  
 Gibt an, ob der HTTP-Verbindungs-Manager Anmeldeinformationen für den Proxyserver verwenden soll.  
  
 **Benutzername**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Kennwort**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Domäne**  
 Wenn der HTTP-Verbindungs-Manager Anmeldeinformationen verwendet, müssen Sie einen Benutzernamen, ein Kennwort und eine Domäne angeben.  
  
 **Proxyumgehungsliste**  
 Die Liste der Adressen, für die Sie den Proxyserver umgehen möchten.  
  
 **Hinzufügen**  
 Geben Sie eine Adresse ein, für die Sie den Proxyserver umgehen möchten.  
  
 **Entfernen**  
 Wählen Sie eine Adresse aus, und entfernen Sie sie dann, indem Sie auf **Entfernen**klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [Webdienst (Task)](../../integration-services/control-flow/web-service-task.md)   
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
