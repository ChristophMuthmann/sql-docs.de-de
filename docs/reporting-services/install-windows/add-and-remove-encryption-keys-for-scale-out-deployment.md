---
title: "Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ffe0a7ea7f46ed7b1ae5d1e5070d58afa0540b12
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment"></a>Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren
  Sie können [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in einem Bereitstellungsmodell für horizontales Skalieren ausführen, indem Sie mehrere Berichtsserver für die Verwendung einer freigegebenen Berichtsserver-Datenbank konfigurieren. Die Mitgliedschaft in einer Bereitstellung für horizontales Skalieren basiert darauf, ob der Berichtsserver in der Berichtsserver-Datenbank einen Verschlüsselungsschlüssel gespeichert hat. Sie können die Mitgliedschaft in einer Bereitstellung für horizontales Skalieren überwachen, indem Sie für bestimmte Berichtsserverinstanzen Verschlüsselungsschlüssel hinzufügen und entfernen. Sie können Knoten aus einer Bereitstellung in beliebiger Reihenfolge entfernen. Beim Hinzufügen von Knoten zu einer Bereitstellung müssen Sie neue Instanzen von einem Berichtsserver aus verknüpfen, der bereits Teil der Bereitstellung ist.  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>Verwenden des Reporting Services-Konfigurationstools zum Konfigurieren der Bereitstellung für horizontales Skalieren  
 Die einfachste Möglichkeit, eine Bereitstellung für horizontales Skalieren zu konfigurieren, ist die Verwendung des Reporting Services-Konfigurationstools. Weitere Informationen und Schritt-für-Schritt-Anleitungen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für Bereitstellungen für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>Verwenden von Rskeymgmt zum Konfigurieren der Bereitstellung für horizontales Skalieren  
 Verwenden Sie das Hilfsprogramm **rskeymgmt** , um eine Berichtsserverinstanz für die Verwendung einer freigegebenen Berichtsserver-Datenbank zu initialisieren. Für das Hinzufügen eines Berichtsservers zu einer Bereitstellung für horizontales Skalieren müssen Sie den Berichtsserver initialisieren. Für die Initialisierung sind Administratorberechtigungen erforderlich. Sie müssen Administratoranmeldeinformationen für den Remotecomputer haben, der den Berichtsserver hostet, den Sie zur Bereitstellung hinzufügen möchten.  
  
### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>Hinzufügen eines Berichtsservers zu einer Bereitstellung für horizontales Skalieren (rskeymgmt)  
  
1.  Führen Sie **rskeymgmt.exe** lokal auf dem Computer aus, der einen Berichtsserver hostet, der bereits ein Element der Bereitstellung für horizontales Skalieren für Berichtsserver ist.  
  
2.  Verwenden Sie das **-j** -Argument, um einen Berichtsserver mit der Berichtsserver-Datenbank zu verknüpfen. Verwenden Sie das Hilfsprogramm **-m** und **-n** zum Angeben der Remoteberichtsserver-Instanz, die Sie der Bereitstellung hinzufügen möchten. Verwenden Sie die Argumente **-u** und **-v** zum Angeben eines Administratorkontos auf dem Remotecomputer. Wenn Sie eine Bereitstellung für horizontales Skalieren mithilfe mehrerer Berichtsserverinstanzen auf demselben Computer erstellen, müssen Sie eine etwas andere Syntax verwenden. Weitere Informationen zu der betreffenden Syntax finden Sie unter [rskeymgmt Utility &#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md).  
  
     Das folgende Beispiel veranschaulicht die anzugebenden Argumente beim Hinzufügen eines Remoteberichtsservers zu einer Bereitstellung für horizontales Skalieren (Sie können die Anmeldeinformationen auslassen, wenn Sie auf dem Remotecomputer über Administratorberechtigungen verfügen):  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```
3. Starten Sie den Reporting Services-Windows-Dienst erneut.
  
### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>Verschieben eines Berichtsservers aus einer Bereitstellung für horizontales Skalieren (rskeymgmt)  
  
1.  Öffnen Sie die Datei rsreportserver.config des Berichtsservers, den Sie entfernen möchten, und suchen Sie die Installations-ID. Diese Datei befindet sich standardmäßig unter Program Files\Microsoft SQL Server\MSSQL.  *n* \Reporting).  
  
     Wenn Sie eine einzelne Instanz installiert haben, befindet sich nur eine einzelne Datei rsreportserver.config auf dem Computer. Wenn mehrere Instanzen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installiert sind, finden Sie die Instanz-ID des zu entfernenden Berichtsservers (beispielsweise MSSQL.2) auf der Seite Serverstatus im Reporting Services-Konfigurationstool. Der Name des Ordners, in dem die Programmdateien für die Berichtsserverinstanz gespeichert sind, basiert auf dem Instanzbezeichner (beispielsweise Programme\Microsoft SQL Server\MSSQL.2).  
  
2.  Führen Sie **rskeymgmt.exe**aus. Sie können die Datei auf jedem Berichtsserver ausführen, der Teil der Bereitstellung für horizontales Skalieren des Berichtsservers ist.  
  
3.  Verwenden Sie das **-r** -Argument, um die Berichtsserverinstanz aus der Bereitstellung für horizontales Skalieren freizugeben. Das folgende Beispiel veranschaulicht die anzugebenden Argumente:  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
4. Starten Sie den Reporting Services-Windows-Dienst erneut.
  
 Mit diesen Schritten entfernen Sie den Berichtsserver aus einer Bereitstellung für horizontales Skalieren. Dabei wird die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Instanz auf dem Berichtsserver jedoch nicht deinstalliert. Nachdem Sie den Berichtsserver aus einer Bereitstellung für horizontales Skalieren entfernt haben, können Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vom Server deinstallieren, wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf dem Server nicht mehr benötigen. Weitere Informationen finden Sie unter [Deinstallieren einer vorhandenen SQL Server-Instanz &#40;Setup&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren und Verwalten von Verschlüsselungsschlüsseln &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Initialisieren eines Berichtsservers &#40; SSRS-Konfigurations-Manager &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  

