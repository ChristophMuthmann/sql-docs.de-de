---
title: Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/17/2017
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
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
caps.latest.revision: "10"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 04e46f640b9715cf39dea1544ca2fcd52c7baab9
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus
  In diesem Abschnitt finden Sie Verfahren zum Konfigurieren einer Berichtsserverinstanz im einheitlichen Modus mithilfe des Reporting Services-Konfigurations-Managers.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 Die Themen in diesem Abschnitt sind in Kategorien geordnet, sodass Sie die benötigten Anweisungen leichter finden können. Der erste Abschnitt enthält Themen zu Basiskonfigurationsaufgaben für einen Berichtsserver im einheitlichen Modus. Der zweite Abschnitt enthält Themen zur erweiterten Konfiguration. Der dritte Abschnitt enthält Themen zum Konfigurieren eines Berichtsservers zur Ausführung im integrierten SharePoint-Modus.  
  
### <a name="basic-configuration"></a>Basiskonfiguration  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 Beschreibt die Schritte zum Starten des Reporting Services-Konfigurationstools.  
  
 [Konfigurieren eines Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)  
 Erläutert, wie Konto- und Kennwortinformationen für den Berichtsserver-Dienst angegeben werden.  
  
 [Registrieren eines Dienstprinzipalnamens &#40;SPN&#41; für einen Berichtsserver](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md)  
 Erläutert die manuelle Registrierung eines SPN für einen Berichtsserver, der unter einem Domänenbenutzerkonto in einem Netzwerk ausgeführt wird, das Kerberos-Authentifizierung verwendet.  
  
 [Konfigurieren einer URL &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
 Beschreibt die Einrichtung einer oder mehrerer URLs, die für den Zugriff auf den Report Server-Webdienst und den Berichts-Manager verwendet werden.  
  
 [Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 Beschreibt die Schritte zum Erstellen einer Berichtsserver-Datenbank. Dieses Verfahren ist für die Bereitstellung einer Reporting Services-Installation erforderlich.  
  
### <a name="advanced-or-optional-configuration"></a>Erweiterte oder optionale Konfiguration  
 [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 Beschreibt die Schritte zum Konfigurieren mehrerer Berichtsserver für das gemeinsame Verwenden einer Berichtsserver-Datenbank.  
  
 [Konfigurieren eines Berichtsservers für die E-Mail-Übermittlung (SSRS-Konfigurations-Manager)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)  
 Beschreibt die Schritte zum Konfigurieren eines Berichtsservers für die E-Mail-Verteilung.  
  
 [Konfigurieren einer Firewall für den Zugriff auf den Berichtsserver](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
 Erklärt, wie für eingehende Anforderungen und ausgehende Antworten von einem Berichtsserver verwendete Ports geöffnet werden.  
  
 [Konfigurieren eines Berichtsservers im einheitlichen Modus für die lokale Verwaltung &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 Beschreibt zusätzliche Schritte, die erforderlich sind, um über `http://localhost` eine Verbindung mit dem Berichts-Manager oder einem Berichtsserver herzustellen.  
  
 [Configure a Report Server for Remote Administration (Konfigurieren eines Berichtsservers für die Remoteverwaltung)](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)  
 Erläutert, wie eine Remote-Berichtsserverinstanz so konfiguriert werden kann, dass Sie mit ihr eine Verbindung herstellen und sie über einen anderen Computer konfigurieren können.  
  
 [Aktivieren und Deaktivieren der Reporting Services-Funktionen](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)  
 Erklärt, wie nicht verwendete Funktionen in einer Reporting Services-Installation entfernt werden können.  
  
 [Aktivieren von Remotefehlern &#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)  
 Erläutert, wie Servereigenschaften auf einem Berichtsserver festgelegt werden, um zusätzliche Informationen zu auf Remoteservern aufgetretenen Fehlerbedingungen zurückzugeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren und Verwalten eines Berichtsservers &#40;einheitlicher SSRS-Modus&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Konfiguration und Verwaltung eines Berichtsservers (SharePoint-Modus von Reporting Services)](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)  
  
  
