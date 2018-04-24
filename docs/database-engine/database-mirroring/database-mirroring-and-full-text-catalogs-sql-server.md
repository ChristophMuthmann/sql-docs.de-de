---
title: Datenbankspiegelung und Volltextkataloge (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
caps.latest.revision: 50
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca9e2962c91cbfaaf13ea7357a903ac89e8bcf82
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>Datenbankspiegelung und Volltextkataloge (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Führen Sie zum Erstellen einer Datenbankspiegelung mit einem Volltextkatalog den üblichen Sicherungsvorgang aus, um eine vollständige Sicherung der Prinzipaldatenbank zu erstellen, und stellen Sie die Sicherung wieder her, um die Datenbank auf den Spiegelserver zu kopieren. Weitere Informationen finden Sie unter [Vorbereiten einer Spiegeldatenbank auf die Spiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)verwendet.  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>Volltextkataloge und -indizes vor dem Failover  
 In einer neu erstellten Spiegeldatenbank ist der Volltextkatalog mit jenem Volltextkatalog identisch, der während der Datenbanksicherung verwendet wurde. Nach Beginn der Datenbankspiegelung werden alle durch DDL-Anweisungen (CREATE FULLTEXT CATALOG, ALTER FULLTEXT CATALOG, DROP FULLTEXT CATALOG) vorgenommenen Änderungen an der Katalogebene protokolliert und an den Spiegelserver gesendet, um in der Spiegeldatenbank wiedergegeben zu werden. Änderungen auf Indexebene werden jedoch nicht in der Spiegeldatenbank reproduziert, da sie nicht auf dem Prinzipalserver protokolliert werden. Daher ist der Inhalt des Volltextkatalogs in der Spiegeldatenbank nicht mehr mit dem Volltextkatalog in der Prinzipaldatenbank synchron, wenn sich letzterer ändert.  
  
## <a name="full-text-indexes-after-failover"></a>Volltextindizes nach einem Failover  
 Nach einem Failover ist in folgenden Situationen eine vollständige Durchforstung des Volltextindexes auf dem neuen Prinzipalserver erforderlich oder zumindest nützlich:  
  
-   Wenn die Änderungsnachverfolgung für den Volltextindex AUSgeschaltet ist, müssen Sie eine vollständige Durchforstung für diesen Index durchführen. Verwenden Sie dazu die folgende Anweisung:  
  
     ALTER FULLTEXT INDEX ON *Tabellenname* START FULL POPULATION  
  
-   Wenn für einen Volltextindex die automatische Änderungsnachverfolgung konfiguriert ist, wird der Volltextindex automatisch synchronisiert. Durch die Synchronisierung wird jedoch die Leistung des Volltextindexes beeinträchtigt. Verlangsamt sich die Ausführung übermäßig, können Sie eine vollständige Durchforstung verursachen, indem Sie die Änderungsnachverfolgung ausschalten und anschließend wieder die automatische Änderungsnachverfolgung festlegen:  
  
    -   So schalten Sie die Änderungsnachverfolgung aus:  
  
         ALTER FULLTEXT INDEX ON *Tabellenname* SET CHANGE_TRACKING OFF  
  
    -   So legen Sie die automatische Änderungsnachverfolgung fest:  
  
         ALTER FULLTEXT INDEX ON *Tabellenname* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  Wenn Sie sehen möchten, ob die automatische Änderungsnachverfolgung aktiviert ist, können Sie die [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md) -Funktion zum Abfragen der **TableFullTextBackgroundUpdateIndexOn** -Eigenschaft der Tabelle verwenden.  
  
 Weitere Informationen finden Sie unter [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
> [!NOTE]  
>  Das Starten eines Durchforstungsvorgangs nach einem Failover funktioniert gleichermaßen wie das Starten eines Durchforstungsvorgangs nach einer Wiederherstellung.  
  
## <a name="after-forcing-service"></a>Nach dem Erzwingen des Diensts  
 Führen Sie einen vollständige Durchforstung durch, nachdem die Ausführung des Diensts auf dem Spiegelserver (mit möglichem Datenverlust) erzwungen wurde. Die zu verwendende Methode zum Starten einer vollständigen Durchforstung hängt davon ab, ob für den betroffenen Volltextindex die Änderungsnachverfolgung aktiviert ist. Weitere Informationen finden Sie weiter oben in diesem Thema unter "Volltextindizes nach einem Failover".  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Sichern und Wiederherstellen von Volltextkatalogen und Indizes](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
  
