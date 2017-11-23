---
title: Erstellen von EXTERNEN Bibliothek (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: 
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 8d0f700ba30b77e892b37e98c43996d6e654e7ea
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-external-library-transact-sql"></a>Erstellen von EXTERNEN Bibliothek (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

Hochladen von R-Pakete in einer Datenbank aus dem angegebenen Stream oder Dateipfad.

Diese Anweisung dient als einen generischen Mechanismus dar, für den Datenbankadministrator, Artefakte, die für alle neuen externen Language-Laufzeiten (R, Python, Java usw.) erforderlich sind und von unterstützten Betriebssystem-Plattformen hochladen [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Derzeit werden nur die R-Sprache und Windows-Plattform unterstützt.

## <a name="syntax"></a>Syntax

```
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: =  
  '[\\computer_name\]share_name\[path\]manifest_file_name'  
| '[local_path\]manifest_file_name'  
| '<relative_path_in_external_data_source>'  

<library_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```

### <a name="arguments"></a>Argumente

**library_name**

Die Datenbank beschränkt, die dem Benutzer werden Bibliotheken hinzugefügt. D. h. Bibliotheksnamen gelten als innerhalb des Kontexts eines bestimmten Benutzers oder Besitzer eindeutig und Bibliotheksnamen müssen pro Benutzer eindeutig sein. Zum Beispiel zwei Benutzer **RUser1** und **RUser2** können sowohl einzeln und separat hochladen die R-Bibliothek `ggplot2`.

**owner_name**

Gibt den Namen des Benutzers oder der Rolle, der die externe Bibliothek besitzt. Wird kein Wert angegeben, wird der aktuelle Benutzer zum Besitzer.

Der Besitz des Datenbankbesitzers Bibliotheken gelten global für die Datenbank und die Common Language Runtime. Das heißt, können Datenbankbesitzer Bibliotheken erstellen, die enthalten einen gemeinsamen Satz von Bibliotheken oder Pakete, die von vielen Benutzern gemeinsam genutzt werden. Wenn eine externe Bibliothek erstellt wird, die ein Benutzer außer dem `dbo` Benutzer, die externe Bibliothek ist für diesen Benutzer nur privat.

Wenn der Benutzer **RUser1** führt ein R-Skript den Wert des `libPath` kann mehrere Pfade enthalten. Der erste Pfad ist immer den Pfad zu der freigegebenen Bibliothek, die vom Datenbankbesitzer erstellt. Der zweite Teil des `libPath` gibt den Pfad mit Paketen, die einzeln nach hochgeladen **RUser1**.

**file_spec**

Gibt den Inhalt des Pakets für eine bestimmte Plattform. Nur eine Datei Artefakt plattformspezifischen wird unterstützt.

Die Datei kann in Form von einem lokalen Pfad oder ein Netzwerkpfad angegeben werden.

Optional kann eine Betriebssystemplattform für die Datei angegeben werden. Für jede Betriebssystemplattform für eine bestimmte Sprache oder die Common Language Runtime ist nur eine Datei Artefakt oder Inhalt zulässig.

**library_bits**

Gibt den Inhalt des Pakets als hexadezimale Literal, wie Assemblys an. Diese Option ermöglicht Benutzern das Erstellen einer Bibliothek, um die Bibliothek zu ändern, wenn sie über die erforderlichen Berechtigungen verfügt, jedoch keine dateipfadzugriff einen beliebigen Ordner aus, auf der Server zugreifen kann.

**PLATTFORM = WINDOWS**

Gibt die Plattform für den Inhalt der Bibliothek. Der Standardwert ist die Hostplattform, auf der SQL Server ausgeführt wird. Aus diesem Grund wird nicht der Benutzer zum Angeben des Werts verfügen. Es ist erforderlich, im Fall einer, in denen mehrere Plattformen unterstützt werden, oder der Benutzer muss eine andere Plattform angeben. Windows ist die einzige unterstützte Plattform.

## <a name="remarks"></a>Hinweise

Für die Sprache R, wenn eine Datei zu verwenden, müssen Pakete vorbereitet werden in Form von ZIP-Archivdateien mit der. ZIP-Erweiterung für Windows. Derzeit wird nur die Windows-Plattform unterstützt.

Die `CREATE EXTERNAL LIBRARY` Anweisung uploads nur die Bits für die Bibliothek mit der Datenbank. Die Bibliothek ist nicht tatsächlich installiert, bis ein Benutzer ein externes Skript anschließend durch Ausführen ausführt [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  

Bibliotheken, die hochgeladen werden, um die Instanz können entweder öffentlich oder privat sein. Wenn die Bibliothek, von einem Mitglied der erstellt wird `dbo`, die Bibliothek ist öffentlich und kann mit allen Benutzern gemeinsam verwendet werden. Andernfalls ist die Bibliothek für diesen Benutzer nur privat.

Sie können keine Blobs als Datenquelle in der SQL Server-2017-Version.

## <a name="permissions"></a>Berechtigungen

Erfordert die `CREATE ANY EXTERNAL LIBRARY` Berechtigung.

So ändern Sie eine Bibliothek erfordert der separate Berechtigung `ALTER ANY EXTERNAL LIBRARY`.

## <a name="examples"></a>Beispiele

### <a name="a-add-an-external-library-to-a-database"></a>A. Fügen Sie eine externe Bibliothek in einer Datenbank  

Im folgenden Beispiel wird eine externe Bibliothek namens CustomPackage in einer Datenbank.

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

Nachdem die Bibliothek mit der Instanz erfolgreich hochgeladen wurde, ein Benutzer führt die `sp_execute_external_script` so verwenden Sie die Bibliothek zu installieren.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
'
```

### <a name="b-installing-packages-with-dependencies"></a>B. Installieren von Paketen mit Abhängigkeiten

Wenn `packageB` abhängt `packageA`, befolgen Sie dann die folgenden allgemeinen Prinzipien:

+ Hochladen der Zielpaket und seine Abhängigkeiten.

    Beide Pakete müssen in einem Ordner befinden, die an den Server zugänglich ist.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    
    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    ```

+ Abhängigkeiten werden zuerst installiert.

    Wenn ein erforderliches Paket `packageA` wurde bereits hochgeladen, auf die Instanz, sie müssen nicht installiert wurde getrennt. Erforderliches Paket `packageA` wird installiert werden, wenn `sp_execute_external_script` wird zuerst ausgeführt werden, um die Paketinstallation `packageB`.

    Jedoch, wenn das benötigte Paket `packageA`, ist nicht verfügbar, die Installation des Pakets Ziel `packageB` schlägt fehl.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load packageB
    library(packageB)
    # call customPackageBFunc
    OutputDataSet <- customPackageBFunc()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. Eine Bibliothek aus einem Bytestream zu erstellen.

Das folgende Beispiel erstellt eine Bibliothek durch Übergabe Bits als eine hexadezimale Literale aktualisiert.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

### <a name="d-change-an-existing-package-library"></a>D. Ändern einer vorhandenen Paket-Bibliothek

Die `ALTER EXTERNAL LIBRARY` DDL-Anweisung kann verwendet werden, neue Bibliotheksinhalte hinzufügen oder Ändern von vorhandenen Library-Inhalt. Zum Ändern einer vorhandenen Bibliotheksfreigabe erfordert die `ALTER ANY EXTERNAL LIBRARY` Berechtigung.

Weitere Informationen finden Sie unter [externe Bibliothek ALTER](alter-external-library-transact-sql.md).

### <a name="e-delete-a-package-library"></a>E. Löschen einer Paket-Bibliothek

Um eine Bibliothek Paket aus der Datenbank zu löschen, führen Sie die Anweisung aus:

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> Im Gegensatz zu anderen `DROP` Anweisungen in [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], diese Anweisung unterstützt einen optionalen Parameter, der angibt, der Autorität für die Benutzer. Diese Option kann Benutzer mit Rollen auf den Besitz von normalen Benutzern hochgeladene Bibliotheken zu löschen.

## <a name="see-also"></a>Siehe auch

[ALTER externe Bibliothek (Transact-SQL)](alter-external-library-transact-sql.md)  
[Löschen von EXTERNEN Bibliothek (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
