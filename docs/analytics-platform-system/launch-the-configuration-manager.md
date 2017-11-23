---
title: Starten Sie den Konfigurations-Manager (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b914ba9a-e4ec-4750-934a-c447fc8909e3
caps.latest.revision: "22"
ms.openlocfilehash: 98ae90d198b4a1b68e1b72305721611a8efa30ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="launch-the-configuration-manager"></a>Starten Sie den Konfigurations-Manager
Dieses Thema enthält Anweisungen für das Starten der **Configuration Manager** für das Analytics Platform System-Gerät.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Das Analytics Platform System**Configuration Manager** kann nur vom Domänenadministrator Einheit ausgeführt werden. Um dieses Tool ausführen zu können, benötigen Sie das Kennwort für die Appliance-Domänenadministrator an. Um zusätzliche APS-Administratoren zu erstellen, finden Sie unter [erstellen Sie ein Domänenadministrator APS &#40; APS &#41; ](create-an-aps-domain-administrator-aps.md).  
  
## <a name="Accessing"></a>Starten Sie das Configuration Manager-Tool  
Verwenden Sie zum Ausführen des Konfigurations-Managers den Remotedesktop für die Verbindung mit dem Steuerungsknoten PDW (***PDW_region*-CTL01**) Knoten, und melden Sie sich als *Appliance_domain* **\Administrator**. Beim Starten der **Configuration Manager** programmieren, verwenden Sie die **als Administrator ausführen** Option, um sicherzustellen, dass Ihre Administratoranmeldeinformationen verwendet werden.  
  
#### <a name="to-launch-from-a-browser-window"></a>Einführung in einem Browserfenster öffnen  
  
1.  Öffnen Sie einen Browser, und navigieren Sie zu dem Verzeichnis `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100`.  
  
2.  Mit der rechten Maustaste `dwconfig.exe` , und klicken Sie dann auf **als Administrator ausführen**.  
  
#### <a name="to-launch-from-a-command-prompt"></a>Um über eine Eingabeaufforderung zu starten.  
  
1.  Öffnen Sie auf dem Desktop die **starten** Menü klicken Sie auf **Programme**, klicken Sie auf **Zubehör**, mit der rechten Maustaste **Eingabeaufforderung** , und klicken Sie dann auf  **Als Administrator ausführen**.  
  
2.  Geben Sie an der Eingabeaufforderung den folgenden Befehl zum Ändern von Verzeichnissen: `cd /d "C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100"`.  
  
3.  Geben Sie an der Eingabeaufforderung `dwconfig.exe`.  
  
Nach der **Configuration Manager** wird gestartet, sehen Sie alle verfügbaren Funktionen im linken Bereich aufgeführt. Der übrige Teil dieses Abschnitts wird erläutert, wie jede Aktion in das Tool ausgeführt.  
  
Schließen und beenden **Configuration Manager**, klicken Sie auf **beenden** in der unteren rechten Ecke von jedem Bildschirm.  
  
![SQL_Server_PDW_DWConfig_ApplTop](./media/launch-the-configuration-manager/SQL_Server_PDW_DWConfig_ApplTop.png "SQL_Server_PDW_DWConfig_ApplTop")  
  
## <a name="see-also"></a>Siehe auch  
[Überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
