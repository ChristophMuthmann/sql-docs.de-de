---
title: Wiederherstellen der Master-Datenbank (Analytics Platform System)
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
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: "11"
ms.openlocfilehash: ff00e17d05b13317e009357e8c2089a46cbce4a4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="restore-the-master-database"></a>Wiederherstellen der Master-Datenbank
Die **Restore Master** Seite von SQL Server PDW-Konfigurations-Manager können Sie die master-Datenbank aus einer Sicherung wiederherstellen.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
> [!IMPORTANT]  
> Beim Ausführen der Wiederherstellung muss SQL Server PDW den aktuellen master-Datenbank löschen, der Sicherheitsinformationen des Benutzers sowie der Datenbankkatalog enthält. Es wird empfohlen, eine Sicherungskopie der aktuellen master-Datenbank vor dem Ausführen der Wiederherstellung.  
  
## <a name="to-restore-the-master-database"></a>So stellen Sie die master-Datenbank wieder her  
  
1.  Starten Sie den Konfigurations-Manager. Weitere Informationen finden Sie unter [starten Sie den Konfigurations-Manager &#40; Analyseplattformsystem &#41; ](launch-the-configuration-manager.md).  
  
2.  Klicken Sie im linken Bereich des Konfigurations-Managers auf **Restore Master**.  
  
3.  Wählen Sie die master Sicherung wiederherstellen.  
  
4.  Klicken Sie auf **Anwenden**.  
  
5.  Beim Ausführen der Wiederherstellung wird SQL Server PDW alle Appliance Dienste heruntergefahren und trennen Sie alle Benutzer. Nach Abschluss der Wiederherstellung wird in SQL Server PDW Appliance Dienste neu gestartet.  
  
![DWConfig-Anwendung, PDW Restore Master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
