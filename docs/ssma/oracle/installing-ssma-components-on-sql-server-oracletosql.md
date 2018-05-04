---
title: Installieren SSMA-Komponenten auf SQLServer (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 1a5ca1dcabd8d9fc860bd803753048ed02ddecc9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Installieren SSMA-Komponenten auf SQLServer (OracleToSQL)
Neben der Installation von SSMA, müssen Sie auch Komponenten installieren, auf dem Computer, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Zu diesen Komponenten gehören das Pack der SSMA-Erweiterung, das Datenmigration und Oracle-Anbieter auf Server-zu-Server-Verbindung aktivieren unterstützt.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA für die Oracle-Erweiterung Pack  
Das SSMA-Erweiterung Pack fügt die Datenbanken **Sysdb** und **Ssmatesterdb**, mit der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Die Datenbank **Sysdb** enthält die Tabellen und gespeicherte Prozeduren, die zum Migrieren von Daten erforderlich sind und die benutzerdefinierte Funktionen, die Oracle-Systemfunktionen zu emulieren. Die **Ssmatesterdb** Datenbank enthält die Tabellen und Prozeduren, die von der Komponente Tester erforderlich sind.  
  
Darüber hinaus beim Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge, wenn Server-Seite-Migration Datenmodul zum Migrieren Ihrer Daten verwendet wird.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Vor der Installation von SSMA für Oracle-Server-Komponenten auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], stellen Sie sicher, dass das System die folgenden Anforderungen erfüllt:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Instanz installiert ist. SSMA unterstützt SQL Server 2008 Express Edition nicht.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 oder höher.  
  
-   Der Oracle-Client-Anbieter oder OLE DB-Anbieter für Oracle und Verbindung mit der Oracle-Datenbank, die Sie migrieren möchten. Sie können den Anbieter aus der Oracle-Produktmedien oder Oracle-Website installieren.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst muss ausgeführt werden, während der Installation. Wird verwendet, um eine Liste der Instanzen des Auffüllen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] im Setup-Assistenten. Sie können Deaktivieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst nach der Installation.  
  
    > [!NOTE]  
    > Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst ausgeführt wird, aber Sie noch nicht sehen, dass eine Liste von Instanzen im Setup, müssen Sie die Blockierung aufheben UDP-Port 1434. Können Sie Windows-Firewall vorübergehend Entsperren des Ports ein, oder Sie können die Windows-Firewall vorübergehend deaktivieren. Möglicherweise müssen auch die Antivirensoftware vorübergehend deaktivieren. Stellen Sie sicher, dass Firewalls und antivirus-Software nach der Installation aktivieren.  
  
### <a name="installing-the-extension-pack"></a>Installieren der Erweiterung-Pakets  
Sie können einem beliebigen Zeitpunkt vor dem Migrieren von Daten an, das Erweiterung Pack installieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Um die Erweiterung Pack zu installieren, muss ein Mitglied der **Sysadmin** -Serverrolle auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**So installieren Sie die Erweiterung pack**  
  
1.  Wenn Sie dies noch nicht getan haben, extrahieren Sie alle Dateien aus der SSMA Zip-Datei.  
  
    Abhängig von der Version der WinZip, Sie haben, können Sie entweder Doppelklicken Sie auf die Datei oder mit der rechten Maustaste in der das und auswählen **alle extrahieren** oder **in WinZip geöffnet**. Führen Sie die Anweisungen in der WinZip-Benutzeroberfläche, um die Dateien zu extrahieren.  
  
2.  Kopieren Sie SSMA für die Erweiterung Pack Oracle. *n*. Install.exe, wobei *n* ist, auf dem Computer, auf denen ausgeführt wird, die Nummer des Builds [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
3.  Doppelklicken Sie SSMA für Oracle-Erweiterung Pack ein. *n*. Install.exe.  
  
4.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
5.  Lesen Sie den Lizenzvertrag auf der Seite Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, Aktivieren der **ich stimme den Bedingungen des Lizenzvertrags** Kontrollkästchen, und klicken Sie dann auf **Weiter**.  
  
6.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
7.  Klicken Sie auf der Seite Installationsbereit auf **installieren**.  
  
8.  Klicken Sie auf den abgeschlossen-der erste Schritt der Installationsseite auf **Weiter**.  
  
    Ein neues Dialogfeld wird angezeigt, in dem Sie die Instanz von auswählen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] für die Erweiterung Paketinstallation.  
  
9. Wählen Sie die Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , in dem Sie migrieren von Oracle-Schemas, und klicken Sie dann auf **Weiter**.  
  
    Die Standardinstanz hat den gleichen Namen wie der Computer an. Benannte Instanzen werden ein umgekehrter Schrägstrich und der Instanzname folgt.  
  
10. Klicken Sie auf der Verbindungsseite wählen Sie die Authentifizierungsmethode aus, und klicken Sie dann auf **Weiter**.  
  
    Windows-Authentifizierung wird Windows-Anmeldeinformationen verwenden, um zu versuchen, melden Sie sich mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Bei Auswahl des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldename und Kennwort.  
  
11. Wählen Sie auf der nächsten Seite **Utilities-Datenbank installieren** *n*, wobei *n* ist die Versionsnummer, und klicken Sie dann auf **Weiter**.  
  
    Die **Sysdb** Datenbank wird erstellt und die benutzerdefinierten Funktionen und gespeicherten Prozeduren werden in dieser Datenbank erstellt.  
  
    Wenn **Tester-Datenbank installieren** Option ist aktiviert, die Tester **Ssmatesterdb** Datenbank erstellt wird.  
  
12. So installieren Sie die Dienstprogramme in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Option **Ja**, und klicken Sie dann auf **Weiter**. Um den Assistenten zu beenden, klicken Sie auf **keine**.  
  
13. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] oder mit dem Sqlcmd-Hilfsprogramm, führen Sie das folgende Skript aus, um CLR zu aktivieren:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    Wenn die CLR nicht aktiviert ist, wird der folgende Fehler ausgegeben, Verbindungsaufbau SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    SSMA konnten Erweiterung Pack Assembly-Versionsinformationen nicht abgerufen werden. Installieren Sie das Pack Erweiterung auf dem Datenbankserver.  
  
### <a name="sql-server-database-objects"></a>SQL Server-Objekte  
Nachdem Sie die Erweiterung Pack installieren, sehen Sie eine ausführliche Informationen finden Sie ein **ssma_oracle.bcp_migration_packages** Tabelle, ein **ssma_oracle.db_storage** Tabelle, und ein **ssma_oracle.db_error_list** -Tabelle in der **Sysdb** Datenbank. Sie sehen auch viele gespeicherte Prozeduren und benutzerdefinierte Funktionen in der **Ssma_oracle** Schema.  
  
Jedes Mal, die Sie zum Migrieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA erstellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrag. Diese Aufträge werden mit dem Namen **Ssma_oracle Migration Datenpaket {GUID}**, und werden in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] im Ordner "Aufträge".  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
