---
title: Herstellen einer Verbindung mit MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
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
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
caps.latest.revision: 13
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 888989c8dbbf7715695f0203e80dcdd768a44a2e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connecting-to-mysql-mysqltosql"></a>Herstellen einer Verbindung mit MySQL (MySQLToSQL)
Um MySQL-Datenbanken zu SQL Server oder SQL Azure zu migrieren, müssen Sie mit der MySQL-Datenbank verbinden, die Sie migrieren möchten. Wenn Sie eine Verbindung herstellen, SSMA Ruft Metadaten über alle MySQL-Schemas ab, und anschließend in der MySQL-Metadaten-Explorer-Bereich angezeigt. SSMA speichert Informationen über den Datenbankserver, aber die Kennwörter werden nicht gespeichert.  
  
Die Verbindung mit der Datenbank bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit der Datenbank verwendet werden soll.  
  
Metadaten für die MySQL-Datenbank wird nicht automatisch aktualisiert. Stattdessen, wenn Sie die Metadaten in MySQL-Metadaten-Explorer aktualisieren möchten, müssen Sie manuell es aktualisieren. Weitere Informationen finden Sie im Abschnitt "Aktualisieren von MySQL-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-mysql-permissions"></a>MySQL erforderliche Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung zur MySQL-Datenbank muss zumindest **verbinden** Berechtigungen. Dies ermöglicht der SSMA zum Abrufen von Metadaten aus Schemas im Besitz des Benutzers eine Verbindung herstellt. Zum Abrufen von Metadaten für Objekte in anderen Schemas, und klicken Sie dann konvertiert die Objekte in diesen Schemas, muss das Konto über die folgenden Berechtigungen verfügen:  
  
-   "SHOW" Berechtigungen für Datenbankobjekte  
  
-   "SELECT-Berechtigung auf"Information_schema"  
  
-   "SELECT-Berechtigung auf Mysql (für UDFs)  
  
## <a name="establishing-a-connection-to-mysql"></a>Herstellen einer Verbindung mit MySQL  
Wenn Sie eine Verbindung mit einer Datenbank herstellen, SSMA liest die Datenbankmetadaten und fügt dann diese Metadaten in die Projektdatei. Diese Metadaten werden von SSMA verwendet, wenn Objekte in SQL Server oder SQL Azure-Syntax konvertiert werden, und wenn sie Daten in SQL Server oder SQL Azure migriert werden. Sie können diese Metadaten im Bereich MySQL-Metadaten-Explorer durchsuchen und überprüfen Sie die Eigenschaften der einzelnen Datenbankobjekte.  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung herstellen, stellen Sie sicher, dass der Datenbankserver ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Für die Verbindung mit MySQL**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit MySQL** (diese Option wird nach der Erstellung des Projekts aktiviert werden).  
  
    Wenn Sie zuvor mit MySQL verbunden sind, wird der Befehlsname sein **eine erneute Verbindung mit MySQL**.  
  
2.  In der **Anbieter** wählen MySQL 5.1 Odbcdriver (vertrauenswürdigen). Es ist der Standardanbieter in den Modus "standard".  
  
3.  In der **Modus** wählen Sie im **Modus "Standard"**. Es handelt sich hierbei um den Standardmodus.  
  
    Verwenden Sie Modus "standard", um den Servernamen und den Port angeben.  
  
4.  In **Modus "Standard"**, geben Sie die folgenden Werte:  
  
    1.  In der **Servernamen** Geben Sie den Namen der MySQL-Server. In der **Serverport** Geben Sie die Portnummer für die 3306 sein. Es ist der Standardport.  
  
    2.  In der **Benutzername** Geben Sie eine MySQL-Konto, das die erforderlichen Berechtigungen verfügt.  
  
    3.  In der **Kennwort** Geben Sie das Kennwort für den angegebenen Benutzernamen ein.  
  
5.  **SSL:** , wenn Sie eine sichere Verbindung mit MySQL möchten, stellen Sie durch Überprüfung des Secure Socket Layer (SSL) verwenden die **SSL** Kontrollkästchen.  
  
6.  **So konfigurieren Sie** es bietet eine Option aus, um die Verbindung mit MySQL über Secure Socket Layer (SSL) konfigurieren.  
  
    > [!NOTE]  
    > So aktivieren Sie **konfigurieren**, SSL muss festgelegt werden, um **"true"**.  
  
    Auf der Schaltfläche "Konfigurieren", ein Dialogfeld wird angezeigt. Definiert [Privacy Enhanced Mail-Zertifikate (PEM)], Verschlüsselung zu verwenden, beim Herstellen einer Verbindung mit MySQL-Datenbank, Pfad, um die folgenden drei Dateien in das Dialogfeld vorhanden sein muss:  
  
    -   **SSL-Zertifizierungsstelle:** gibt den Pfad zu einer Datei mit einer Liste von vertrauenswürdigen Zertifizierungsstellen SSL an.  
  
    -   **SSL-Zertifikat:** gibt den Namen des SSL-Zertifikatdatei zum Herstellen einer sicheren Verbindung verwendet werden soll.  
  
    -   **SSL-Schlüssel:** gibt den Namen der SSL-Schlüsseldatei zum Herstellen einer sicheren Verbindung verwendet werden soll.  
  
    > [!NOTE]  
    > -   Die **OK** Schaltfläche ist aktiviert, wenn die erforderliche Informationen angegeben wurden. Wenn die Dateipfade ungültig sind, bleiben die Schaltfläche "OK" wird deaktiviert.  
    > -   Die **"Abbrechen"** Schaltfläche wird das Dialogfeld geschlossen und **deaktiviert** die Option "SSL" aus der Verbindung Hauptformular.  
  
7.  Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>Erneutes Herstellen einer Verbindung mit MySQL  
Die Verbindung mit dem Datenbankserver bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit der Datenbank verwendet werden soll. Sie können offline arbeiten, bis Sie die Metadaten zu aktualisieren, laden Datenbankobjekte in SQL Server oder SQL Azure und Daten migrieren möchten.  
  
## <a name="refreshing-mysql-metadata"></a>Aktualisieren von MySQL-Metadaten  
Metadaten für die MySQL-Datenbank wird nicht automatisch aktualisiert. Die Metadaten in MySQL-Metadaten-Explorer wird eine Momentaufnahme der Metadaten, wenn Sie zuerst eine Verbindung hergestellt oder der letzten, dass Sie manuell die Metadaten aktualisiert werden. Sie können die Metadaten für alle Schemas, ein einzelnes Schema oder einzelne Datenbankobjekte manuell aktualisieren.  
  
**Aktualisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit der Datenbank verbunden sind.  
  
2.  Wählen Sie in MySQL-Metadaten-Explorer das Kontrollkästchen neben jedem Schema oder Datenbank-Objekt, das Sie aktualisieren möchten.  
  
3.  Mit der rechten Maustaste **Schemas**, einzelnes Schema oder eine Datenbank-Objekt, und wählen Sie dann **aus der Datenbank aktualisieren**.  
  
    SSMA wird angezeigt, wenn Sie nicht über eine aktive Verbindung verfügen, die **Herstellen einer Verbindung mit MySQL** Dialogfeld, sodass Sie eine Verbindung herstellen können.  
  
4.  Geben Sie die zu aktualisierenden Objekte in die Aktualisierung über Datenbank-Dialogfeld.  
  
    -   Um ein Objekt zu aktualisieren, klicken Sie auf die **Active** Feld neben dem Objekt, bis ein Pfeil angezeigt wird.  
  
    -   Um zu verhindern, dass ein Objekt aktualisiert wird, klicken Sie auf die **Active** Feld neben solange ein **X** angezeigt wird.  
  
    -   Klicken Sie zum Aktualisieren oder Ablehnen einer Kategorie von Objekten, auf die **Active** Feld neben der Kategorieordner.  
  
    -   Um die Definitionen der Farbcode anzuzeigen, klicken Sie auf die **Legende** Schaltfläche.  
  
5.  Klicken Sie auf **OK**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [Herstellen einer Verbindung mit SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
