---
title: Deploying a Delivery Extension | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d072577828375a08c133bb1a68d93e652e5cf168
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="deploying-a-delivery-extension"></a>Bereitstellen von Übermittlungserweiterungen
  Übermittlungserweiterungen geben ihre Konfigurationsinformationen in Form einer XML-Konfigurationsdatei an. Die XML-Datei entspricht dem für Übermittlungserweiterungen definierten XML-Schema. Übermittlungserweiterungen verfügen über eine Infrastruktur zum Einstellen und Ändern der Konfigurationsdatei.  
  
 Wenn eine Übermittlungserweiterung ersetzt oder aktualisiert wird, bleiben alle Abonnements, die auf die Übermittlungserweiterung verweisen, gültig.  
  
 Nachdem Sie geschrieben und kompiliert Ihre [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] übermittlungserweiterung in eine [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Bibliothek, müssen Sie die Erweiterung in das entsprechende Verzeichnis kopieren und fügen Sie einen Eintrag in das entsprechende [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] -Konfigurationsdatei vornehmen, damit der Berichtsserver gefunden werden kann.  
  
## <a name="configuration-file-extension-element"></a>Extension-Element für die Konfigurationsdatei  
 Übermittlungserweiterungen, die Sie auf dem Berichtsserver bereitstellen müssen eingegeben werden, als **Erweiterung** Elemente in der Konfigurationsdatei. Die Konfigurationsdatei für den Berichtsserver heißt RSReportServer.config.  
  
 Die folgende Tabelle beschreibt die Attribute für die **Erweiterung** -Element für übermittlungserweiterungen.  
  
|Attribut|Description|  
|---------------|-----------------|  
|**Name**|Ein eindeutiger Name für die Erweiterung (z. B. "Berichtsserver-E-Mail" für eine E-Mail-Übermittlungserweiterung oder "Berichtsserver-Dateifreigabe" für eine Dateifreigabe-Übermittlungserweiterung). Die maximale Länge für das **Name** -Attribut beträgt 255 Zeichen. Der Name muss für sämtliche Einträge im **Extension** -Element einer Konfigurationsdatei eindeutig sein. Wenn ein Name doppelt vorhanden ist, gibt der Berichtsserver einen Fehler zurück.|  
|**Typ**|Eine durch Trennzeichen getrennte Liste, die den vollqualifizierten Namespace und den Namen der Assembly enthält|  
|**Visible**|Der Wert **"false"** gibt an, dass die übermittlungserweiterung auf Benutzeroberflächen nicht sichtbar sollten. Wenn das Attribut nicht enthalten ist, ist **true**der Standardwert.|  
  
 Weitere Informationen zu der Datei "rsreportserver.config", finden Sie unter [Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Bereitstellen der Erweiterung auf dem Berichtsserver  
 Der Berichtsserver verwendet Übermittlungserweiterungen zur Verarbeitung und Übermittlung von Benachrichtigungen oder Berichten. Sie sollten die Assembly für Übermittlungserweiterungen auf dem Berichtsserver als private Assembly bereitstellen. Sie müssen auch einen Eintrag in der Konfigurationsdatei des Berichtsservers RSReportServer.config vornehmen.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>So stellen Sie eine Assembly für Übermittlungserweiterungen auf einem Berichtsserver bereit  
  
1.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das BIN-Verzeichnis des Berichtsservers, auf dem Sie die Übermittlungserweiterung verwenden möchten. Der Standardspeicherort des Bin-Verzeichnis des Berichtsservers ist %ProgramFiles%\Microsoft SQL Server\MSRS13. \<InstanceName > \Reporting Services\ReportServer\bin.  
  
    > [!IMPORTANT]  
    >  Wenn Sie versuchen, eine vorhandene Assembly für Übermittlungserweiterungen zu überschreiben, müssen Sie zuerst den Berichtsserverdienst anhalten, bevor Sie die aktualisierte Assembly kopieren können. Starten Sie den Dienst neu, nachdem die Assembly kopiert wurde.  
  
2.  Nachdem die Assemblydatei kopiert wurde, öffnen Sie die Datei RSReportServer.config. Die Datei "rsreportserver.config" befindet sich in %ProgramFiles%\Microsoft SQL Server\MSRS13. \<InstanceName > \reporting-Verzeichnis. Sie müssen einen Eintrag in der Konfigurationsdatei für die Assemblydatei der Übermittlungserweiterung vornehmen. Sie können die Konfigurationsdatei mit öffnen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder einem einfachen Text-Editor, z. B. Notepad.  
  
3.  Suchen Sie die **Übermittlung** Element in der Datei "rsreportserver.config". In folgendem Verzeichnis muss ein Eintrag für die neu erstellte Übermittlungserweiterung erstellt werden:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für die Übermittlungserweiterung hinzu. Der Eintrag sollte enthalten eine **Erweiterung** Element mit Werten für **Namen** und **Typ**, und kann wie folgt aussehen:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     Der Wert für **Namen** ist der eindeutige Name der übermittlungserweiterung. Der Wert für **Typ** ist eine durch Trennzeichen getrennte Liste, die einen Eintrag für den vollqualifizierten Namespace der Klasse enthält, implementiert die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> -Schnittstelle, gefolgt vom Namen Assembly (ohne die Dateierweiterung .dll). Übermittlungserweiterungen sind standardmäßig sichtbar. Eine Erweiterung in Benutzeroberflächen wie dem Webportal auszublenden Hinzufügen einer **sichtbar** -Attribut auf die **Erweiterung** Element, und legen Sie dafür **"false"**.  
  
5.  Schließlich fügen Sie eine Codegruppe für die benutzerdefinierte Assembly, die gewährt **FullTrust** Berechtigung für die übermittlungserweiterung. Dazu fügen Sie die Codegruppe zur Datei "rssrvpolicy.config" befindet sich standardmäßig in %ProgramFiles%\Microsoft SQL Server\MSRS13. \<InstanceName > \reporting. Die Codegruppe kann folgendermaßen aussehen:  
  
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
  
     Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für die Übermittlungserweiterung auswählen können. Weitere Informationen zur Codezugriffssicherheit in [!INCLUDE[ssRS](../../../includes/ssrs-md.md)], finden Sie unter.[ Sichere Entwicklung &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>Überprüfen der Bereitstellung  
 Sie können prüfen, ob die Übermittlungserweiterung erfolgreich auf dem Berichtsserver bereitgestellt wurde, indem Sie die Webdienstmethode <xref:ReportService2010.ReportingService2010.ListExtensions%2A> verwenden. Sie können auch das Webportal öffnen, und stellen Sie sicher, dass die Erweiterung in der Liste der verfügbaren übermittlungserweiterungen für ein Abonnement enthalten ist. Weitere Informationen über das Webportal und Abonnements finden Sie unter [Abonnements und Übermittlung &#40; Reporting Services &#41; ](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

