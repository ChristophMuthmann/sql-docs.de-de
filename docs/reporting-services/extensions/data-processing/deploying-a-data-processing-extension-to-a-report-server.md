---
title: "Vorgehensweise: Bereitstellen einer Datenverarbeitungserweiterung für einen Berichtsserver | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c364b4811da7a34c7f186e99ba042d3f1b336910
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="deploying-a-data-processing-extension-to-a-report-server"></a>Bereitstellen einer Datenverarbeitungserweiterung für einen Berichtsserver
  Berichtsserver verwenden Datenverarbeitungserweiterungen zum Abrufen und Verarbeiten von Daten in gerenderten Berichten. Sie sollten Ihre Assembly für Datenverarbeitungserweiterungen auf dem Berichtsserver als private Assembly bereitstellen. Sie müssen auch einen Eintrag in der Konfigurationsdatei des Berichtsservers RSReportServer.config vornehmen.  
  
## <a name="procedures"></a>Vorgehensweisen  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>So stellen Sie eine Assembly für Datenverarbeitungserweiterungen bereit  
  
1.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das BIN-Verzeichnis des Berichtsservers, auf dem Sie die Datenverarbeitungserweiterung verwenden möchten. Das Standardverzeichnis für das BIN-Verzeichnis des Berichtsservers lautet %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<*Instanzname*>\Reporting Services\ReportServer\bin.  
  
    > [!NOTE]  
    >  Dieser Schritt verhindert ein Upgrade auf eine neuere Instanz von SQL Server. Weitere Informationen finden Sie unter [Upgrade and Migrate Reporting Services](../../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
2.  Nachdem die Assemblydatei kopiert wurde, öffnen Sie die Datei RSReportServer.config. Die Datei RSReportServer.config befindet sich im Verzeichnis "ReportServer". Sie müssen einen Eintrag in der Konfigurationsdatei für die Datei Ihrer Datenverarbeitungserweiterungsassembly vornehmen. Sie können die Konfigurationsdatei mit Visual Studio oder mit einem einfachen Text-Editor wie dem Microsoft-Editor öffnen.  
  
3.  Suchen Sie das **Data** -Element in der Datei RSReportServer.config. In folgendem Verzeichnis muss ein Eintrag für Ihre neu erstellte Datenverarbeitungserweiterung erstellt werden:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für die Datenverarbeitungserweiterung hinzu. Der Eintrag sollte ein **Extension**-Element mit den Werten **Name** und **Typ** enthalten und kann folgendermaßen aussehen:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     Der Wert für **Name** ist der eindeutige Name der Datenverarbeitungserweiterung. Der Wert für **Typ** ist eine durch Trennzeichen getrennte Liste, die einen Eintrag für den vollqualifizierten Namespace der Klasse enthält, welche die Schnittstellen <xref:Microsoft.ReportingServices.Interfaces.IExtension> und <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> implementiert, gefolgt vom Namen der Assembly (ohne die DLL-Dateierweiterung). Standardmäßig sind Datenverarbeitungserweiterungen sichtbar. Um eine Erweiterung auf Benutzeroberflächen wie dem Berichts-Manager auszublenden, fügen Sie dem **Extension** -Element das Attribut **Visible** hinzu und legen es auf **false**fest.  
  
5.  Fügen Sie eine Codegruppe für die benutzerdefinierte Assembly hinzu, die die Berechtigung **FullTrust** für Ihre Erweiterung erteilt. Hierzu fügen Sie die Codegruppe zur Datei „rssrvpolicy.config“ hinzu, die sich standardmäßig in %ProgramFiles%\Microsoft SQL Server\\<MSRS10_50.\<*Instanzname*>\Reporting Services\ReportServer befindet. Die Codegruppe kann folgendermaßen aussehen:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<Instance Name>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für die Datenverarbeitungserweiterung auswählen können. Weitere Informationen zur Codezugriffssicherheit in [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] finden Sie unter [Sichere Entwicklung (Reporting Services)](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="verifying-the-deployment"></a>Überprüfen der Bereitstellung  
 Sie können prüfen, ob Ihre Datenverarbeitungserweiterung erfolgreich auf dem Berichtsserver bereitgestellt wurde, indem Sie die Webdienstmethode <xref:ReportService2010.ReportingService2010.ListExtensions%2A> verwenden. Sie können auch den Berichts-Manager öffnen und prüfen, ob die Erweiterung in der Liste der verfügbaren Datenquellen enthalten ist. Weitere Informationen zu Berichts-Manager und Datenquellen finden Sie unter [Erstellen, Ändern und Löschen von freigegebenen Datenquellen (SSRS)](../../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Bereitstellen von Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Erweiterungen für Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementieren von Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
