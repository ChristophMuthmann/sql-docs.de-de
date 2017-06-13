---
title: 'Vorgehensweise: Bereitstellen eine Datenverarbeitungserweiterung auf einem Berichtsserver | Microsoft Docs'
ms.custom: 
ms.date: 03/06/2017
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
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
caps.latest.revision: 45
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ed23ebf2bd6cbecbd028488c5188368e1a076d46
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="deploying-a-data-processing-extension-to-a-report-server"></a>Deploying a Data Processing Extension auf einem Berichtsserver
  Berichtsserver verwenden Datenverarbeitungserweiterungen zum Abrufen und Verarbeiten von Daten in gerenderten Berichten. Sie sollten Ihre Assembly für Datenverarbeitungserweiterungen auf dem Berichtsserver als private Assembly bereitstellen. Sie müssen auch einen Eintrag in der Konfigurationsdatei des Berichtsservers RSReportServer.config vornehmen.  
  
## <a name="procedures"></a>Vorgehensweisen  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>So stellen Sie eine Assembly für Datenverarbeitungserweiterungen bereit  
  
1.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das BIN-Verzeichnis des Berichtsservers, auf dem Sie die Datenverarbeitungserweiterung verwenden möchten. Der Standardspeicherort des Bin-Verzeichnis des Berichtsservers ist %ProgramFiles%\Microsoft SQL Server\MSRS10_50. \< *Instanzname*> \Reporting Services\ReportServer\bin.  
  
    > [!NOTE]  
    >  Dieser Schritt verhindert ein Upgrade auf eine neuere Instanz von SQL Server. Weitere Informationen finden Sie unter [Upgrade and Migrate Reporting Services](../../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
2.  Nachdem die Assemblydatei kopiert wurde, öffnen Sie die Datei RSReportServer.config. Die Datei RSReportServer.config befindet sich im Verzeichnis "ReportServer". Sie müssen einen Eintrag in der Konfigurationsdatei für die Datei Ihrer Datenverarbeitungserweiterungsassembly vornehmen. Sie können die Konfigurationsdatei mit Visual Studio oder einem einfachen Text-Editor wie Editor öffnen.  
  
3.  Suchen Sie das **Data** -Element in der Datei RSReportServer.config. In folgendem Verzeichnis muss ein Eintrag für Ihre neu erstellte Datenverarbeitungserweiterung erstellt werden:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für die Datenverarbeitungserweiterung hinzu. Der Eintrag sollte enthalten eine **Erweiterung** Element mit Werten für **Namen** und **Typ** und kann wie folgt aussehen:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     Der Wert für **Namen** ist der eindeutige Name der datenverarbeitungserweiterung. Der Wert für **Typ** ist eine durch Trennzeichen getrennte Liste, die einen Eintrag für den vollqualifizierten Namespace der Klasse enthält, implementiert die <xref:Microsoft.ReportingServices.Interfaces.IExtension> und <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> Schnittstellen, gefolgt vom Namen Assembly (ohne die Dateierweiterung .dll). Standardmäßig sind Datenverarbeitungserweiterungen sichtbar. Um eine Erweiterung auf Benutzeroberflächen wie dem Berichts-Manager auszublenden, fügen Sie dem **Extension** -Element das Attribut **Visible** hinzu und legen es auf **false**fest.  
  
5.  Fügen Sie eine Codegruppe für die benutzerdefinierte Assembly, die gewährt **FullTrust** Berechtigung für die Erweiterung. Hierzu fügen die Codegruppe zur Datei "rssrvpolicy.config" befindet sich standardmäßig in %ProgramFiles%\Microsoft SQL Server\\< MSRS10_50.\< *Instanzname*> \reporting. Die Codegruppe kann folgendermaßen aussehen:  
  
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
  
 Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für die Datenverarbeitungserweiterung auswählen können. Weitere Informationen zur Codezugriffssicherheit in [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], finden Sie unter [sichere Entwicklung &#40; Reporting Services &#41; ](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="verifying-the-deployment"></a>Überprüfen der Bereitstellung  
 Sie können prüfen, ob Ihre Datenverarbeitungserweiterung erfolgreich auf dem Berichtsserver bereitgestellt wurde, indem Sie die Webdienstmethode <xref:ReportService2010.ReportingService2010.ListExtensions%2A> verwenden. Sie können auch den Berichts-Manager öffnen und prüfen, ob die Erweiterung in der Liste der verfügbaren Datenquellen enthalten ist. Weitere Informationen zu Berichts-Manager und Datenquellen finden Sie unter [Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Deploying a Data Processing Extension](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
