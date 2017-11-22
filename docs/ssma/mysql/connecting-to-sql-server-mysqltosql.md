---
title: Herstellen einer Verbindung mit SQLServer (MySQLToSQL) | Microsoft Docs
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
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
caps.latest.revision: "18"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 556b9ceec47aeb78fb534b5cac9e87c15adfae7f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Herstellen einer Verbindung mit SQLServer (MySQLToSQL)
Um MySQL-Datenbanken zu SQL Server zu migrieren, müssen Sie mit der Zielinstanz von SQL Server verbinden. Wenn Sie eine Verbindung herstellen, wird SSMA Ruft Metadaten zu allen Datenbanken in der Instanz von SQL Server ab und Datenbankmetadaten in der SQL Server-Metadaten-Explorer angezeigt. SSMA speichert Informationen der Instanz von SQL Server Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit SQL Server bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie ggf. eine aktive Verbindung mit dem Server mit SQL Server herstellen. Sie können offline arbeiten, bis Sie Datenbankobjekte in SQL Server laden und Migrieren von Daten.  
  
Metadaten zur Instanz von SQL Server werden nicht automatisch synchronisiert. Um die Metadaten in SQL Server-Metadaten-Explorer zu aktualisieren, müssen Sie stattdessen manuell die SQL Server-Metadaten aktualisieren. Weitere Informationen finden Sie im Abschnitt "Synchronisieren von SQL Server-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-server-permissions"></a>Erforderliche SQL Server-Berechtigungen  
Das Konto, mit dem eine Verbindung mit SQL Server, erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die das Konto ausführt:  
  
-   MySQL-Objekte zu konvertieren [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, um Metadaten von SQL Server zu aktualisieren oder konvertierte Syntax zum Speichern von Skripts, das Konto muss über die Berechtigung zum Anmelden bei der SQL Server-Instanz verfügen.  
  
-   Um die Datenbankobjekte in SQL Server zu laden, die minimal erforderliche Berechtigungen-Anforderung ist die Mitgliedschaft in der **Db_owner** Datenbankrolle in der Zieldatenbank.  
  
## <a name="establishing-a-sql-server-connection"></a>Herstellen einer SQL Server-Verbindung  
Bevor Sie Objekte des MySQL-Datenbank in SQL Server-Syntax konvertieren, müssen Sie eine Verbindung mit der Instanz von SQL Server einrichten, Sie die MySQL-Datenbank bzw. sekundären Datenbanken zu migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Schemaebene MySQL anpassen, nach dem Herstellen einer Verbindung mit SQL Server. Weitere Informationen finden Sie unter [Zuordnen von MySQL-Datenbanken zu SQL Server-Schemas &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung mit SQL Server, stellen Sie sicher, dass die Instanz von SQL Server ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit SQL Server**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Server** (diese Option ist nach der Erstellung eines Projekts).  
  
    Wenn Sie zuvor eine Verbindung mit SQL Server hergestellt haben, wird der Befehlsname sein **eine erneute Verbindung mit SQL Server**.  
  
2.  Klicken Sie im Dialogfeld Verbindung geben Sie ein, oder wählen Sie den Namen der Instanz von SQL Server.  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf dem lokalen Computer herstellen, geben Sie **"localhost"** oder einen Punkt (**.**).  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf einem anderen Computer herstellen, geben Sie den Namen des Computers aus.  
  
    -   Wenn Sie eine Verbindung mit einer benannten Instanz auf einem anderen Computer herstellen, geben Sie den Computernamen gefolgt von einem umgekehrten Schrägstrich und den Instanznamen, z. B. MyServer\MyInstance.  
  
3.  Wenn Ihre Instanz von SQL Server für die Annahme von Verbindungen über einen nicht standardmäßigen Port konfiguriert ist, geben Sie die Portnummer für die in SQL Server-Verbindungen verwendeten die **Serverport** Feld. Für die Standardinstanz von SQL Server wird die Standardportnummer 1433. SSMA versucht für benannte Instanzen, die Portnummer aus der SQL Server-Browser-Dienst zu erhalten.  
  
4.  In der **Authentifizierung** wählen den Authentifizierungstyp, der für die Verbindung verwendet. Um die aktuelle Windows-Konto verwenden möchten, wählen **Windows-Authentifizierung**. Um einen SQL Server-Anmeldenamen verwenden, wählen Sie SQL Server-Authentifizierung, und geben Sie den Benutzernamen und Kennwort.  
  
5.  Für sichere Verbindung zwei Steuerelemente hinzugefügt werden, die **Verbindung verschlüsseln** und **"TrustServerCertificate"** Kontrollkästchen. Nur wenn **Verbindung verschlüsseln** aktiviert ist, wird die **"TrustServerCertificate"** Kontrollkästchen wird angezeigt. Wenn **Verbindung verschlüsseln** ("true") aktiviert ist und **"TrustServerCertificate"** ist deaktiviert (false) ist, erfolgt Überprüfen der SQL Server-SSL-Zertifikat. Das Überprüfen des Serverzertifikats ist Teil des SSL-Handshakes und stellt sicher, dass es sich bei dem Server tatsächlich um den Server handelt, mit dem eine Verbindung hergestellt werden soll. Um dies sicherzustellen, muss sowohl auf Clientseite als auch auf dem Server ein Zertifikat installiert sein.  
  
6.  Klicken Sie auf Verbinden.  
  
**Höhere Versionskompatibilität**  
  
Es ist zulässig, eine Verbindung herstellen/sich auf höhere Versionen von SQL Server herzustellen.  
  
1.  Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Projekt erstellt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
2.  Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Projekt erstellt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, aber es ist nicht zulässig, d. h. mit niedrigeren Versionen verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
3.  Sie werden mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Projekt erstellt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012.  
  
4.  Sie werden nur Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016, wenn das Projekt erstellt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014.  
  
5.  Höhere Versionskompatibilität gilt nicht für "SQL Azure".  
  
||||||||  
|-|-|-|-|-|-|-|  
|**Projekt Typ Vs-SERVER-ZIELVERSION**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (Version: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (Version: mit "10.x")|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|ja|ja|ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||ja|ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014||||ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016|||||ja||  
|SQL Azure||||||ja|  
  
> [!IMPORTANT]  
> Konvertierung der Datenbankobjekte erfolgt gemäß den Projekttyp, aber nicht gemäß der Version von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verbunden. Im Fall von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005-Projekt Konvertierung erfolgt gemäß [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, obwohl Sie mit einer höheren Version verbunden sind [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (SQL Server 2008 oder SQL Server 2012 oder SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Synchronisieren von SQL Server-Metadaten  
Metadaten zu SQL Server-Datenbanken wird nicht automatisch aktualisiert. Die Metadaten in SQL Server-Metadaten-Explorer ist eine Momentaufnahme der Metadaten, wenn Sie zunächst mit SQL Server verbunden, oder der letzten Ausführung, die Sie manuell die Metadaten aktualisiert. Sie können die Metadaten für alle Datenbanken oder für jede einzelne Datenbank oder ein Datenbankobjekt manuell aktualisieren.  
  
**Zum Synchronisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit SQL Server verbunden sind.  
  
2.  Wählen Sie in SQL Server-Metadaten-Explorer das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
    Angenommen, um die Metadaten für alle Datenbanken zu aktualisieren, wählen Sie das Kontrollkästchen neben den Datenbanken an.  
  
3.  Mit der rechten Maustaste Datenbanken, oder die einzelne Datenbank oder das Datenbankschema, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt der Migration hängt von Ihren Anforderungen Projekt:  
  
-   Wenn Sie die Zuordnung zwischen Schemas MySQL und SQL Server-Datenbanken und Schemas anpassen zu können, finden Sie unter [Zuordnung MySQL-Datenbanken zu SQL Server-Schemas &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Konfigurationsoptionen für die Projekte anpassen können, finden Sie unter [Einstellung Projektoptionen &#40; MySQLToSQL &#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Zum Anpassen der Zuordnung von Quelle und Ziel-Datentypen finden Sie unter [Zuordnung MySQL und SQL Server-Datentypen &#40; MySQLToSQL &#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Wenn Sie nicht verfügen, um diese Aufgaben auszuführen, können Sie die Objektdefinitionen für MySQL-Datenbank in SQL Server-Objektdefinitionen konvertieren. Weitere Informationen finden Sie unter [MySQL-Datenbanken konvertieren &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
