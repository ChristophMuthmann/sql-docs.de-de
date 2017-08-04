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
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4cf63461848933530a215a75b19d40128327f356
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [HTTP-Verbindungs-Manager-Editor &#40;Seite „Server“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
-   [HTTP-Verbindungs-Manager-Editor &#40;Seite „Proxy“&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="see-also"></a>Siehe auch  
 [Webdienst (Task)](../../integration-services/control-flow/web-service-task.md)   
 [Integrationsservices &#40; SSIS &#41; Verbindungen](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
