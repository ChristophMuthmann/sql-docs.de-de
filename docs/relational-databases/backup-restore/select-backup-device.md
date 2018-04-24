---
title: Sicherungsmedium auswählen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
caps.latest.revision: 27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6f319e92843f9d13240f3a34a329d4d6351b987
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="select-backup-device"></a>Sicherungsmedium auswählen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe des Dialogfelds **Sicherungsmedium auswählen** können Sie ein logisches Sicherungsmedium für die Wiederherstellung auswählen.  
  
 Ein logisches Sicherungsmedium ist ein benutzerdefiniertes logisches Medium, das einem vom Betriebssystem bereitgestellten physischen Medium, entweder Bandlaufwerk oder Disketten- bzw. Festplattenlaufwerk, entspricht.  
  
> [!NOTE]  
>  Wenn eine Sicherung mehrere Sicherungsmedien verwendet, müssen diese alle einem einzigen Medientyp entsprechen.  
  
 **So verwenden Sie SQL Server Management Studio zum Anzeigen des Inhalts eines Sicherungsmediums**  
  
-   [Anzeigen der Inhalte eines Sicherungsbands oder einer -datei &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Tastatur  
 **Sicherungsmedium**  
 Wählen Sie im Listenfeld den Namen eines logischen Sicherungsmediums aus, von dem die Wiederherstellung erfolgen soll.  
  
 Weitere Informationen zum Anzeigen des Inhalts eines Sicherungsmediums finden Sie unter [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md).  
  
## <a name="remarks"></a>Remarks  
 Wenn kein logisches Sicherungsmedium in der Liste angezeigt wird, das die gesuchte Sicherung enthält, wurde die Sicherung möglicherweise direkt in eine oder mehrere Dateien oder Bandlaufwerke geschrieben. Schließen Sie in diesem Fall das Dialogfeld **Sicherungsmedium auswählen** , und wählen Sie im Dialogfeld **Sicherung angeben** im Listenfeld **Sicherungsmedium** die Option **Datei** oder **Band** aus.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
