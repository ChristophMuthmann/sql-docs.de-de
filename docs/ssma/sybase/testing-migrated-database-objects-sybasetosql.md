---
title: Testen von Datenbankobjekten (SybaseToSQL) migriert | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4937f6b4-86bd-4070-88df-3d216306c33a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1d66b93de265c4976c1c570de7cffe828c7424ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="testing-migrated-database-objects-sybasetosql"></a>Testen von Datenbankobjekten (SybaseToSQL) migriert
Microsoft SQL Server Migration Assistant für Sybase Tester (SSMA Tester) automatisch die Konvertierung der Datenbank-Objekt und überprüft die Datenmigration von SSMA vorgenommen werden. Nachdem Sie alle Schritte der SSMA-Migration abgeschlossen wurden, verwenden Sie SSMA Tester, stellen Sie sicher, dass die konvertierte Objekte die gleiche Weise funktioniert und alle Daten ordnungsgemäß übertragen wurde.  
  
> [!NOTE]  
> Tester Komponente ist im Fall von Azure-Verbindung deaktiviert.  
  
Sie können die folgenden Objekttypen mit SSMA Tester testen:  
  
-   Tabellen  
  
-   Gespeicherte Prozeduren  
  
-   Ansichten.  
  
-   Eigenständige Anweisungen.  
  
SSMA-Tester führt zum Testen auf Sybase und ihren äquivalenten in SQL Server ausgewählten Objekte. Anschließend vergleicht er die Ergebnisse entsprechend den folgenden Kriterien:  
  
-   Unterscheiden sich die Änderungen in Tabellendaten?  
  
-   Unterscheiden sich die Werte von Ausgabeparametern für Prozeduren und Funktionen?  
  
-   Führen Sie Funktionen, die die gleichen Ergebnisse zurück?  
  
-   Sind die Resultsets identisch?  
  
> [!NOTE]  
> Achtung! Verwenden Sie niemals SSMA Tester in Produktionssystemen. Während der Tester Ausführung werden dem Quellschema und Daten geändert. In der Zwischenzeit kann die vollständige Wiederherstellen des ursprünglichen Zustands für einige Typen von getesteten Code nicht möglich.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Wenn Sie SSMA Tester verwenden möchten, installieren Sie SSMA Sybase Erweiterung Pack mit der **installieren Tester Datenbank** aktiviert.  
  
Überprüfen Sie außerdem Folgendes:  
  
-   Sybase OLE DB-Anbieter auf dem Computer installiert ist, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird.  
  
-   Common Language Runtime (CLR)-Integration aktiviert wurde, auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbankmoduls.  
  
Beachten Sie, dass die aktuelle Version von SSMA Tester die parallele Ausführung von verschiedenen Benutzern auf demselben Server Quelle oder Ziel nicht unterstützt.  
  
## <a name="getting-started"></a>Erste Schritte  
[Erstellen von Testfällen &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-test-cases-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA-Komponenten in SQLServer &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Projekteinstellungen &#40;Konvertierung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)  
  
