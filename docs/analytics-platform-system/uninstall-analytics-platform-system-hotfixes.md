---
title: Deinstallieren Sie Analytics Platform System-Hotfixes auf | Microsoft Docs
description: Analyseplattformsystem Hotfixes zu deinstallieren.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 83e57a676ee0eff21eb3a736484d8e286cdeee01
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Deinstallieren Sie Analytics Platform System-hotfixes 
Die folgenden Schritte beschreiben, wie eine zuvor installierte Analytics Platform System Update zu deinstallieren.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Um diese Schritte ausführen zu können, benötigen Sie Folgendes:  
  
-   Ein Analytics Platform System Anmeldenamen mit Berechtigungen zum Zugriff auf die Admin-Konsole zum Überwachen der Einheit.  
  
-   Das Konto des Domänenadministrators Anmeldung die *< Appliance_domain > ***-HST01** Knoten.  
  
-   Nummer des Knowledge Base-Artikel für den Hotfix zu deinstallieren.  
  
## <a name="HowToUninstallPDW"></a>So deinstallieren Sie einen SQL Server PDW-hotfix  
  
1.  Melden Sie sich an den *< Appliance_domain > ***-HST01** als Domänenadministrator Fabric-Knoten.  
  
2.  Verwenden Sie zum Öffnen einer Eingabeaufforderung Ausführen als Administrator aus.  
  
3.  Wechseln Sie `C:\PDWINST\Patches\<kbarticle>\media` , in denen *<kbarticle>* ist die Nummer des Knowledge Base-Artikel für den Hotfix zu deinstallieren.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Um den Hotfix zu entfernen, führen Sie den folgenden Befehl ein.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Herunterladen und Anwenden von Microsoft-Updates &#40;Analyseplattformsystem&#41;](download-and-apply-microsoft-updates.md)  
[Deinstallieren Sie Microsoft Updates &#40;Analyseplattformsystem&#41;](uninstall-microsoft-updates.md)  
[Anwenden von Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](apply-analytics-platform-system-hotfixes.md)  
[Wartung von Software &#40;Analyseplattformsystem&#41;](software-servicing.md)  
  
