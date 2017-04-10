---
title: "Starten und Beenden des Berichtsserverdiensts | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Beenden des Berichtsserverdiensts"
  - "Report Server-Windows-Dienst, Starten"
  - "Berichtsserverdienst, Starten"
  - "Starten des Berichtsserverdiensts"
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
caps.latest.revision: 55
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 55
---
# Starten und Beenden des Berichtsserverdiensts
  Der Berichtsserver wird als Windows-Dienst implementiert, der den Report Server-Webdienst, den Berichts-Manager und eine Hintergrundverarbeitungsanwendung umfasst. Der Dienst muss ausgeführt werden, damit Sie die Berichtsserverfunktionalitäten nutzen können. Durch Beenden des Diensts werden alle Berichtsservervorgänge beendet.  
  
 Wenn der Dienst beendet ist, werden Anforderungen für die Verarbeitung von geplanten Berichts- und Abonnementverarbeitungen in die Warteschlange gestellt. Dies liegt daran, dass diese Ereignisse von vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ausgeführten Aufträgen erstellt werden. Wenn Sie einen Backlog von Vorgängen vermeiden möchten, während der Dienst deaktiviert ist, sollten Sie erwägen, den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ebenfalls zu beenden.  
  
 Sie können den Berichtsserverdienst mit einer Vielzahl von Tools starten oder beenden, u.&amp;nbsp;a. mit dem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager und dem Services-Tool von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Wenn Sie über das Starten und Beenden des Diensts hinaus weitere Vorgänge durchführen möchten, z.&amp;nbsp;B. Ändern des Dienstkontos, müssen Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool verwenden. Wenn Sie zum Ändern des Dienstkontos andere Tools verwenden, kann dadurch Ihre [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Installation beschädigt werden. Weitere Informationen finden Sie unter [Konfigurieren des Berichtsserver-Dienstkontos &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Der Dienst kann nicht angehalten und fortgesetzt werden. Es gibt keine Startparameter. Obwohl keine expliziten Abhängigkeiten vorhanden sind, muss der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ausgeführt werden, wenn auf dem Berichtsserver Abonnements oder geplante Berichtsvorgänge unterstützt werden sollen.  
  
### So starten oder beenden Sie den Dienst mit dem Reporting Services-Konfigurationstool  
  
1.  Starten Sie das [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Konfigurationstool, und stellen Sie eine Verbindung mit dem Berichtsserver her.  
  
2.  Klicken Sie auf der Seite Berichtsserverstatus auf **Beenden** oder auf **Starten**.  
  
### So starten oder beenden Sie den Dienst mit der Option Dienste unter Verwaltung  
  
-   Öffnen Sie unter „Verwaltung“ den Eintrag „Dienste“, klicken Sie mit der rechten Maustaste auf **SQL Server Reporting Services (MSSQLSERVER)**, und klicken Sie auf **Beenden** bzw. **Neu starten**.  
  
 Wenn mehrere Instanzen ausgeführt werden oder der Berichtsserver als eine benannte Instanz ausgeführt wird, überprüfen Sie, ob der Instanzname in Klammern der Berichtsserverinstanz entspricht, die beendet oder neu gestartet werden soll.  
  
### So starten oder beenden Sie den Dienst mit dem SQL Server-Konfigurations-Manager  
  
1.  Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager.  
  
2.  Wählen Sie „SQL Server-Dienste“ aus, klicken Sie mit der rechten Maustaste auf **SQL Server Reporting Services**, und klicken Sie auf **Beenden** oder **Neu starten**.  
  
## Siehe auch  
 [Reporting Services-Konfigurations-Manager &#40;einheitlicher Modus&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  