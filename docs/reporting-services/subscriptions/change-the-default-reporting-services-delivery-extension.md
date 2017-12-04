---
title: "Ändern der Standardübermittlungserweiterung für Reporting Services | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Report Manager [Reporting Services], default delivery extension
ms.assetid: 5f6fee72-01bf-4f6c-85d2-7863c46c136b
caps.latest.revision: "19"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e46c81c5c96bc3c71eef8a2ca48a89c177ca1700
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="change-the-default-reporting-services-delivery-extension"></a>Ändern der Standardübermittlungserweiterung für Reporting Services
  Sie können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationseinstellungen ändern, um die Standardübermittlungserweiterung in der Liste **Übermittelt von** einer Abonnementdefinitionsseite zu ändern. Sie können die Konfiguration z. B. so ändern, dass beim Erstellen eines neuen Abonnements durch den Benutzer standardmäßig eine Dateifreigabeübermittlung statt einer E-Mail-Übermittlung ausgewählt wird. Sie können auch die Reihenfolge der in der Benutzeroberfläche aufgeführten Übermittlungserweiterungen ändern.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | SharePoint-Modus von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]   
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthält E-Mail- und Windows-Dateifreigabe-Übermittlungserweiterungen. Ihr Berichtsserver verfügt möglicherweise über zusätzliche Übermittlungserweiterungen, wenn Sie benutzerdefinierte Erweiterungen oder Drittanbietererweiterungen zur Unterstützung der benutzerdefinierten Übermittlung bereitgestellt haben. Die Verfügbarkeit einer Übermittlungserweiterung hängt davon ab, ob sie auf einem Berichtsserver bereitgestellt wurde.  
  
## <a name="default-native-mode-report-server-configuration"></a>Standardkonfiguration für einen Berichtsserver im einheitlichen Modus  
 Die Reihenfolge der Übermittlungserweiterungen im Berichts-Manager in der Liste **Übermittelt von** basiert auf der Reihenfolge der Übermittlungserweiterungseinträge in der Datei **RSReportServer.config** . Im folgenden Bild wird E-Mail zuerst in der Liste angezeigt und ist standardmäßig ausgewählt.  
  
 ![Standardliste der Übermittlungserweiterungen](../../reporting-services/subscriptions/media/ssrs-default-delivery.png "default list of delivery extensions")  
  
 Im Folgenden ist der Standardabschnitt von **RSReportServer.config** dargestellt, der die Standardübermittlungserweiterung und die Reihenfolge steuert, in der diese im Berichts-Manager angezeigt werden. Beachten Sie, dass die E-Mail in der Datei zuerst angezeigt und als Standard festgelegt wird.  
  
```  
<DeliveryUI>  
     <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
          <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
               <Configuration>  
               <RSEmailDPConfiguration>  
                    <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
               </RSEmailDPConfiguration>  
               </Configuration>  
     </Extension>  
     <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>  
</DeliveryUI>  
```  
  
#### <a name="configure-file-share-delivery-as-the-default-delivery-extension-in-report-manager"></a>Konfigurieren der Dateifreigabeübermittlung als Standardübermittlungserweiterung im Berichts-Manager  
  
1.  Mit den Schritten in diesem Verfahren können Sie die Konfiguration so ändern, dass die Dateifreigabe-Übermittlung als erste Option in der Benutzeroberfläche aufgeführt wird und Standardauswahl ist.  
  
     Öffnen Sie die Datei RSReportServer.config in einem Text-Editor. Weitere Informationen zur Konfigurationsdatei finden Sie unter [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md). Nach Änderung der Konfiguration sieht die Benutzeroberfläche wie folgt aus:  
  
     ![Geänderte Liste der Übermittlungserweiterungen](../../reporting-services/subscriptions/media/ssrs-modified-delivery.png "modified list of delivery extensions")  
  
2.  Ändern Sie den Abschnitt DeliveryUI wie folgt und beachten Sie die wichtigsten Änderungen:  
  
    1.  Die FileShare-Erweiterung befindet sich vor der E-Mail-Erweiterung. Dadurch wird die Reihenfolge geändert, in der die Erweiterungen im Berichts-Manager aufgeführt sind.  
  
    2.  Die Dateifreigabeerweiterung enthält das DefaultExtension-Tag `<DefaultDeliveryExtension>True</DefaultDeliveryExtension>` , und das Extension-Tag wurde hinzugefügt `</Extension>`.  
  
    3.  Die E-Mail-Erweiterung ist nicht mehr als Standard konfiguriert. `<DefaultDeliveryExtension>False</DefaultDeliveryExtension>`  
  
    ```  
    <DeliveryUI>  
         <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider">  
              <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
         </Extension>  
         <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
         <DefaultDeliveryExtension>False</DefaultDeliveryExtension>  
         <Configuration>  
              <RSEmailDPConfiguration>  
                   <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
              </RSEmailDPConfiguration>  
         </Configuration>  
         </Extension>  
    </DeliveryUI>  
    ```  
  
3.  Speichern Sie die Konfigurationsdatei.  
  
4.  Innerhalb weniger Minuten wird der Berichtsserver die Konfigurationsdatei laden und die neuen Einstellungen übernehmen. Sie können den Berichtsserverdienst neu starten, um das Laden der Konfigurationsdatei zu erzwingen.  
  
     Das folgende Ereignis wird beim Lesen der Konfiguration im Windows-Ereignisprotokoll geschrieben.  
  
     **Ereignis-ID:** 109  
  
     **Quelle:** Berichtsserver-Windows-Dienst (Instanzname)  
  
     Die Datei „RSReportServer.config“ wurde geändert.  
  
## <a name="sharepoint-mode-report-servers"></a>Berichtsserver im SharePoint-Modus  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint-Modus speichert Erweiterungsinformationen in den SharePoint-Dienstanwendungsdatenbanken, und nicht in der Datei „RsrReportServer.config“. Im SharePoint-Modus wird die Konfiguration für die Übermittlungserweiterung mit PowerShell geändert.  
  
#### <a name="configure-the-default-delivery-extension"></a>Konfigurieren der Standardübermittlungserweiterung  
  
1.  Öffnen Sie die **SharePoint-Verwaltungsshell**.  
  
2.  Sie können diesen Schritt überspringen, wenn Sie den Namen Ihrer [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung bereits kennen. Verwenden Sie den folgende PowerShell-Befehl zum Auflisten der [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendungen in der SharePoint-Farm.  
  
    ```  
    get-sprsserviceapplication | format-list *  
    ```  
  
3.  Führen Sie den folgenden PowerShell-Befehl zum Überprüfen der aktuellen Standardübermittlungserweiterung für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung „ssrsapp“ aus.  
  
    ```  
    $app=get-sprsserviceapplication | where {$_.name -like "ssrsapp*"};Get-SPRSExtension -identity $app | where{$_.ServerDirectivesXML -like "<DefaultDelivery*"} | format-list *  
  
    ```
  
## <a name="see-also"></a>Siehe auch  
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [RsReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Dateifreigabeübermittlung in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [E-Mail Delivery in Reporting Services (E-Mail-Übermittlung in Reporting Services)](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   
 [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)  
  
  
