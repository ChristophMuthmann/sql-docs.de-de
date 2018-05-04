---
title: Migrieren von MySQL-Datenbanken zu SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
caps.latest.revision: 12
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 771b28d558c9f34e1e41934ba6837678ee8b2415
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank (MySQLToSql)
SQL Server Migration Assistant (SSMA) for MySQL ist eine umfassende Umgebung, mit die Sie schnell MySQL-Datenbanken zu SQL Server oder SQL Azure migriert werden kann. SSMA für MySQL verwenden, können Sie überprüfen von Datenbankobjekten und Daten, Datenbanken für die Migration bewerten, Datenbankobjekte zu SQL Server oder SQL Azure migrieren und Migrieren von Daten klicken Sie dann auf SQL Server- oder SQL Azure.  
  
## <a name="recommended-migration-process"></a>Migrationsprozess empfohlen  
Verwenden Sie zum erfolgreichen Objekte und Daten aus MySQL-Datenbanken zu SQL Server oder SQL Azure Migrieren von folgendem Prozess:  
  
1.  [Arbeiten mit Projekten SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    Nachdem Sie das Projekt erstellt haben, können Sie die projektkonvertierung, Migrations- und Optionen des Typmappings festlegen. Weitere Informationen zu projekteinstellungen, finden Sie unter [Einstellung Projektoptionen &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md). Informationen zum Anpassen der datentypzuordnungen finden Sie unter [Zuordnung MySQL und SQL Server-Datentypen &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [Herstellen einer Verbindung mit MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [Herstellen einer Verbindung mit SQLServer &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [Zuordnen von MySQL-Datenbanken zu SQL Server-Schemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Herstellen einer Verbindung mit Azure SQL-Datenbank &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  Optional, [Bewerten von MySQL-Datenbanken für die Konvertierung &#40;MySQLToSQL&#41; ](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) zum Bewerten der Datenbankobjekte für die Konvertierung und schätzen Sie die Konvertierungszeit.  
  
7.  [Konvertieren von MySQL-Datenbanken &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [Synchronisierung](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
9. Sie können dies in eine der folgenden Arten erfolgen:  
  
    -   Speichern Sie ein Skript aus, und führen Sie sie auf SQL Server oder SQL Azure.  
  
    -   Synchronisieren Sie die Datenbankobjekte.  
  
10. [Migrieren von MySQL-Daten in SQLServer - Azure SQL-Datenbank &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. Bei Bedarf datenbankanwendungen zu aktualisieren.  
  
> [!NOTE]  
> Information_schema und MySQL-Schemas können nicht migriert werden.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Erste Schritte mit SSMA für MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
