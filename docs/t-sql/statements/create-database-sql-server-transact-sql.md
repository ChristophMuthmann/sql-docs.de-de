---
title: Erstellen der Datenbank (SQL Server Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs: TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
caps.latest.revision: "212"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 57fe9fffdb553dffc3cd019d36692a8c34681817
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE (SQL Server Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine neue Datenbank und die zum Speichern der Datenbank verwendeten Dateien, erstellt eine Datenbank-Momentaufnahme oder hängt eine Datenbank aus den getrennten Dateien einer zuvor erstellten Datenbank an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      Create a database  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
[;]  
  
<option> ::=  
{  
      FILESTREAM ( <filestream_option> [,...n ] )  
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }  
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }  
    | NESTED_TRIGGERS = { OFF | ON }  
    | TRANSFORM_NOISE_WORDS = { OFF | ON}  
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>   
    | DB_CHAINING { OFF | ON }  
    | TRUSTWORTHY { OFF | ON }  
}  
  
<filestream_option> ::=  
{  
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
    | DIRECTORY_NAME = 'directory_name'   
}  
  
<filespec> ::=   
{  
(  
    NAME = logical_file_name ,  
    FILENAME = { 'os_file_name' | 'filestream_path' }   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]  
)  
}  
  
<filegroup> ::=   
{  
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    <filespec> [ ,...n ]  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
}  
  
```  
  
```  
  
      Attach a database  
CREATE DATABASE database_name   
    ON <filespec> [ ,...n ]   
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }  
        | ATTACH_REBUILD_LOG }  
[;]  
  
<attach_database_option> ::=  
{  
      <service_broker_option>  
    | RESTRICTED_USER  
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )  
}  
  
```  
  
```  
  
      Create a database snapshot  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Ist der Name der neuen Datenbank. Datenbanknamen müssen innerhalb einer Instanz eindeutig sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und entsprechen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 *Database_name* kann maximal 128 Zeichen sein, es sei denn, ein logischer Name für die Protokolldatei nicht angegeben ist. Wenn ein logische Protokolldateiname nicht angegeben wird, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generiert die *Logical_file_name* und *logische* für das Protokoll durch Anfügen eines Suffixes an *Database_name*. Dies schränkt *Database_name* auf 123 Zeichen, sodass der generierte logische Protokolldateiname nicht mehr als 128 Zeichen lang ist.  
  
 Wenn kein Datendateiname angegeben wird, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet *Database_name* wie die *Logical_file_name* und als die *physischer Dateiname*. Der Standardpfad wird aus der Registrierung abgerufen. Der Standardpfad kann geändert werden, indem die **Servereigenschaften (Seite Datenbankeinstellungen)** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Zum Ändern des Standardpfads muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet werden.  
  
 CONTAINMENT = { NONE | PARTIAL }  

**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt den Kapselungsstatus der Datenbank an. NONE = nicht eigenständige Datenbank. PARTIAL = teilweise eigenständige Datenbank.  
  
 ON  
 Gibt an, dass die zum Speichern der Datenabschnitte der Datenbank (Datendateien) verwendeten Datenträgerdateien explizit definiert sind. ON ist erforderlich, wenn gefolgt von einer durch Trennzeichen getrennte Liste von \<Filespec > Elemente, die die Datendateien für die primäre Dateigruppe definieren. Die Liste der Dateien in der primären Dateigruppe kann eine optionale durch Trennzeichen getrennte Liste von folgen \<Dateigruppe > Elemente, die Benutzerdateigruppen und deren Dateien definieren.  
  
 PRIMARY  
 Gibt an, dass die zugeordnete \<Filespec >-Liste die Primärdatei definiert. Die erste Datei im angegebenen der \<Filespec > Eintrag in der primären Dateigruppe wird die primäre Datei. Eine Datenbank kann nur eine primäre Datei haben. Weitere Informationen finden Sie unter [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 Ist PRIMARY nicht angegeben, wird die erste in der CREATE DATABASE-Anweisung aufgeführte Datei die primäre Datei.  
  
 LOG ON  
 Gibt an, dass die zum Speichern des Datenbankprotokolls verwendeten Datenträgerdateien (Protokolldateien) explizit definiert sind. Eine durch Trennzeichen getrennte Liste der LOG ON folgt \<Filespec > Elemente, die die Protokolldateien definieren. Wenn LOG ON nicht angegeben ist, wird eine Protokolldatei automatisch erstellt wird, wird die Größe beträgt 25 Prozent der Summe der Größen aller Dateien, die Daten für die Datenbank, oder 512 KB ist, welcher Wert größer ist. Diese Datei wird am Standard-Protokolldateispeicherort eingefügt. Informationen zu diesem Speicherort finden Sie unter [anzeigen oder Ändern der Standardspeicherorte für Daten- und Protokolldateien &#40; SQL Server Management Studio &#41; ](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
 LOG ON kann nicht in einer Datenbankmomentaufnahme angegeben werden.  
  
 COLLATE *Collation_name*  
 Gibt die Standardsortierung für die Datenbank an. Als Sortierungsname kann entweder der Name einer Windows-Sortierreihenfolge oder ein SQL-Sortierungsname verwendet werden. Wenn keine Sortierung angegeben ist, wird der Datenbank die Standardsortierung der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zugewiesen. In einer Datenbankmomentaufnahme kann kein Sortierungsname angegeben werden.  
  
 Mit den Klauseln FOR ATTACH und FOR ATTACH_REBUILD_LOG kann kein Sortierungsname angegeben werden. Informationen dazu, wie die Sortierung einer angefügten Datenbank ändern, finden Sie auf diese [Microsoft-Website](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335).  
  
 Weitere Informationen zu den Windows- und SQL-Sortierungsnamen finden Sie unter [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
> [!NOTE]  
>  Eigenständige Datenbanken werden anders sortiert als nicht eigenständige Datenbanken. Finden Sie unter [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md) für Weitere Informationen.  
  
 MIT \<Option >  
 -   **\<Filestream_options >** 
  
     NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | VOLLSTÄNDIGE}  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
     Gibt die Ebene des nicht transaktionalen FILESTREAM-Zugriffs auf die Datenbank an.  
  
    |Wert|Beschreibung|  
    |-----------|-----------------|  
    |OFF|Nicht transaktionaler Zugriff ist deaktiviert.|  
    |READONLY|FILESTREAM-Daten in dieser Datenbank können von nicht transaktionalen Prozessen gelesen werden.|  
    |FULL|Der vollständige nicht transaktionale Zugriff auf FILESTREAM-FileTables ist aktiviert.|  
  
     DIRECTORY_NAME = \<Directory_name > **betrifft**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     Ein Windows-kompatibler Verzeichnisname. Dieser Name sollte für alle Database_Directory-Namen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz eindeutig sein. Bei Eindeutigkeitsvergleichen wird die Groß-/Kleinschreibung nicht beachtet, unabhängig von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortiereinstellungen. Diese Option sollte vor dem Erstellen einer FileTable in dieser Datenbank festgelegt werden.  
  
 Die folgenden Optionen sind nur zulässig, wenn CONTAINMENT auf PARTIAL festgelegt wurde. Wenn CONTAINMENT auf NONE festgelegt wird, treten Fehler auf.  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<Lcid > | \<Sprachenname > | \<Sprachenalias >**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<Lcid > | \<Sprachenname > | \<Sprachenalias >**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = {DEAKTIVIEREN | ON}**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS AN = {DEAKTIVIEREN | ON}**  
  
**Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = {2049 | \<beliebiges Jahr zwischen 1753 und 9999 >}**  
  
     Vier Ziffern, die ein Jahr darstellen. Der Standardwert lautet 2049. Finden Sie unter [konfigurieren two Digit Year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) für eine vollständige Beschreibung dieser Option.  
  
-   **DB_CHAINING {DEAKTIVIEREN | ON}**  
  
     Wenn ON angegeben wird, kann die Datenbank Quelle oder Ziel einer datenbankübergreifenden Besitzverkettung sein.  
  
     Wenn OFF festgelegt ist, darf die Datenbank nicht Teil einer datenbankübergreifenden Besitzverkettung sein. Der Standardwert ist OFF.  
  
    > [!IMPORTANT]  
    >  Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erkennt diese Einstellung, wenn die Datenbankübergreifende Besitzverkettung-Serveroption deaktiviert (0 bzw. OFF) ist. Wenn für Datenbankübergreifende Besitzverkettung der Wert 1 (ON) festgelegt ist, können alle Benutzerdatenbanken unabhängig vom Wert dieser Option Teile von datenbankübergreifenden Besitzketten sein. Diese Option wird festgelegt, mit [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
     Sie müssen Mitglied der festen Serverrolle sysadmin sein, um diese Option festlegen zu können. Die Option DB_CHAINING kann auf folgenden Systemdatenbanken nicht festgelegt werden: master, model, tempdb.  
  
-   **TRUSTWORTHY {DEAKTIVIEREN | ON}**  
  
     Wenn ON angegeben wird, können Datenbankmodule (z. B. Sichten, benutzerdefinierte Funktionen oder gespeicherte Prozeduren), die den Identitätswechselkontext verwenden, auf Ressourcen außerhalb der Datenbank zugreifen.  
  
     Wenn OFF angegeben wird, können Datenbankmodule in einem Identitätswechselkontext nicht auf Ressourcen außerhalb der Datenbank zugreifen. Der Standardwert ist OFF.  
  
     TRUSTWORTHY wird auf OFF festgelegt, wenn die Datenbank angefügt wird.  
  
     Standardmäßig ist TRUSTWORTHY für alle Systemdatenbanken mit Ausnahme der msdb-Datenbank auf OFF festgelegt. Für die model-Datenbank und für die tempdb-Datenbank kann der Wert nicht geändert werden. Für die master-Datenbank sollten Sie die Option TRUSTWORTHY niemals auf ON festlegen.  
  
     Sie müssen Mitglied der festen Serverrolle sysadmin sein, um diese Option festlegen zu können.  
  
 FOR ATTACH [WITH \< Attach_database_option >] Gibt an, die von der Datenbankerstellung [Anfügen](../../relational-databases/databases/database-detach-and-attach-sql-server.md) eines vorhandenen Satzes von Betriebssystemdateien. Es muss eine \<Filespec > Eintrag, der die primäre Datei angibt. Der einzige andere \<Filespec > Einträge erforderlich getroffenen für alle Dateien, die über einen anderen Pfad als wenn die Datenbank beim Erstellen oder letzten anhängen. Ein \<Filespec > Eintrag für diese Dateien angegeben werden.  
  
 Für FOR ATTACH ist Folgendes erforderlich:  
  
-   Alle Datendateien (MDF und NDF) müssen verfügbar sein.  
  
-   Wenn mehrere Protokolldateien vorhanden sind, müssen alle verfügbar sein.  
  
 Wenn eine Datenbank im Lese-/Schreibmodus eine einzige Protokolldatei hat, die derzeit nicht verfügbar ist, und wenn die Datenbank vor dem Anfügen heruntergefahren wurde und keine Benutzer oder offene Transaktionen vorhanden sind, dann wird mit FOR ATTACH automatisch die Protokolldatei neu erstellt und die primäre Datei aktualisiert. Im Gegensatz dazu kann für eine schreibgeschützte Datenbank das Protokoll nicht neu erstellt werden, da das Hochladen der primären Datei nicht möglich ist. Aus diesem Grund, wenn Sie eine schreibgeschützte Datenbank mit einem Protokoll, die nicht verfügbar ist anfügen, müssen Sie die Protokolldateien oder die Dateien in der FOR ATTACH-Klausel bereitstellen.  
  
> [!NOTE]  
>  Eine Datenbank, die in einer neueren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt wurde, kann in früheren Versionen nicht angefügt werden.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden alle Volltextdateien, die zur angefügten Datenbank gehören, mit der Datenbank angefügt. Geben Sie den neuen Speicherort ohne Betriebssystem-Dateinamen der Volltextdatei an, um einen neuen Pfad für den Volltextkatalog anzugeben. Weitere Informationen finden Sie in Abschnitt "Beispiele".  
  
 Anfügen einer Datenbank, die in einer FILESTREAM-Option "Namen des Verzeichnisses" enthält einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz fordert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu überprüfen, ob der Database_Directory-Name eindeutig ist. Wenn sie nicht der Fall ist, anzufügen tritt der Fehler "FILESTREAM Database_Directory-Name \<Name > ist in dieser SQLServer-Instanz nicht eindeutig". Zur Vermeidung dieses Fehlers den optionalen Parameter *Directory_name*, sollte für diesen Vorgang übergeben werden.  
  
 FOR ATTACH kann nicht in einer Datenbank-Momentaufnahme angegeben werden.  
  
 FOR ATTACH kann die RESTRICTED_USER-Option angeben. RESTRICTED_USER ermöglicht nur Mitgliedern der festen Datenbankrolle db_owner und der festen Serverrollen dbcreator und sysadmin eine Verbindung mit der Datenbank, begrenzt jedoch nicht deren Anzahl. Versuche von nicht qualifizierten Benutzern werden abgelehnt.  
  
 Wenn die Datenbank verwendet [!INCLUDE[ssSB](../../includes/sssb-md.md)], verwenden Sie die WITH \<Service_broker_option > in der FOR ATTACH-Klausel: 
  
 \<Service_broker_option > Steuerelemente [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Nachrichtenübermittlung und den [!INCLUDE[ssSB](../../includes/sssb-md.md)] Bezeichner für die Datenbank. [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Optionen können nur bei Verwendung der FOR ATTACH-Klausel angegeben werden.  
  
 ENABLE_BROKER  
 Gibt an, dass [!INCLUDE[ssSB](../../includes/sssb-md.md)] für die angegebene Datenbank aktiviert ist. D. h. die Nachrichtenübermittlung ist gestartet und Is_broker_enabled auf festgelegt ist "true" in der sys.databases-Katalogsicht. Die Datenbank behält den vorhandenen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner bei.  
  
 NEW_BROKER  
 Erstellt einen neuen Wert für service_broker_guid in sys.databases und in der wiederhergestellten Datenbank und beendet alle Konversationsendpunkte mit einem Cleanup. Der Broker ist aktiviert, es wird jedoch keine Meldung an die Remote-Konversationsendpunkte gesendet. Jede Route, die auf den alten [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner verweist, muss mit dem neuen Bezeichner neu erstellt werden.  
  
 ERROR_BROKER_CONVERSATIONS  
 Beendet alle Konversationen mit einem Fehler, der angibt, dass die Datenbank angefügt oder wiederhergestellt wird. Der Broker ist deaktiviert, bis dieser Vorgang abgeschlossen ist, und wird dann aktiviert. Die Datenbank behält den vorhandenen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Bezeichner bei.  
  
 Berücksichtigen Sie Folgendes, wenn Sie eine replizierte Datenbank anfügen, die kopiert statt getrennt wurde:  
  
-   Wenn Sie die Datenbank an die gleiche Serverinstanz und -version wie die ursprüngliche Datenbank anfügen, sind keine weiteren Schritte erforderlich.  
  
-   Wenn Sie die Datenbank mit der gleichen Serverinstanz anfügen, aber Sie müssen mit einer aktualisierten Version ausführen [Sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) auf die Replikation zu aktualisieren, nachdem der Anfügevorgang abgeschlossen wurde.  
  
-   Wenn Sie die Datenbank an eine andere Serverinstanz unabhängig von der Version anfügen müssen Sie ausführen [Sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) zum Entfernen der Replikation, nachdem der Anfügevorgang abgeschlossen wurde.  
  
> [!NOTE]  
>  Anfügen der **Vardecimal** Speicherformat, aber die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] muss auf mindestens aktualisiert werden [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2. Sie können keine Datenbank mit "vardecimal"-Speicherformat an eine frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anfügen. Weitere Informationen zu den **Vardecimal** Speicherformat, finden Sie unter [Datenkomprimierung](../../relational-databases/data-compression/data-compression.md).  
  
 Wird eine Datenbank zum ersten Mal an eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angefügt oder wiederhergestellt, ist noch keine Kopie des Datenbank-Hauptschlüssels (verschlüsselt vom Diensthauptschlüssel) auf dem Server gespeichert. Der Datenbank-Hauptschlüssel (Database Master Key, DMK) muss mithilfe der Anweisung **OPEN MASTER KEY** entschlüsselt werden. Nachdem der Datenbank-Hauptschlüssel entschlüsselt wurde, können Sie für die Zukunft die automatische Entschlüsselung aktivieren, indem Sie die Anweisung **ALTER MASTER KEY REGENERATE** verwenden. Auf diese Weise können Sie eine Kopie des mit dem Diensthauptschlüssel (Service Master Key, SMK) verschlüsselten Datenbank-Hauptschlüssels für den Server bereitstellen. Wenn eine Datenbank von einer früheren Version aktualisiert wurde, sollte der DMK neu generiert werden, damit er den neueren AES-Algorithmus verwendet. Weitere Informationen zum Neugenerieren des DMK finden Sie unter [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md). Die zum Neugenerieren des DMK zum Upgrade auf AES erforderliche Zeit hängt von der Anzahl der Objekte ab, die durch den DMK geschützt werden. Der DMK muss nur einmal auf AES aktualisiert und neu generiert werden. Dies hat keine Auswirkungen auf zukünftige Neugenerierungen im Rahmen einer Schlüsselrotationsstrategie. Informationen zum Aktualisieren einer Datenbank mithilfe von anfügen, finden Sie unter [Upgrade einer Datenbank durch Trennen und Anfügen von Datenbanken &#40; Transact-SQL &#41; ](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md).  
  
 **Sicherheitshinweis** es wird empfohlen, dass Sie keine Datenbanken aus unbekannten oder nicht vertrauenswürdigen Quellen anfügen. Solche Datenbanken können bösartigen Code enthalten, der möglicherweise unbeabsichtigten [!INCLUDE[tsql](../../includes/tsql-md.md)] -Code ausführt oder Fehler verursacht, indem er das Schema oder die physische Datenbankstruktur ändert. Bevor Sie eine Datenbank aus einer unbekannten oder nicht vertrauenswürdigen Quelle verwenden, führen Sie [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) für die Datenbank auf einem nichtproduktionsserver, und überprüfen Sie außerdem den Code, z. B. gespeicherte Prozeduren oder anderen benutzerdefinierten Code, in der Datenbank.  
  
> [!NOTE]  
>  Die **TRUSTWORTHY** und **DB_CHAINING** Optionen haben keinen Einfluss auf, wenn eine Datenbank anfügen.  
  
 FOR ATTACH_REBUILD_LOG  
 Gibt an, dass die Datenbank durch Anfügen eines vorhandenen Satzes von Betriebssystemdateien erstellt wird. Diese Option ist auf Datenbanken mit Lese-/Schreibzugriff beschränkt. Es muss ein  *\<Filespec >* Eintrag, der die primäre Datei angibt. Wenn eines oder mehrere Transaktionsprotokolle fehlen, wird das Protokoll neu erstellt. Der ATTACH_REBUILD_LOG erstellt automatisch eine neue, 1 MB-Protokolldatei. Diese Datei wird am Standard-Protokolldateispeicherort eingefügt. Informationen zu diesem Speicherort finden Sie unter [anzeigen oder Ändern der Standardspeicherorte für Daten- und Protokolldateien &#40; SQL Server Management Studio &#41; ](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
> [!NOTE]  
>  Wenn die Protokolldateien verfügbar sind, verwendet [!INCLUDE[ssDE](../../includes/ssde-md.md)] diese Dateien und erstellt nicht die Protokolldateien neu.  
  
 Für FOR ATTACH_REBUILD_LOG ist Folgendes erforderlich:  
  
-   Ein fehlerfreies Herunterfahren der Datenbank.  
  
-   Alle Datendateien (MDF und NDF) müssen verfügbar sein.  
  
> [!IMPORTANT]  
>  Mit diesem Vorgang wird die Protokollsicherungskette unterbrochen. Wir empfehlen, nach Abschluss dieses Vorgangs eine vollständige Datenbanksicherung auszuführen. Weitere Informationen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
 In der Regel wird FOR ATTACH_REBUILD_LOG verwendet, wenn Sie eine Datenbank mit Lese-/Schreibzugriff mit einem großen Protokoll auf einen anderen Server kopieren, auf dem die Kopie hauptsächlich oder ausschließlich für Lesevorgänge verwendet wird und deshalb weniger Speicherplatz für das Protokoll benötigt wird, als bei der ursprünglichen Datenbank.  
  
 FOR ATTACH_REBUILD_LOG kann nicht auf einer Datenbank-Momentaufnahme angegeben werden.  
  
 Weitere Informationen über das Anfügen und Trennen von Datenbanken finden Sie unter [Datenbank trennen und Anfügen von Datenbanken &#40; SQLServer &#41; ](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 \<Filespec >  
 Steuert die Dateieigenschaften.  
  
 Namen *Logical_file_name*  
 Gibt den logischen Namen für die Datei an. NAME ist erforderlich, wenn FILENAME angegeben wird, dies gilt jedoch nicht, wenn eine der FOR ATTACH-Klauseln angegeben wird. Einer FILESTREAM-Dateigruppe kann der Name PRIMARY nicht zugewiesen werden.  
  
 *logical_file_name*  
 Der logische Dateiname, der in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beim Verweis auf die Datei verwendet wird. *Logical_file_name* muss in der Datenbank eindeutig sein und entsprechen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md). Der Name kann eine Zeichen- oder Unicode-Konstante oder ein regulärer oder Begrenzungsbezeichner sein.  
  
 FILENAME { **"***logische***"** | **"***Filestream_path* **'** }  
 Gibt einen Betriebssystem-Dateinamen (physischer Dateiname) an.  
  
 **"** *logische* **"**  
 Der Pfad und der Dateiname, die vom Betriebssystem beim Erstellen der Datei verwendet werden. Die Datei muss sich auf einem der folgenden Geräten bzw. Netzwerken befinden: auf dem lokalen Server, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist, in einem SAN (Storage Area Network) oder in einem Netzwerk auf iSCSI-Basis. Der angegebene Pfad muss bereits vorhanden sein, bevor die CREATE DATABASE-Anweisung ausgeführt wird. Weitere Informationen finden Sie im Abschnitt mit Hinweisen unter "Datenbankdateien und Dateigruppen".  
  
 Die Parameter SIZE, MAXSIZE und FILEGROWTH können festgelegt werden, wenn ein UNC-Pfad für die Datei angegeben wird.  
  
 Wenn die Datei auf einer Rawpartition befindet *logische* müssen nur den Laufwerkbuchstaben einer vorhandenen Rawpartition angeben. Auf einer Rawpartition kann nur eine einzige Datendatei erstellt werden.  
  
 Datendateien sollten nicht in komprimierten Dateisystemen abgelegt werden, es sei denn, alle Dateien sind schreibgeschützte sekundäre Dateien oder die Datenbank ist schreibgeschützt. Protokolldateien sollten niemals in komprimierten Dateisystemen abgelegt werden.  
  
 **"** *Filestream_path* **"**  
 Für eine FILESTREAM-Dateigruppe verweist FILENAME auf einen Pfad, wo FILESTREAM-Daten gespeichert werden. Der Pfad muss bis zum letzten Ordner vorhanden sein, und der letzte Ordner darf nicht vorhanden sein. Wenn Sie z. B. den Pfad C:\MyFiles\MyFilestreamData angeben, muss C:\MyFiles vor der Ausführung von ALTER DATABASE vorhanden sein, der Ordner MyFilestreamData muss jedoch noch nicht existieren.  
  
 Die Dateigruppe und die Datei (`<filespec>`) müssen in derselben Anweisung erstellt werden.  
  
 Die Eigenschaften SIZE und FILEGROWTH gelten nicht für eine FILESTREAM-Dateigruppe.  
  
 Größe *Größe*  
 Gibt die Größe der Datei an.  
  
 Größe nicht angegeben, wann die *logische* als UNC-Pfad angegeben ist. SIZE gilt nicht für eine FILESTREAM-Dateigruppe.  
  
 *Größe*  
 Die Anfangsgröße der Datei.  
  
 Wenn *Größe* nicht angegeben wird, für die primäre Datei der [!INCLUDE[ssDE](../../includes/ssde-md.md)] verwendet die Größe der primären Datei in der Model-Datenbank. Die Standardgröße des Modells liegt bei 8 MB (beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) oder 1 MB (für frühere Versionen). Wenn eine sekundäre Datendatei oder Protokolldatei angegeben wird, aber *Größe* für die Datei nicht angegeben ist die [!INCLUDE[ssDE](../../includes/ssde-md.md)] macht die Datei 8 MB (beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) oder 1 MB (für frühere Versionen). Die für die primäre Datei angegebene Größe muss mindestens der Größe der primären Datei der model-Datenbank entsprechen.  
  
 Es kann das Suffix Kilobyte (KB), Megabyte (MB), Gigabyte (GB) oder Terabyte (TB) verwendet werden. Die Standardeinheit ist MB. Geben Sie eine ganze Zahl; Verwenden Sie keine Dezimalzahl. *Größe* ist ein Ganzzahlwert. Verwenden Sie für Werte größer als 2.147.483.647 größere Einheiten.  
  
 MAXSIZE *Max_size*  
 Gibt die maximale Größe an, auf die die Datei vergrößert werden kann. MAXSIZE nicht angegeben, wann die *logische* als UNC-Pfad angegeben ist.  
  
 *max_size*  
 Die maximale Dateigröße. Die Suffixe KB, MB, GB und TB können verwendet werden. Die Standardeinheit ist MB. Geben Sie eine ganze Zahl; Verwenden Sie keine Dezimalzahl. Wenn *Max_size* nicht angegeben ist, wird die Datei vergrößert werden, bis der Datenträger voll ist. *Max_size* ist ein Ganzzahlwert. Verwenden Sie für Werte größer als 2.147.483.647 größere Einheiten.  
  
 UNLIMITED  
 Gibt an, dass die Größe der Datei so lange zunehmen kann, bis auf dem Datenträger kein Speicherplatz mehr verfügbar ist. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gilt für eine Protokolldatei, für die keine Größenbeschränkung festgelegt ist, eine Maximalgröße von 2 TB und für eine Datendatei eine Maximalgröße von 16 TB.  
  
> [!NOTE]  
>  Wenn diese Option für einen FILESTREAM-Container angegeben wird, gilt keine Maximalgröße. Die Dateigröße erhöht sich so lange, bis der Datenträger voll ist.  
  
 FILEGROWTH *Growth_increment*  
 Gibt das automatische Dateivergrößerungs-Inkrement an. Die FILEGROWTH-Einstellung für eine Datei darf die MAXSIZE-Einstellung nicht überschreiten. FILEGROWTH nicht angegeben, wann die *logische* als UNC-Pfad angegeben ist. FILEGROWTH gilt nicht für eine FILESTREAM-Dateigruppe.  
  
 *growth_increment*  
 Die Menge an Speicherplatz, die der Datei hinzugefügt wird, wenn neuer Speicherplatz erforderlich wird.  
  
 Der Wert kann in MB, KB, GB, TB oder Prozent (%) angegeben werden. Bei Zahlen ohne Angabe von MB, KB oder % wird standardmäßig MB verwendet. Wenn der Wert in Prozent angegeben wird, ist die growth_increment-Größe der angegebene Prozentsatz der Dateigröße zum Zeitpunkt der Vergrößerung. Die angegebene Größe wird auf den nächsten durch 64 KB gerundet, und der Mindestwert beträgt 64 KB.  
  
 Der Wert 0 zeigt an, dass die automatische Vergrößerung deaktiviert ist und kein zusätzlicher Platz zulässig ist.  
  
 Ist FILEGROWTH nicht angegeben ist, sind die Standardwerte:  
  
|Version|Standardwerte|  
|-------------|--------------------|  
|Anfang[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Data 64 MB. Protokolldateien 64 MB.|  
|Anfang[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Data 1 MB. Protokolldateien Sie 10 %.|  
|Vor dem[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|Daten 10 %. Protokolldateien Sie 10 %.|  
  
 \<Dateigruppe >  
 Steuert die Dateigruppeneigenschaften. Kann nicht in einer Datenbankmomentaufnahme angegeben werden.  
  
 DATEIGRUPPE *Filegroup_name*  
 Der logische Name der Dateigruppe.  
  
 *filegroup_name*  
 *Filegroup_name* muss in der Datenbank eindeutig sein und darf nicht die vom System bereitgestellten Namen PRIMARY bzw. primary_log besitzen. Der Name kann eine Zeichen- oder Unicode-Konstante oder ein regulärer oder Begrenzungsbezeichner sein. Der Name muss den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 CONTAINS FILESTREAM  
 Gibt an, dass die Dateigruppe FILESTREAM-BLOBs (Binary Large Objects) im Dateisystem speichert.  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] über[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Gibt an, dass die Dateigruppe speicheroptimierte Daten im Dateisystem speichert. Weitere Informationen finden Sie unter [In-Memory OLTP &#40;Arbeitsspeicheroptimierung&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Nur eine MEMORY_OPTIMIZED_DATA-Dateigruppe ist pro Datenbank zulässig. Codebeispiele, die eine Dateigruppe zum Speichern von speicheroptimierten Daten zu erstellen, finden Sie unter [Erstellen einer speicheroptimierten Tabelle und einer systemintern kompilierten gespeicherten Prozedur](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
 DEFAULT  
 Gibt an, dass die benannte Dateigruppe die Standarddateigruppe in der Datenbank ist.  
  
 *database_snapshot_name*  
 Der Name der neuen Datenbankmomentaufnahme. Die Namen von Datenbankmomentaufnahmen müssen innerhalb einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eindeutig sein und den Regeln für Bezeichner entsprechen. *Database_snapshot_name* kann maximal 128 Zeichen sein.  
  
 ON **(** Namen  **=**  *Logical_file_name***,** FILENAME **= "**  *physischer Dateiname***")** [ **,**... *n* ]  
 Gibt für das Erstellen einer Datenbankmomentaufnahme eine Liste von Dateien in der Quelldatenbank an. Damit die Momentaufnahme funktionsfähig ist, müssen alle Datendateien einzeln angegeben werden. Protokolldateien sind jedoch für Datenbankmomentaufnahmen nicht zulässig. FILESTREAM-Dateigruppen werden von Datenbankmomentaufnahmen nicht unterstützt. Wenn eine FILESTREAM-Datendatei in eine CREATE DATABASE ON-Klausel eingeschlossen wird, schlägt die Anweisung fehl, und ein Fehler wird ausgelöst.  
  
 Beschreibungen der NAME und FILENAME sowie deren Werte finden Sie in der Beschreibung die entsprechende \<Filespec > Werte.  
  
> [!NOTE]  
>  Beim Erstellen einer Datenbank-Momentaufnahme, die andere \<Filespec > Optionen und das PRIMARY-Schlüsselwort sind nicht zulässig.  
  
 ALS SNAPSHOT OF *Name der Quelldatenbank*  
 Gibt an, dass die Datenbank, die erstellt eine Datenbankmomentaufnahme der Quelldatenbank gemäß *Name der Quelldatenbank*. Die Momentaufnahme- und Quelldatenbank müssen sich auf derselben Instanz befinden.  
  
 Weitere Informationen finden Sie im Abschnitt mit Hinweisen unter "Datenbankmomentaufnahmen".  
  
## <a name="remarks"></a>Hinweise  
 Die [master-Datenbank](../../relational-databases/databases/master-database.md) sollte gesichert werden, einrichten, wenn eine Benutzerdatenbank erstellt, geändert oder gelöscht wird.  
  
 Die CREATE DATABASE-Anweisung muss im Autocommitmodus (dem Standardmodus für die Transaktionsverwaltung) ausgeführt werden und ist in einer expliziten oder impliziten Transaktion nicht zulässig.  
  
 Sie können mit einer CREATE DATABASE-Anweisung eine Datenbank und die Dateien erstellen, in denen die Datenbank gespeichert ist. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implimiert die CREATE DATABASE-Anweisung, indem die folgenden Schritte ausgeführt werden:  
  
1.  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet eine Kopie der [Modelldatenbank](../../relational-databases/databases/model-database.md) zum Initialisieren der Datenbank und die zugehörigen Metadaten.  
  
2.  Der Datenbank wird eine Service Broker-GUID zugewiesen.  
  
3.  Dann füllt das [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Rest der Datenbank mit leeren Seiten auf, mit Ausnahme der Seiten mit internen Daten, in denen aufgezeichnet ist, wie der Speicherplatz in der Datenbank verwendet wird.  
  
 Maximal 32.767 Datenbanken können auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angegeben werden.  
  
 Jede Datenbank hat einen Besitzer, der besondere Aktivitäten in der Datenbank ausführen kann. Der Besitzer ist der Benutzer, der die Datenbank erstellt. Der Datenbankbesitzer kann geändert werden, mithilfe von [Sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md).  

Einige Funktionen hängen von Features oder Funktionen, die im Dateisystem für die vollständige Funktionalität einer Datenbank vorhanden. Einige Beispiele für Funktionen, die Datei System Funktionsgruppe abhängig sind:
- DBCC CHECKDB
- FileStream
- Onlinesicherungen Verwenden von VSS und Datei-Momentaufnahmen
- Erstellen von datenbankmomentaufnahmen
- Arbeitsspeicher Speicheroptimierte Datendateigruppe
   
## <a name="database-files-and-filegroups"></a>Datenbankdateien und Dateigruppen  
 Jede Datenbank verfügt über mindestens zwei Dateien über eine *Primärdatei* und ein *Transaktionsprotokolldatei*, und mindestens eine Dateigruppe. Für jede Datenbank können maximal 32.767 Dateien und 32.767 Dateigruppen angegeben werden.  
  
 Wenn Sie eine Datenbank erstellen, sollten Sie die Datendateien so groß wie möglich orientieren Sie sich an den maximal zu erwartenden Datenmengen, die Sie in der Datenbank zu erwarten  
  
 Wir empfehlen, dass Sie ein Storage Area Network (SAN), ein Netzwerk auf iSCSI-Basis oder einen lokal zugeordneten Datenträger für die Speicherung Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbankdateien verwenden, da bei dieser Konfiguration die Leistung und Zuverlässigkeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] optimiert werden.  
  
## <a name="database-snapshots"></a>Datenbank-Momentaufnahmen  
 Können Sie die CREATE DATABASE-Anweisung, erstellen Sie eine schreibgeschützte, statische Sicht einer *Datenbankmomentaufnahme* von der *Quelldatenbank*. Ein Datenbank-Momentaufnahme ist im Hinblick auf Transaktionen konsistent mit der Quelldatenbank zu dem Zeitpunkt, an dem die Momentaufnahme erstellt wurde. Für eine Quelldatenbank kann es mehrere Momentaufnahmen geben.  
  
> [!NOTE]  
>  Wenn Sie eine Datenbankmomentaufnahme erstellen, kann die CREATE DATABASE-Anweisung nicht auf Protokolldateien, Offlinedateien, Wiederherstellungsdateien und außer Kraft gesetzte Dateien verweisen.  
  
 Wenn das Erstellen einer Datenbankmomentaufnahme fehlschlägt, wird der Snapshot fehlerverdächtig und muss gelöscht werden. Weitere Informationen finden Sie unter [DROP DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Jede Momentaufnahme wird so lange persistent gespeichert, bis sie mit DROP DATABASE gelöscht wird.  
  
 Weitere Informationen finden Sie unter [Datenbankmomentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="database-options"></a>Datenbankoptionen  
 Mehrere Datenbankoptionen werden automatisch festgelegt, wenn Sie eine Datenbank erstellen. Eine Liste dieser Optionen finden Sie [ALTER DATABASE SET-Optionen &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="the-model-database-and-creating-new-databases"></a>Die model-Datenbank und das Erstellen neuer Datenbanken  
 Alle benutzerdefinierten Objekte in der [Modelldatenbank](../../relational-databases/databases/model-database.md) in alle neu erstellten Datenbanken kopiert werden. Sie können der model-Datenbank beliebige Objekte (z. B. Tabellen, Sichten, gespeicherte Prozeduren, Datentypen usw.) hinzufügen, die in allen neu erstellten Datenbanken enthalten sein sollen.  
  
 Wenn eine CREATE DATABASE *Database_name* Anweisung ohne zusätzliche Größenparameter angegeben wird die primäre Datendatei die gleiche Größe wie die primäre Datei in der Model-Datenbank vorgenommen.  
  
 Jede neue Datenbank erbt die Einstellungen der Datenbankoptionen von der model-Datenbank, es sei denn, FOR ATTACH ist angegeben. Z. B. die Option Automatisches Verkleinern der Datenbank festgelegt ist, um **"true"** im Modell und in allen neuen Datenbanken, die Sie erstellen. Wenn Sie die Optionen in der model-Datenbank ändern, werden diese neuen Einstellungen in jeder neu erstellten Datenbank verwendet. Änderungen in der model-Datenbank haben jedoch keine Auswirkungen auf vorhandene Datenbanken. Wenn FOR ATTACH in der CREATE DATABASE-Anweisung angegeben ist, erbt die neue Datenbank die Einstellungen der Datenbankoptionen der ursprünglichen Datenbank.  
  
## <a name="viewing-database-information"></a>Anzeigen von Datenbankinformationen  
 Sie können Katalogsichten, Systemfunktionen und gespeicherte Systemprozeduren verwenden, um Informationen zu Datenbanken, Dateien und Dateigruppen zurückzugeben. Weitere Informationen finden Sie unter [Systemsichten &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Berechtigung CREATE DATABASE, CREATE ANY DATABASE oder ALTER ANY DATABASE.  
  
 Zur Steuerung der Datenträgernutzung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird die Berechtigung zum Erstellen von Datenbanken in der Regel auf einige wenige Anmeldekonten beschränkt.  
  
 Im folgenden Beispiel wird dem Datenbankbenutzer Fay die Berechtigung zum Erstellen einer Datenbank erteilt.  
  
```  
USE master;  
GO  
GRANT CREATE DATABASE TO [Fay];  
GO  
```  
  
### <a name="permissions-on-data-and-log-files"></a>Berechtigungen für Daten und Protokolldateien  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Berechtigungen für die Daten und Protokolldateien der einzelnen Datenbanken festgelegt. Die folgenden Berechtigungen werden stets festgelegt, wenn die folgenden Vorgänge auf eine Datenbank angewendet werden:  
  
|||  
|-|-|  
|Erstellt|Ändern, um eine neue Datei hinzuzufügen|  
|Angefügt|Gesichert|  
|Getrennt|Wiederherstellen|  
  
 Durch die Berechtigungen wird verhindert, dass die Dateien versehentlich manipuliert werden, wenn sie sich in einem Verzeichnis mit offenen Berechtigungen befinden.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] legt keine Berechtigungen für Daten und Protokolldateien fest.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-database-without-specifying-files"></a>A. Erstellen einer Datenbank ohne Angabe von Dateien  
 Mit dem folgenden Beispiel werden die Datenbank `mytest` sowie eine entsprechende primäre Datei und Transaktionsprotokolldatei erstellt. Da die Anweisung keine \<Filespec > Elemente, die primäre Datenbankdatei ist die Größe der primären modelldatenbankdatei. Für das Transaktionsprotokoll wird der größere der beiden folgenden Werte festgelegt: 512 KB oder 25 Prozent der Größe der primären Datendatei. Da MAXSIZE nicht angegeben ist, können die Dateien so lange vergrößert werden, bis der gesamte verfügbare Speicherplatz auf dem Datenträger gefüllt ist. Dieses Beispiel zeigt auch, wie Sie die Datenbank mit dem Namen `mytest`, falls vorhanden, vor dem Erstellen der Datenbank `mytest` löschen.  
  
```  
USE master;  
GO  
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;  
GO  
-- Verify the database files and sizes  
SELECT name, size, size*1.0/128 AS [Size in MBs]   
FROM sys.master_files  
WHERE name = N'mytest';  
GO  
  
```  
  
### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>B. Erstellen einer Datenbank mit Angabe der Datendatei und der Transaktionsprotokolldatei  
 Im folgenden Beispiel wird die Datenbank mit dem Namen `Sales` erstellt. Da das PRIMARY-Schlüsselwort nicht verwendet wird, wird die erste Datei (`Sales_dat`) zur primären Datei. Da im SIZE-Parameter für die Datei `Sales_dat` weder MB noch KB angegeben ist, wird die Einheit MB verwendet und in Megabyte zugeordnet. Die `Sales_log` wird in Megabyte zugeordnet, weil das Suffix `MB` explizit im `SIZE` -Parameter angegeben ist.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. Erstellen einer Datenbank unter Angabe mehrerer Daten- und Transaktionsprotokolldateien  
 Mit dem folgenden Beispiel wir die `Archive`-Datenbank erstellt, die über drei Datendateien mit `100-MB` und zwei Transaktionsprotokolldateien mit `100-MB` verfügt. Die primäre Datei ist die erste Datei in der Liste und wird explizit mit dem `PRIMARY`-Schlüsselwort angegeben. Die Transaktionsprotokolldateien werden nach den `LOG ON`-Schlüsselwörtern angegeben. Beachten Sie die Erweiterungen, die für die Dateien in der Option `FILENAME` verwendet werden: `.mdf` wird für primäre Datendateien verwendet, `.ndf` wird für sekundäre Datendateien verwendet, und `.ldf` wird für Transaktionsprotokolldateien verwendet. In diesem Beispiel wird die Datenbank auf dem Laufwerk `D:` abgelegt, anstatt an demselben Speicherort wie die `master`-Datenbank.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Archive   
ON  
PRIMARY    
    (NAME = Arch1,  
    FILENAME = 'D:\SalesData\archdat1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch2,  
    FILENAME = 'D:\SalesData\archdat2.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch3,  
    FILENAME = 'D:\SalesData\archdat3.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20)  
LOG ON   
   (NAME = Archlog1,  
    FILENAME = 'D:\SalesData\archlog1.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
   (NAME = Archlog2,  
    FILENAME = 'D:\SalesData\archlog2.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20) ;  
GO  
```  
  
### <a name="d-creating-a-database-that-has-filegroups"></a>D. Erstellen einer Datenbank mit Dateigruppen  
 Im folgenden Beispiel wird die `Sales`-Datenbank erstellt, die über folgende Dateigruppen verfügt:  
  
-   Die primäre Dateigruppe mit den Dateien `Spri1_dat` und `Spri2_dat`. Die FILEGROWTH-Inkremente für diese Dateien werden mit `15%` angegeben.  
  
-   Eine Dateigruppe mit dem Namen `SalesGroup1` mit den Dateien `SGrp1Fi1` und `SGrp1Fi2`.  
  
-   Eine Dateigruppe mit dem Namen `SalesGroup2` mit den Dateien `SGrp2Fi1` und `SGrp2Fi2`.  
  
 In diesem Beispiel werden die Daten und Protokolldateien auf verschiedenen Datenträgern angeordnet, um die Leistung zu verbessern.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Sales  
ON PRIMARY  
( NAME = SPri1_dat,  
    FILENAME = 'D:\SalesData\SPri1dat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
( NAME = SPri2_dat,  
    FILENAME = 'D:\SalesData\SPri2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
FILEGROUP SalesGroup1  
( NAME = SGrp1Fi1_dat,  
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp1Fi2_dat,  
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
FILEGROUP SalesGroup2  
( NAME = SGrp2Fi1_dat,  
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp2Fi2_dat,  
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'E:\SalesLog\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="e-attaching-a-database"></a>E. Anfügen einer Datenbank  
 Im folgenden Beispiel wird die in Beispiel D erstellte `Archive`-Datenbank gelöst und dann mithilfe der `FOR ATTACH`-Klausel angefügt. `Archive` wurde so definiert, dass mehrere Daten- und Protokolldateien vorhanden sind. Da sich jedoch der Speicherort der Dateien seit ihrem Erstellen nicht geändert hat, muss nur die primäre Datei in der `FOR ATTACH`-Klausel angegeben werden. Ab Version [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] werden alle Volltextdateien, die zur angefügten Datenbank gehören, mit der Datenbank angefügt.  
  
```tsql  
USE master;  
GO  
sp_detach_db Archive;  
GO  
CREATE DATABASE Archive  
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')   
      FOR ATTACH ;  
GO  
```  
  
### <a name="f-creating-a-database-snapshot"></a>F. Erstellen einer Datenbankmomentaufnahme  
 Das folgende Beispiel erstellt die Datenbank-Momentaufnahme `sales_snapshot0600`. Da eine Datenbankmomentaufnahme schreibgeschützt ist, kann keine Protokolldatei angegeben werden. In Übereinstimmung mit der Syntax wird jede Datei in der Quelldatenbank angegeben, Dateigruppen werden nicht angegeben.  
  
 Die Quelldatenbank für dieses Beispiel ist die `Sales`-Datenbank, die in Beispiel D erstellt wurde.  
  
```tsql  
USE master;  
GO  
CREATE DATABASE sales_snapshot0600 ON  
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),  
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),  
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),  
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),  
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),  
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')  
AS SNAPSHOT OF Sales ;  
GO  
```  
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. Erstellen einer Datenbank, Angeben eines Sortierungsnamens und Angeben von Optionen  
 Im folgenden Beispiel wird die Datenbank mit dem Namen `MyOptionsTest` erstellt. Ein Sortierungsname wird angegeben, und für die Optionen `TRUSTYWORTHY` und `DB_CHAINING` wird `ON` festgelegt.  
  
```tsql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE French_CI_AI  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO  
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. Anhängen eines Volltextkatalogs, der verschoben wurde  
 Im folgenden Beispiel wird der Volltextkatalog `AdvWksFtCat` zusammen mit den Daten und Protokolldateien von `AdventureWorks2012` angefügt. In diesem Beispiel wird der Volltextkatalog vom Standardspeicherort an den neuen Speicherort `c:\myFTCatalogs` verschoben. Die Daten- und Protokolldateien bleiben an ihrem jeweiligen Standardspeicherort.  
  
```tsql  
USE master;  
GO  
--Detach the AdventureWorks2012 database  
sp_detach_db AdventureWorks2012;  
GO  
-- Physically move the full text catalog to the new location.  
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.  
CREATE DATABASE AdventureWorks2012 ON   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),  
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')  
FOR ATTACH;  
GO  
```  
  
### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>I. Erstellen einer Datenbank, die eine Zeilendateigruppe und zwei FILESTREAM-Dateigruppen angibt  
 Im folgenden Beispiel wird die `FileStreamDB`-Datenbank erstellt. Die Datenbank wird mit einer Zeilendateigruppe und zwei FILESTREAM-Dateigruppen erstellt. Jede Dateigruppe enthält eine Datei:  
  
-   `FileStreamDB_data` enthält Zeilendaten. Darin enthalten ist eine Datei `FileStreamDB_data.mdf` mit dem Standardpfad.  
  
-   `FileStreamPhotos` enthält FILESTREAM-Daten. Darin enthalten sind zwei FILESTREAM-Datencontainer: `FSPhotos` unter `C:\MyFSfolder\Photos` und `FSPhotos2` unter `D:\MyFSfolder\Photos`. Er ist als FILESTREAM-Standarddateigruppe gekennzeichnet.  
  
-   `FileStreamResumes` enthält FILESTREAM-Daten. Darin enthalten ist ein FILESTREAM-Datencontainer `FSResumes`, der sich unter `C:\MyFSfolder\Resumes` befindet.  
  
```tsql  
USE master;  
GO  
-- Get the SQL Server data path.  
DECLARE @data_path nvarchar(256);  
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)  
                  FROM master.sys.master_files  
                  WHERE database_id = 1 AND file_id = 1);  
  
 -- Execute the CREATE DATABASE statement.   
EXECUTE ('CREATE DATABASE FileStreamDB  
ON PRIMARY   
    (  
    NAME = FileStreamDB_data   
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''  
    ,SIZE = 10MB  
    ,MAXSIZE = 50MB  
    ,FILEGROWTH = 15%  
    ),  
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT  
    (  
    NAME = FSPhotos  
    ,FILENAME = ''C:\MyFSfolder\Photos''  
-- SIZE and FILEGROWTH should not be specified here.  
-- If they are specified an error will be raised.  
, MAXSIZE = 5000 MB  
    ),  
    (  
      NAME = FSPhotos2  
      , FILENAME = ''D:\MyFSfolder\Photos''  
      , MAXSIZE = 10000 MB  
     ),  
FILEGROUP FileStreamResumes CONTAINS FILESTREAM  
    (  
    NAME = FileStreamResumes  
    ,FILENAME = ''C:\MyFSfolder\Resumes''  
    )   
LOG ON  
    (  
    NAME = FileStream_log  
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''  
    ,SIZE = 5MB  
    ,MAXSIZE = 25MB  
    ,FILEGROWTH = 5MB  
    )'  
);  
GO  
```  
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. Erstellen einer Datenbank mit einer FILESTREAM-Dateigruppe mit mehreren Dateien  
 Im folgenden Beispiel wird die `BlobStore1`-Datenbank erstellt. Die Datenbank wird mit einer Zeilendateigruppe und einer FILESTREAM-Dateigruppe, `FS`, erstellt. Die FILESTREAM-Dateigruppe enthält die beiden Dateien `FS1` und `FS2`. Dann wird die Datenbank durch das Hinzufügen der dritten Datei `FS3` zur FILESTREAM-Dateigruppe geändert.  
  
```tsql  
USE master;  
GO  
  
CREATE DATABASE [BlobStore1]  
CONTAINMENT = NONE  
ON PRIMARY   
(   
    NAME = N'BlobStore1',   
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = UNLIMITED,  
    FILEGROWTH = 1MB  
),   
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT   
(  
    NAME = N'FS1',  
    FILENAME = N'C:\BlobStore\FS1',  
    MAXSIZE = UNLIMITED  
),   
(  
    NAME = N'FS2',  
    FILENAME = N'C:\BlobStore\FS2',  
    MAXSIZE = 100MB  
)  
LOG ON   
(  
    NAME = N'BlobStore1_log',  
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 1GB,  
    FILEGROWTH = 1MB  
);  
GO  
  
ALTER DATABASE [BlobStore1]  
ADD FILE  
(  
    NAME = N'FS3',  
    FILENAME = N'C:\BlobStore\FS3',  
    MAXSIZE = 100MB  
)  
TO FILEGROUP [FS];  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Anfügen und Trennen von Datenbanken &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Sp_changedbowner &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Sp_detach_db &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [Sp_removedbreplication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [Datenbank-Momentaufnahmen &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)   
 [Datenbanken](../../relational-databases/databases/databases.md)   
 [Binary Large Object &#40;Blob&#41; Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  

