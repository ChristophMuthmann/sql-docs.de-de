---
title: Partitionierung mit temporären Tabellen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/26/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c97854b8b9264c7bd52cbb24cc3ac7ae90c8609
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="partitioning-with-temporal-tables"></a>Partitionierung mit temporären Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Sie können die Partitionierung unabhängig voneinander für die aktuelle und die Verlaufstabelle verwenden. Ohne Systemversionsverwaltung können mittels Partitionierung jedoch keine Dateninhalte geändert werden.  
  
> [!NOTE]  
>  Die Partitionierung ist eine Funktion der Enterprise Edition von SQL Server 2016 vor dem Service Pack 1 und früheren Versionen. Sämtliche Editionen von SQL Server 2016 Service Pack 1 und spätere Versionen unterstützen die Partitionierung.
  
-   **Aktuelle Tabelle:**  
  
    -   **SWITCH IN** für die aktuelle Tabelle kann zum Laden und Abfragen von Daten verwendet werden, solange **SYSTEM_VERSIONING** mit **ON**  
  
    -   **SWITCH OUT** ist nicht zulässig, wenn **SYSTEM_VERSIONING** mit **ON**  
  
-   **Verlaufstabelle:**  
  
    -   **SWITCH OUT** kann über die Verlaufstabelle ausgeführt werden, solange **SYSTEM_VERSIONING** aktiviert ist ( **ON** ), um Teile der Verlaufsdaten zu löschen, die nicht mehr relevant sind.  
  
    -   **SWITCH IN** ist nicht zulässig, solange **SYSTEM_VERSIONING** aktiviert ist ( **ON** ), da es die Konsistenz temporaler Daten beeinträchtigen kann.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Systemkonsistenzprüfungen von temporalen Tabellen](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
