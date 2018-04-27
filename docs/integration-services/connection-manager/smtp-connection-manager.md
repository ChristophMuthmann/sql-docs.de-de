---
title: SMTP-Verbindungs-Manager | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.smtpconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ec3b8528955446f54f870fb134006cf0b5cdd86c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
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
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
## <a name="smtp-connection-manager-editor"></a>SMTP-Verbindungs-Manager-Editor
  Mithilfe des Dialogfelds **SMTP-Verbindungs-Manager-Editor** können Sie einen SMTP-Server (Simple Mail Transfer Protocol) angeben.  
  
 Weitere Informationen zum SMTP-Verbindungs-Manager finden Sie unter [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
### <a name="options"></a>Tastatur  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Verbindungs-Manager an.  
  
 **Beschreibung**  
 Beschreiben Sie den Verbindungs-Manager. Die bewährte Methode ist hierbei, den Verbindungs-Manager zweckbezogen zu beschreiben, sodass Pakete selbsterklärend und leichter zu verwalten sind.  
  
 **SMTP-Server**  
 Geben Sie den Namen des SMTP-Servers an.  
  
 **Windows-Authentifizierung verwenden**  
 Wählen Sie diese Option aus, um E-Mail über einen SMTP-Server zu senden, der zum Authentifizieren des Zugriffs auf den Server die Windows-Authentifizierung verwendet.  
  
> [!IMPORTANT]  
>  Der SMTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Windows-Authentifizierung. Er unterstützt keine Standardauthentifizierung.  
  
> [!NOTE]  
>  Wenn Microsoft Exchange als SMTP-Server verwendet wird, müssen Sie u. U. **Windows-Authentifizierung verwenden** auf **True**festlegen. Exchange-Server können so konfiguriert sein, dass keine nicht authentifizierten SMTP-Verbindungen zugelassen sind.  
  
 **Secure Sockets Layer (SSL) aktivieren**  
 Wählen Sie diese Option aus, um beim Senden von E-Mail-Nachrichten die Kommunikation mit SSL (Secure Sockets Layer) zu verschlüsseln.  
  
