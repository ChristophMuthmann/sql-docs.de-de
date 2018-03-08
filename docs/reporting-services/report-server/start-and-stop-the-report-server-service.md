---
title: Starten und Beenden des Berichtsserverdiensts | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
caps.latest.revision: "55"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 48d0f1dddabd461401027633a70a0d51b9efa345
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="start-and-stop-the-report-server-service"></a>Starten und Beenden des Berichtsserverdiensts
  Der Berichtsserver wird als Windows-Dienst implementiert, der den Report Server-Webdienst, den Berichts-Manager und eine Hintergrundverarbeitungsanwendung umfasst. Der Dienst muss ausgeführt werden, damit Sie die Berichtsserverfunktionalitäten nutzen können. Durch Beenden des Diensts werden alle Berichtsservervorgänge beendet.  
  
 Wenn der Dienst beendet ist, werden Anforderungen für die Verarbeitung von geplanten Berichts- und Abonnementverarbeitungen in die Warteschlange gestellt. Dies liegt daran, dass diese Ereignisse von vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ausgeführten Aufträgen erstellt werden. Wenn Sie einen Backlog von Vorgängen vermeiden möchten, während der Dienst deaktiviert ist, sollten Sie erwägen, den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ebenfalls zu beenden.  
  
 Sie können den Berichtsserverdienst mit einer Vielzahl von Tools starten oder beenden, u.&nbsp;a. mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager und dem Services-Tool von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Wenn Sie über das Starten und Beenden des Diensts hinaus weitere Vorgänge durchführen möchten, z.&nbsp;B. Ändern des Dienstkontos, müssen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwenden. Wenn Sie zum Ändern des Dienstkontos andere Tools verwenden, kann dadurch Ihre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation beschädigt werden. Weitere Informationen finden Sie unter [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Der Dienst kann nicht angehalten und fortgesetzt werden. Es gibt keine Startparameter. Obwohl keine expliziten Abhängigkeiten vorhanden sind, muss der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ausgeführt werden, wenn auf dem Berichtsserver Abonnements oder geplante Berichtsvorgänge unterstützt werden sollen.  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>So starten oder beenden Sie den Dienst mit dem Reporting Services-Konfigurationstool  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung mit dem Berichtsserver her.  
  
2.  Klicken Sie auf der Seite Berichtsserverstatus auf **Beenden** oder auf **Starten**.  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>So starten oder beenden Sie den Dienst mit der Option Dienste unter Verwaltung  
  
-   Öffnen Sie unter „Verwaltung“ den Eintrag „Dienste“, klicken Sie mit der rechten Maustaste auf **SQL Server Reporting Services (MSSQLSERVER)**, und klicken Sie auf **Beenden** bzw. **Neu starten**.  
  
 Wenn mehrere Instanzen ausgeführt werden oder der Berichtsserver als eine benannte Instanz ausgeführt wird, überprüfen Sie, ob der Instanzname in Klammern der Berichtsserverinstanz entspricht, die beendet oder neu gestartet werden soll.  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>So starten oder beenden Sie den Dienst mit dem SQL Server-Konfigurations-Manager  
  
1.  Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager.  
  
2.  Wählen Sie „SQL Server-Dienste“ aus, klicken Sie mit der rechten Maustaste auf **SQL Server Reporting Services**, und klicken Sie auf **Beenden** oder **Neu starten**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Starten, Beenden oder Anhalten des SQL Server-Agent-Diensts](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
