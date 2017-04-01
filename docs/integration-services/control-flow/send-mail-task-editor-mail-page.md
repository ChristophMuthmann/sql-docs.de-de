---
title: "Editor f&#252;r den Task &#39;Mail senden&#39; (Seite E-Mail) | Microsoft Docs"
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
  - "sql13.dts.designer.sendmailtask.mail.f1"
helpviewer_keywords: 
  - "Editor für den Task Mail senden"
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Editor f&#252;r den Task &#39;Mail senden&#39; (Seite E-Mail)
  Auf der Seite **E-Mail** im Dialogfeld **Editor für den Task „Mail senden“** können Sie die Empfänger, den Nachrichtentyp und die Priorität einer Nachricht angeben. Sie können der Nachricht auch Dateien anfügen. Bei dem Nachrichtentext kann es sich um eine bereitgestellte Zeichenfolge, eine Dateiverbindung mit einer Datei mit Text oder den Namen einer Variablen mit Text handeln.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Send Mail Task](../../integration-services/control-flow/send-mail-task.md).  
  
## enthalten  
 **SMTPConnection**  
 Wählen Sie in der Liste einen SMTP-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung…>**, um einen neuen Verbindungs-Manager zu erstellen.  
  
> [!IMPORTANT]  
>  Der SMTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Windows-Authentifizierung. Er unterstützt keine Standardauthentifizierung.  
  
 **Verwandte Themen:** [SMTP-Verbindungs-Manager](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
 **Von**  
 Geben Sie die E-Mail-Adresse des Absenders an.  
  
 **Aktion**  
 Stellen Sie die E-Mail-Adresse der Empfänger bereit. Verwenden Sie als Trennzeichen ein Semikolon.  
  
 **Cc**  
 Geben Sie die E-Mail-Adressen der Personen an, die Kopien der Nachricht erhalten sollen. Verwenden Sie als Trennzeichen ein Semikolon.  
  
 **Bcc**  
 Geben Sie die E-Mail-Adressen der Personen an, die Blindkopien der Nachricht erhalten sollen. Verwenden Sie als Trennzeichen ein Semikolon.  
  
 **Betreff**  
 Geben Sie einen Betreff für die E-Mail-Nachricht an.  
  
 **MessageSourceType**  
 Wählen Sie den Quelltyp der Nachricht aus. Diese Eigenschaft besitzt die in der folgenden Tabelle aufgeführten Optionen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie für die Quelle den Nachrichtentext fest. Bei Auswahl dieses Wertes wird die dynamische Option **MessageSource** angezeigt.|  
|**File connection**|Legen Sie für die Quelle die Datei fest, die den Nachrichtentext enthält. Bei Auswahl dieses Wertes wird die dynamische Option **MessageSource** angezeigt.|  
|**Variable**|Legen Sie für die Quelle eine Variable fest, die den Nachrichtentext enthält. Bei Auswahl dieses Wertes wird die dynamische Option **MessageSource** angezeigt.|  
  
 **Priority**  
 Legen Sie die Priorität der Nachricht fest.  
  
 **Attachments**  
 Geben Sie die Dateinamen der Anlagen für die E-Mail-Nachricht an. Verwenden Sie als Trennzeichen das Pipe-Zeichen (|).  
  
> [!NOTE]  
>  Die Zeilen An, Cc und Bcc sind in Übereinstimmung mit Internetstandards auf 256 Zeichen begrenzt.  
  
## MessageSourceType (dynamische Optionen)  
  
### MessageSourceType = Direct Input  
 **MessageSource**  
 Geben Sie den Nachrichtentext ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (…), und geben Sie die Nachricht in das Dialogfeld **Nachrichtenquelle** ein.  
  
### MessageSourceType = File connection  
 **MessageSource**  
 Wählen Sie in der Liste einen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung…**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### MessageSourceType = Variable  
 **MessageSource**  
 Wählen Sie in der Liste eine Variable aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](../Topic/Add%20Variable.md)  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Task „Mail senden“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/send-mail-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)  
  
  