---
title: 'Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016 | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 328214976c50ff07b92376ae8061f97870980b24
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>Tutorial: Verwenden des Microsoft Azure BLOB-Speicherdiensts mit SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Willkommen zum Tutorial über das Arbeiten mit SQL Server 2016 im Dienst Microsoft Azure Blob Storage. Dieses Tutorial hilft Ihnen dabei, zu verstehen, wie der Dienst Microsoft Azure Blob Storage für SQL Server-Datendateien und SQL Server-Sicherungen verwendet wird.  
  
Die Unterstützung der SQL Server-Integration für den Dienst Microsoft Azure Blob Storage startete als eine Erweiterung von SQL Server 2012 Servicepack 1 CU2 und wurde zudem mit SQL Server 2014 und SQL Server 2016 erweitert. Eine Übersicht der Funktionen und Vorteile finden Sie unter [SQL Server-Datendateien in Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). Eine Livedemo finden Sie unter [Demo of Point in Time Restore](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)(in englischer Sprache).  
  
  
**Download**<br /><br />**>>**  Um [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]herunterzuladen, gehen Sie unter  **[Evaluierungscenter](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.<br /><br />**>>**  Sie haben ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/)** , um einen virtuellen Computer zu starten, auf dem [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] bereits installiert ist.  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Tutorial erfahren Sie in mehreren Lektionen, wie Sie im Dienst Microsoft Azure Blob Storage mit SQL Server-Datendateien arbeiten. Jede Lektion ist auf eine bestimmte Aufgabe fokussiert, und die Lektionen sollten nacheinander ausgeführt werden. Zunächst erfahren Sie, wie Sie in Blob Storage einen neuen Container mit einer gespeicherten Zugriffsrichtlinie und einer Shared Access Signature (SAS) erstellen. Danach erfahren Sie, wie Sie SQL Server-Anmeldeinformationen erstellen, um SQL Server in Azure Blob Storage zu integrieren. Als Nächstes sichern Sie eine Datenbank in Blob Storage und stellen sie in einem virtuellen Azure-Computer wieder her. Anschließend verwenden Sie die Protokollsicherung für die Übertragung von Dateimomentaufnahmen von SQL Server 2016, um den Stand eines bestimmten Zeitpunkts in einer neuen Datenbank wiederherzustellen. Das Tutorial wird schließlich die Verwendung der gespeicherten Meta Data-Prozeduren und -Funktionen demonstrieren, um Ihnen dabei zu helfen, Dateimomentaufnahme-Sicherungen zu verstehen und mit ihnen zu arbeiten.  
  
In diesem Artikel wird Folgendes vorausgesetzt:  
  
-   Sie verfügen über eine lokale Instanz von SQL Server 2016 mit einer installierten Kopie von AdventureWorks2014.  
  
-   Sie verfügen über ein Azure-Speicherkonto.  
  
-   Sie besitzen mindestens einen virtuellen Azure-Computer auf dem SQL Server 2016 installiert ist, und haben diesen virtuellen Computer gemäß [Bereitstellen eines virtuellen Computers mit SQL Server im Azure-Portal](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-provision-sql-server/)bereitgestellt. Optional kann für das Szenario in [Lektion 8: Wiederherstellen als neue Datenbank aus der Protokollsicherung](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md) ein zweiter virtueller Computer verwendet werden.  
  
Dieses Tutorial ist in neun Lektionen aufgeteilt, die nach der Reihenfolge abgeschlossen werden müssen:  
  
**[Lektion 1: Erstellen einer Richtlinie und einer Shared Access Signature (SAS) in einem Azure-Container](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
In dieser Lektion erstellen Sie eine Richtlinie für den neuen Blobcontainer und generieren zusätzlich eine SAS (Shared Access Signature, Signatur für gemeinsamen Zugriff), die für die Erstellung einer SQL Server-Anmeldeinformation verwendet wird.  
  
**[Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
In dieser Lektion erstellen Sie mithilfe eines SAS-Schlüssels eine Anmeldeinformation, um die Sicherheitsinformationen für den Zugriff auf das Microsoft Azure-Speicherkonto zu speichern.  
  
**[Lektion 3: Datenbanksicherung über URLs](../relational-databases/lesson-3-database-backup-to-url.md)**  
In dieser Lektion sichern Sie eine lokale Datenbank in Microsoft Azure Blob Storage.  
  
**[Lektion 4: Wiederherstellen einer Datenbank auf einem virtuellen Computer über URLs](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
In dieser Lektion stellen Sie eine Datenbank auf einem virtuellen Azure-Computer in Microsoft Azure Blob Storage wieder her.  
  
**[Lektion 5: Backup einer Datenbank mit Dateimomentaufnahme-Sicherung](../relational-databases/lesson-5-backup-database-using-file-snapshot-backup.md)**  
In dieser Lektion sichern Sie eine Datenbank mithilfe der Dateimomentaufnahme-Sicherung und Anzeigen von Metadaten zu Datei-Momentaufnahmen.  
  
**[Lektion 6: Generate activity and backup log using file-snapshot backup (Generieren von Aktivität und Erstellen einer Sicherung eines Protokolls mithilfe der Dateimomentaufnahme-Sicherung)](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
In dieser Lektion generieren Sie Aktivitäten in der Datenbank und führen mehrere Protokollsicherungen mithilfe der Dateimomentaufnahme-Sicherung und der Dateimomentaufnahme-Metadaten durch.  
  
**[Lektion 7: Wiederherstellen des Standes einer Datenbank zu einem bestimmten Zeitpunkt](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
In dieser Lektion stellen Sie eine Datenbank bis zu einem Zeitpunkt mithilfe von zwei Dateimomentaufnahme-Sicherungen wieder her.  
  
**[Lektion 8: Wiederherstellen als neue Datenbank aus der Protokollsicherung](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)**  
In dieser Lektion führen Sie aus einer Sicherung einer Protokolldatei für Datei-Momentaufnahmen eine Wiederherstellung auf einem anderen virtuellen Computer durch.  
  
**[Lektion 9: Verwalten von Sicherungssätzen und Dateimomentaufnahme-Sicherungen](../relational-databases/lesson-9-manage-backup-sets-and-file-snapshot-backups.md)**  
In dieser Lektion löschen Sie nicht benötigte Sicherungssätze und lernen, wie Sie verwaiste Dateimomentaufnahme-Sicherungen (falls nötig) löschen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[SQL Server-Datendateien in Microsoft Azure](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Dateimomentaufnahme-Sicherungen für Datenbankdateien in Azure](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[SQL Server-Sicherung über URLs](../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
  

