---
title: Konfigurieren von benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver | Microsoft Docs
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Forms authentication, configuring
- custom authentication [Reporting Services]
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 325b7d6f1015b6e5e81565df37d1c02d20e5802f
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="configure-custom-or-forms-authentication-on-the-report-server"></a>Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver

Reporting Services stellt eine erweiterbare Architektur zur Verfügung, mit der Sie benutzerdefinierte oder formularbasierte Authentifizierungsmodule integrieren können. Möglicherweise ist es ratsam, eine benutzerdefinierte Authentifizierungserweiterung zu implementieren, wenn die Bereitstellungsanforderungen keine Windows-integrierte Sicherheit oder grundlegende Authentifizierung umfassen. Das häufigste Szenario für die Verwendung der benutzerdefinierten Authentifizierung ist eine Unterstützung des Internet- oder Extranetzugriffs auf eine Webanwendung. Durch das Ersetzen der standardmäßigen Windows-Authentifizierungserweiterung durch eine benutzerdefinierte Erweiterung können Sie besser steuern, wie externen Benutzern Zugriff auf den Berichtsserver gewährt wird.  

In der Praxis erfordert das Bereitstellen einer benutzerdefinierten Authentifizierungserweiterung mehrere Schritte, darunter das Kopieren von Assemblys und Anwendungsdateien, das Bearbeiten von Konfigurationsdateien und das Testen. Dieses Thema konzentriert sich ganz auf die Authentifizierungseinstellungen, die Sie in den Konfigurationsdateien angeben.  

> [!NOTE]
>  Zum Erstellen einer benutzerdefinierten Authentifizierungserweiterung sind benutzerdefinierter Code und Kenntnisse der [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Sicherheit erforderlich. Wenn Sie keine benutzerdefinierte Authentifizierungserweiterung erstellen möchten, können Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory-Gruppen und -Konten verwenden, aber Sie sollten den Rahmen einer Berichtsserverbereitstellung deutlich verringern. Weitere Informationen zur benutzerdefinierten Authentifizierung finden Sie unter [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).

Darüber hinaus sollten Sie Formularauthentifizierung oder eine benutzerdefinierte authentifizierungserweiterung in einer SQL Server Reporting Services-Umgebung verwenden, die mit einem SharePoint-Produkt integriert ist, müssen Sie konfigurieren die SharePoint-Website für die Verwendung der Authentifizierungsmethode, die Sie auswählen. Weitere Informationen über das Konfigurieren der Authentifizierung in SharePoint finden Sie unter [Authentication Samples](http://go.microsoft.com/fwlink/?LinkId=115575) im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).



### <a name="to-configure-a-report-server-to-use-custom-authentication"></a>So konfigurieren Sie einen Berichtsserver für die Verwendung der benutzerdefinierten Authentifizierung

1.  Öffnen Sie RSReportServer.config in einem Text-Editor.

2.  Suchen \< **Authentifizierung**>.

3.  Kopieren Sie die folgende XML-Struktur:

    ```
    <Authentication>
          <AuthenticationTypes>
                 <Custom />
          </AuthenticationTypes>
          <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    ```

4.  Fügen Sie ihn über die vorhandenen Einträge für \< **Authentifizierung**>.

     Beachten Sie, dass Sie **Custom** nicht mit anderen Authentifizierungstypen verwenden können.

5.  Speichern Sie die Datei.

6.  Öffnen Sie die Datei Web.config für den Berichtsserver. Standardmäßig befindet sich diese Datei unter "Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportServer".

7.  Suchen Sie **authentication mode** , und legen Sie dafür **Forms**fest.

    ```
    <authentication mode = "Forms" />
    ```

8.  Suchen Sie **identity impersonate** , und legen Sie dafür **False**fest.

    ```
    <identity impersonate = "false" />  
    ```
9. Fügen Sie der Konfigurationsdatei die Elementstruktur **PassThroughCookies** hinzu. Weitere Informationen finden Sie unter [im Web-Portal zum Übergeben von benutzerdefinierten Authentifizierungscookies konfigurieren](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
10. Speichern Sie die Datei.  
  
11. Wenn Sie eine horizontal skalierte Bereitstellung konfiguriert haben, wiederholen Sie alle vorherigen Schritte für andere in der Bereitstellung vorhandene Berichtsserver.  
  
12. Starten Sie den Berichtsserver neu, um alle momentan geöffneten Sitzungen zu beenden.  

## <a name="see-also"></a>Siehe auch

[Implementieren von Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
[Reporting Services benutzerdefinierte Sicherheitsrolle Beispiel (GitHub)](https://github.com/Microsoft/Reporting-Services/tree/master/CustomSecuritySample)  
[Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
[RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
[Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
Weiteren Fragen wenden? [Wiederholen Sie den Reporting Services-forum](http://go.microsoft.com/fwlink/?LinkId=620231)
