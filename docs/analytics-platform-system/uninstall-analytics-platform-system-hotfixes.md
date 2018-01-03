---
title: Deinstallieren Sie Analytics Platform System Hotfixes (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: "21"
ms.openlocfilehash: 32d733f2e05855eb361095d23d6c34acefd343dc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Deinstallieren Sie Analytics Platform System Hotfixes
Die folgenden Schritte beschreiben, wie eine zuvor installierte Analytics Platform System Update zu deinstallieren.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Voraussetzungen  
Um diese Schritte ausführen zu können, benötigen Sie Folgendes:  
  
-   Ein Analytics Platform System Anmeldenamen mit Berechtigungen zum Zugriff auf die Admin-Konsole zum Überwachen der Einheit.  
  
-   Das Konto des Domänenadministrators Anmeldung die *< Appliance_domain >***-HST01** Knoten.  
  
-   Nummer des Knowledge Base-Artikel für den Hotfix zu deinstallieren.  
  
## <a name="HowToUninstallPDW"></a>So deinstallieren Sie einen SQL Server PDW-hotfix  
  
1.  Melden Sie sich an den *< Appliance_domain >***-HST01** als Domänenadministrator Fabric-Knoten.  
  
2.  Verwenden Sie zum Öffnen einer Eingabeaufforderung Ausführen als Administrator aus.  
  
3.  Wechseln Sie `C:\PDWINST\Patches\<kbarticle>\media` , in denen  *<kbarticle>*  ist die Nummer des Knowledge Base-Artikel für den Hotfix zu deinstallieren.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Um den Hotfix zu entfernen, führen Sie den folgenden Befehl ein.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Herunterladen und Anwenden von Microsoft Updates &#40; Analyseplattformsystem &#41;](download-and-apply-microsoft-updates.md)  
[Deinstallieren Sie Microsoft Updates &#40; Analyseplattformsystem &#41;](uninstall-microsoft-updates.md)  
[Anwenden von Analytics Platform System Hotfixes &#40; Analyseplattformsystem &#41;](apply-analytics-platform-system-hotfixes.md)  
[Wartung von Software &#40; Analyseplattformsystem &#41;](software-servicing.md)  
  
