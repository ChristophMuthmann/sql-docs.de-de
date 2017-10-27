---
title: Umbenennen ein Berichtsservercomputers | Microsoft Docs
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
helpviewer_keywords:
- renaming report servers
ms.assetid: 82fc4ba2-291a-4939-a025-271b8d687c54
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 349180bb3cfe2b03bee076dfc2dbb90265118fa4
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="rename-a-report-server-computer"></a>Umbenennen eines Berichtsservercomputers
  Durch das Umbenennen eines Computers wird eine entsprechende Namensänderung für den Webserver und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verursacht (falls sie auf demselben Computer installiert ist). In einigen Fällen kann nach einer Computernamensänderung möglicherweise nicht mehr auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] zugegriffen werden. Führen Sie die Schritte in diesem Thema aus, um einen Berichtsserver nach einer Änderung des Computernamens neu zu konfigurieren.  
  
## <a name="renaming-a-sql-server-database-engine"></a>Umbenennen eines SQL Server-Datenbankmoduls  
 Führen Sie die folgenden Aktionen aus, wenn Sie die  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz umbenannt haben, in der die Berichtsserver-Datenbank ausgeführt wird:  
  
1.  Starten Sie das Reporting Services-Konfigurationstool, und stellen Sie eine Verbindung mit dem Berichtsserver her, der die Berichtsserver-Datenbank auf dem umbenannten Server verwendet.  
  
2.  Öffnen Sie die Seite Setup der Datenbank.  
  
3.  Geben Sie unter **Servername**den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Namen ein, und klicken Sie anschließend auf **Verbinden**.  
  
4.  Klicken Sie auf **Anwenden**.  
  
 Falls der Berichtsserver eine lokale [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Instanz verwendet, können Sie den Server mit *(local)* oder *(local)\instancename* angeben. Wenn Sie mit *(local)* auf den Server verweisen, sind die Verbindungen mit dem Server auch nach einer Umbenennung des Servers weiterhin funktionsfähig. Wenn Sie einen Remoteserver verwenden oder wenn [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mithilfe des Servernamens konfiguriert ist, müssen Sie die Datenbank-Verbindungsinformationen bei jeder Änderung des Servernamens aktualisieren.  
  
## <a name="renaming-a-report-server-computer"></a>Umbenennen eines Berichtsservercomputers  
 Führen Sie die folgenden Aktionen aus, wenn Sie einen Computer umbenannt haben, auf dem ein Berichtsserver ausgeführt wird:  
  
1.  Öffnen Sie RSReportServer.config in einem Text-Editor, und ändern Sie die **UrlRoot** -Einstellung so, dass sie den neuen Servernamen wiedergibt. Die **UrlRoot** -Einstellung wird von Übermittlungserweiterungen zum Angeben der URL für den Zugriff auf Elemente verwendet, die auf dem Berichtsserver gespeichert sind. Wenn Sie die URL-Adresse des Berichtsservers ändern, müssen Sie die **UrlRoot** -Einstellung aktualisieren, damit Berichte weiterhin erwartungsgemäß von Abonnements übermittelt werden.  
  
2.  Ändern Sie in der gleichen Datei ggf. die **ReportServerUrl** -Einstellung so, dass sie den neuen Servernamen wiedergibt. Beachten Sie, dass diese Einstellung nicht in jeder Installation verwendet wird. Falls die Einstellung leer ist, brauchen Sie nichts zu tun.  
  
    > [!NOTE]  
    >  Falls Sie WINS (Windows Internet Naming Service) im Unternehmensnetzwerk verwenden, sind der Berichtsserver und der Berichts-Manager möglicherweise noch eine Zeit lang unter dem vorherigen Namen verfügbar. WINS ordnet jedem Computer, für den es einen Dienst bereitstellt, eine IP-Adresse zu. Nachdem die IP-Adresse für den umbenannten Computer von WINS aktualisiert wurde, kann über den alten Computernamen nicht mehr auf einen Berichtsserver oder auf den Berichts-Manager zugegriffen werden.  
  
## <a name="see-also"></a>Siehe auch  
 [RSReportServer.config-Konfigurationsdatei](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services-Konfigurations-Manager &#40; Im einheitlichen Modus &#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Reporting Services-Berichtsserver &#40; Im einheitlichen Modus &#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Starten Sie und beenden Sie des Berichtsserver-Diensts](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)   
 [RSConfig-Hilfsprogramm &#40; SSRS &#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)  
  
  

