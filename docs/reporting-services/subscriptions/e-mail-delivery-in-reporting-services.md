---
title: "Die e-Mail-Übermittlung in Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0498dfe642a927744c7a0b5c7cefb5803cb0d469
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="e-mail-delivery-in-reporting-services"></a>E-Mail-Übermittlung in Reporting Services
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält eine E-Mail-Übermittlungserweiterung, mit der Sie einen Bericht per E-Mail an einzelne Benutzer oder Gruppen senden können. Um einen Bericht per E-Mail zu verteilen, 1) konfigurieren Sie den Berichtsserver für die E-Mail-Zustellung und 2) definieren entweder ein Standardabonnement oder ein datengesteuertes Abonnement. Ein einzelnes Abonnement kann nicht mehrere Berichte in einer einzigen E-Mail-Nachricht übermitteln. Sie können jedoch mehrere Abonnements erstellen.  
  
 Der Berichtsserver stellt über eine Standardverbindung eine Verbindung mit einem E-Mail-Server her. Mit Secure Sockets Layer (SSL) verschlüsselte Kommunikation wird nicht verwendet. Der E-Mail-Server muss ein Remoteserver oder lokaler SMTP-Server (Simple Mail Transport Protocol) im selben Netzwerk wie der Berichtsserver sein.  
  
 Ausführliche Schritte zum Erstellen eines Abonnements finden Sie hier:  
  
-   [Erstellen und Verwalten von Abonnements für Berichtsserver im einheitlichen Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [Erstellen und Verwalten von Abonnements für Berichtsserver im SharePoint-Modus](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Einheitlicher Modus|  
  
## <a name="e-mail-delivery-options"></a>Optionen für die E-Mail-Übermittlung  
 Die Berichtsserver-E-Mail-Übermittlung kann Berichte wie folgt übermitteln:  
  
-   Senden einer Benachrichtigung und eines Links zu dem generierten Bericht.  
  
-   Senden einer Benachrichtigung in der Betreffzeile einer E-Mail-Nachricht. Standardmäßig enthält die Betreffzeile in der Abonnementdefinition die folgenden Variablen, die bei der Verarbeitung des Abonnements durch berichtsspezifische Informationen ersetzt werden:  
  
     **@ReportName** gibt den Namen des Berichts an.  
  
     **@ExecutionTime** gibt an, wann der Bericht ausgeführt wurde.  
  
     Diese Variablen können Sie mit statischem Text kombinieren, und den Text in der Betreffzeile können Sie für jedes Abonnement ändern.  
  
-   Senden eines eingebetteten oder angefügten Berichts. Durch das Renderingformat und den Browser wird festgelegt, ob der Bericht eingebettet oder angefügt wird.  
  
     Falls Ihr Browser HTML 4.0 und MHTML unterstützt und Sie das Webarchiv-Renderingformat auswählen, wird der Bericht in die Nachricht eingebettet. Bei allen anderen Renderingformaten (CSV, PDF usw.) werden Berichte als Anlagen übermittelt. Für Server im einheitlichen Modus können Sie diese Funktion in der Konfigurationsdatei RSReportServer.config deaktivieren.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] führt keine Überprüfung der Größe der Anlage oder Nachricht vor dem Senden des Berichts durch. Überschreitet die Anlage oder Nachricht den von Ihrem Mailserver zugelassenen Höchstwert, wird der Bericht nicht übermittelt. Wählen Sie bei großen Berichten eine andere Übermittlungsoption aus (z.B. URL oder Benachrichtigung).  
  
 Die Übermittlungsoptionen, die bestimmen, wie ein Bericht übermittelt wird, werden beim Erstellen des Abonnements festgelegt. Wenn Sie im Abonnement z.B. **Link einschließen** auswählen, enthält die E-Mail-Nachricht einen Link zum Bericht.  
  
## <a name="native-mode-role-based-e-mail-settings"></a>Rollenbasierte E-Mail-Einstellungen im einheitlichen Modus  
 In einer Umgebung mit einheitlichen Berichtsservern variieren die verwendeten E-Mail-Übermittlungseinstellungen je nachdem, ob Ihre Rolle die Aufgabe "Einzelne Abonnements verwalten" oder "Alle Abonnements verwalten" enthält.  
  
|Task|Verfügbare Einstellungen|  
|----------|------------------------|  
|Einzelne Abonnements verwalten|Zeigt Felder an, mit denen ein Benutzer einen Bericht automatisieren und an sich übermitteln kann. In diesem Modus sind keine Felder vorhanden, die E-Mail-Aliasnamen akzeptieren.|  
|Alle Abonnements verwalten|Zeigt Felder an, die eine breiter angelegte Verteilung unterstützen, einschließlich der Felder An, Cc, Bcc und Antwort an. Auf diese Weise stehen zusätzliche Möglichkeiten zur Verfügung, um einen Bericht an mehrere Abonnenten weiterzuleiten. Die Verfügbarkeit von E-Mail-Aliasfeldern wird durch Einstellungen in der Konfigurationsdatei RSReportServer definiert.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>Angeben von E-Mail-Adressen in einem Abonnement  
 Wenn Sie Berichte innerhalb eines Intranets übermitteln und ein SMTP-Gateway zu einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange-Server verwenden, geben Sie den E-Mail-Alias ein (so als ob Sie eine E-Mail an einen Mitarbeiter senden würden). Bei der Übermittlung an ein externes E-Mail-Konto geben Sie die vollständige E-Mail-Adresse ein. Falls Sie zusätzliche E-Mail-Adressen angeben, um Ihrem Abonnement weitere Benutzer hinzuzufügen, erhalten die Abonnenten eine exakte Kopie des Berichts, der anhand dieses Abonnements erstellt wird.  
  
 Der Berichtsserver führt keine Überprüfung von E-Mail-Adressen durch und ruft keine E-Mail-Adressen von einem E-Mail-Server ab. Sie müssen die E-Mail-Adressen bereits kennen, die Sie verwenden möchten. Standardmäßig können Sie Berichte per E-Mail an jedes gültige E-Mail-Konto innerhalb oder außerhalb Ihrer Organisation senden. Mithilfe von Konfigurationseinstellungen kann allerdings die E-Mail-Übermittlung auf namentlich angegebene Hosts des Mailservers beschränkt werden. Sie können zusätzliche Hosts angeben, um die E-Mail-Übermittlung an Personen zu ermöglichen, die nicht zu Ihrer Organisation gehören.  
  
 Die E-Mail-Nachricht, mit der der Bericht übermittelt wird, muss von einem auf dem E-Mail-Server definierten E-Mail-Konto gesendet werden. Das E-Mail-Konto wird durch eine Konfigurationseinstellung angegeben. Das E-Mail-Konto wird für alle Berichte verwendet, die von der E-Mail-Übermittlungserweiterung gesendet werden. Es ist nicht möglich, mehrere Konten anzugeben oder für jeden Bericht ein anderes Konto zu verwenden.  
  
## <a name="controlling-e-mail-delivery"></a>Steuern der E-Mail-Übermittlung  
 Sie können einen Berichtsserver so konfigurieren, dass die E-Mail-Verteilung auf bestimmte Hostdomänen beschränkt wird. Beispielsweise können Sie verhindern, dass ein Berichtsserver im einheitlichen Modus einen Bericht an alle Domänen übermittelt, außer an jene, die in der Konfigurationsdatei **RSReportServer.config** aufgeführt sind.  
  
 Darüber hinaus können Sie mithilfe von Konfigurationseinstellungen das Feld **An** in einem Abonnement ausblenden. In diesem Fall werden Berichte nur an den Benutzer übermittelt, den das Abonnement definiert. Wenn jedoch ein Bericht an einen Benutzer gesendet wurde, können Sie nicht verhindern, dass der Bericht weitergeleitet wird.  
  
 Die effizienteste Möglichkeit zum Steuern der Berichtsverteilung besteht darin, einen Berichtsserver so konfigurieren, dass nur eine Berichtsserver-URL gesendet wird. Der Berichtsserver verwendet die Windows-Authentifizierung und das rollenbasierte Autorisierungsmodell, um den Zugriff auf einen Bericht zu steuern. Falls ein Benutzer versehentlich per E-Mail einen Bericht erhält, für den er keine Anzeigeberechtigung hat, zeigt der Berichtsserver den Bericht nicht an. Weitere Informationen zu Abonnements finden Sie unten.  
  
## <a name="e-mail-server-configuration"></a>E-Mail-Server-Konfiguration  
 Für einen Berichtsserver im einheitlichen Modus wird die E-Mail-Übermittlungserweiterung mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurations-Manager im einheitlichen Modus und durch Bearbeiten der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationsdateien konfiguriert. Für einen Berichtsserver im SharePoint-Modus wird die E-Mail-Übermittlungserweiterung auf SharePoint-Verwaltungsseiten und in PowerShell-Skripts konfiguriert.  
  
 
 Informationen zum Konfigurieren eines Berichtsservers im einheitlichen Modus finden Sie unter [E-Mail-Einstellungen – Einheitlicher Modus von Reporting Services (Konfigurations-Manager)](https://msdn.microsoft.com/library/ms189342.aspx).
 
 
 Informationen zum Konfigurieren eines Berichtsservers im SharePoint-Modus finden Sie im folgenden Thema:  
  
  
## <a name="see-also"></a>Siehe auch  
 [Aufgaben und Berechtigungen](../../reporting-services/security/tasks-and-permissions.md)   
 [Abonnements und Übermittlung &#40; Reporting Services &#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Datengesteuerte Abonnements](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Role Assignments (Rollenzuweisungen)](../../reporting-services/security/role-assignments.md)  
  
  
