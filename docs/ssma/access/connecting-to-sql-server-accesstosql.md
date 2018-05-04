---
title: Herstellen einer Verbindung mit SQLServer (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 771a4ad9c493108c47df3c840da79be7b5674466
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-sql-server-accesstosql"></a>Herstellen einer Verbindung mit SQLServer (AccessToSQL)
Zum Migrieren von Access-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie müssen die Verbindung mit der Zielinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie eine Verbindung herstellen, erhält SSMA Metadaten zu den Datenbanken in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und zeigt Sie Datenbank-Metadaten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer. SSMA speichert Informationen zu welcher Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Sie verbunden sind, jedoch werden Kennwörter nicht gespeichert.  
  
Die Verbindung mit SQL Server bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie ggf. eine aktive Verbindung mit dem Server mit SQL Server herstellen. Sie können offline arbeiten, bis Sie Datenbankobjekte in SQL Server laden und Migrieren von Daten.  
  
Metadaten zur Instanz von SQL Server werden nicht automatisch synchronisiert. Um die Metadaten in SQL Server-Metadaten-Explorer zu aktualisieren, müssen Sie stattdessen manuell die SQL Server-Metadaten aktualisieren. Weitere Informationen finden Sie im Abschnitt "Synchronisieren von SQL Server-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-sql-server-permissions"></a>Erforderliche SQL Server-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erfordert unterschiedliche Berechtigungen abhängig von den Aktionen, die von diesem Konto ausgeführt werden.  
  
-   Zugreifen auf Objekte zu konvertieren [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, um Metadaten aus zu aktualisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder um konvertierte Syntax auf Skripts speichern zu können, muss das Konto über die Berechtigung zum Anmelden bei der Instanzstatus von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Beim Laden von Datenbankobjekten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und zum Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], die minimal erforderliche Berechtigungen-Anforderung ist die Mitgliedschaft in der **Db_owner** Datenbankrolle in der Zieldatenbank.  
  
## <a name="establishing-a-sql-server-connection"></a>Herstellen einer SQL Server-Verbindung  
Bevor Sie den Zugriff auf Datenbankobjekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax müssen Sie eine Verbindung mit der Instanz von herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wo Sie die Access-Datenbanken migrieren möchten.  
  
Wenn Sie die Verbindungseigenschaften definieren, geben Sie auch die Datenbank, in denen Objekte und Daten migriert werden sollen. Sie können diese Zuordnung auf Datenbankebene Zugriff anpassen, nach dem Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [Zuordnen von Quell- und Zieldatenbanken](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
> [!IMPORTANT]  
> Vor dem Verbinden mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], stellen Sie sicher, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgeführt wird und Verbindungen akzeptieren können. Weitere Informationen finden Sie unter "Herstellen einer Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbankmodul" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
**Verbindung mit SQL Server**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Server**.  
  
    Wenn Sie zuvor verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], den Namen des Befehls werden **eine erneute Verbindung mit SQL Server**.  
  
2.  In der **Servernamen** Feld, geben Sie ein oder wählen Sie den Namen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf dem lokalen Computer herstellen, geben Sie **"localhost"** oder einen Punkt (**.**).  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf einem anderen Computer herstellen, geben Sie den Namen des Computers aus.  
  
    -   Wenn Sie eine Verbindung mit einer benannten Instanz herstellen, geben Sie den Computernamen, einen umgekehrten Schrägstrich und den Instanznamen. Zum Beispiel: MyServer\MyInstance.  
  
    -   Zur Verbindung mit einer aktiven Benutzerinstanz von [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], eine Verbindung herstellen über named Pipes-Protokoll und den Pipenamen an, wie z. B. angeben \\ \\.\pipe\sql\query. Weitere Informationen finden Sie in der Dokumentation zu [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].  
  
3.  Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] konfiguriert ist auf einen nicht standardmäßigen Port Clientverbindungen akzeptiert werden, geben die Portnummer für die verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verbindungen in der **Serverport** Feld. Für die Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], die Standardportnummer ist 1433. Für benannte Instanzen SSMA wird versucht, erhalten die Portnummer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst.  
  
4.  In der **Datenbank** Geben Sie den Namen der Zieldatenbank für die Migration von Objekt und Daten.  
  
    Diese Option ist nicht verfügbar, wenn es sich bei einer erneuten Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    Der Name der Zieldatenbank darf keine Leerzeichen oder Sonderzeichen enthalten. Sie können z. B. Access-Datenbanken zum Migrieren einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mit dem Namen "Abc". Access-Datenbanken, können nicht migriert werden, aber eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mit dem Namen "eine b-c".  
  
    Sie können diese Zuordnung pro Datenbank anpassen, nachdem Sie eine Verbindung herstellen. Weitere Informationen finden Sie unter [Zuordnen von Quell- und Zieldatenbanken](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4)  
  
5.  In der **Authentifizierung** Dropdown-Menü Wählen Sie den Authentifizierungstyp, der für die Verbindung verwendet. Um die aktuelle Windows-Konto verwenden möchten, wählen **Windows-Authentifizierung**. Verwenden einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldung wählen **SQL Server-Authentifizierung**, und geben Sie dann einen Benutzernamen und ein Kennwort.  
  
6.  Für sichere Verbindung zwei Steuerelemente hinzugefügt werden, **Verbindung verschlüsseln** Kontrollkästchen und **"TrustServerCertificate"** Kontrollkästchen. Nur wenn **Verbindung verschlüsseln** aktiviert ist **"TrustServerCertificate"** Kontrollkästchen wird angezeigt. Wenn **Verbindung verschlüsseln** ist checked(true) und **"TrustServerCertificate"** unchecked(false) ist, wird das SQL Server-SSL-Zertifikat zu überprüfen. Das Überprüfen des Serverzertifikats ist Teil des SSL-Handshakes und stellt sicher, dass es sich bei dem Server tatsächlich um den Server handelt, mit dem eine Verbindung hergestellt werden soll. Um dies sicherzustellen, muss sowohl auf Clientseite als auch auf dem Server ein Zertifikat installiert sein.  
  
7.  Klicken Sie auf **Verbinden**.  
  
**Höhere Versionskompatibilität**  
  
Es ist zulässig, eine Verbindung herstellen/sich auf höhere Versionen von SQL Server herzustellen.  
  
1.  Sie werden auf SQL Server 2008 oder SQL Server 2012 herstellen, wenn das Projekt erstellt haben, SQL Server 2005 ist.  
  
2.  Sie werden für die Verbindung mit SQL Server 2012, wenn das Projekt erstellt haben, SQL Server 2008 ist, aber es nicht zulässig ist, mit niedrigeren Versionen d. h. SQL Server 2005 verwendet werden können.  
  
3.  Sie werden nur SQL Server 2012 herstellen, wenn das Projekt erstellt haben, SQL Server 2012 ist.  
  
4.  Höhere Versionskompatibilität gilt nicht für SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**Projekt Typ Vs-SERVER-ZIELVERSION**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 (Version: 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 (Version: mit "10.x")|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 (Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 (Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 (Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|ja|ja|ja|ja|ja||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||ja|ja|ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||ja|ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||ja|ja||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||ja||
|SQL Azure||||||ja|
  
> [!IMPORTANT]  
> Konvertierung der Datenbankobjekte ist gemäß den Projekttyp, aber nicht gemäß der Version von SQL Server verbunden durchgeführt. Im Falle von SQL Server 2005-Projekt wird Konvertierung gemäß SQL Server 2005 ausgeführt, obwohl Sie mit einer höheren Version von SQL Server (SQL Server 2008 oder SQL Server 2012 oder SQL Server 2014/SQL Server 2016) verbunden sind.  
  
## <a name="synchronizing-sql-server-metadata"></a>Synchronisieren von SQL Server-Metadaten  
Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas ändern, nachdem Sie eine Verbindung herstellen, können Sie die Metadaten mit dem Server synchronisieren.  
  
**Zum Synchronisieren von SQL Server-Metadaten**  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer mit der rechten Maustaste **Datenbanken**, und wählen Sie dann **mit Datenbank synchronisieren**.  
  
## <a name="reconnecting-to-sql-server"></a>Erneutes Herstellen einer Verbindung mit SQLServer  
Die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, muss die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gegebenenfalls eine aktive Verbindung mit dem Server. Sie können offline arbeiten, bis Sie Datenbankobjekte in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Daten migrieren.  
  
Das Verfahren zum Wiederherstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ist identisch mit dem Verfahren zum Herstellen einer Verbindung.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie die Zuordnung zwischen den Quell-und Zieldatenbanken anpassen möchten, finden Sie unter [Zuordnung Quell- und Zieldatenbanken](http://msdn.microsoft.com/en-us/69bee937-7b2c-49ee-8866-7518c683fad4) , andernfalls ist der nächste Schritt zu Datenbankobjekte, die zu konvertierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax mit [konvertieren Datenbankobjekte](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
