---
title: Herstellen einer Verbindung mit SQLServer (SybaseToSQL) | Microsoft Docs
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
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3dd8b595d897aad93d580447af4afed330cb71f9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connecting-to-sql-server-sybasetosql"></a>Herstellen einer Verbindung mit SQLServer (SybaseToSQL)
Zum Migrieren von Datenbanken von Sybase Adaptive Server Enterprise (ASE) zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], müssen Sie die Verbindung zum Ziel-Instanzen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie eine Verbindung herstellen, erhält SSMA Metadaten zu allen Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und zeigt Sie Datenbank-Metadaten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. SSMA speichert Informationen zu welcher Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, muss die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gegebenenfalls eine aktive Verbindung mit dem Server. Sie können offline arbeiten, bis Sie Datenbankobjekte in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Daten migrieren.  
  
Metadaten zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird nicht automatisch synchronisiert. Stattdessen ggf. so aktualisieren Sie Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, müssen Sie manuell aktualisieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten, wie beschrieben in der "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-server-permissions"></a>Erforderliche SQL Server-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die von diesem Konto ausgeführt werden.  
  
-   ASE Objekte konvertieren [!INCLUDE[tsql](../../includes/tsql_md.md)] -Syntax so aktualisieren Sie Metadaten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder um konvertierte Syntax auf Skripts speichern zu können, muss das Konto über die Berechtigung zum Anmelden bei der Instanzstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Beim Laden von Datenbankobjekten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], die minimal erforderliche Berechtigungen-Anforderung ist die Mitgliedschaft in der **Db_owner** Datenbankrolle in der Zieldatenbank.  
  
-   Zum Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], das Konto muss ein Mitglied der **Sysadmin** -Serverrolle. Dies ist erforderlich, um die Ausführung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Data Migration-Paketen.  
  
-   Das Konto muss zum Ausführen des Codes, die von SSMA generiert wird, verfügen **Execute** Berechtigungen für alle benutzerdefinierten Funktionen in der **Ssma_syb** Schema der **Sysdb** Datenbank. Diese Funktionen geben Sie die gleiche Funktionalität wie ASE Systemfunktionen und konvertierte Objekte verwendet werden.  
  
Wenn das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird in alle Migration führen Verwaltungsaufgaben auszuführen, das Konto muss ein Mitglied der **Sysadmin** -Serverrolle.  
  
## <a name="establishing-a-sql-server-connection"></a>Herstellen einer SQL Server-Verbindung  
Vor dem Konvertieren ASE Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax müssen Sie eine Verbindung mit der Instanz von herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wo Sie die Datenbank(en) von ASE migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Schemaebene ASE anpassen, nach dem Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [Mapping Sybase ASE Schemas zum SQL Server-Schemas &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
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
  
    Diese Option ist nicht verfügbar, wenn es sich bei einer erneuten Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
5.  In der **Authentifizierung** wählen den Authentifizierungstyp, der für die Verbindung verwendet. Um die aktuelle Windows-Konto verwenden möchten, wählen **Windows-Authentifizierung**. Verwenden einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldenamen select **SQL Server-Authentifizierung** , und geben Sie Benutzername und Kennwort.  
  
6.  Für sichere Verbindung zwei Steuerelemente hinzugefügt werden, die **Verbindung verschlüsseln** und **"TrustServerCertificate"** Kontrollkästchen. Nur wenn **Verbindung verschlüsseln** aktiviert ist, wird die **"TrustServerCertificate"** Kontrollkästchen wird angezeigt. Wenn **Verbindung verschlüsseln** ("true") aktiviert ist und **"TrustServerCertificate"** ist deaktiviert (false) ist, erfolgt Überprüfen der SQL Server-SSL-Zertifikat. Das Überprüfen des Serverzertifikats ist Teil des SSL-Handshakes und stellt sicher, dass es sich bei dem Server tatsächlich um den Server handelt, mit dem eine Verbindung hergestellt werden soll. Um dies sicherzustellen, muss sowohl auf Clientseite als auch auf dem Server ein Zertifikat installiert sein.  
  
7.  Klicken Sie auf **Verbinden**.  
  
**Höhere Version zur Anwendungskompatibilität**  
  
-   Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Migrationsprojekt erstellt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 beim Migrationsprojekt erstellt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, aber Sie werden nicht in der Lage sind, d. h. mit niedrigeren Versionen verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   Sie werden nur Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Projekt erstellt SQL Server 2012 ist.  
  
-   Höhere Versionskompatibilität gilt nicht für SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**Projekt Typ Vs-SERVER-ZIELVERSION**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (Version: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (Version: mit "10.x")|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|ja|ja|ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||ja|ja|ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||ja|ja|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||ja||  
|SQL Azure||||||ja|  
  
> [!IMPORTANT]  
> Konvertierung der Datenbankobjekte erfolgt gemäß den Projekttyp, aber nicht gemäß der Version von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind. Im Fall von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005-Projekt Konvertierung erfolgt gemäß [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, obwohl Sie mit einer höheren Version verbunden sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016)  
  
## <a name="reconnecting-to-sql-server"></a>Erneutes Herstellen einer Verbindung mit SQLServer  
Die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, muss die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gegebenenfalls eine aktive Verbindung mit dem Server. Sie können offline arbeiten, bis Sie Metadaten, Laden von Datenbankobjekten in aktualisieren, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Daten migrieren.  
  
Das Verfahren zum Wiederherstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ist identisch mit dem Verfahren zum Herstellen einer Verbindung.  
  
## <a name="synchronizing-sql-server-metadata"></a>Synchronisieren von SQL Server-Metadaten  
Metadaten zu den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken wird nicht automatisch aktualisiert. Die Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer ist eine Momentaufnahme der Metadaten aus, wenn Sie sich zunächst mit verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder der letzten Ausführung, die Sie manuell aktualisierten Metadaten. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, wählen Sie das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Z. B. um die Metadaten für alle Datenbanken zu aktualisieren, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
3.  Mit der rechten Maustaste Datenbanken, die einzelne Datenbank oder Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Wenn Sie die Zuordnung zwischen ASE Datenbanken und Schemas anpassen möchten, und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken und Schemas, finden Sie unter [Zuordnungsschemas Sybase ASE zum SQL Server-Schemas &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md).  
  
-   Wenn Sie die Konfigurationsoptionen für die Projekte anpassen möchten, finden Sie unter [Einstellung Projektoptionen &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
-   An benutzerdefinierte die Zuordnung der Quell- und Datentypen, finden Sie unter [Zuordnung Sybase ASE und SQL Server-Datentypen &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
-   Falls Sie nicht dazu verwenden, können Sie die Objektdefinitionen für Sybase ASE Datenbank in konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Objektdefinitionen. Weitere Informationen finden Sie unter [Konvertierung von Sybase ASE Datenbankobjekte &#40; SybaseToSQL &#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

