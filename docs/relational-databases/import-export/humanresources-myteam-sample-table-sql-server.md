---
title: HumanResources.myTeam-Beispieltabelle (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7c82b62908b8004c9ef93c77b5d980cb65b0787
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>HumanResources.myTeam-Beispieltabelle (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Viele der Codebeispiele in [Importieren und Exportieren von Massendaten](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) erfordern eine besondere Testtabelle namens **myTeam**. Bevor Sie die Beispiele ausführen können, müssen Sie die **myTeam** -Tabelle im **HumanResources** -Schema der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank erstellen.  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ist eine der Beispieldatenbanken in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Die **myTeam** -Tabelle enthält die folgenden Spalten.  
  
|Column|Datentyp|NULL-Zulässigkeit|Beschreibung|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|**smallint**|Nicht NULL|Primärschlüssel für die Zeilen. Mitarbeiter-ID eines Mitglieds meines Teams.|  
|**Name**|**nvarchar(50)**|Nicht NULL|Name eines Mitglieds meines Teams.|  
|**Titel**|**nvarchar(50)**|NULL zulassen|Titel des Mitarbeiters in meinem Team.|  
|**Hintergrund**|**nvarchar(50)**|Nicht NULL|Datum und Uhrzeit des letzten Updates der Zeile. (Standardwert)|  
  
**So erstellen Sie HumanResources.myTeam**  
  
-   Verwenden Sie die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen:  
  
    ```sql
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
**So füllen Sie HumanResources.myTeam auf**  
  
-   Führen Sie die folgenden `INSERT` -Anweisungen zum Auffüllen der Tabelle mit zwei Zeilen aus:  
  
    ```sql
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  Bei diesen Anweisungen wird die vierte Spalte ( `Background`) ausgelassen. Diese besitzt einen Standardwert. Das Auslassen dieser Spalte bewirkt, dass diese Spalte bei der `INSERT` -Anweisung leer bleibt.  
  
## <a name="see-also"></a>Siehe auch  
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  
