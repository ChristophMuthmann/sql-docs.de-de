---
title: "Konfigurieren von E-mail für eine Reporting-Dienstanwendung Services | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38fc34a6-aae7-4dde-9ad2-f1eee0c42a9f
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 23cf66b01385b3c0f3e9ddc6ff24ea578cf5eec3
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="configure-e-mail-for-a-reporting-services-service-application"></a>Konfigurieren von E-Mail für eine Reporting Services-Dienstanwendung

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Datenwarnung sendet Warnungen in E-Mail-Nachrichten. Um E-Mails übermitteln zu können, kann es notwendig sein, dass Sie Ihre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung konfigurieren und die E-Mail-Übermittlungserweiterung für die Dienstanwendung ändern müssen. Die E-Mail-Einstellungen sind ebenfalls notwendig, wenn Sie beabsichtigen, die E-Mail-Übermittlungserweiterung für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnementfunktion zu verwenden.  

> [!NOTE]
> Reporting Services-Integration in SharePoint ist nach SQL Server 2016 nicht mehr verfügbar.
  
### <a name="to-configure-e-mail-for-the-shared-service"></a>So konfigurieren Sie E-Mail-Einstellungen für den freigegebenen Service  
  
1.  Klicken Sie in der SharePoint-Zentraladministration auf **Anwendungsverwaltung**.  
  
2.  Klicken Sie in der Gruppe **Dienstanwendungen** auf **Dienstanwendungen verwalten**.  
  
3.  Klicken Sie in der Liste **Name** auf den Namen Ihrer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.  
  
4.  Klicken Sie auf der Seite **Reporting Services-Anwendung verwalten** auf **E-Mail-Einstellungen** .  
  
5.  Wählen Sie **SMTP-Server verwenden**aus.  
  
6.  Geben Sie im Feld **SMTP-Server für ausgehende Nachrichten** den Namen eines SMTP-Servers ein.  
  
7.  Geben Sie im Feld **Absenderadresse** eine E-Mail-Adresse ein.  
  
     Diese Adresse wird als Absender für alle Warnungs-E-Mail-Nachrichten verwendet.  
  
     Das Konto des in **Absenderadresse** angegebenen Benutzers muss ein verwaltetes Konto sein, das Sie bei der Konfiguration des Anwendungspools für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung angegeben haben. Wenn Sie die entsprechenden Rechte besitzen, können Sie eine Liste aller vorhandenen verwalteten Konten auf der Seite Dienstkonten in der SharePoint-Zentraladministration anzeigen.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="ntlm-authentication"></a>NTLM-Authentifizierung  
  
1.  Wenn Ihre E-Mail-Umgebung NTLM-Authentifizierung erfordert und keinen anonymen Zugriff zulässt, müssen Sie die Konfiguration der E-Mail-Übermittlungserweiterung für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen ändern. Beispielsweise, wenn die folgende Meldung für **Letzte Ergebnisse** unter „ **Abonnements verwalten** -Seite: Abonnements“ angezeigt wird.  
  
    -   Fehler beim Senden von E-Mail: Für den SMTP-Server ist eine sichere Verbindung erforderlich, oder der Client wurde nicht authentifiziert. Die Serverantwort war: „5.7.1 Client wurde nicht authentifiziert. E-Mails werden nicht erneut gesendet“.  
  
     Ändern Sie **SMTPAuthenticate** so, dass der Wert "2" verwendet wird. Dieser Wert kann nicht über die Benutzeroberfläche geändert werden. Das folgende PowerShell-Skript-Beispiel aktualisiert die vollständige Konfiguration für die Berichtsserver-E-Mail-Übermittlungserweiterung für die Dienstanwendung mit dem Namen "SSRS_TESTAPPLICATION". Beachten Sie, dass einige der im Skript aufgeführten Knoten, wie z. B. die Absenderadresse, über die Benutzeroberfläche festgelegt werden können.  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION *"}  
    $emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
    $emailXml = [xml]$emailCfg   
    $emailXml.SelectSingleNode("//SMTPServer").InnerText = “your email server name"  
    $emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
    $emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
    $emailXml.SelectSingleNode("//From").InnerText = “your FROM email address”  
    Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
    ```  
  
2.  Wenn Sie den Namen Ihrer Dienstanwendung überprüfen müssen, führen Sie das Cmdlet **Get-SPRSServiceApplication**aus.  
  
    ```  
    get-sprsserviceapplication  
    ```  
  
3.  Das folgende Beispiel ruft den aktuellen Wert der E-Mail-Erweiterung für die Dienstanwendung mit dem Namen "SSRS_TESTAPPLICATION" ab.  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRSTEST_APPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
    ```  
  
4.  Das folgende Beispiel erstellt eine neue Datei mit dem Namen "emailconfig.txt" mit den aktuellen Werten der E-Mail-Erweiterung für die Dienstanwendung mit dem Namen "SSRS_TESTAPPLICATION".  
  
    ```  
    $app=get-sprsserviceapplication |where {$_.name -like "SSRS_TESTAPPLICATION*"}  
    Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml | out-file c:\emailconfig.txt  
    ```  
  
  
Weiteren Fragen wenden? [Versuchen Sie das Reporting Services-Forum stellen](http://go.microsoft.com/fwlink/?LinkId=620231)
