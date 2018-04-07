---
title: Migrieren von Sybase ASE Daten in SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab42e495eb4e76b6e9d7b6a2cca3d031eed12448
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Migrieren von Sybase ASE-Daten in SQLServer - Azure SQL-Datenbank (SybaseToSQL)
Nachdem Sie die Datenbankobjekte Sybase Adaptive Server Enterprise (ASE) in erfolgreich geladen wurde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, können Sie Daten aus ASE zum Migrieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
> [!IMPORTANT]  
> Wenn das Modul verwendeten Server Side Migration Datenmodul ist, müssen klicken Sie dann vor dem Migrieren von Daten, Sie installieren die SSMA für Sybase ASE Erweiterung Pack und die Sybase ASE-Anbieter auf dem Computer mit SSMA. Der SQL Server-Agent-Dienst muss außerdem ausgeführt werden. Weitere Informationen zur Installation der Erweiterung Packs finden Sie unter [SSMA-Komponenten installieren, auf SQL Server (SybaseToSQL)](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>Einstellungsoptionen für die Migration  
Vor dem Migrieren von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, überprüfen Sie die Migrationsoptionen Projekt in der **Projekteinstellungen** (Dialogfeld).  
  
-   Mithilfe dieses Dialogfelds können Sie Optionen wie z. B. Migration Batchgröße Tabellensperre, einschränkungsüberprüfung, Behandlung von null-Werten und Behandlung von Identity-Werten festlegen. Weitere Informationen zu den Projekteinstellungen für die Migration, finden Sie unter [Projekteinstellungen (Migration) (Sybase)](http://msdn.microsoft.com/en-us/82f8857f-7ab1-4738-ab6e-b1e95ea94924).  
  
    Weitere Informationen zu **erweiterte Daten Migrationseinstellungen**, finden Sie unter [Einstellungen für die Migration von Daten](http://msdn.microsoft.com/en-us/94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d)  
  
-   Die **Migrationsmodul** in der **Projekteinstellungen** Dialogfeld ermöglicht es dem Benutzer zum Ausführen des Migrationsprozesses mithilfe von zwei Typen von Data Migration-Datenbankmodulen, begrenzt.:  
  
    1.  Client-Seite-Migration Datenmodul  
  
    2.  Server-Seite-Migration Datenmodul  
  
**Client-Side-Datenmigration:**  
  
-   Wählen Sie die Option, um die Datenmigration auf der Clientseite zu initiieren, **Client Side Migration Datenmodul** in der **Projekteinstellungen** (Dialogfeld).  
  
-   In **Projekteinstellungen**, **Client Side Migration Datenmodul** Option standardmäßig festgelegt ist.  
  
    > [!NOTE]  
    > Das Client-Side-Datenmodul Migration befindet sich in der SSMA-Anwendung und ist daher nicht die Verfügbarkeit der Erweiterung Pack abhängig.  
  
**Datenmigration für Server-Seite:**  
  
-   Während der Datenmigration für Server-Seite befindet sich das Modul in der Zieldatenbank ein. Er wird über die Erweiterung Pack installiert. Weitere Informationen zum Installieren der Erweiterung Pack finden Sie unter [SSMA-Komponenten installieren, auf SQL Server (SybaseToSQL)](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   Wählen Sie zur Migration auf dem Server zu initiieren, die **Server Side Migration Datenmodul** option die **Projekteinstellungen** Dialogfeld.  
  
> [!NOTE]  
> Wenn Azure SQL-Datenbank verwendet wird, als die Zieldatenbank nur **Datenmigration für Client-Side** ist zulässig, und Server Seite Daten-Migration wird nicht unterstützt.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>Migrieren von Daten in SQLServer oder Azure SQL-Datenbank  
Migrieren von Daten eines Massenladevorgangs, die Zeilen mit Daten aus den Tabellen ASE in SQL Server-Tabellen in Transaktionen verschiebt. Die Anzahl der Zeilen, die in SQL Server oder Azure SQL-Datenbank geladen werden, in der jeweiligen Transaktion ist in den projekteinstellungen konfiguriert.  
  
Zum Anzeigen der Migration Nachrichten sicher, dass im Ausgabebereich angezeigt wird. Wählen Sie andernfalls **Ausgabe** aus der **Ansicht** Menü.  
  
**Zum Migrieren von Daten**  
  
1.  Überprüfen Sie Folgendes:  
  
    -   Die ASE-Anbieter sind auf dem Computer installiert, die SSMA ausgeführt wird.  
  
    -   Sie haben die konvertierten Objekte mit der Zieldatenbank (SQL Server oder Azure SQL-Datenbank) synchronisiert.  
  
2.  Wählen Sie die Objekte, die Daten enthalten, die Sie migrieren möchten, im Sybase-Metadaten-Explorer:  
  
    -   Um Daten für alle Schemas migrieren möchten, aktivieren Sie das Kontrollkästchen neben **Schemas**.  
  
    -   Zum Migrieren von Daten, oder lassen einzelne Tabellen, zuerst das Schema, erweitern Sie dann **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
3.  Zum Migrieren von Daten auftreten, zwei Fällen:  
  
    **Client-Side-Datenmigration:**  
  
    Zum Ausführen von **Datenmigration für Client-Side**, wählen die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
    **Datenmigration für Server-Seite:**  
  
    -   Bevor Sie die Datenmigration für Server-Seite ausführen, stellen Sie Folgendes sicher:  
  
        1.  SSMA für Sybase Erweiterung Pack ist für die Instanz von SQL Server installiert.  
  
        2.  Der SQL Server-Agent-Dienst wird auf der Instanz von SQL Server ausgeführt.  
  
    -   Zum Ausführen von **Server Side Datenmigration**, wählen die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
4.  Mit der rechten Maustaste **Schemas** Sybase-Metadaten-Explorer, und klicken Sie auf **Migrieren von Daten**. Sie können auch Datenmigration für einzelne Objekte oder Kategorien von Objekten: mit der rechten Maustaste das Objekt oder der übergeordnete Ordner, und wählen Sie die **Migrieren von Daten** Option.  
  
    > [!NOTE]  
    > Wenn SSMA für Sybase Erweiterung Pack nicht auf die Instanz von SQL Server installiert ist und **Server Side Migration Datenmodul** ausgewählt ist, wird bei der Migration der das in die Zieldatenbank an, der folgende Fehler aufgetreten ist: "Datenmigration SSMA-Komponenten wurden nicht gefunden für SQL Server, serverseitige Datenmigration ist nicht möglich. Überprüfen Sie, ob die Erweiterung Pack ordnungsgemäß installiert ist ". Klicken Sie auf **"Abbrechen"** die Datenmigration beendet.  
  
5.  In der **Herstellen einer Verbindung mit der Sybase ASE** (Dialogfeld), geben Sie die Anmeldeinformationen der Verbindung, und klicken Sie dann auf **verbinden**. Weitere Informationen zum Verbinden mit Sybase ASE finden Sie unter [Herstellen einer Verbindung mit der Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    Wenn die Zieldatenbank, SQL Server befindet, und geben Sie dann die Anmeldeinformationen in der **Herstellen einer Verbindung mit SQL Server** (Dialogfeld), und klicken Sie auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit SQL Server finden Sie unter [Herstellen einer Verbindung mit SQL-Server(SybaseToSQL)](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    Wenn die Zieldatenbank Azure SQL-Datenbank ist, und geben Sie dann die Anmeldeinformationen in der **Herstellen einer Verbindung mit Azure SQL-Datenbank** (Dialogfeld), und klicken Sie auf **verbinden**. Weitere Informationen zum Verbinden mit Azure SQL-Datenbank finden Sie unter [Herstellen einer Verbindung mit Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    Nachrichten werden angezeigt, der **Ausgabe** Bereich. Wenn die Migration abgeschlossen ist, ist die **Migrationsbericht Daten** angezeigt wird. Wenn keine Daten migriert haben, klicken Sie auf die Zeile, die Fehler enthält, und klicken Sie dann auf **Details**. Wenn Sie mit dem Bericht fertig sind, klicken Sie auf **schließen**. Weitere Informationen zu Daten Migrationsbericht, finden Sie unter [Migrationsbericht für Daten (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Wenn SQL Express-Edition als die Zieldatenbank verwendet wird, wird nur Client Side Datenmigration ist zulässig, und Server Seite Daten-Migration wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
