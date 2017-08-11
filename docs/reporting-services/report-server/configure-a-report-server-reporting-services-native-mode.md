---
title: Konfigurieren eines Berichtsservers (Reporting Services im einheitlichen Modus) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
caps.latest.revision: 17
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da2a367b582d39ea8cc8dc7ffc281a3515bb2d8b
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>Konfigurieren eines Berichtsservers (einheitlicher Reporting Services-Modus)
  Je nach den bei der Installation ausgewählten Optionen muss der Berichtsserver zusätzlich konfiguriert werden, bevor Sie ihn verwenden können. Mindestkonfigurationsvoraussetzungen für den Berichtsserver:  
  
-   Konto für Berichtsserverdienst (Konfiguration während der Installation)  
  
-   Webdienst-URL, die Zugriff auf den Berichtsserver gewährt  
  
-   Berichtsserverdatenbank, die Anwendungsdaten, Berichte und andere Elemente speichert  
  
 Setup konnfiguriert die Mindesteinstellungen, wenn Sie eine der folgenden Installationsoptionen auswählen: Standardkonfiguration im einheitlichen Modus oder integrierter SharePoint-Modus. Wenn Sie den Berichtsserver im Dateimodus installiert haben (Option **Server installieren, jedoch nicht konfigurieren** im Installationsassistenten), wird nur das Dienstkonto konfiguriert. Die Webdienst-URL und die Berichtsserverdatenbank müssen konfiguriert werden, nachdem Setup beendet wurde.  
  
 Der Berichts-Manager ist eine optionale Funktion für einen Berichtsserver im einheitlichen Modus. Es wird jedoch empfohlen, den Berichts-Manager so zu konfigurieren, dass Sie den Benutzerzugriff auf den Berichtsserver gewähren und den Berichtsserverinhalt verwalten können. Wenn Sie einen Berichtsserver im integrierten SharePoint-Modus bereitstellen, verwenden Sie das Web-Front-End eines SharePoint-Servers, um Zugriff zu gewähren.  
  
 Zusätzliche Funktionen, z. B. Berichtsserver-E-Mail und das unbeaufsichtigte Ausführungskonto, können nach Bedarf konfiguriert werden. Weitere Informationen finden Sie unter [Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Verwenden Sie das Reporting Services-Konfigurationstool, um den Berichtsserver zu konfigurieren.  
  
### <a name="to-minimally-configure-a-report-server-installation"></a>So konfigurieren Sie eine minimale Berichtsserverinstallation  
  
1.  Starten Sie das Reporting Services-Konfigurationstool, und stellen Sie eine Verbindung mit der Berichtsserverinstanz her. Weitere Informationen finden Sie unter [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Klicken Sie auf **Webdienst-URL** , um die Seite zum Konfigurieren einer URL für den Berichtsserver zu öffnen. Anweisungen wie die URL definieren, finden Sie unter [Konfigurieren einer URL &#40; SSRS-Konfigurations-Manager &#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3.  Klicken Sie auf **Datenbank** , um die Berichtsserverdatenbank zu erstellen. Anweisungen finden Sie unter [Erstellen einer Berichtsserver-Datenbank im einheitlichen Modus &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Navigieren Sie zurück zur Seite **Webdienst-URL** , und klicken Sie auf die URL, um zu prüfen, ob sie funktioniert.  
  
5.  Folgen Sie den Anweisungen unter 'Nächste Schritte', um die Bereitstellung abzuschließen.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Um die Bereitstellung abzuschließen, konfigurieren Sie die Berichts-Manager- oder SharePoint-Integration. Weitere Informationen finden Sie unter [Konfigurieren des Berichts-Managers &#40;einheitlicher Modus&#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md).  
  
 Wenn die Windows-Firewall aktiviert ist, ist der Port, für den der Berichtsserver konfiguriert ist, höchstwahrscheinlich geschlossen. Ein Hinweis darauf, dass ein Port geschlossen ist, kann darin bestehen, dass beim Öffnen des Berichts-Managers von einem Remoteclientcomputer aus eine leere Seite angezeigt wird. Informationen zum Konfigurieren der Firewall finden Sie unter [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
 Wenn Sie Windows Vista oder Windows Server 2008 verwenden, sind zusätzliche Schritte nötig, bevor Sie den Berichts-Manager lokal verwalten können. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für die lokale Verwaltung &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 Überprüfen Sie die Installation durch das Erstellen von Ordnern, das Hochladen von Elementen und das Ausführen von Berichten. Befolgen Sie die Anweisungen in [Überprüfen einer Installation von Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) , um Ihre Installation zu überprüfen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten eines Berichtsservers von Reporting Services im einheitlichen Modus](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Konfigurieren einer Firewall für den Berichtsserverzugriff](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Konfigurieren Sie einen Berichtsserver im einheitlichen Modus für die lokale Verwaltung &#40; SSRS &#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [Konfigurieren eines Berichtsservers für die Remoteverwaltung](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)   
 [Reporting Services-Konfigurations-Manager &#40; Im einheitlichen Modus &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
  
