---
title: "Sicherungsziel auswählen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dd0f291ca7863b653546243d18c3a289f1551a41
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="select-backup-destination"></a>Sicherungsziel auswählen
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Wählen Sie im Dialogfeld **Sicherungsziel auswählen** ein Gerät als Sicherungsziel aus. Ein Sicherungsziel kann entweder ein Datenträger oder ein logisches Sicherungsmedium sein.  
  
 **So verwenden Sie SQL Server Management Studio zum Sichern einer Datenbank**  
  
-   [Erstellen einer vollständigen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Sichern von Dateien und Dateigruppen &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Optionen  
 Die Optionen in diesem Dialogfeld sind davon abhängig, ob Sie ein Ziel auf einem Datenträger oder einem Band auswählen.  
  
 **Ziele auf dem Datenträger**  
 Zum Angeben eines Sicherungsziels wählen Sie eine der folgenden Optionen aus.  
  
|||  
|-|-|  
|**Dateiname**|Wählen Sie diese Option aus, um eine lokale Datei oder Remotedatei als Sicherungsziel im Textfeld einzugeben.<br /><br /> Klicken Sie zum Angeben einer lokalen Datei rechts vom Textfeld auf die Schaltfläche zum Durchsuchen, und wählen Sie dann auf den Festplatten des Computers, auf dem der Server ausgeführt wird, eine Datei aus. Sie können auch den vollständigen Pfad und Dateinamen direkt eingeben, z. B. `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Zum Angeben einer Remotedatei als Sicherungsziel geben Sie ihren vollqualifizierten UNC-Namen (Universal Naming Convention) ein. Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).<br /><br /> <br /><br /> **\*\* Wichtig \*\*** Beim Sichern von Daten über ein Netzwerk können Netzwerkfehler auftreten. Aus diesem Grund wird empfohlen, dass Sie den Sicherungsvorgang nach der Fertigstellung überprüfen. Weitere Informationen finden Sie unter [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).|  
|**Sicherungsmedium**|Wählen Sie diese Option aus, um ein logisches Sicherungsmedium auszuwählen.<br /><br /> Hinweis: Informationen zum Erstellen eines Datenträgersicherungsmediums finden Sie unter [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Ziele auf Band**  
 Gibt ein Sicherungsziel auf einem Bandlaufwerk an, das physisch mit dem Computer verbunden ist, auf dem der Server ausgeführt wird (d. h. die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Wählen Sie eine der folgenden Optionen.  
  
|||  
|-|-|  
|**Bandlaufwerk**|Wählen Sie diese Option aus, um ein Bandlaufwerk als Sicherungsziel aus der Liste der Bandlaufwerke auszuwählen, die physisch mit dem Computer verbunden sind, auf dem die Serverinstanz ausgeführt wird.<br /><br /> Hinweis: Bandsicherungsmedien auf Remotecomputern sind keine gültigen Sicherungsziele.|  
|**Sicherungsmedium**|Wählen Sie diese Option aus, um ein vorhandenes logisches Sicherungsmedium auszuwählen. Diese logischen Sicherungsmedien entsprechen Bandgeräten, die physisch mit dem Computer verbunden sind, auf dem die Serverinstanz ausgeführt wird.<br /><br /> Hinweis: Informationen zum Erstellen eines Bandsicherungsmediums finden Sie unter [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
