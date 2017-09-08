---
title: Installieren SSMA-Komponenten auf SQLServer (SybaseToSQL) | Microsoft Docs
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
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 716a45f706292e3011ed5c8c2871bfc8176fb5a5
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Installieren SSMA-Komponenten auf SQLServer (SybaseToSQL)
Neben der Installation von SSMA für die Verwendung von Server-Side-Datenmigration, müssen Sie auch Komponenten installieren, auf dem Computer, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Zu diesen Komponenten gehören das Pack der SSMA-Erweiterung, das Datenmigration und Sybase-Anbieter auf Server-zu-Server-Verbindung aktivieren unterstützt.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA für Sybase-Erweiterung Pack  
Das SSMA-Erweiterung Pack fügt die Datenbanken **Sysdb** und **Ssmatesterdb_syb**, mit der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Die **Sysdb** Datenbank enthält die Tabellen und gespeicherten Prozeduren, die zum Migrieren von Daten erforderlich sind. Die **Ssmatester_syb** Datenbank enthält das Schema **Ssma_sybase_utilities**, in dem die von der Komponente der SSMA-Tester verwendeten Objekte (Tabellen, Trigger, Views) erstellt werden.  
  
Darüber hinaus beim Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge, wenn Server-Seite-Migration Datenmodul zum Migrieren Ihrer Daten verwendet wird.  
  
### <a name="installing-the-extension-pack"></a>Installieren der Erweiterung-Pakets  
Sie können einem beliebigen Zeitpunkt vor dem Migrieren von Daten an, das Erweiterung Pack installieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Um die Erweiterung Pack zu installieren, müssen Sie Mitglied der Serverrolle "Sysadmin" auf der Instanz von werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**So installieren Sie die Erweiterung pack**  
  
1.  Kopieren Sie SSMA für Sybase-Erweiterung Pack. *n*. Install.exe, wobei  *n*  ist, auf dem Computer, auf denen ausgeführt wird, die Nummer des Builds [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Doppelklicken Sie SSMA für Sybase-Erweiterung Pack ein. *n*. Install.exe.  
  
3.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
4.  Lesen Sie den Lizenzvertrag auf der Seite Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, Aktivieren der **ich stimme den Bedingungen des Lizenzvertrags** Kontrollkästchen, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
6.  Klicken Sie auf der Seite Installationsbereit auf **installieren**.  
  
7.  Klicken Sie auf den abgeschlossen-der erste Schritt der Installationsseite auf **Weiter**.  
  
    Ein neues Dialogfeld wird angezeigt, in dem Sie die Instanz von auswählen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] für die Erweiterung Paketinstallation.  
  
8.  Wählen Sie die Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wo Sie bei der Migration ASE Datenbanken, und klicken Sie dann auf **Weiter**.  
  
    Die Standardinstanz hat den gleichen Namen wie der Computer an. Benannte Instanzen werden ein umgekehrter Schrägstrich und der Instanzname folgt.  
  
9. Klicken Sie auf der Seite "Verbindungsparameter" Wählen Sie die Authentifizierungsmethode aus, und klicken Sie dann auf **Weiter**.  
  
    Windows-Authentifizierung wird Windows-Anmeldeinformationen verwenden, um zu versuchen, melden Sie sich mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Bei Auswahl des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldename und Kennwort.  
  
10. Wählen Sie auf der Seite "Server verwalten" **Utilities-Datenbank installieren**  *n* , wobei  *n*  ist die Versionsnummer, und klicken Sie dann auf **Weiter**.  
  
    Die **Sysdb** Datenbank wird erstellt, und die gespeicherten Prozeduren werden in dieser Datenbank erstellt.  
  
    Wenn **Tester-Datenbank installieren** Option ist aktiviert, die Tester **Ssmatesterdb_syb** Datenbank erstellt wird.  
  
11. So installieren Sie die Dienstprogramme in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Option **zurück zu Instanzen**, und klicken Sie dann auf **Weiter**. Um den Assistenten zu beenden, klicken Sie auf **beenden**.  
  
### <a name="sql-server-database-objects"></a>SQL Server-Objekte  
Nachdem Sie die Erweiterung Pack installieren, sehen Sie eine ausführliche Informationen finden Sie eine **ssma_syb.bcp_migration_packages** -Tabelle in der **Sysdb** Datenbank. Sehen Sie auch die folgenden gespeicherten Prozeduren:  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
Jedes Mal, die Sie zum Migrieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA erstellt eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Auftrag. Diese Aufträge werden mit dem Namen **Ssma_syb Migration Datenpaket {GUID}**, und werden in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Knoten von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] im Ordner "Aufträge".  
  
## <a name="sybase-providers"></a>Anbieter für Sybase  
Beim Migrieren von Daten aus ASE auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure, die Daten direkt zwischen ASE migriert und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure. Es ist nicht SSMA durchlaufen, da dies die Datenmigration verlangsamen würde.  
  
### <a name="installing-the-sybase-providers"></a>Installieren die Anbieter für Sybase  
Die folgenden Anweisungen bieten die grundlegenden Installationsschritte für Sybase-Anbieter zu installieren. Die genaue Anweisungen variieren je nach Version der Sybase-Setupprogramm.  
  
> [!IMPORTANT]  
> Bevor Sie das Setupprogramm ausführen, stellen Sie sicher, dass Sie nicht die lizenzveREINBARUNG verstoßen.  
  
1.  Führen Sie das Setupprogramm für Sybase ASE.  
  
2.  Wählen Sie die benutzerdefinierte Installation.  
  
3.  Wählen Sie auf der Seite Funktionsauswahl den Datenanbieter für ODBC, OLE DB und ADO.NET.  
  
4.  Überprüfen Sie die ausgewählten Features, und klicken Sie dann auf **Fertig stellen** Datenanbieter zu installieren.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für Sybase Client &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

