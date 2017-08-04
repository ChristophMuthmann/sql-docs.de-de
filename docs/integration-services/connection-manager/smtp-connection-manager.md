---
title: SMTP-Verbindungs-Manager | Microsoft Docs
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
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d350ca1ef990278eb64fc0589787fc5ea9b6125f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="smtp-connection-manager"></a>SMTP-Verbindungs-Manager
  Mit einem SMTP-Verbindungs-Manager kann ein Paket eine Verbindung mit einem SMTP-Server (Simple Mail Transfer Protocol) herstellen. Der Task Mail senden von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verwendet einen SMTP-Verbindungs-Manager.  
  
 Wenn Sie Microsoft Exchange als SMTP-Server verwenden, müssen Sie den SMTP-Verbindungs-Manager u. U. für die Verwendung der Windows-Authentifizierung konfigurieren. Exchange-Server können so konfiguriert werden, dass keine nicht authentifizierten SMTP-Verbindungen zugelassen werden.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Konfiguration des SMTP-Verbindungs-Managers  
 Wenn Sie einem Paket einen SMTP-Verbindungs-Manager hinzufügen, erstellt [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] einen Verbindungs-Manager, der zur Laufzeit in eine SMTP-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers festlegt und den Verbindungs-Manager zur **Connections** -Sammlung im Paket hinzufügt. Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **SMTP**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um einen SMTP-Verbindungs-Manager zu konfigurieren:  
  
-   Geben Sie eine Verbindungszeichenfolge an.  
  
-   Geben Sie den Namen eines SMTP-Servers an.  
  
-   Geben Sie die zu verwendende Authentifizierungsmethode an.  
  
    > [!IMPORTANT]  
    >  Der SMTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Windows-Authentifizierung. Er unterstützt keine Standardauthentifizierung.  
  
-   Geben Sie an, ob beim Senden von E-Mail-Nachrichten SSL (Secure Sockets Layer) zur Verschlüsselung der Kommunikation verwendet werden soll.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können, finden Sie unter [SMTP-Verbindungs-Manager-Editor](../../integration-services/connection-manager/smtp-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
  
