---
title: "FTP-Verbindungs-Manager-Editor | Microsoft Docs"
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
  - "sql13.dts.designer.ftpconnectionmanager.f1"
helpviewer_keywords: 
  - "FTP-Verbindungs-Manager-Editor"
ms.assetid: 874b6585-255b-4a43-8396-bb08c3e8ac2b
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# FTP-Verbindungs-Manager-Editor
  Mithilfe des Dialogfelds **FTP-Verbindungs-Manager-Editor** können Sie Eigenschaften für Verbindungen mit einem FTP-Server angeben.  
  
> [!IMPORTANT]  
>  Der FTP-Verbindungs-Manager unterstützt nur die anonyme Authentifizierung und die Standardauthentifizierung. Er unterstützt keine Windows-Authentifizierung.  
  
 Weitere Informationen zum FTP-Verbindungs-Manager finden Sie unter [FTP Connection Manager](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
## enthalten  
 **Servername**  
 Geben Sie den Namen des FTP-Servers an.  
  
 **Serverport**  
 Geben Sie die Portnummer des FTP-Servers an, der für die Verbindung verwendet werden soll. Der Standardwert dieser Eigenschaft ist **21**.  
  
 **Benutzername**  
 Geben Sie einen Benutzernamen für den Zugriff auf den FTP-Server an. Der Standardwert dieser Eigenschaft ist **anonymous**.  
  
 **Kennwort**  
 Geben Sie das Kennwort für den Zugriff auf den FTP-Server an.  
  
 **Timeout (in Sekunden)**  
 Geben Sie die Dauer in Sekunden an, bevor ein Timeout für den Task eintritt. Der Wert **0** gibt einen unbegrenzten Zeitraum an. Der Standardwert dieser Eigenschaft ist **60**.  
  
 **Passivmodus verwenden**  
 Geben Sie an, ob die Verbindung durch den Server oder durch den Client initiiert wird. Die Initiierung der Verbindung durch den Server erfolgt im Aktivmodus; der Client aktiviert die Verbindung im Passivmodus. Der Standardwert dieser Eigenschaft ist der **Aktivmodus**.  
  
 **Wiederholungen**  
 Geben Sie die Häufigkeit an, mit der der Task versucht, eine Verbindung herzustellen. Der Wert **0** gibt eine unbegrenzte Anzahl von Versuchen an.  
  
 **Segmentgröße (in KB)**  
 Geben Sie eine Segmentgröße in KB für das Übertragen von Daten an.  
  
 **Verbindung testen**  
 Nachdem die Konfiguration des FTP-Verbindungs-Managers abgeschlossen ist, bestätigen Sie die Gültigkeit der Verbindung, indem Sie auf **Verbindung testen** klicken.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  