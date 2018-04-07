---
title: Wiederherstellen der Master-Datenbank (Analytics Platform System)
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
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: 11
ms.openlocfilehash: 0f1acb692198873897d5dc26e2074beab4517e44
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="restore-the-master-database"></a>Wiederherstellen der Master-Datenbank
Die **Restore Master** Seite von SQL Server PDW-Konfigurations-Manager können Sie die master-Datenbank aus einer Sicherung wiederherstellen.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
> [!IMPORTANT]  
> Beim Ausführen der Wiederherstellung muss SQL Server PDW den aktuellen master-Datenbank löschen, der Sicherheitsinformationen des Benutzers sowie der Datenbankkatalog enthält. Es wird empfohlen, eine Sicherungskopie der aktuellen master-Datenbank vor dem Ausführen der Wiederherstellung.  
  
## <a name="to-restore-the-master-database"></a>So stellen Sie die master-Datenbank wieder her  
  
1.  Starten Sie den Konfigurations-Manager. Weitere Informationen finden Sie unter [Starten des Konfigurations-Managers &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md).  
  
2.  Klicken Sie im linken Bereich des Konfigurations-Managers auf **Restore Master**.  
  
3.  Wählen Sie die master Sicherung wiederherstellen.  
  
4.  Klicken Sie auf **Anwenden**.  
  
5.  Beim Ausführen der Wiederherstellung wird SQL Server PDW alle Appliance Dienste heruntergefahren und trennen Sie alle Benutzer. Nach Abschluss der Wiederherstellung wird in SQL Server PDW Appliance Dienste neu gestartet.  
  
![DWConfig-Anwendung, PDW Restore Master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
