---
title: Deinstallieren Sie Microsoft Updates – Analytics Platform System | Microsoft Docs"
description: Deinstallieren Sie Microsoft-Updates in Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57d0eb3616cf3567f63d75029f79cea6709ed955
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Deinstallieren Sie Microsoft-Updates in Analytics Platform System
Dieser Artikel beschreibt die Vorgehensweise beim Deinstallieren eines zuvor installierten Microsoft-Updates auf dem Gerät Analytics Platform System.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Um diese Schritte ausführen zu können, benötigen Sie Folgendes:  
  
-   Ein Analytics Platform System Anmeldenamen mit Berechtigungen zum Zugriff auf die Admin-Konsole zum Überwachen der Einheit.  
  
-   Kenntnisse über die Fabric-Domänenadministratorkonto zum Anmelden bei der  *<Fabric Domain>***-HST01** Knoten.  
  
## <a name="HowToUninstallMSFT"></a>So deinstallieren Sie Microsoft-updates  
  
1.  Melden Sie sich auf die  *<Fabric Domain>***-HST01** als Domänenadministrator Fabric-Knoten.  
  
2.  Um alle Updates zu deinstallieren, die für die WSUS für die Deinstallation genehmigt ist, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl aus. Ersetzen Sie die Platzhalterelemente *< >* mit den entsprechenden Informationen.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie in den folgenden Themen:
- [Herunterladen und Anwenden von Microsoft-Updates &#40;Analyseplattformsystem&#41;](download-and-apply-microsoft-updates.md) 
- [Anwenden von Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Deinstallieren Sie Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Wartung von Software &#40;Analyseplattformsystem&#41;](software-servicing.md)  
  
