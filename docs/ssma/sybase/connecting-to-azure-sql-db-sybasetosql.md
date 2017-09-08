---
title: Herstellen einer Verbindung mit Azure SQL-Datenbank (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 217492904d3d21818fed28222dcc6acaf193c92b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Herstellen einer Verbindung mit Azure SQL-Datenbank (SybaseToSQL)
Zum Migrieren von Sybase-Datenbanken in Azure SQL-Datenbank müssen Sie mit der Zielinstanz von Azure SQL-Datenbank verbinden. Wenn Sie eine Verbindung herstellen, wird SSMA Ruft Metadaten zu allen Datenbanken in der Instanz von Azure SQL-Datenbank ab und Datenbankmetadaten in der Azure SQL-DB-Metadaten-Explorer angezeigt. SSMA speichert Informationen der Instanz von Azure SQL-Datenbank, Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit Azure SQL-Datenbank bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie Azure SQL-Datenbank erneut, wenn Sie möchten, dass eine aktive Verbindung mit dem Server verbinden. Sie können offline arbeiten, bis Sie Datenbankobjekte in Azure SQL-Datenbank laden und Migrieren von Daten.  
  
Metadaten zu der Instanz von Azure SQL-Datenbank wird nicht automatisch synchronisiert. Um die Metadaten in Azure SQL-DB-Metadaten-Explorer zu aktualisieren, müssen Sie stattdessen manuell die Metadaten für die Azure SQL-Datenbank aktualisieren. Weitere Informationen finden Sie im Abschnitt "Synchronisieren von Azure SQL DB-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-azure-sql-db-permissions"></a>Erforderliche Berechtigungen für Azure SQL-DB  
Das Konto, das verwendet wird, für die Verbindung mit der Azure SQL-Datenbank erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die das Konto ausführt:  
  
1.  Konvertieren von Sybase-Objekten, [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, um Metadaten von Azure SQL-Datenbank zu aktualisieren oder konvertierte Syntax zum Speichern von Skripts, das Konto muss über die Berechtigung zum Anmelden bei der Instanz von Azure SQL-Datenbank verfügen.  
  
2.  Um die Datenbankobjekte in Azure SQL-Datenbank zu laden, die minimal erforderliche Berechtigungen-Anforderung ist die Mitgliedschaft in der **Db_owner** Datenbankrolle in der Zieldatenbank.  
  
## <a name="establishing-a-azure-sql-db-connection"></a>Herstellen einer Azure SQL-DB-Verbindung  
Vor dem Konvertieren Sybase-Datenbankobjekte auf Azure SQL-Datenbank-Syntax müssen Sie eine Verbindung mit der Instanz von Azure SQL-Datenbank einrichten, in dem Sie die Sybase-Datenbank bzw. sekundären Datenbanken migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Schemaebene Sybase anpassen, nach dem Herstellen einer Verbindung mit Azure SQL-Datenbank. Weitere Informationen finden Sie unter [Mapping Sybase ASE Schemas zum SQL Server-Schemas &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Bevor Sie versuchen, Azure SQL-Datenbank herstellen, stellen Sie sicher, dass die Instanz von Azure SQL-Datenbank ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit Azure SQL-Datenbank**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit Azure SQL-Datenbank**(diese Option ist nach der Erstellung eines Projekts).  
  
    Wenn Sie zuvor eine Verbindung mit der Azure SQL-Datenbank hergestellt haben, wird der Befehlsname sein **eine erneute Verbindung mit der Azure SQL-Datenbank**  
  
2.  Klicken Sie im Dialogfeld Verbindung geben Sie ein, oder wählen Sie den Namen des Azure SQL-Datenbank.  
  
3.  Geben Sie ein, wählen oder **Durchsuchen** den Datenbanknamen.  
  
4.  Geben Sie ein oder wählen Sie **Benutzername**.  
  
5.  Geben Sie die **Kennwort**.  
  
6.  SSMA empfiehlt verschlüsselte Verbindung mit der Azure SQL-Datenbank.  
  
7.  Klicken Sie auf **Verbinden**.  
  
> [!IMPORTANT]  
> SSMA für Sybase unterstützt keine Verbindung mit **master** Datenbank in Azure SQL-Datenbank.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Synchronisieren von Azure SQL-DB-Anweisungsmetadaten  
Metadaten zu Azure SQL-Datenbank-Datenbanken wird nicht automatisch aktualisiert. Die Metadaten in Azure SQL-DB-Metadaten-Explorer ist eine Momentaufnahme der Metadaten aus, wenn Sie zuerst mit Azure SQL-Datenbank bzw. den letzten, dass Sie manuell Metadaten aktualisiert verbunden. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit Azure SQL-Datenbank verbunden sind.  
  
2.  Wählen Sie in Azure SQL DB-Metadaten-Explorer das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Angenommen, um die Metadaten für alle Datenbanken zu aktualisieren, wählen Sie das Kontrollkästchen neben den Datenbanken an.  
  
3.  Mit der rechten Maustaste Datenbanken, oder die einzelne Datenbank oder das Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Wenn Sie die Zuordnung zwischen Sybase-Schemas und Azure SQL-Datenbank-Datenbanken und Schemas anpassen zu können, finden Sie unter [Zuordnungsschemas Sybase ASE zum SQL Server-Schemas &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Konfigurationsoptionen für die Projekte anpassen können, finden Sie unter [Einstellung Projektoptionen &#40; SybaseToSQL &#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung Sybase ASE und SQL Server-Datentypen &#40; SybaseToSQL &#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Wenn Sie nicht verfügen, um diese Aufgaben auszuführen, können Sie die Objektdefinitionen für Sybase-Datenbank in Azure SQL-Datenbank-Objektdefinitionen konvertieren. Weitere Informationen finden Sie unter [Konvertierung von Sybase ASE Datenbankobjekte &#40; SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

