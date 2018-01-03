---
title: Herstellen einer Verbindung mit SQLServer (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
caps.latest.revision: "16"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 1b550ddd57803772be53832ba8feb840021c5732
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-sql-server-oracletosql"></a>Herstellen einer Verbindung mit SQLServer (OracleToSQL)
Zum Migrieren von Oracle-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 R2 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014, Sie müssen die Verbindung mit einer dieser, abzielen, Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie eine Verbindung herstellen, erhält SSMA Metadaten zu allen Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und zeigt Sie Datenbank-Metadaten in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. SSMA speichert Informationen zu welcher Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, muss die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gegebenenfalls eine aktive Verbindung mit dem Server. Sie können offline arbeiten, bis Sie Datenbankobjekte in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Daten migrieren.  
  
Metadaten zu der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird nicht automatisch synchronisiert. Stattdessen aktualisiert die Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, müssen Sie manuell aktualisieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Weitere Informationen finden Sie unter der "Synchronizing [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-server-permissions"></a>Erforderliche SQL Server-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die das Konto ausführt:  
  
-   Konvertieren von Oracle-Objekten, [!INCLUDE[tsql](../../includes/tsql_md.md)] -Syntax so aktualisieren Sie Metadaten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder um konvertierte Syntax auf Skripts speichern zu können, muss das Konto über Berechtigung zum Anmelden bei der Instanzstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Beim Laden von Datenbankobjekten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], das Konto muss ein Mitglied der **Sysadmin** -Serverrolle. Dies ist erforderlich, um CLR-Assemblys zu installieren.  
  
-   Zum Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], das Konto muss ein Mitglied der **Sysadmin** -Serverrolle. Dies ist erforderlich, um die Ausführung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Data Migration-Paketen.  
  
-   Das Konto muss zum Ausführen des Codes, die von SSMA generiert wird, verfügen **Execute** Berechtigungen für alle benutzerdefinierten Funktionen in der **Ssma_oracle** Schema der Zieldatenbank. Diese Funktionen geben Sie die entsprechende Funktionalität der Oracle-Systemfunktionen und konvertierte Objekte verwendet werden.  
  
Wenn das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird in alle Migration führen Verwaltungsaufgaben auszuführen, das Konto muss ein Mitglied der **Sysadmin** -Serverrolle.  
  
## <a name="establishing-a-sql-server-connection"></a>Herstellen einer SQL Server-Verbindung  
Vor dem Konvertieren von Oracle-Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax müssen Sie eine Verbindung mit der Instanz von herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wo Sie die Oracle-Datenbank oder Datenbanken migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Schemaebene Oracle anpassen, nach dem Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [Zuordnen von Oracle-Schemas zu SQL Server-Schemas &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
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
  
||||||||  
|-|-|-|-|-|-|-|  
|**Projekt Typ Vs-SERVER-ZIELVERSION**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (Version: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (Version: mit "10.x")|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|Azure SQL-Datenbank|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|ja|ja|ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||ja|ja|ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||ja|ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||ja||
|Azure SQL-Datenbank||||||ja|
  
> [!IMPORTANT]  
> Konvertierung der Datenbankobjekte erfolgt gemäß den Projekttyp, aber nicht gemäß der Version von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind. Im Fall von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005-Projekt Konvertierung erfolgt gemäß [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, obwohl Sie mit einer höheren Version verbunden sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Synchronisieren von SQL Server-Metadaten  
Metadaten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken wird nicht automatisch aktualisiert. Die Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer ist eine Momentaufnahme der Metadaten aus, wenn Sie sich zunächst mit verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder der letzten Ausführung, die Sie manuell aktualisierten Metadaten. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, wählen Sie das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Z. B. um die Metadaten für alle Datenbanken zu aktualisieren, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
3.  Mit der rechten Maustaste **Datenbanken**, oder die einzelne Datenbank oder Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Die Zuordnung zwischen dem Oracle-Schemas anpassen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken und Schemas, finden Sie unter [Zuordnungsschemas für Oracle zu SQL Server-Schemas &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
-   Konfigurationsoptionen für die Projekte anpassen können, finden Sie unter [Einstellung Projektoptionen &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung Oracle und SQL Server-Datentypen &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Wenn Sie nicht verfügen, um diese Aufgaben auszuführen, können Sie die Oracle-Datenbank-Objektdefinitionen in konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Objektdefinitionen. Weitere Informationen finden Sie unter [Oracle-Schemas konvertieren &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
