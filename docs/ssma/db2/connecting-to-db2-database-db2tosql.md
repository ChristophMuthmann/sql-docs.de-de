---
title: Herstellen einer Verbindung mit DB2-Datenbank (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5eb5801d-f0c3-4127-97c0-0b1ef49f4844
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3c7d7f8162968d579f1e3e1346fb2498ebf941cb
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-db2-database-db2tosql"></a>Herstellen einer Verbindung mit DB2-Datenbank (DB2ToSQL)
Zum Migrieren von DB2-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie müssen die Verbindung mit der DB2-Datenbank, die Sie migrieren möchten. Wenn Sie eine Verbindung herstellen, SSMA Ruft Metadaten über alle DB2-Schemas ab, und anschließend in der DB2-Metadaten-Explorer-Bereich angezeigt. SSMA speichert Informationen über den Datenbankserver, aber die Kennwörter werden nicht gespeichert.  
  
Die Verbindung mit der Datenbank bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit der Datenbank verwendet werden soll.  
  
Metadaten zu den DB2-Datenbank wird nicht automatisch aktualisiert. Stattdessen, wenn Sie die Metadaten in DB2-Metadaten-Explorer aktualisieren möchten, müssen Sie manuell es aktualisieren. Weitere Informationen finden Sie im Abschnitt "Aktualisieren von DB2 Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-db2-permissions"></a>Erforderlichen DB2-Berechtigungen  
Benutzerautorisierung definiert die Liste der Befehle und Objekte, die für einen Benutzer verfügbar sind. Dadurch werden Benutzeraktionen Listensteuerelemente. Befinden sich in DB2 vordefinierte Gruppen von Berechtigungen für die Autorisierung, sowohl auf Instanzebene und auf der Ebene einer DB2-Datenbank. Dies ermöglicht der SSMA zum Abrufen von Metadaten aus Schemas im Besitz des Benutzers eine Verbindung herstellt. Zum Abrufen von Metadaten für Objekte in anderen Schemas, und klicken Sie dann konvertiert die Objekte in diesen Schemas, muss das Konto über die folgenden Berechtigungen verfügen:  
  
-   Zugriff auf die Schemas für die Migration von Schema ist normalerweise Public erteilt, es sei denn, das beschränken-Schlüsselwort in CREATE verwendet wurde  
  
-   Datenzugriff für die Datenmigration erfordert DATAACCESS  
  
## <a name="establishing-a-connection-to-db2"></a>Herstellen einer Verbindung mit DB2  
Wenn Sie eine Verbindung mit einer Datenbank herstellen, SSMA liest die Datenbankmetadaten und fügt dann diese Metadaten in die Projektdatei. Diese Metadaten werden von SSMA verwendet, wenn Objekte konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und wenn sie Daten migriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können diese Metadaten im DB2-Metadaten-Explorer durchsuchen und überprüfen Sie die Eigenschaften der einzelnen Datenbankobjekte.  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung herstellen, stellen Sie sicher, dass der Datenbankserver ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit DB2**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit DB2**.  
  
    Wenn Sie zuvor mit DB2 verbunden, wird der Befehlsname sein **eine erneute Verbindung mit DB2**.  
  
2.  In der **Anbieter** Feld Sie sehen die **OLE DB-Anbieter** dort gilt zurzeit der einzige DB2 Client Access-Anbieter.  
  
3.  In der **Manager** Feld Wählen Sie entweder **Db2 für zOS erörtert**, oder **DB2 für LUW**  
  
4.  In der **Modus** wählen **Modus "Standard"**, oder **Zeichenfolge Verbindungsmodus**.  
  
    Verwenden Sie Modus "standard", um den Servernamen und den Port angeben. Verwenden Sie Namen Dienstmodus, um die DB2-Dienstname manuell anzugeben. Verwenden Sie Zeichenfolge Verbindungsmodus, um eine vollständige Verbindungszeichenfolge bereitzustellen.  
  
5.  Bei Auswahl des **Modus "Standard"**, geben Sie die folgenden Werte:  
  
    -   In der **Servernamen** Feld eingeben oder auswählen den Namen oder IP-Adresse des Datenbankservers.  
  
    -   Wenn der Datenbankserver nicht konfiguriert ist, um Verbindungen zuzulassen, auf die Standardeinstellung (1521) port verwenden, geben Sie die Portnummer für die DB2-Verbindungen in verwendeten die **Serverport** Feld.  
  
    -   In der **Serverport** Geben Sie die TCP/IP-Portnummer an.  
  
    -   In der **Anfangskatalog** Geben Sie den Datenbanknamen  
  
    -   In der **Benutzername** Geben Sie ein DB2-Konto, das die erforderlichen Berechtigungen verfügt.  
  
    -   In der **Kennwort** Geben Sie das Kennwort für den angegebenen Benutzernamen ein.  
  
6.  Bei Auswahl des **Zeichenfolge Verbindungsmodus**, geben Sie eine Verbindungszeichenfolge in der **Verbindungszeichenfolge** Feld.  
  
    Das folgende Beispiel zeigt eine OLE DB-Verbindungszeichenfolge:  
  
    `Provider=OraOLEDB.DB2;Data Source=MyDB2DB;User Id=myUsername;Password=myPassword;`  
  
    Das folgende Beispiel zeigt eine DB2-Client-Verbindungszeichenfolge, die die integrierte Sicherheit verwendet:  
  
    `Data Source=MyDB2DB;Integrated Security=yes;`  
  
    Weitere Informationen finden Sie unter [auf Oracle Verbinden &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-db2"></a>Erneutes Herstellen einer Verbindung mit DB2  
Die Verbindung mit dem Datenbankserver bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit der Datenbank verwendet werden soll. Sie können offline arbeiten, bis Sie verwenden möchten, aktualisieren Sie Metadaten an, und laden die Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Daten migrieren.  
  
## <a name="refreshing-db2-metadata"></a>Aktualisieren von DB2-Metadaten  
Metadaten zu den DB2-Datenbank wird nicht automatisch aktualisiert. Die Metadaten in DB2-Metadaten-Explorer wird eine Momentaufnahme der Metadaten, wenn Sie zuerst eine Verbindung hergestellt oder der letzten, dass Sie manuell die Metadaten aktualisiert werden. Sie können die Metadaten für alle Schemas, ein einzelnes Schema oder einzelne Datenbankobjekte manuell aktualisieren.  
  
**Aktualisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit der Datenbank verbunden sind.  
  
2.  Wählen Sie in DB2-Metadaten-Explorer das Kontrollkästchen neben jedem Schema oder Datenbank-Objekt, das Sie aktualisieren möchten.  
  
3.  Mit der rechten Maustaste **Schemas**, einzelnes Schema oder eine Datenbank-Objekt, und wählen Sie dann **aus der Datenbank aktualisieren**.  
  
    SSMA wird angezeigt, wenn Sie nicht über eine aktive Verbindung verfügen, die **Herstellen einer Verbindung mit DB2** Dialogfeld, sodass Sie eine Verbindung herstellen können.  
  
4.  Geben Sie die zu aktualisierenden Objekte in die Aktualisierung über Datenbank-Dialogfeld.  
  
    -   Um ein Objekt zu aktualisieren, klicken Sie auf die **Active** Feld neben dem Objekt, bis ein Pfeil angezeigt wird.  
  
    -   Um zu verhindern, dass ein Objekt aktualisiert wird, klicken Sie auf die **Active** Feld neben solange ein **X** angezeigt wird.  
  
    -   Klicken Sie zum Aktualisieren oder Ablehnen einer Kategorie von Objekten, auf die **Active** Feld neben der Kategorieordner.  
  
    Um die Definitionen der Farbcode anzuzeigen, klicken Sie auf die **Legende** Schaltfläche.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>Nächster Schritt  
  
-   Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Datenbanken zu SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

