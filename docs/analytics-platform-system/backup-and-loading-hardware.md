---
title: Sicherung und Laden von Hardwareübersicht für APS PDW
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Um die End-to-End Data warehousing-Lösung auf Analytics Platform System (APS) mit SQL Server Parallel Data Warehouse (PDW) bereitstellen, müssen Sie einen Plan für das Datawarehouse sichern, und Laden von Daten zu erstellen.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 3a2ae046-f8d8-4a5c-b3c1-6ecee005df6c
caps.latest.revision: 9
ms.openlocfilehash: 8979b0d7b14f3e6b3de2834fdc800c5281d057ad
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="backup-and-loading-hardware-overview"></a>Sicherung und Laden von Hardware (Übersicht)
Um die End-to-End Data warehousing-Lösung auf Analytics Platform System (APS) mit SQL Server Parallel Data Warehouse (PDW) bereitstellen, müssen Sie einen Plan für das Datawarehouse sichern, und Laden von Daten zu erstellen. Verwenden Sie diese Anleitung erwerben und Konfigurieren der Sicherung und Laden von Servern, die Ihren geschäftsanforderungen erfüllen.  
  
## <a name="acquire-and-configure-backup-servers"></a>Erwerben Sie und konfigurieren Sie die backup-Server  
![Sichern von Prozess](media/backup-process.png "Prozess sichern")  
  
Um einen PDW-Datenbank zu sichern, benötigen Sie eine oder mehrere Sicherungsserver. Sie können eigene vorhandenen Hardware verwenden oder neuen Hardware zu erwerben. Weitere Informationen finden Sie unter [erwerben und Konfigurieren eines Servers für die Sicherung](acquire-and-configure-backup-server.md). Diese Anweisungen beinhalten eine [Backup Server Capacity planning Arbeitsblatt](backup-capacity-planning-worksheet.md) helfen Ihnen beim Planen der richtigen Lösung für die Sicherung.  
  
## <a name="acquire-and-configure-loading-servers"></a>Erwerben Sie und konfigurieren Sie beim Laden von Servern  
![Prozess des Ladens](media/loading-process.png "Prozess des Ladens")  
  
Um Daten zu laden, benötigen Sie eine oder mehrere beim Laden von Servern. Können Sie eigene vorhandene ETL oder auf anderen Servern, oder Sie können neue Server erwerben. Weitere Informationen finden Sie unter [abrufen und Konfigurieren eines Servers geladen](acquire-and-configure-loading-server.md). Diese Anweisungen beinhalten eine [Server Capacity planning Arbeitsblatt laden](loading-server-capacity-planning-worksheet.md) helfen Ihnen beim Planen der richtigen Lösung für das Laden.  
  
## <a name="see-also"></a>Siehe auch  
[Sicherung und Wiederherstellung (Übersicht)](backup-and-restore-overview.md)  
[– Übersicht](load-overview.md)  
  
