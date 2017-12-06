---
title: Herstellen einer Verbindung mit Azure SQL-Datenbank (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to SQL Azure, SQL Azure permissions
- Connecting to SQL Azure, synchronization
ms.assetid: d0b6f16a-1880-459d-a0c7-28b7ef15c56a
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0368f95d842dfeae1cdc25d3f838f00bfc302483
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="connecting-to-azure-sql-db-mysqltosql"></a>Herstellen einer Verbindung mit Azure SQL-Datenbank (MySQLToSQL)
Um MySQL-Datenbanken zu SQL Azure zu migrieren, müssen Sie mit der Zielinstanz von SQL Azure verbinden. Wenn Sie eine Verbindung herstellen, wird SSMA Ruft Metadaten zu allen Datenbanken in der Instanz von SQL Azure ab und Datenbank-Metadaten in der SQL Azure-Metadaten-Explorer zeigt. SSMA speichert Informationen der Instanz von SQL Azure Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit SQL Azure bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie in SQL Azure erneut, wenn Sie möchten, dass eine aktive Verbindung mit dem Server verbinden. Sie können offline arbeiten, bis Sie Datenbankobjekte in SQL Azure laden und Migrieren von Daten.  
  
Metadaten zur Instanz von SQL Azure werden nicht automatisch synchronisiert. Um die Metadaten in SQL Azure-Metadaten-Explorer zu aktualisieren, müssen Sie stattdessen manuell die SQL Azure-Metadaten aktualisieren. Weitere Informationen finden Sie im Abschnitt "Synchronisieren von SQL Azure-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-azure-permissions"></a>Erforderliche SQL Azure-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung zu SQL Azure erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die das Konto ausführt:  
  
-   MySQL-Objekte zu konvertieren [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, um Metadaten von SQL Azure zu aktualisieren oder konvertierte Syntax zum Speichern von Skripts, das Konto muss über die Berechtigung zum Anmelden bei der Instanz von SQL Azure.  
  
-   Zum Laden von Datenbankobjekten in SQL Azure ist die Mindestberechtigung Anforderung die Mitgliedschaft in der **Db_owner** Datenbankrolle in der Zieldatenbank.  
  
## <a name="establishing-a-sql-azure-connection"></a>Einrichten einer SQL Azure-Verbindung  
Bevor Sie MySQL-Datenbankobjekte auf Azure SQL-Syntax konvertieren, müssen Sie eine Verbindung mit der Instanz von SQL Azure einrichten, wo Sie die MySQL-Datenbank bzw. sekundären Datenbanken migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Schemaebene MySQL anpassen, nach dem Herstellen einer Verbindung mit SQL Azure. Weitere Informationen finden Sie unter [Zuordnen von MySQL-Datenbanken zu SQL Server-Schemas &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung zu SQL Azure herstellen, stellen Sie sicher, dass die Instanz von SQL Azure ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit SQL Azure**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Azure** (diese Option ist nach der Erstellung eines Projekts).  
  
    Wenn Sie zuvor eine Verbindung zu SQL Azure hergestellt haben, wird der Befehlsname sein **eine erneute Verbindung mit SQL Azure**.  
  
2.  Klicken Sie im Dialogfeld Verbindung geben Sie ein, oder wählen Sie den Namen des SQL Azure.  
  
3.  Geben Sie ein, wählen oder **Durchsuchen** den Datenbanknamen.  
  
4.  Geben Sie ein oder wählen Sie **Benutzername**.  
  
5.  Geben Sie die **Kennwort**.  
  
6.  SSMA empfiehlt verschlüsselte Verbindung zu SQL Azure.  
  
7.  Klicken Sie auf **Verbinden**.  
  
> [!IMPORTANT]  
> SSMA für die MySQL unterstützt keine Verbindung mit **master** Datenbank in SQL Azure.  
  
## <a name="synchronizing-sql-azure-metadata"></a>Synchronisieren von SQL Azure-Metadaten  
Metadaten zu SQL Azure-Datenbanken wird nicht automatisch aktualisiert. Die Metadaten im Metadaten-Explorer von SQL Azure ist eine Momentaufnahme der Metadaten, wenn Sie zunächst mit SQL Azure verbunden, oder der letzten Ausführung, die Sie manuell die Metadaten aktualisiert. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit SQL Azure verbunden sind.  
  
2.  Wählen Sie in SQL Azure-Metadaten-Explorer das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Angenommen, um die Metadaten für alle Datenbanken zu aktualisieren, wählen Sie das Kontrollkästchen neben den Datenbanken an.  
  
3.  Mit der rechten Maustaste Datenbanken, oder die einzelne Datenbank oder das Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Wenn Sie die Zuordnung zwischen Schemas MySQL und SQL Azure-Datenbanken und Schemas anpassen zu können, finden Sie unter [Zuordnung MySQL-Datenbanken zu SQL Server-Schemas &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Konfigurationsoptionen für die Projekte anpassen können, finden Sie unter [Einstellung Projektoptionen &#40; MySQLToSQL &#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung MySQL und SQL Server-Datentypen &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Wenn Sie nicht verfügen, um diese Aufgaben auszuführen, können Sie die Objektdefinitionen für MySQL-Datenbank in SQL Azure-Objektdefinitionen konvertieren. Weitere Informationen finden Sie unter [MySQL-Datenbanken konvertieren &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
