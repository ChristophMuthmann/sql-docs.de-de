---
title: "Übersicht über Sicherheitserweiterungen | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], extensions
ms.assetid: 24ccd795-6506-457c-93ac-6a9dd6bb9a46
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: f7e8c95a478e733722d3c80da4b5e12e992ef4da
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="security-extensions-overview"></a>Übersicht über Sicherheitserweiterungen
  Eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Sicherheitserweiterung ermöglicht die Authentifizierung und Autorisierung von Benutzern oder Gruppen. Das heißt, verschiedene Benutzer können sich bei einem Berichtsserver anmelden und anhand ihrer Identitäten verschiedene Aufgaben oder Vorgänge ausführen. Standardmäßig [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verwendet eine Windows-basierte authentifizierungserweiterung, die Windows-kontoprotokollen die Identitäten der Benutzer überprüft, der vorgibt zu Konten im System verfügen. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]wird ein Sicherheitssystem mit der rollenbasierten zum Autorisieren von Benutzern verwendet. Die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] rollenbasierte Sicherheitsmodell ähnelt den rollenbasierten Sicherheitsmodelle anderer Technologien.  
  
 Da sicherheitserweiterungen auf einer offenen und erweiterbaren API beruhen, können Sie neue Erweiterungen für Authentifizierung und Autorisierung in erstellen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Im Folgenden sehen Sie ein Beispiel einer typischen Sicherheitserweiterungsimplementierung, die mit formularbasierter Authentifizierung und Autorisierung arbeitet:  
  
 ![Reporting Services-sicherheitserweiterungsprozess](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionflow.gif "Reporting Services-sicherheitserweiterungsprozess")  
  
 Wie in der Abbildung dargestellt, treten Authentifizierung und Autorisierung folgendermaßen auf:  
  
1.  Ein Benutzer versucht über eine URL auf den Berichts-Manager zuzugreifen und wird zu einem Formular umgeleitet, das Anmeldeinformationen von Benutzern für die Clientanwendung sammelt.  
  
2.  Der Benutzer gibt die Anmeldeinformationen an das Formular.  
  
3.  Die Anmeldeinformationen des Benutzers werden gesendet, um den Reporting Services-Webdienst über die <xref:ReportService2010.ReportingService2010.LogonUser%2A> Methode.  
  
4.  Der Webdienst ruft die vom Benutzer angegebene Sicherheitserweiterung auf und überprüft, ob der Benutzername und das Kennwort in der benutzerdefinierten Sicherheitsinstanz vorhanden sind.  
  
5.  Nach der Authentifizierung erstellt der Webdienst für die Startseite des Berichts-Managers ein Authentifizierungsticket (auch "Cookie" genannt), verwaltet das Ticket und überprüft die Rolle des Benutzers.  
  
6.  Der Webdienst gibt das Cookie an den Browser zurück und zeigt die entsprechende Benutzeroberfläche im Berichts-Manager an.  
  
7.  Nachdem der Benutzer authentifiziert wurde, sendet der Browser Anforderungen an den Berichts-Manager, während das Cookie im HTTP-Header übertragen wird. Diese Anforderungen sind Reaktionen auf Benutzeraktionen im Berichts-Manager.  
  
8.  Das Cookie wird zusammen mit der angeforderten Benutzeroperation im HTTP-Header an den Webdienst übertragen.  
  
9. Das Cookie wird überprüft. Wenn es gültig ist, gibt der Berichtsserver die Sicherheitsbeschreibung und andere im Zusammenhang mit der angeforderten Operation stehende Informationen aus der Berichtsserver-Datenbank zurück.  
  
10. Wenn das Cookie gültig ist, ruft der Berichtsserver die Sicherheitserweiterung auf und überprüft, ob der Benutzer zur Ausführung der bestimmten Operation autorisiert ist.  
  
11. Wenn der Benutzer autorisiert ist, führt der Berichtsserver die angeforderte Operation aus und gibt die Steuerung an den Aufrufer zurück.  
  
12. Nach der Authentifizierung des Benutzers verwendet der URL-Zugriff des Berichtsservers dasselbe Cookie. Das Cookie wird im HTTP-Header übertragen.  
  
13. Der Benutzer fordert so lange Operationen auf dem Berichtsserver an, bis die Sitzung beendet ist.  
  
## <a name="when-to-implement-a-security-extension"></a>Sinnvolles Implementieren von Sicherheitserweiterungen  
 Es wird empfohlen, dass Sie Windows-Authentifizierung, wenn überhaupt möglich verwenden. In den folgenden Fällen ist jedoch möglicherweise eine benutzerdefinierte Authentifizierung und Autorisierung für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] angemessener:  
  
-   Sie haben eine Internet- oder Extranetanwendung, die keine Windows-Konten nutzen kann.  
  
-   Sie haben benutzerdefinierte Benutzer und Rollen, die ein übereinstimmendes Autorisierungsschema in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] bereitstellen müssen.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Sicherheitserweiterungen](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
 [Konfigurieren Sie Berichts-Manager, um die Übergabe von benutzerdefinierten Authentifizierungscookies](https://msdn.microsoft.com/library/ms345241(v=sql.110).aspx)  
  
  
