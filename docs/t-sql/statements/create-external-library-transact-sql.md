---
title: Erstellen von EXTERNEN Bibliothek (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f11a6b7633be392e1f789e12c43f2e5d6e56b47
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

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

**PLATTFORM = WINDOWS**

Gibt die Plattform für den Inhalt der Bibliothek. Der Standardwert ist die Hostplattform, auf der SQL Server ausgeführt wird. Aus diesem Grund wird nicht der Benutzer zum Angeben des Werts verfügen. Es ist erforderlich, im Fall einer, in denen mehrere Plattformen unterstützt werden, oder der Benutzer muss eine andere Plattform angeben. Windows ist die einzige unterstützte Plattform.

## <a name="remarks"></a>Hinweise

Für die Sprache R-Pakete müssen in Form von ZIP-Archivdateien mit vorbereitet werden die. ZIP-Erweiterung für Windows. Derzeit wird nur die Windows-Plattform unterstützt.  

Die `CREATE EXTERNAL LIBRARY` Anweisung uploads nur die Bits für die Bibliothek mit der Datenbank. Die Bibliothek ist nicht tatsächlich installiert, bis ein Benutzer ein externes Skript anschließend durch Ausführen ausführt [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  

## <a name="permissions"></a>Berechtigungen  
Erfordert die `CREATE EXTERNAL LIBRARY` Berechtigung.  

## <a name="examples"></a>Beispiele

### <a name="a-add-an-external-library-to-a-database"></a>A. Fügen Sie eine externe Bibliothek in einer Datenbank  
Im folgenden Beispiel wird eine externe Bibliothek namens CustomPackage in einer Datenbank.   
```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  
Führen Sie dann die `sp_execute_external_script` so verwenden Sie die Bibliothek zu installieren.  
```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)

# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
with result sets (([result] int));    
```

### <a name="b-installing-packages-with-dependencies"></a>B. Installieren von Paketen mit Abhängigkeiten

Wenn `packageB` abhängt `packageA`, und klicken Sie dann den Code, z. B. diese allgemeine Prinzipale folgt:   
```
CREATE EXTERNAL LIBRARY packageA 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R'); 

CREATE EXTERNAL LIBRARY packageB FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R');
```

`packageA`und `packageB` sind sowohl bei der Installation `sp_execute_external_script` zuerst ausgeführt wird.   
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

Damit dies funktioniert muss der Ordner, in dem die Pakete gespeichert sind, für den Server zugänglich sein. 

### <a name="change-an-existing-package-library"></a>Ändern einer vorhandenen Paket-Bibliothek

Die `ALTER EXTERNAL LIBRARY` DDL-Anweisung kann verwendet werden, neue Bibliotheksinhalte hinzufügen oder Ändern von vorhandenen Library-Inhalt.   

### <a name="delete-a-package-library"></a>Löschen einer Paket-Bibliothek

Um eine Bibliothek Paket aus der Datenbank zu löschen, führen Sie die Anweisung aus:

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

> [!NOTE]
> Im Gegensatz zu anderen `DROP` Anweisungen in [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)], diese Anweisung unterstützt einen optionalen Parameter, der angibt, der Autorität für die Benutzer. Diese Option kann Benutzer mit Rollen auf den Besitz von normalen Benutzern hochgeladene Bibliotheken zu löschen. 

## <a name="see-also"></a>Siehe auch  
[ALTER externe Bibliothek (Transact-SQL)](alter-external-library-transact-sql.md)  
[Löschen von EXTERNEN Bibliothek (Transact-SQL)](drop-external-library-transact-sql.md)  
[Sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[Sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

