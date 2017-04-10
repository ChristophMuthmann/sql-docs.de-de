---
title: "Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Formularauthentifizierung, konfigurieren"
  - "Benutzerdefinierte Authentifizierung [Reporting Services]"
ms.assetid: e8601a8f-e66d-4649-8e4d-a46ca20ec7d0
caps.latest.revision: 20
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# Konfiguration der benutzerdefinierten oder Formularauthentifizierung auf dem Berichtsserver
  Reporting Services stellt eine erweiterbare Architektur zur Verfügung, mit der Sie benutzerdefinierte oder formularbasierte Authentifizierungsmodule integrieren können. Möglicherweise ist es ratsam, eine benutzerdefinierte Authentifizierungserweiterung zu implementieren, wenn die Bereitstellungsanforderungen keine Windows-integrierte Sicherheit oder grundlegende Authentifizierung umfassen. Das häufigste Szenario für die Verwendung der benutzerdefinierten Authentifizierung ist eine Unterstützung des Internet- oder Extranetzugriffs auf eine Webanwendung. Durch das Ersetzen der standardmäßigen Windows-Authentifizierungserweiterung durch eine benutzerdefinierte Erweiterung können Sie besser steuern, wie externen Benutzern Zugriff auf den Berichtsserver gewährt wird.  
  
 In der Praxis erfordert das Bereitstellen einer benutzerdefinierten Authentifizierungserweiterung mehrere Schritte, darunter das Kopieren von Assemblys und Anwendungsdateien, das Bearbeiten von Konfigurationsdateien und das Testen. Dieses Thema konzentriert sich ganz auf die Authentifizierungseinstellungen, die Sie in den Konfigurationsdateien angeben.  
  
> [!NOTE]  
>  Zum Erstellen einer benutzerdefinierten Authentifizierungserweiterung sind benutzerdefinierter Code und Kenntnisse der [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] -Sicherheit erforderlich. Wenn Sie keine benutzerdefinierte Authentifizierungserweiterung erstellen möchten, können Sie [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory-Gruppen und -Konten verwenden, aber Sie sollten den Rahmen einer Berichtsserverbereitstellung deutlich verringern. Weitere Informationen zur benutzerdefinierten Authentifizierung finden Sie unter [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md).  
  
 Wenn Sie eine Formular- oder benutzerdefinierte Authentifizierungserweiterung in einer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Umgebung verwenden möchten, die mit einem SharePoint-Produkt integriert ist, müssen Sie zusätzlich die SharePoint-Website für die Verwendung der von Ihnen gewählten Authentifizierungsmethode konfigurieren. Weitere Informationen über das Konfigurieren der Authentifizierung in SharePoint finden Sie unter [Authentication Samples](http://go.microsoft.com/fwlink/?LinkId=115575) im [!INCLUDE[msCoName](../../includes/msconame-md.md)] Developer Network (MSDN).  
  
### So konfigurieren Sie einen Berichtsserver für die Verwendung der benutzerdefinierten Authentifizierung  
  
1.  Öffnen Sie RSReportServer.config in einem Text-Editor.  
  
2.  Suchen Sie nach \<**Authentication**>.  
  
3.  Kopieren Sie die folgende XML-Struktur:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <Custom />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
4.  Ersetzen Sie damit die vorhandenen Einträge für \<**Authentication**>.  
  
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
  
9. Öffnen Sie die Datei Web.config für den Berichts-Manager. Standardmäßig befindet sich diese Datei unter \Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\ReportManager.  
  
10. Suchen Sie **authentication mode** , und legen Sie dafür **Forms**fest.  
  
    ```  
    <authentication mode = "Forms" />  
    ```  
  
11. Suchen Sie **identity impersonate** , und legen Sie dafür **False**fest.  
  
    ```  
    <identity impersonate = "false" />  
    ```  
  
12. Fügen Sie der Konfigurationsdatei die Elementstruktur **PassThroughCookies** hinzu. Weitere Informationen finden Sie unter [Konfigurieren des Berichts-Managers für die Übergabe von benutzerdefinierten Authentifizierungscookies](../Topic/Configure%20Report%20Manager%20to%20Pass%20Custom%20Authentication%20Cookies.md).  
  
13. Speichern Sie die Datei.  
  
14. Wenn Sie eine horizontal skalierte Bereitstellung konfiguriert haben, wiederholen Sie alle vorherigen Schritte für andere in der Bereitstellung vorhandene Berichtsserver.  
  
15. Starten Sie den Berichtsserver neu, um alle momentan geöffneten Sitzungen zu beenden.  
  
## Siehe auch  
 [Implementieren von Sicherheitserweiterungen](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
 [Authentifizierung mit dem Berichtsserver](../../reporting-services/security/authentication-with-the-report-server.md)   
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Konfigurieren der Standardauthentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)   
 [Konfigurieren der Windows-Authentifizierung auf dem Berichtsserver](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
  
  