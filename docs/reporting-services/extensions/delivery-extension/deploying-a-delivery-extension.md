---
title: "Bereitstellen von Übermittlungserweiterungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: "45"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ac89e662415b74bab2003af1462453ad96b369b1
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="deploying-a-delivery-extension"></a>Bereitstellen von Übermittlungserweiterungen
  Übermittlungserweiterungen geben ihre Konfigurationsinformationen in Form einer XML-Konfigurationsdatei an. Die XML-Datei entspricht dem für Übermittlungserweiterungen definierten XML-Schema. Übermittlungserweiterungen verfügen über eine Infrastruktur zum Einstellen und Ändern der Konfigurationsdatei.  
  
 Wenn eine Übermittlungserweiterung ersetzt oder aktualisiert wird, bleiben alle Abonnements, die auf die Übermittlungserweiterung verweisen, gültig.  
  
 Nachdem Sie die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung geschrieben und in eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Bibliothek kompiliert haben, müssen Sie die Erweiterung in das entsprechende Verzeichnis kopieren und einen Eintrag in der entsprechenden [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Konfigurationsdatei vornehmen, damit sie vom Berichtsserver gefunden werden kann.  
  
## <a name="configuration-file-extension-element"></a>Extension-Element für die Konfigurationsdatei  
 Übermittlungserweiterungen, die Sie für den Berichtsserver bereitstellen, müssen in der Konfigurationsdatei als **Extension**-Elemente hinzugefügt werden. Die Konfigurationsdatei für den Berichtsserver heißt RSReportServer.config.  
  
 In der folgenden Tabelle werden die Attribute für das **Extension**-Element für Übermittlungserweiterungen beschrieben.  
  
|attribute|Description|  
|---------------|-----------------|  
|**Name**|Ein eindeutiger Name für die Erweiterung (z. B. "Berichtsserver-E-Mail" für eine E-Mail-Übermittlungserweiterung oder "Berichtsserver-Dateifreigabe" für eine Dateifreigabe-Übermittlungserweiterung). Die maximale Länge für das **Name** -Attribut beträgt 255 Zeichen. Der Name muss für sämtliche Einträge im **Extension** -Element einer Konfigurationsdatei eindeutig sein. Wenn ein Name doppelt vorhanden ist, gibt der Berichtsserver einen Fehler zurück.|  
|**Typ**|Eine durch Trennzeichen getrennte Liste, die den vollqualifizierten Namespace und den Namen der Assembly enthält|  
|**Visible**|Der Wert **FALSE** gibt an, dass die Übermittlungserweiterung auf Benutzeroberflächen nicht sichtbar sein soll. Wenn das Attribut nicht enthalten ist, ist **true**der Standardwert.|  
  
 Weitere Informationen über die Datei „RSReportServer.config“ finden Sie unter [Reporting Services-Konfigurationsdateien](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Bereitstellen der Erweiterung auf dem Berichtsserver  
 Der Berichtsserver verwendet Übermittlungserweiterungen zur Verarbeitung und Übermittlung von Benachrichtigungen oder Berichten. Sie sollten die Assembly für Übermittlungserweiterungen auf dem Berichtsserver als private Assembly bereitstellen. Sie müssen auch einen Eintrag in der Konfigurationsdatei des Berichtsservers RSReportServer.config vornehmen.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>So stellen Sie eine Assembly für Übermittlungserweiterungen auf einem Berichtsserver bereit  
  
1.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das BIN-Verzeichnis des Berichtsservers, auf dem Sie die Übermittlungserweiterung verwenden möchten. Das Standardverzeichnis für das BIN-Verzeichnis des Berichtsservers lautet %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer\bin.  
  
    > [!IMPORTANT]  
    >  Wenn Sie versuchen, eine vorhandene Assembly für Übermittlungserweiterungen zu überschreiben, müssen Sie zuerst den Berichtsserverdienst anhalten, bevor Sie die aktualisierte Assembly kopieren können. Starten Sie den Dienst neu, nachdem die Assembly kopiert wurde.  
  
2.  Nachdem die Assemblydatei kopiert wurde, öffnen Sie die Datei RSReportServer.config. Die Datei „RSReportServer.config“ befindet sich im Verzeichnis %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer directory. Sie müssen einen Eintrag in der Konfigurationsdatei für die Assemblydatei der Übermittlungserweiterung vornehmen. Sie können die Konfigurationsdatei mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder in einem einfachen Text-Editor wie Editor öffnen.  
  
3.  Suchen Sie das **Delivery**-Element in der Datei „RSReportServer.config“. In folgendem Verzeichnis muss ein Eintrag für die neu erstellte Übermittlungserweiterung erstellt werden:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für die Übermittlungserweiterung hinzu. Der Eintrag sollte ein **Extension**-Element mit den Werten **Name** und **Typ** enthalten und kann folgendermaßen aussehen:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     Der Wert für **Name** ist der eindeutige Name der Übermittlungserweiterung. Der Wert für **Typ** ist eine durch Trennzeichen getrennte Liste, die einen Eintrag für den vollqualifizierten Namespace der Klasse enthält, die die Schnittstelle <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> implementiert, gefolgt vom Namen der Assembly (ohne die DLL-Dateierweiterung). Übermittlungserweiterungen sind standardmäßig sichtbar. Fügen Sie dem **Extension**-Element das Attribut **Visible** hinzu und legen es auf **FALSE** fest, um eine Erweiterung auf Benutzeroberflächen wie dem Webportal auszublenden.  
  
5.  Zum Schluss müssen Sie eine Codegruppe für die benutzerdefinierte Assembly hinzufügen, die die Berechtigung **FullTrust** für Ihre Erweiterung erteilt. Hierzu fügen Sie die Codegruppe zur Datei „rssrvpolicy.config“ hinzu, die sich standardmäßig in %ProgramFiles%\Microsoft SQL Server\MSRS13.\<InstanceName>\Reporting Services\ReportServer befindet. Die Codegruppe kann folgendermaßen aussehen:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für die Übermittlungserweiterung auswählen können. Weitere Informationen zur Codezugriffssicherheit in [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] finden Sie unter [Sichere Entwicklung (Reporting Services)](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
   
## <a name="verifying-the-deployment"></a>Überprüfen der Bereitstellung  
 Sie können prüfen, ob die Übermittlungserweiterung erfolgreich auf dem Berichtsserver bereitgestellt wurde, indem Sie die Webdienstmethode <xref:ReportService2010.ReportingService2010.ListExtensions%2A> verwenden. Sie können auch das Webportal öffnen und prüfen, ob die Erweiterung in der Liste der für ein Abonnement verfügbaren Übermittlungserweiterungen enthalten ist. Weitere Informationen zu Abonnements finden Sie unter [Abonnements und Übermittlung (Reporting Services)](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Implementieren von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
