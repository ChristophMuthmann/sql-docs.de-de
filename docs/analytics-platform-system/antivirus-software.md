---
title: Antivirus-Software (Analytics Platform System)
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
ms.assetid: 60ab9a88-d339-4917-a38b-f9481aef38fd
caps.latest.revision: "29"
ms.openlocfilehash: f1d5c81381b486ec89198fed6aa22ccff22a544a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="antivirus-software"></a>Antivirus-Software
Wenn Ihr Rechenzentrum antivirus-Software erfordert, verwenden Sie diese Richtlinien antivirus-Software auf Analytics Platform System zu installieren. Es wird empfohlen, antivirus-Software, wenn sie über gute zwingend Ihres Rechenzentrums ist nicht installiert.  
  
> [!WARNING]  
> Es wird dringend empfohlen, dass das Sicherheitsrisiko Analytics Platform System als Ganzes und für jeden Computer einzeln zu bewerten und Sie die Tools auswählen, die für das Sicherheitsrisiko Maß an jedem Computer geeignet sind. Darüber hinaus wird empfohlen, bevor Sie ein beliebiges Projekt Virenschutz Rollout, testen Sie das gesamte System unter voller Auslastung Änderungen Stabilität und Leistung zu messen.  
>   
> Virenschutzsoftware erfordert einige Systemressourcen ausgeführt. Sie müssen durchführen, testen, bevor und nachdem Sie Ihre antivirus-Software um zu bestimmen, ob es Auswirkung auf die Leistung auf das Analytics Platform System ist installiert.  
  
In diesem Thema basiert auf der Anleitungen im [Gewusst wie: Auswählen von antivirus-Software auf Computern ausgeführt werden, auf denen SQL Server ausgeführt werden](http://support.microsoft.com/kb/309422) und [KB-Artikel 961804](http://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Ausschlussliste für physische Hosts  
Um die antivirus-Software auf physischen Hosts installieren, schließen Sie die folgende Liste von Verzeichnissen und Prozesse. Diese sollen nicht durch die Antivirensoftware durchsucht werden.  
  
**Schließen Sie diese Verzeichnisse:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V - Konfigurationsverzeichnis für die virtuelle Maschine  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual Festplatten - Standardverzeichnis für die virtuelle Festplatte  
  
-   C:\clusterStorage - Verzeichnisse virtuelle Festplattenlaufwerk  
  
**Diese Prozesse ausschließen:**  
  
-   Verwaltungsdienst für virtuelle Computer (Vmms.exe)  
  
-   Virtual Machine-Arbeitsprozesse (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Ausschlussliste für den virtuellen Computern (VMs)  
Um die antivirus-Software auf den virtuellen Computern zu installieren, schließen Sie die folgende Liste von Verzeichnissen und Dateien. Diese sollen nicht durch die Antivirensoftware durchsucht werden.  
  
***PDW_region*-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***Appliance_domain*-AD01** und  ***Appliance_domain*-AD02**  
  
-   Keine Einschränkungen  
  
**Virtuellen serverknotencomputern**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***Appliance_domain*– VMM**  
  
-   Keine Einschränkungen  
  
***Appliance_domain*- Windows-Bereitstellungsdienste**  
  
-   Keine Einschränkungen  
  
***Appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Siehe auch  
[Appliance-Verwaltungsaufgaben &#40; Analyseplattformsystem &#41;](appliance-management-tasks.md)  
  
