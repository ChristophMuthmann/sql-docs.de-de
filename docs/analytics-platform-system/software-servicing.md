---
title: Wartung von Software - Analytics Platform System | Microsoft Docs
description: Software Wartung in Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7d9991dfb310e2cebc3c61bbd6f9f04a40a0f38e
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="software-servicing-in-analytics-platform-system"></a>Software-Wartung in Analytics Platform System
In diesem Abschnitt wird die Software, die wartungsanforderungen für Analytics Platform System-Einheiten, z. B. WSUS und Analytics Platform System Updates zusammengefasst.  
  
## <a name="Basics"></a>Software, die Grundlagen der Wartung  
**WSUS:** Ihre Appliance Analytics Platform System muss konfiguriert werden, um Updates von Windows Server Update Services (WSUS) zu erhalten. Diese Updates enthalten wichtige Änderungen an der Appliance-Software. Nachdem sie konfiguriert wurden, werden viele Updates automatisch installiert und erfordern keine praktische Management. In der Regel werden während der WSUS-Updates konfiguriert die [Konfigurieren von Windows Server Update Services &#40;WSUS&#41; &#40;Analyseplattformsystem&#41; ](configure-windows-server-update-services-wsus.md) Schritt ausgeführt wird, während der Installation der neuen Anwendung. Wenn dies nicht der Fall ist, kann dieser Konfigurationsschritt später ausgeführt werden. Informationen zu WSUS finden Sie unter der [WSUS-Website Handbuch](http://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Hotfixes:** außerdem, müssen Sie möglicherweise Analytics Platform System Hotfixes angewendet. Ein *Hotfix* ist ein Softwareupdate, das für einen bestimmten Kunden zur Behebung eines Problems mit der Software Analytics Platform System erstellt wird. Jedes Update ist eine ausführbare Datei, die die Korrektur des Problems kundenspezifische installiert wird. Jedes Update enthält auch eine Häufung von alle zuvor veröffentlichten Updates für Windows, SQLServer und Analytics Platform System. Wenn Sie einen Hotfix installieren möchten, geben Sie Microsoft-Support wird mit dem Hotfix und Anweisungen.  
  
**Bereich von Updates:** Anwenden von einem Hotfix oder ein Service Pack auf das Analytics Platform System muss die gesamte Anwendung offline schalten. D. h. werden Regionen PDW "und" HDInsight beeinflusst.  
  
**Zieladapter für SSIS und Clienttools:** beim einen Hotfix anwenden, die Änderungen an den SSIS-Ziel Adapter MSIS umfasst oder Client-Tools-MSI, wird die MSI-Dateien in aktualisiert die **C:\PDWINST\ClientTools** Verzeichnis auf dem Knoten "Zugriffssteuerung". Der Hotfix installiert die Komponenten aus der aktualisierten MSI-Dateien nicht automatisch. Um diese Komponenten zu aktualisieren, muss der Kunde die alten Versionen der Komponenten zu deinstallieren und installieren Sie die neuen Versionen von die aktualisierte MSI-Dateien. Wenn Sie einen Hotfix deinstallieren, die Änderungen an den SSIS-Ziel Adapter MSI umfasst oder Client Tools MSI, die MSI-Dateien für diese Komponenten werden auf früheren Versionen zurückgesetzt. Um diese Komponenten zu einer früheren Version wiederherzustellen, muss der Kunde die vorhandenen (neueren) Versionen der Komponenten deinstallieren und installieren die älteren Versionen von den in der wiederhergestellten MSI-Dateien.  
  
## <a name="software-servicing-topics"></a>Software, die Wartung von Themen  
In den folgenden Themen wird beschrieben, wie zum Verwalten von Software auf dem Gerät verarbeitet:  
  
-   [Herunterladen und Anwenden von Microsoft-Updates &#40;Analyseplattformsystem&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Deinstallieren Sie Microsoft Updates &#40;Analyseplattformsystem&#41;](uninstall-microsoft-updates.md)  
  
-   [Anwenden von Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Deinstallieren Sie Analytics Platform System Hotfixes &#40;Analyseplattformsystem&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
