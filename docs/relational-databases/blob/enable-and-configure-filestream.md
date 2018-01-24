---
title: Aktivieren und Konfigurieren von FILESTREAM | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FILESTREAM [SQL Server], enabling
ms.assetid: 78737e19-c65b-48d9-8fa9-aa6f1e1bce73
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d3adbba8dfe371014517a6e5290c649395f351d9
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="enable-and-configure-filestream"></a>Aktivieren und Konfigurieren von FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Vor der Verwendung von FILESTREAM müssen Sie FILESTREAM in der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]-Instanz aktivieren. In diesem Thema erfahren Sie, wie Sie FILESTREAM mit dem SQL Server-Konfigurations-Manager aktivieren.  
  
##  <a name="enabling"></a> Aktivieren von FILESTREAM  
  
#### <a name="to-enable-and-change-filestream-settings"></a>So aktivieren und ändern Sie FILESTREAM-Einstellungen  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], zeigen Sie auf **Konfigurationstools**, und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
2.  Klicken Sie in der Dienstliste mit der rechten Maustaste auf **SQL Server-Dienste**, und klicken Sie dann auf **Öffnen**.  
  
3.  Suchen Sie im Snap-In **SQL Server-Konfigurations-Manager** die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , auf der Sie FILESTREAM aktivieren möchten.  
  
4.  Klicken Sie mit der rechten Maustaste auf die Instanz, und klicken Sie dann auf **Eigenschaften**.  
  
5.  Klicken Sie im Dialogfeld **Eigenschaften von SQL Server** auf die Registerkarte **FILESTREAM** .  
  
6.  Aktivieren Sie das Kontrollkästchen **FILESTREAM für Transact-SQL-Zugriff aktivieren** .  
  
7.  Wenn das Lesen und Schreiben von FILESTREAM-Daten über Windows erforderlich ist, klicken Sie auf **FILESTREAM für E/A-Streamingzugriff auf Datei aktivieren**. Geben Sie den Namen der Windows-Freigabe in das Feld **Windows-Freigabename** ein.  
  
8.  Wenn Remoteclients auf FILESTREAM-Daten auf dieser Freigabe zugreifen müssen, wählen Sie **Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen**.  
  
9. Klicken Sie auf **Anwenden**.  
  
10. Klicken Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auf **Neue Abfrage** , um den Abfrage-Editor zu öffnen.  
  
11. Geben Sie im Abfrage-Editor den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code ein:  
  
    ```sql  
    EXEC sp_configure filestream_access_level, 2  
    RECONFIGURE  
    ```  
  
12. Klicken Sie auf **Ausführen**.  
  
13. Starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu.  
  
  
##  <a name="best"></a> Bewährte Methoden  
  
###  <a name="config"></a> Physische Konfiguration und Verwaltung  
 Beachten Sie beim Einrichten von FILESTREAM-Speichervolumes die folgenden Richtlinien:  
  
-   Deaktivieren Sie kurze Dateinamen auf FILESTREAM-Computersystemen. Bei kurzen Dateinamen dauert das Erstellen erheblich länger. Um kurze Dateinamen zu deaktivieren, verwenden Sie das Windows-Hilfsprogramm **fsutil** .  
  
-   Defragmentieren Sie FILESTREAM-Computersysteme in regelmäßigen Abständen.  
  
-   Verwenden Sie 64-KB-NTFS-Cluster. Komprimierte Volumes müssen auf 4-KB-NTFS-Cluster festgelegt werden.  
  
-   Deaktivieren Sie die Indizierung auf FILESTREAM-Volumes, und legen Sie **disablelastaccess** fest. Verwenden Sie zum Festlegen von **disablelastaccess** das Windows-Hilfsprogramm **fsutil**.  
  
-   Deaktivieren Sie die Virenüberprüfung für FILESTREAM-Volumes, wenn diese nicht erforderlich ist. Wenn eine Virenüberprüfung erforderlich ist, sollten keine Richtlinien festgelegt werden, durch die verdächtige oder infizierte Dateien automatisch gelöscht werden.  
  
-   Richten Sie die RAID-Stufe ein, die für Fehlertoleranz und die für Anwendungen erforderliche Leistung optimal geeignet ist.  
  
||||||  
|-|-|-|-|-|  
|RAID-Stufe|Schreibleistung|Leseleistung|Fehlertoleranz|Remarks|  
|RAID 5|Normal|Normal|Hervorragend|Die Leistung ist besser als bei einem einzelnen Datenträger oder JBOD und geringer als bei RAID 0 oder RAID 5 mit Striping.|  
|RAID 0|Hervorragend|Hervorragend|InclusionThresholdSetting||  
|RAID 5 + Striping|Hervorragend|Hervorragend|Hervorragend|Die aufwendigste Option.|  
  
  
###  <a name="database"></a> Physischer Datenbankentwurf  
 Beachten Sie beim Entwerfen einer FILESTREAM-Datenbank die folgenden Richtlinien:  
  
-   FILESTREAM-Spalten müssen von einer entsprechenden **uniqueidentifier**ROWGUID-Spalte begleitet werden. Diese Arten von Tabellen müssen auch über einen eindeutigen Index verfügen. In der Regel ist dieser Index kein gruppierter Index. Wenn die Geschäftslogik für Datenbanken einen gruppierten Index erfordert, müssen Sie sicherstellen, dass die im Index gespeicherten Werte nicht zufällig sind. Zufallswerte bewirken, dass der Index neu sortiert wird, sobald in der Tabelle eine Zeile hinzugefügt oder entfernt wird.  
  
-   Aus Leistungsgründen sollten die FILESTREAM-Dateigruppen und -Container nicht auf Volumes gespeichert werden, auf denen sich das Betriebssystem, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Protokoll, tempdb oder die Auslagerungsdatei befindet.  
  
-   Speicherplatzverwaltung und Richtlinien werden von FILESTREAM nicht direkt unterstützt. Sie können jedoch indirekt Speicherplatz verwalten und Richtlinien anwenden, indem Sie jede FILESTREAM-Dateigruppe einem separaten Volume zuweisen und die Verwaltungsfunktionen des Volumes verwenden.  
  
  
