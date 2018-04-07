---
title: Antivirus-Software (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60ab9a88-d339-4917-a38b-f9481aef38fd
caps.latest.revision: 29
ms.openlocfilehash: 27e3bc7eae50c0418c0dcb4df99565b3f0edeadf
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="antivirus-software"></a>Antivirus Software
Wenn Ihr Rechenzentrum antivirus-Software erfordert, verwenden Sie diese Richtlinien antivirus-Software auf Analytics Platform System zu installieren. Es wird empfohlen, antivirus-Software, wenn sie über gute zwingend Ihres Rechenzentrums ist nicht installiert.  
  
> [!WARNING]  
> Es wird dringend empfohlen, dass das Sicherheitsrisiko Analytics Platform System als Ganzes und für jeden Computer einzeln zu bewerten und Sie die Tools auswählen, die für das Sicherheitsrisiko Maß an jedem Computer geeignet sind. Darüber hinaus wird empfohlen, bevor Sie ein beliebiges Projekt Virenschutz Rollout, testen Sie das gesamte System unter voller Auslastung Änderungen Stabilität und Leistung zu messen.  
>   
> Virenschutzsoftware erfordert einige Systemressourcen ausgeführt. Sie müssen durchführen, testen, bevor und nachdem Sie Ihre antivirus-Software um zu bestimmen, ob es Auswirkung auf die Leistung auf das Analytics Platform System ist installiert.  
  
In diesem Thema basiert auf der Anleitungen im [Gewusst wie: Auswählen von antivirus-Software auf Computern ausgeführt werden, auf denen SQL Server ausgeführt werden](http://support.microsoft.com/kb/309422) und [KB-Artikel 961804](http://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Ausschlussliste für physische Hosts  
Um die antivirus-Software auf physischen Hosts installieren, schließen Sie die folgende Liste von Verzeichnissen und Prozesse. Diese sollen nicht durch die Antivirensoftware durchsucht werden.  
  
**Schließen Sie diese Verzeichnisse:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V - Virtual machine configuration directory  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks - Default virtual hard disk drive directory  
  
-   C:\clusterStorage - Verzeichnisse virtuelle Festplattenlaufwerk  
  
**Diese Prozesse ausschließen:**  
  
-   Verwaltungsdienst für virtuelle Computer (Vmms.exe)  
  
-   Virtual Machine-Arbeitsprozesse (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Ausschlussliste für den virtuellen Computern (VMs)  
Um die antivirus-Software auf den virtuellen Computern zu installieren, schließen Sie die folgende Liste von Verzeichnissen und Dateien. Diese sollen nicht durch die Antivirensoftware durchsucht werden.  
  
***PDW_region*-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***Appliance_domain *-AD01** und ***Appliance_domain *-AD02**  
  
-   Keine Einschränkungen  
  
**Virtuellen serverknotencomputern**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-VMM**  
  
-   Keine Einschränkungen  
  
***Appliance_domain *-Windows-Bereitstellungsdienste**  
  
-   Keine Einschränkungen  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Siehe auch  
[Appliance-Verwaltungsaufgaben &#40;Analyseplattformsystem&#41;](appliance-management-tasks.md)  
  
