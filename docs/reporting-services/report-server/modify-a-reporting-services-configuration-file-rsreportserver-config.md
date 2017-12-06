---
title: "Ändern einer Reporting Services-Konfigurationsdatei („RSreportserver.config“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
caps.latest.revision: "9"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d1b8d12e3b01fc8717770ae5fdb117f114ae324d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>Ändern einer Reporting Services-Konfigurationsdatei (RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] werden Anwendungseinstellungen in einem Satz von Konfigurationsdateien gespeichert. Beim Setup werden die Konfigurationsdateien für jede Berichtsserverinstanz erstellt, die Sie installieren. In jeder Datei werden Werte entweder während der Installation festgelegt oder aber wenn Sie Tools und Anwendungen zum Konfigurieren eines Servers für einen Vorgang verwenden. In einigen Fällen müssen Sie eine Datei direkt ändern, um erweiterte Einstellungen hinzuzufügen oder zu konfigurieren. Konfigurationseinstellungen werden als XML-Elemente oder -Attribute angegeben. Wenn Sie sich mit XML und Konfigurationsdateien auskennen, können Sie mit einem Text- oder Code-Editor benutzerdefinierbare Einstellungen ändern.  
  
 Einige Konfigurationseinstellungen können nur mithilfe eines Tools festgelegt werden. Einstellungen, die verschlüsselte Werte enthalten, müssen mit dem Reporting Services-Konfigurationstool, dem Setupprogramm oder dem Befehlszeilen-Hilfsprogramm **rsconfig** geändert werden. Zum Ausführen dieser Tools müssen Sie ein Mitglied der lokalen Administratorengruppe sein.  
  
> [!IMPORTANT]  
>  Gehen Sie beim Ändern der Konfigurationsdateien vorsichtig vor. Wenn Sie eine Einstellung ändern, die für die interne Verwendung reserviert ist, wird möglicherweise die Installation deaktiviert. Im Allgemeinen sollten Sie Konfigurationseinstellungen nur ändern, wenn ein bestimmtes Problem behoben werden muss. Weitere Informationen darüber, welche Einstellungen problemlos geändert werden können, finden Sie unter [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) oder [RSReportDesigner-Konfigurationsdatei](../../reporting-services/report-server/rsreportdesigner-configuration-file.md). Weitere Informationen zu Konfigurationsdateien finden Sie in der [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Produktdokumentation.  
  
 In diesem Thema:  
  
-   [Lesen und Verwenden von Konfigurationswerten](#bkmk_read_values)  
  
-   [Informationen zu Standardwerten](#bkmk_default_values)  
  
-   [Löschen von Konfigurationseinstellungen](#bkmk_delete_config_settings)  
  
-   [So bearbeiten Sie eine Reporting Services-Konfigurationsdatei](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> Lesen und Verwenden von Konfigurationswerten  
 Ein Berichtsserver liest die Konfigurationsdateien beim Starten des Diensts und bei jedem Speichern der Konfigurationsdatei. Neue und überarbeitete Werte werden in einer neuen Anwendungsdomäne wirksam, nachdem die aktuelle Anwendungsdomäne abgelaufen ist. Wenn möglich werden Anforderungen, die in der aktuellen Anwendungsdomäne noch verarbeitet werden, noch abgeschlossen. Einige Einstellungen erfordern jedoch einen unmittelbaren Wiederverwendungsvorgang der Anwendungsdomäne. In diesem Fall werden alle Anforderungen, die gerade verarbeitet werden, in einer neuen Anwendungsdomäne neu gestartet.  
  
 Wenn der Berichtsserver einen ungültigen Wert entdeckt, schreibt er einen Fehler in das Windows-Anwendungsprotokoll und startet dann nicht oder verwendet den Standardwert, abhängig vom Fehler.  
  
-   Wenn der Fehler wegen fehlerhafter XML auftritt, wird der Berichtsserver nicht gestartet. Wird der Berichtsserver ausgeführt, während Sie den Fehler einführen, ignoriert der Berichtsserver die ungültige Konfigurationsdatei solange, bis der Berichtsserver erneut startet oder die Anwendungsdomäne wiederverwendet wird. Nach Erkennung des Fehlers wird der Berichtsserver nicht mehr gestartet.  
  
-   Wenn der Fehler wegen eines fehlerhaften Konfigurationswerts auftritt, verwendet der Server interne Standardwerte und schreibt einen Fehler in das Ablaufverfolgungsprotokoll. In den wenigen Fällen, in denen interne Standardwerte nicht verfügbar sind, gibt der Server den rsServerConfigurationError-Fehler zurück, wenn die ungültige Konfigurationseinstellung kritisch für Servervorgänge ist. Fehler zu fehlenden oder ungültigen kritischen Einstellungen werden an die Clientanwendung in Form einer HTML-Fehlerseite zurückgegeben und in das Ereignisprotokoll geschrieben.  
  
 Alle Konfigurationsdateiänderungen werden einschließlich erfolgreicher Änderungen im Ablaufverfolgungsprotokoll des Berichtsservers aufgezeichnet. Nur Fehler werden im Ereignisprotokolldatei der Anwendung protokolliert.  
  
##  <a name="bkmk_default_values"></a> Informationen zu Standardwerten  
 Die meisten Konfigurationseinstellungen haben Standardwerte, die intern im Berichtsserver festgelegt sind. Der Berichtsserver verwendet diese Werte, wenn ein benutzerdefinierter Wert ungültig oder nicht angegeben ist. Wenn ein Standardwert wegen einer fehlerhaften Konfigurationseinstellung verwendet werden muss, wird ein Fehler in das Ablaufverfolgungsprotokoll geschrieben.  
  
##  <a name="bkmk_delete_config_settings"></a> Löschen von Konfigurationseinstellungen  
 Bei Konfigurationseinstellungen, die Standardwerte aufweisen, hat die Löschung der Einstellung aus der Konfigurationsdatei keinerlei Auswirkungen. Die meisten Konfigurationseinstellungen werden tatsächlich intern definiert und konfiguriert. Wenn Sie ein Element aus der Konfigurationsdatei löschen, ist die interne Kopie nach wie vor vorhanden, und es wird der dafür definierte Standardwert verwendet.  
  
##  <a name="bkmk_edit_configuation_file"></a> So bearbeiten Sie eine Reporting Services-Konfigurationsdatei  
  
1.  Suchen Sie die Konfigurationsdatei, die Sie bearbeiten möchten:  
  
    -   **RSReportServer.config** befindet sich im folgenden Ordner:  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
        
        ||  
        |-|  
        |**[!INCLUDE[applies](../../includes/applies-md.md)]** Januar 2017 Technical Preview von Power BI-Berichten in SQL Server Reporting Services|
        
        ```  
        C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
        ```
  
    -   **RSReportServerServices.exe.config** befindet sich im folgenden Ordner:  
    
        > [!NOTE] 
        > Dies steht in der Technical Preview von Berichten von Power BI in SQL Server Reporting Services von Januar 2017 nicht zur Verfügung.
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   **RSReportDesigner.config** befindet sich im folgenden Ordner:  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  Speichern Sie eine Kopie der Datei, falls Sie einen Rollback für die Änderungen ausführen müssen.  
  
3.  Öffnen Sie die ursprüngliche Datei im Editor oder einem Code-Editor. Verwenden Sie nicht WordPad; dadurch wird die Dateilänge vor dem Speichern der Datei festgelegt und ein Fehler wegen ungültiger Zeichen in das Ablaufverfolgungsprotokoll geschrieben.  
  
4.  Geben Sie das Element oder den Wert ein, das bzw. den Sie hinzufügen oder verwenden möchten. Bei Elementen wird zwischen Groß- und Kleinschreibung unterschieden. Wenn Sie ein Element hinzufügen, stellen Sie sicher, die richtigen Groß- und Kleinbuchstaben zu verwenden. Spezifische Anweisungen zum Bearbeiten von Konfigurationsdateien sind verfügbar, wenn Sie Renderingerweiterungen, Authentifizierungserweiterungen oder Datenverarbeitungserweiterungen anpassen:  
  
    -   [Authentication with the Report Server (Authentifizierung mit dem Berichtsserver)](../../reporting-services/security/authentication-with-the-report-server.md)  
  
    -   [Configure the Web Portal to Pass Custom Authentication Cookies (Konfigurieren des Webportals für die Übergabe von benutzerdefinierten Authentifizierungscookies)](../../reporting-services/security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)
  
    -   [Anpassen der Parameter für Renderingerweiterungen in der Datei RSReportServer.config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  Speichern Sie die Datei.  
  
6.  Überprüfen Sie die Ablaufverfolgungs-Protokolldateien, um zu überprüfen, dass keine Fehler aufgetreten sind. Wenn Fehlerbedingungen auftreten, wurde eine Einstellung oder ihr Wert falsch angegeben. Gültige Werte für die Einstellungen, die Fehler verursachen, finden Sie unter [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) . Weitere Informationen zum Anzeigen von Ablaufverfolgungsprotokollen finden Sie unter [Berichtsserverdienst-Ablaufverfolgungsprotokoll](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="see-also"></a>Siehe auch  
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [ReportingServicesService-Konfigurationsdatei](../../reporting-services/report-server/reportingservicesservice-configuration-file.md)   
 [RSReportDesigner-Konfigurationsdatei](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Bereitstellen von Datenverarbeitungserweiterungen](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Bereitstellen von Übermittlungserweiterungen](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [Bereitstellen von Renderingerweiterungen](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)  
  
  
