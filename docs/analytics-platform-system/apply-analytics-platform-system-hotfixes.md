---
title: Anwenden von Analytics Platform System Hotfixes (Analytics Platform System)
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
ms.assetid: fca5eec9-86b8-4d20-b498-1678c367b5c8
caps.latest.revision: "25"
ms.openlocfilehash: af879486885f2c27ad4c3d80ef9a3d41279ff0ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Anwenden von Analytics Platform System Hotfixes
Dieses Thema erläutert das Anwenden von Hotfixes auf dem Softwareupdatepunkt Analytics Platform System.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
> [!WARNING]  
> Versuchen Sie nicht, einen Analytics Platform System-Hotfix installieren, wird dem Gerät oder eine beliebige Komponente Appliance heruntergefahren oder in einem fehlerhaften Zustand. In diesem Fall erhalten Sie Support um Unterstützung zu erhalten.  
  
> [!WARNING]  
> Einen Hotfix Analytics Platform System nicht angewendet, während das Gerät verwendet wird. Anwendung eines Hotfixes kann dazu führen, dass Appliance Knoten neu starten. Der Hotfix sollte während eines Wartungsfensters übernommen werden, wenn das Gerät nicht verwendet wird.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Um diese Schritte ausführen zu können, benötigen Sie Folgendes:  
  
-   Eine Analytics Platform System Anmeldung mit Zugriffsberechtigungen für die Admin-Konsole, um den Anwendungszustand zu überwachen. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Kenntnisse über die Fabric-Domänenadministratorkonto zum Herstellen von Verbindungen die *< Domänenname >***-HST01** Knoten.  
  
## <a name="HowToInstallPDW"></a>Zum Installieren eines Hotfixes Analytics Platform System  
Im Gegensatz zu den Microsoft-Updates werden die Hotfixes für die Software Analytics Platform System nicht über WSUS behandelt. Sie haben einen anderen Workflownamen und durch Ausführen eines Hotfixpakets installiert werden.  
  
1.  **Vergewissern Sie sich Statusindikatoren Appliance.**  
  
    1.  Öffnen Sie die Admin-Konsole, und navigieren Sie zu der Seite "Anwendungszustand". Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40; Analyseplattformsystem &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Alle rote oder gelbe Indikatoren müssen geklärt werden, bevor Sie mit dem nächsten Schritt fortfahren. Einige Ausnahmen sind:  
  
        -   Wenn Datenträgerfehler sind, verwenden der Admin-Konsole Warnungsseite, stellen Sie sicher, dass nicht mehr als ein Fehler auf dem Datenträger in jedem Server oder SAN-Array vorhanden ist. Ist nicht mehr als ein Datenträgerfehler in jedem Server oder SAN-Array, können Sie vor der Behebung der Datenträger der Dateien mit dem nächsten Schritt fortfahren. Achten Sie darauf, wenden Sie sich an Microsoft Support, um die Datenträger Fehler(n) so bald wie möglich zu beheben.  
  
        -   Ist ein unkritische (gelb) Volume Datenträgerfehler, der nicht auf dem Laufwerk C:\ ist, können Sie vor dem Lösen der Datenträgerfehler Volume mit dem nächsten Schritt fortfahren.  
  
2.  **Installieren Sie den Hotfix Analytics Platform System**  
  
    1.  Melden Sie sich die <*Appliance_domain*>-HST01 Knoten als Domänenadministrator an.  
  
    2.  Verwenden der **als Administrator ausführen** Option aus, um ein Eingabeaufforderungsfenster zu öffnen.  
  
    3.  Führen Sie den folgenden Befehl ein, und Ersetzen Sie dabei  *<HotfixPackageName>*  mit dem Namen des ausführbaren Hotfixpakets und anderen Platzhalter Elemente ersetzen *< >* mit den entsprechenden Informationen.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Führen Sie die Schritte, dargestellt durch das Hotfixpaket.  
  
## <a name="see-also"></a>Siehe auch  
[Herunterladen und Anwenden von Microsoft Updates &#40; Analyseplattformsystem &#41;](download-and-apply-microsoft-updates.md)  
[Deinstallieren Sie Microsoft Updates &#40; Analyseplattformsystem &#41;](uninstall-microsoft-updates.md)  
[Vorgehensweise: Deinstallieren Sie Analytics Platform System Hotfixes &#40; Analyseplattformsystem &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Wartung von Software &#40; Analyseplattformsystem &#41;](software-servicing.md)  
  
