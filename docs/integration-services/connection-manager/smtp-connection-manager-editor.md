---
title: SMTP-Verbindungs-Manager-Editor | Microsoft Docs
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
- sql13.dts.designer.smtpconnection.f1
helpviewer_keywords:
- SMTP Connection Manager Editor
ms.assetid: 2693de0d-b04d-4325-a856-ce667d2b8aa1
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ef8edce1f187ac427463a0a0722c12666265d93
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="smtp-connection-manager-editor"></a>SMTP-Verbindungs-Manager-Editor
  Mithilfe des Dialogfelds **SMTP-Verbindungs-Manager-Editor** können Sie einen SMTP-Server (Simple Mail Transfer Protocol) angeben.  
  
 Weitere Informationen zum SMTP-Verbindungs-Manager finden Sie unter [SMTP Connection Manager](../../integration-services/connection-manager/smtp-connection-manager.md).  
  
## <a name="options"></a>enthalten  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Verbindungs-Manager an.  
  
 **Description**  
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
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)  
  
  
