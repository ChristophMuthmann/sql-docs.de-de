---
title: Migrieren von Oracle-Daten in SQLServer (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: e88983497744eef31efd5aa7e27645da7c62b468
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Migrieren von Oracle-Daten in SQLServer (OracleToSQL)
Nachdem Sie die konvertierten Objekte mit erfolgreich synchronisiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Migrieren von Daten aus Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Wenn das Modul verwendeten Server Side Migration Datenmodul ist, klicken Sie dann müssen vor dem Migrieren von Daten, Sie installieren SSMA für die Erweiterung Pack Oracle und Oracle-Anbieter auf dem Computer mit SSMA. Der SQL Server-Agent-Dienst muss außerdem ausgeführt werden. Weitere Informationen zur Installation der Erweiterung Packs finden Sie unter [Installieren von Server-Komponenten (OracleToSQL)](http://msdn.microsoft.com/en-us/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>Einstellungsoptionen für die Migration  
Vor dem Migrieren von Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], überprüfen Sie die Migrationsoptionen Projekt in der **Projekteinstellungen** (Dialogfeld).  
  
-   Mithilfe dieses Dialogfelds können Sie Optionen wie z. B. die Batchgröße für die Migration, Tabellensperre einschränkungsüberprüfung, Behandlung von null-Werten und Behandlung von Identity-Werten festlegen. Weitere Informationen zu den Projekteinstellungen für die Migration, finden Sie unter [Projekteinstellungen (Migration) (OracleToSQL)](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60).  
  
-   Die **Migrationsmodul** in der **Projekteinstellungen** Dialogfeld ermöglicht dem Benutzer, die Migration mithilfe von zwei Arten von Daten Migration Module auszuführen:  
  
    1.  Client-Seite-Migration Datenmodul  
  
    2.  Server-Seite-Migration Datenmodul  
  
**Client-Side-Datenmigration:**  
  
-   Um die Datenmigration auf der Clientseite zu initiieren, wählen Sie die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
-   In **Projekteinstellungen**, **Client Side Migration Datenmodul** Option festgelegt ist.  
  
    > [!NOTE]  
    > Die **clientseitige Migration Datenmodul** befindet sich in der SSMA-Anwendung und ist daher nicht abhängig von der Verfügbarkeit des Packs Erweiterung.  
  
**Datenmigration für Server-Seite:**  
  
-   Während der Datenmigration von Server-Seite befindet sich das Modul in der Zieldatenbank ein. Er wird über die Erweiterung Pack installiert. Weitere Informationen zum Installieren der Erweiterung Pack finden Sie unter [Server-Komponenten installieren, auf SQL Server](http://msdn.microsoft.com/en-us/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
-   Um Migration auf dem Server zu initiieren, wählen Sie die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
## <a name="migrating-data-to-sql-server"></a>Migrieren von Daten mit SQLServer  
Migrieren von Daten eines Massenladevorgangs, die Zeilen mit Daten aus Oracle-Tabellen in Verschiebt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Tabellen in Transaktionen. Anzahl der Zeilen in den geladenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in jeder Transaktion ist in den projekteinstellungen konfiguriert.  
  
Um die Migration der Meldungsansicht sicher, dass im Ausgabebereich angezeigt wird. Andernfalls, aus der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Zum Migrieren von Daten**  
  
1.  Überprüfen Sie Folgendes:  
  
    -   Oracle-Anbieter sind auf dem Computer installiert, die SSMA ausgeführt wird.  
  
    -   Sie haben die konvertierten Objekte mit synchronisiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
2.  Wählen Sie in Oracle-Metadaten-Explorer die Objekte, die die Daten enthalten, die Sie migrieren möchten:  
  
    -   Um Daten für alle Schemas migrieren möchten, aktivieren Sie das Kontrollkästchen neben **Schemas**.  
  
    -   Zum Migrieren von Daten, oder lassen einzelne Tabellen, zuerst das Schema, erweitern Sie dann **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
3.  Zum Migrieren von Daten auftreten, zwei Fällen:  
  
    **Client-Side-Datenmigration:**  
  
    -   Zum Ausführen von **Datenmigration für Client-Side**, wählen die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
    **Datenmigration für Server-Seite:**  
  
    -   Bevor Sie die Datenmigration auf dem Server durchführen, stellen Sie Folgendes sicher:  
  
        1.  SSMA für die Erweiterung Pack Oracle installiert ist, auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
        2.  Der SQL Server-Agent-Dienst wird auf der Instanz von SQL Server ausgeführt.  
  
    -   Zum Ausführen von **Server Side Datenmigration**, wählen die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
4.  Mit der rechten Maustaste **Schemas** in Oracle-Metadaten-Explorer, und klicken Sie dann auf **Migrieren von Daten**. Sie können auch Datenmigration für einzelne Objekte oder Kategorien von Objekten: mit der rechten Maustaste das Objekt oder die übergeordneten Ordner; Wählen Sie die **Migrieren von Daten** Option.  
  
    > [!NOTE]  
    > Wenn SSMA für die Erweiterung Pack Oracle nicht auf der Instanz installiert ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und wenn **Server Side Migration Datenmodul** ausgewählt ist, wird bei der Migration der das in die Zieldatenbank an, der folgende Fehler aufgetreten ist: "Datenmigration SSMA-Komponenten wurden nicht gefunden für SQL Server, serverseitige Datenmigration ist nicht möglich. Überprüfen Sie, ob die Erweiterung Pack ordnungsgemäß installiert ist ". Klicken Sie auf **"Abbrechen"** die Datenmigration beendet.  
  
5.  In der **Connect to Oracle** (Dialogfeld), geben Sie die Anmeldeinformationen der Verbindung, und klicken Sie dann auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit Oracle finden Sie unter [auf Oracle Verbinden &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    Zum Herstellen einer Verbindung in die Zieldatenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], geben Sie die Anmeldeinformationen in der **Herstellen einer Verbindung mit SQL Server** (Dialogfeld), und klicken Sie auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Herstellen einer Verbindung mit SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    Nachrichten werden angezeigt, der **Ausgabe** Bereich. Wenn die Migration abgeschlossen ist, ist die **Migrationsbericht Daten** angezeigt wird. Wenn keine Daten migriert haben, klicken Sie auf die Zeile, die Fehler enthält, und klicken Sie dann auf **Details**. Wenn Sie mit dem Bericht fertig sind, klicken Sie auf **schließen**. Weitere Informationen zu Daten Migrationsbericht, finden Sie unter [Migrationsbericht für Daten (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Wenn SQL Express-Edition als die Zieldatenbank verwendet wird, wird nur Client Side Datenmigration ist zulässig, und Server Seite Daten-Migration wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
