---
title: Herstellen einer Verbindung mit SQLServer (DB2eToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
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
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 373e9e080f839a6c2ea66291118991488ac73c17
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connecting-to-sql-server-db2etosql"></a>Herstellen einer Verbindung mit SQLServer (DB2eToSQL)
Zum Migrieren von DB2-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014 oder Azure SQL-Datenbank müssen Sie mit keines dieser Zielinstanzen von verbinden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie eine Verbindung herstellen, erhält SSMA Metadaten zu allen Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und zeigt Sie Datenbank-Metadaten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. SSMA speichert Informationen zu welcher Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, muss die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gegebenenfalls eine aktive Verbindung mit dem Server. Sie können offline arbeiten, bis Sie Datenbankobjekte in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Daten migrieren.  
  
Metadaten zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird nicht automatisch synchronisiert. Stattdessen aktualisiert die Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, müssen Sie manuell aktualisieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Weitere Informationen finden Sie unter der "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-server-permissions"></a>Erforderliche SQL Server-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die das Konto ausführt:  
  
-   Konvertieren von DB2-Objekten, [!INCLUDE[tsql](../../includes/tsql_md.md)] -Syntax so aktualisieren Sie Metadaten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder um konvertierte Syntax auf Skripts speichern zu können, muss das Konto über Berechtigung zum Anmelden bei der Instanzstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Beim Laden von Datenbankobjekten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], das Konto muss ein Mitglied der **Sysadmin** -Serverrolle. Dies ist erforderlich, um CLR-Assemblys zu installieren.  
  
-   Zum Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], das Konto muss ein Mitglied der **Sysadmin** -Serverrolle. Dies ist erforderlich, um die Ausführung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Data Migration-Paketen.  
  
-   Das Konto muss zum Ausführen des Codes, die von SSMA generiert wird, verfügen **Execute** Berechtigungen für alle benutzerdefinierten Funktionen in der **ssma_DB2** Schema der Zieldatenbank. Diese Funktionen bieten die gleiche Funktionalität wie DB2-Systemfunktionen und konvertierte Objekte verwendet werden.  
  
Wenn das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird in alle Migration führen Verwaltungsaufgaben auszuführen, das Konto muss ein Mitglied der **Sysadmin** -Serverrolle.  
  
## <a name="establishing-a-sql-server-connection"></a>Herstellen einer SQL Server-Verbindung  
Vor dem Konvertieren von DB2-Datenbankobjekte auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax müssen Sie eine Verbindung mit der Instanz von herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wo Sie mindestens eine DB2-Datenbank migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Schemaebene DB2 anpassen, nach dem Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [DB2-Schemas in SQL Server-Schemas zuordnen &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], stellen Sie sicher, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird und Verbindungen akzeptieren können.  
  
**Verbindung mit SQL Server**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Server**.  
  
    Wenn Sie zuvor verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], den Namen des Befehls werden **eine erneute Verbindung mit SQL Server**.  
  
2.  Klicken Sie im Dialogfeld "Verbindung" eingeben, oder wählen Sie den Namen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf dem lokalen Computer herstellen, geben Sie **"localhost"** oder einen Punkt (**.**).  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf einem anderen Computer herstellen, geben Sie den Namen des Computers aus.  
  
    -   Wenn Sie eine Verbindung mit einer benannten Instanz auf einem anderen Computer herstellen, geben Sie den Computernamen gefolgt von einem umgekehrten Schrägstrich und den Instanznamen, z. B. MyServer\MyInstance.  
  
3.  Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] konfiguriert ist auf einen nicht standardmäßigen Port Clientverbindungen akzeptiert werden, geben die Portnummer für die verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verbindungen in der **Serverport** Feld. Für die Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], die Standardportnummer ist 1433. Für benannte Instanzen SSMA wird versucht, erhalten die Portnummer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst.  
  
4.  In der **Datenbank** Geben Sie den Namen der Zieldatenbank.  
  
    Diese Option ist nicht verfügbar, wenn Sie die Verbindung wiederherstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
5.  In der **Authentifizierung** wählen den Authentifizierungstyp, der für die Verbindung verwendet. Um die aktuelle Windows-Konto verwenden möchten, wählen **Windows-Authentifizierung**. Verwenden einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldenamen select **SQL Server-Authentifizierung**, und geben Sie den Benutzernamen und Kennwort.  
  
6.  Für sichere Verbindung zwei Steuerelemente hinzugefügt werden, die **Verbindung verschlüsseln** und **"TrustServerCertificate"** Kontrollkästchen. Nur wenn **Verbindung verschlüsseln** aktiviert ist, wird die **"TrustServerCertificate"** Kontrollkästchen wird angezeigt. Wenn **Verbindung verschlüsseln** ("true") aktiviert ist und **"TrustServerCertificate"** ist deaktiviert (false) ist, erfolgt Überprüfen der SQL Server-SSL-Zertifikat. Das Überprüfen des Serverzertifikats ist Teil des SSL-Handshakes und stellt sicher, dass es sich bei dem Server tatsächlich um den Server handelt, mit dem eine Verbindung hergestellt werden soll. Um dies sicherzustellen, muss sowohl auf Clientseite als auch auf dem Server ein Zertifikat installiert sein.  
  
7.  Klicken Sie auf **Verbinden**.  
  
**Höhere Version zur Anwendungskompatibilität**  
  
-   Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Migrationsprojekt erstellt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 beim Migrationsprojekt erstellt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, aber Sie werden nicht in der Lage sind, d. h. mit niedrigeren Versionen verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Projekt erstellt SQL Server 2012 ist.  
  
||||||  
|-|-|-|-|-|  
|**Projekt Typ Vs-SERVER-ZIELVERSION**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|Azure SQL-Datenbank|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014|||ja||  
|Azure SQL-Datenbank||||ja|  
  
> [!IMPORTANT]  
> Konvertierung der Datenbankobjekte erfolgt gemäß den Projekttyp, aber nicht gemäß der Version von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind. Im Fall von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 oder Azure SQL-Datenbank.  
  
## <a name="synchronizing-sql-server-metadata"></a>Synchronisieren von SQL Server-Metadaten  
Metadaten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken wird nicht automatisch aktualisiert. Die Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer ist eine Momentaufnahme der Metadaten aus, wenn Sie sich zunächst mit verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder der letzten Ausführung, die Sie manuell aktualisierten Metadaten. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, wählen Sie das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Z. B. um die Metadaten für alle Datenbanken zu aktualisieren, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
3.  Mit der rechten Maustaste **Datenbanken**, oder die einzelne Datenbank oder Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Die Zuordnung zwischen DB2 Schemas anpassen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken und Schemas, finden Sie unter [DB2 Zuordnungsschemas in SQL Server-Schemas &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
-   Konfigurationsoptionen für die Projekte anpassen können, finden Sie unter [Projekteinstellungen &#40;Konvertierung&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) und Verwandte Abschnitte.  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung DB2 und SQL Server-Datentypen &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Wenn Sie nicht verfügen, um diese Aufgaben auszuführen, können Sie die DB2-Datenbank-Objektdefinitionen in konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Objektdefinitionen. Weitere Informationen finden Sie unter [DB2-Schemas konvertieren &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Datenbanken zu SQLServer &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
