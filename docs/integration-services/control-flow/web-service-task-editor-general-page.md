---
title: Web Service Task-Editor (Seite Allgemein) | Microsoft Docs
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
- sql13.dts.designer.webservicestask.general.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c65419846e21225c6b5fe41bc07cfbae6dffe01
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="web-service-task-editor-general-page"></a>Editor für den Task 'Webdienst' (Seite Allgemein)
  Auf der Seite **Allgemein** des Dialogfelds **Editor für den Task 'Webdienst'** können Sie einen HTTP-Verbindungs-Manager und den Speicherort der WSDL-Datei (Web Services Description Language) angeben, die der Task „Webdienst“ verwendet, den Task „Webdienst“ beschreiben und die WSDL-Datei herunterladen.  
  
 Weitere Informationen zu diesem Task finden Sie unter [Webdienst (Task)](../../integration-services/control-flow/web-service-task.md).  
  
## <a name="options"></a>enthalten  
 **HTTPConnection**  
 Wählen Sie einen Verbindungs-Manager in der Liste aus, oder klicken Sie auf \< **neue Verbindung...** > um einen neuen Verbindungs-Manager zu erstellen.  
  
> [!IMPORTANT]  
>  Der HTTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 **Verwandte Themen:** [HTTP-Verbindungs-Manager](../../integration-services/connection-manager/http-connection-manager.md), [HTTP-Verbindungs-Manager-Editor &#40;Seite Server&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Geben Sie den vollqualifizierten Pfad der auf dem Computer lokalen WSDL-Datei an, oder klicken Sie auf die Schaltfläche zum Durchsuchen **(…)** , um nach dieser Datei zu suchen.  
  
 Wenn Sie die WSDL-Datei bereits manuell auf den Computer heruntergeladen haben, wählen Sie diese Datei aus. Wenn die WSDL-Datei jedoch noch nicht heruntergeladen wurde, führen Sie folgende Schritte aus:  
  
-   Erstellen Sie eine leere Datei mit der Dateinamenerweiterung WSDL.  
  
-   Wählen Sie diese leere Datei für die Option **WSDLFile** aus.  
  
-   Legen Sie den Wert von **OverwriteWSDLFile** auf **True** fest, damit die leere Datei mit der tatsächlichen WSDL-Datei überschrieben werden kann.  
  
-   Klicken Sie auf **WSDL herunterladen** , um die tatsächliche WSDL-Datei herunterzuladen und die leere Datei zu überschreiben.  
  
    > [!NOTE]  
    >  Die Option **WSDL herunterladen** wird erst aktiviert, wenn Sie den Namen einer vorhandenen lokalen Datei im Feld **WSDLFile** angeben.  
  
 **OverwriteWSDLFile**  
 Geben Sie an, ob die WSDL-Datei für den Task Webdienst überschrieben werden kann.  
  
 Wenn Sie die WSDL-Datei mithilfe der Schaltfläche **WSDL herunterladen** herunterladen möchten, legen Sie diesen Wert auf **True**fest.  
  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Task Webdienst an. Dieser Name wird im Tasksymbol als Bezeichnung verwendet.  
  
> [!NOTE]  
>  Tasknamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Description**  
 Geben Sie eine Beschreibung des Tasks Webdienst ein.  
  
 **WSDL herunterladen**  
 Lädt die WSDL-Datei herunter.  
  
 Diese Schaltfläche wird erst aktiviert, wenn Sie den Namen einer vorhandenen lokalen Datei im Feld **WSDLFile** angeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Meldungsreferenz von Integration Services-Fehler](../../integration-services/integration-services-error-and-message-reference.md)   
 [Web-Service-Task-Editor &#40; Eingabe Seite &#41;](../../integration-services/control-flow/web-service-task-editor-input-page.md)   
 [Editor für den Task Webdienst &#40; Seite "Fehlerausgabe" &#41;](../../integration-services/control-flow/web-service-task-editor-output-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  
