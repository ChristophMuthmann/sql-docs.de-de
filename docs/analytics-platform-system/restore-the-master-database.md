---
title: Wiederherstellen der master-Datenbank – Analytics Platform System | Microsoft Docs
description: Wiederherstellen Sie den master-Datenbank in Analytics Platform System an.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>Wiederherstellen der master-Datenbank in Analytics Platform System
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
  
