---
title: Migrieren von DB2-Daten in SQLServer (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45039e39cc04c75f0d2f92de8cf3ad95b55d8e0a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>Migrieren von DB2-Daten in SQLServer (DB2ToSQL)
Nachdem Sie die konvertierten Objekte mit erfolgreich synchronisiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Migrieren von Daten aus DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Wenn das Modul verwendeten Server Side Migration Datenmodul ist, klicken Sie dann müssen vor dem Migrieren von Daten, Sie installieren die SSMA für DB2 Erweiterung Pack und die DB2-Anbieter auf dem Computer mit SSMA. Der SQL Server-Agent-Dienst muss außerdem ausgeführt werden. Weitere Informationen zur Installation der Erweiterung Packs finden Sie unter [SSMA-Komponenten installieren, auf SQL Server](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>Einstellungsoptionen für die Migration  
Vor dem Migrieren von Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], überprüfen Sie die Migrationsoptionen Projekt in der **Projekteinstellungen** (Dialogfeld).  
  
-   Mithilfe dieses Dialogfelds können Sie Optionen wie z. B. die Batchgröße für die Migration, Tabellensperre einschränkungsüberprüfung, Behandlung von null-Werten und Behandlung von Identity-Werten festlegen. Weitere Informationen zu den Projekteinstellungen für die Migration, finden Sie unter [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae).  
  
-   Die **Migrationsmodul** in der **Projekteinstellungen** Dialogfeld ermöglicht dem Benutzer, die Migration mithilfe von zwei Arten von Daten Migration Module auszuführen:  
  
    1.  Client-Seite-Migration Datenmodul  
  
    2.  Server-Seite-Migration Datenmodul  
  
**Client-Side-Datenmigration:**  
  
-   Um die Datenmigration auf der Clientseite zu initiieren, wählen Sie die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
-   In **Projekteinstellungen**, **Client Side Migration Datenmodul** Option festgelegt ist.  
  
    > [!NOTE]  
    > Die **clientseitige Migration Datenmodul** befindet sich in der SSMA-Anwendung und ist daher nicht abhängig von der Verfügbarkeit des Packs Erweiterung.  
  
**Datenmigration für Server-Seite:**  
  
-   Während der Datenmigration von Server-Seite befindet sich das Modul in der Zieldatenbank ein. Er wird über die Erweiterung Pack installiert. Weitere Informationen zum Installieren der Erweiterung Pack finden Sie unter [SSMA-Komponenten installieren, auf SQL Server](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   Um Migration auf dem Server zu initiieren, wählen Sie die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
## <a name="migrating-data-to-sql-server"></a>Migrieren von Daten mit SQLServer  
Migrieren von Daten eines Massenladevorgangs, die Zeilen mit Daten aus DB2-Tabellen in Verschiebt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Tabellen in Transaktionen. Anzahl der Zeilen in den geladenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in jeder Transaktion ist in den projekteinstellungen konfiguriert.  
  
Um die Migration der Meldungsansicht sicher, dass im Ausgabebereich angezeigt wird. Andernfalls, aus der **Ansicht** klicken Sie im Menü **Ausgabe**.  
  
**Zum Migrieren von Daten**  
  
1.  Überprüfen Sie Folgendes:  
  
    -   Die DB2-Anbieter sind auf dem Computer installiert, die SSMA ausgeführt wird.  
  
    -   Sie haben die konvertierten Objekte mit synchronisiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
2.  Wählen Sie die Objekte, die Daten enthalten, die Sie migrieren möchten, im DB2-Metadaten-Explorer:  
  
    -   Um Daten für alle Schemas migrieren möchten, aktivieren Sie das Kontrollkästchen neben **Schemas**.  
  
    -   Zum Migrieren von Daten, oder lassen einzelne Tabellen, zuerst das Schema, erweitern Sie dann **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
3.  Zum Migrieren von Daten auftreten, zwei Fällen:  
  
    **Client-Side-Datenmigration:**  
  
    -   Zum Ausführen von **Datenmigration für Client-Side**, wählen die **Client Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
    **Datenmigration für Server-Seite:**  
  
    -   Bevor Sie die Datenmigration auf dem Server durchführen, stellen Sie Folgendes sicher:  
  
        1.  SSMA für DB2 Erweiterung Pack installiert ist, auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
        2.  Der SQL Server-Agent-Dienst wird auf der Instanz von SQL Server ausgeführt.  
  
    -   Zum Ausführen von **Server Side Datenmigration**, wählen die **Server Side Migration Datenmodul** -Option in der **Projekteinstellungen** (Dialogfeld).  
  
4.  Mit der rechten Maustaste **Schemas** in DB2-Metadaten-Explorer, und klicken Sie dann auf **Migrieren von Daten**. Sie können auch Datenmigration für einzelne Objekte oder Kategorien von Objekten: mit der rechten Maustaste das Objekt oder die übergeordneten Ordner; Wählen Sie die **Migrieren von Daten** Option.  
  
    > [!NOTE]  
    > Wenn SSMA für DB2 Erweiterung Pack nicht auf der Instanz installiert ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und wenn **Server Side Migration Datenmodul** ausgewählt ist, wird bei der Migration der das in die Zieldatenbank an, der folgende Fehler aufgetreten ist: "Datenmigration SSMA-Komponenten wurden nicht gefunden für SQL Server, serverseitige Datenmigration ist nicht möglich. Überprüfen Sie, ob die Erweiterung Pack ordnungsgemäß installiert ist ". Klicken Sie auf **"Abbrechen"** die Datenmigration beendet.  
  
5.  In der **Herstellen einer Verbindung mit DB2** (Dialogfeld), geben Sie die Anmeldeinformationen der Verbindung, und klicken Sie dann auf **verbinden**. Weitere Informationen zum Verbinden mit DB2 finden Sie unter [Herstellen einer Verbindung mit DB2-Datenbank &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    Zum Herstellen einer Verbindung in die Zieldatenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], geben Sie die Anmeldeinformationen in der **Herstellen einer Verbindung mit SQL Server** (Dialogfeld), und klicken Sie auf **verbinden**. Weitere Informationen zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Herstellen einer Verbindung mit SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    Nachrichten werden angezeigt, der **Ausgabe** Bereich. Wenn die Migration abgeschlossen ist, ist die **Migrationsbericht Daten** angezeigt wird. Wenn keine Daten migriert haben, klicken Sie auf die Zeile, die Fehler enthält, und klicken Sie dann auf **Details**. Wenn Sie mit dem Bericht fertig sind, klicken Sie auf **schließen**. Weitere Informationen zu Daten Migrationsbericht, finden Sie unter [Migrationsbericht für Daten (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> Wenn SQL Express-Edition als die Zieldatenbank verwendet wird, wird nur Client Side Datenmigration ist zulässig, und Server Seite Daten-Migration wird nicht unterstützt.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Daten in SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
