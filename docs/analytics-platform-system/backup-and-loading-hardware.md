---
title: Sicherung und Laden von Hardware - Parallel Data Warehouse
description: Um Ihre End-to-End Data warehousing-Lösung auf Analytics Platform System (APS) mit Parallel Data Warehouse (PDW) bereitstellen, müssen Sie einen Plan für das Datawarehouse sichern, und Laden von Daten zu erstellen. Verwenden Sie diese Anleitung erwerben und Konfigurieren der Sicherung und Laden von Servern, die Ihren geschäftsanforderungen erfüllen.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4d7f7b6b4edea9dacab7287a7936b7fd87fd7973
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Sicherung und laden die Übersicht über Hardware - Parallel Data Warehouse
Um Ihre End-to-End Data warehousing-Lösung auf Analytics Platform System (APS) mit Parallel Data Warehouse (PDW) bereitstellen, müssen Sie einen Plan für das Datawarehouse sichern, und Laden von Daten zu erstellen. Verwenden Sie diese Anleitung erwerben und Konfigurieren der Sicherung und Laden von Servern, die Ihren geschäftsanforderungen erfüllen.  
  
## <a name="acquire-and-configure-backup-servers"></a>Erwerben Sie und konfigurieren Sie die backup-Server  
![Sichern von Prozess](media/backup-process.png "Prozess sichern")  
  
Um einen PDW-Datenbank zu sichern, benötigen Sie eine oder mehrere Sicherungsserver. Sie können eigene vorhandenen Hardware verwenden oder neuen Hardware zu erwerben. Weitere Informationen finden Sie unter [erwerben und Konfigurieren eines Servers für die Sicherung](acquire-and-configure-backup-server.md). Diese Anweisungen beinhalten eine [Backup Server Capacity planning Arbeitsblatt](backup-capacity-planning-worksheet.md) helfen Ihnen beim Planen der richtigen Lösung für die Sicherung.  
  
## <a name="acquire-and-configure-loading-servers"></a>Erwerben Sie und konfigurieren Sie beim Laden von Servern  
![Prozess des Ladens](media/loading-process.png "Prozess des Ladens")  
  
Um Daten zu laden, benötigen Sie eine oder mehrere beim Laden von Servern. Können Sie eigene vorhandene ETL oder auf anderen Servern, oder Sie können neue Server erwerben. Weitere Informationen finden Sie unter [abrufen und Konfigurieren eines Servers geladen](acquire-and-configure-loading-server.md). Diese Anweisungen beinhalten eine [Server Capacity planning Arbeitsblatt laden](loading-server-capacity-planning-worksheet.md) helfen Ihnen beim Planen der richtigen Lösung für das Laden.  
  
## <a name="see-also"></a>Siehe auch  
[Sicherung und Wiederherstellung (Übersicht)](backup-and-restore-overview.md)  
[– Übersicht](load-overview.md)  
  
