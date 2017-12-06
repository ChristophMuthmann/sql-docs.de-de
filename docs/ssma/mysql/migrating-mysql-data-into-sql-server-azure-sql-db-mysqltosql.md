---
title: Migrieren von MySQL-Daten in SQLServer - Azure SQL-Datenbank (MySQLToSQL) | Microsoft Docs
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
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
caps.latest.revision: "24"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d50bf548e5e9d64aef5aa306937b03a9c27c669
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>Migrieren von MySQL-Daten in SQLServer - Azure SQL-Datenbank (MySQLToSQL)
Nachdem Sie die konvertierten Objekte mit erfolgreich synchronisiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure können Sie Daten aus MySQL zu migrieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
> [!IMPORTANT]  
> Ist das Modul verwendeten Server Side Migration Datenmodul, klicken Sie dann vor dem Migrieren von Daten, müssen Sie die SSMA für die MySQL-Anbieter auf dem Computer mit SSMA und MySQL-Erweiterung Packs installieren. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst muss außerdem ausgeführt werden. Weitere Informationen zur Installation der Erweiterung Packs finden Sie unter [SSMA-Komponenten installieren, auf SQL Server (MySQL zu SQL)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>Einstellungsoptionen für die Migration  
Vor dem Migrieren von Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, überprüfen Sie die Migrationsoptionen Projekt in der **Projekteinstellungen** (Dialogfeld).  
  
-   Mithilfe dieses Dialogfelds können Sie Optionen wie z. B. Migration Batchgröße Tabellensperre, einschränkungsüberprüfung, Behandlung von null-Werten und Identity-Wert-Behandlung festlegen. Weitere Informationen zu den Projekteinstellungen für die Migration, finden Sie unter [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9).  
  
    Weitere Informationen zu **erweiterte Daten Migrationseinstellungen**, finden Sie unter [Einstellungen für die Migration von Daten](http://msdn.microsoft.com/en-us/9c396df4-5676-4f32-9c57-70d4f15f9b7a)  
  
-   Die **Migrationsmodul** in der **Projekteinstellungen** Dialogfeld ermöglicht dem Benutzer, die Migration mithilfe von zwei Arten von Daten Migration Module auszuführen:  
  
    1.  Client-Seite-Migration Datenmodul  
  
    2.  Server-Seite-Migration Datenmodul  
  
**Client-Side-Datenmigration:**  
  
-   Um die Datenmigration auf der Clientseite zu initiieren, wählen Sie die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
-   In **Projekteinstellungen**, **Client Side Migration Datenmodul** Option festgelegt ist.  
  
    > [!NOTE]  
    > Die **clientseitige Migration Datenmodul** befindet sich in der SSMA-Anwendung und ist daher nicht abhängig von der Verfügbarkeit des Packs Erweiterung.  
  
**Datenmigration für Server-Seite:**  
  
-   Während der Datenmigration von Server-Seite befindet sich das Modul in der Zieldatenbank ein. Er wird über die Erweiterung Pack installiert. Weitere Informationen zum Installieren der Erweiterung Pack finden Sie unter [SSMA-Komponenten installieren, auf SQL Server (MySQL zu SQL)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   Um Migration auf dem Server zu initiieren, wählen Sie die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
> [!IMPORTANT]  
> **Client-Side-Datenmigration** Option ist nur für SQL Azure verfügbar.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>Migrieren von Daten in SQLServer oder SQL Azure  
Migrieren von Daten eines Massenladevorgangs, die Zeilen mit Daten aus MySQL-Tabellen in Verschiebt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen in Transaktionen. Anzahl der Zeilen in den geladenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in jeder Transaktion ist in den projekteinstellungen konfiguriert.  
  
Um die Migration der Meldungsansicht sicher, dass im Ausgabebereich angezeigt wird. Andernfalls, aus der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Zum Migrieren von Daten**  
  
1.  Überprüfen Sie Folgendes:  
  
    -   Die MySQL-Anbieter sind auf dem Computer installiert, die SSMA ausgeführt wird.  
  
    -   Sie haben die konvertierten Objekte synchronisiert, mit der Zieldatenbank (SQL Server / SQL Azure).  
  
2.  Wählen Sie im MySQL-Metadaten-Explorer die Objekte, die die Daten enthalten, die Sie migrieren möchten:  
  
    -   Um Daten für alle Schemas migrieren möchten, aktivieren Sie das Kontrollkästchen neben **Schemas**.  
  
    -   Zum Migrieren von Daten, oder lassen einzelne Tabellen, zuerst das Schema, erweitern Sie dann **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
3.  Zum Migrieren von Daten auftreten, zwei Fällen:  
  
    **Client-Side-Datenmigration:**  
  
    -   Zum Ausführen von **Datenmigration für Client-Side**, wählen die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
    **Datenmigration für Server-Seite:**  
  
    -   Bevor Sie die Datenmigration auf dem Server durchführen, stellen Sie Folgendes sicher:  
  
        1.  SSMA für MySQL-Erweiterung Pack ist für die Instanz von SQL Server installiert.  
  
        2.  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] für die Instanz von SQL Server-Agent-Dienst ausgeführt wird  
  
    -   Zum Ausführen von **Server Side Datenmigration**, wählen die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
4.  Mit der rechten Maustaste **Schemas** in MySQL-Metadaten-Explorer, und klicken Sie dann auf **Migrieren von Daten**. Sie können auch Datenmigration für einzelne Objekte oder Kategorien von Objekten: mit der rechten Maustaste das Objekt oder die übergeordneten Ordner; Wählen Sie die **Migrieren von Daten** Option.  
  
    > [!NOTE]  
    > Wenn die SSMA für die MySQL-Erweiterung Pack nicht auf die Instanz von SQL Server installiert ist und **Server Side Migration Datenmodul** ausgewählt ist, wird bei der Migration der das in die Zieldatenbank an, der folgende Fehler aufgetreten ist: "Datenmigration SSMA-Komponenten wurden nicht gefunden für SQL Server, serverseitige Datenmigration ist nicht möglich. Überprüfen Sie, ob die Erweiterung Pack ordnungsgemäß installiert ist ". Klicken Sie auf **"Abbrechen"** die Datenmigration beendet.  
  
5.  In der **Herstellen einer Verbindung mit MySQL** (Dialogfeld), geben Sie die Anmeldeinformationen der Verbindung, und klicken Sie dann auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit MySQL finden Sie unter [Herstellen einer Verbindung mit MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    Wenn die Zieldatenbank, SQL Server befindet, und geben Sie dann die Anmeldeinformationen in der **Herstellen einer Verbindung mit SQL Server** (Dialogfeld), und klicken Sie auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit SQL Server finden Sie unter [Herstellen einer Verbindung mit SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Wenn die Zieldatenbank SQL Azure ist, und geben Sie dann die Anmeldeinformationen in der **Herstellen einer Verbindung mit SQL Azure** (Dialogfeld), und klicken Sie auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit SQL Azure finden Sie unter [Herstellen einer Verbindung mit Azure SQL-Datenbank &#40; MySQLToSQL &#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    Nachrichten werden angezeigt, der **Ausgabe** Bereich. Wenn die Migration abgeschlossen ist, ist die **Migrationsbericht Daten** angezeigt wird. Wenn keine Daten migriert haben, klicken Sie auf die Zeile, die Fehler enthält, und klicken Sie dann auf **Details**. Wenn Sie mit dem Bericht fertig sind, klicken Sie auf **schließen**. Weitere Informationen zu Daten Migrationsbericht, finden Sie unter [Migrationsbericht für Daten (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Wenn SQL Express-Edition als die Zieldatenbank verwendet wird, wird nur Client Side Datenmigration ist zulässig, und Server Seite Daten-Migration wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
