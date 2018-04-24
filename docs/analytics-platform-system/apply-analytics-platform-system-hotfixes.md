---
title: Anwenden von Hotfixes Analytics Platform System | Microsoft Docs
description: In diesem Artikel erläutert, wie das Anwenden von Hotfixes auf dem Softwareupdatepunkt Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b3a7a31ce791fbe44c38d1d30ce408235720e241
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Anwenden von Hotfixes Analytics Platform System
In diesem Artikel erläutert, wie das Anwenden von Hotfixes auf dem Softwareupdatepunkt Analytics Platform System.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
> [!WARNING]  
> Versuchen Sie nicht, einen Analytics Platform System-Hotfix installieren, wird dem Gerät oder eine beliebige Komponente Appliance heruntergefahren oder in einem fehlerhaften Zustand. In diesem Fall erhalten Sie Support um Unterstützung zu erhalten.  
  
> [!WARNING]  
> Einen Hotfix Analytics Platform System nicht angewendet, während das Gerät verwendet wird. Anwendung eines Hotfixes kann dazu führen, dass Appliance Knoten neu starten. Der Hotfix sollte während eines Wartungsfensters übernommen werden, wenn das Gerät nicht verwendet wird.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Um diese Schritte ausführen zu können, benötigen Sie Folgendes:  
  
-   Eine Analytics Platform System Anmeldung mit Zugriffsberechtigungen für die Admin-Konsole, um den Anwendungszustand zu überwachen. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Kenntnisse über die Fabric-Domänenadministratorkonto zum Herstellen von Verbindungen die *< Domänenname > ***-HST01** Knoten.  
  
## <a name="HowToInstallPDW"></a>Zum Installieren eines Hotfixes Analytics Platform System  
Im Gegensatz zu den Microsoft-Updates werden die Hotfixes für die Software Analytics Platform System nicht über WSUS behandelt. Sie haben einen anderen Workflownamen und durch Ausführen eines Hotfixpakets installiert werden.  
  
1.  **Vergewissern Sie sich Statusindikatoren Appliance.**  
  
    1.  Öffnen Sie die Admin-Konsole, und navigieren Sie zu der Seite "Anwendungszustand". Weitere Informationen finden Sie unter [überwachen Sie die Anwendung mithilfe der Verwaltungskonsole &#40;Analyseplattformsystem&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Alle rote oder gelbe Indikatoren müssen geklärt werden, bevor Sie mit dem nächsten Schritt fortfahren. Einige Ausnahmen sind:  
  
        -   Wenn Datenträgerfehler sind, verwenden der Admin-Konsole Warnungsseite, stellen Sie sicher, dass nicht mehr als ein Fehler auf dem Datenträger in jedem Server oder SAN-Array vorhanden ist. Ist nicht mehr als ein Datenträgerfehler in jedem Server oder SAN-Array, können Sie vor der Behebung der Datenträger der Dateien mit dem nächsten Schritt fortfahren. Achten Sie darauf, wenden Sie sich an Microsoft Support, um die Datenträger Fehler(n) so bald wie möglich zu beheben.  
  
        -   Ist ein unkritische (gelb) Volume Datenträgerfehler, der nicht auf dem Laufwerk C:\ ist, können Sie vor dem Lösen der Datenträgerfehler Volume mit dem nächsten Schritt fortfahren.  
  
2.  **Installieren Sie den Hotfix Analytics Platform System**  
  
    1.  Melden Sie sich die <*Appliance_domain*>-HST01 Knoten als Domänenadministrator an.  
  
    2.  Verwenden der **als Administrator ausführen** Option aus, um ein Eingabeaufforderungsfenster zu öffnen.  
  
    3.  Führen Sie den folgenden Befehl ein, und Ersetzen Sie dabei *<HotfixPackageName>* mit dem Namen des ausführbaren Hotfixpakets und anderen Platzhalter Elemente ersetzen *< >* mit den entsprechenden Informationen.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Führen Sie die Schritte, dargestellt durch das Hotfixpaket.  
  
## <a name="see-also"></a>Siehe auch  
[Herunterladen und Anwenden von Microsoft-Updates &#40;Analyseplattformsystem&#41;](download-and-apply-microsoft-updates.md)  
[Deinstallieren Sie Microsoft Updates &#40;Analyseplattformsystem&#41;](uninstall-microsoft-updates.md)  
[Deinstallieren Sie Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Wartung von Software &#40;Analyseplattformsystem&#41;](software-servicing.md)  
  
