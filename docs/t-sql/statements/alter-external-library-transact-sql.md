---
title: ALTER externe Bibliothek (Transact-SQL) | Microsoft Docs
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
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 541419770828e01cca82fb33ead1b22170f8e4f3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-library-transact-sql"></a>ALTER externe Bibliothek (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

Ändert vorhandene Library-Inhalt.  

## <a name="syntax"></a>Syntax

```
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
(CONTENT = { <client_library_specifier> | <library_bits> | NONE}
[, PLATFORM = WINDOWS )
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

Gibt den Namen einer vorhandenen Paket-Bibliothek. Bibliotheken beziehen sich auf den Benutzer. D. h. gelten Bibliotheksnamen innerhalb des Kontexts eines bestimmten Benutzers oder Besitzer eindeutig.

**owner_name**

Gibt den Namen des Benutzers oder der Rolle, der die externe Bibliothek besitzt.

**file_spec**

Gibt den Inhalt des Pakets für eine bestimmte Plattform. Nur eine Datei Artefakt plattformspezifischen wird unterstützt.

Die Datei kann in Form von ein lokaler Pfad oder ein Netzwerkpfad angegeben werden. Wenn Sie die Datenquellenoption angegeben wird, kann der Dateiname einen relativen Pfad in Bezug auf den verwiesen wird, im Container der `EXTERNAL DATA SOURCE`.

Optional kann eine Betriebssystemplattform für die Datei angegeben werden. Für jede Betriebssystemplattform für eine bestimmte Sprache oder die Common Language Runtime ist nur eine Datei Artefakt oder Inhalt zulässig.

**DATA_SOURCE = External_data_source_name**

Gibt den Namen der externen Datenquelle, die den Speicherort der Bibliotheksdatei enthält. Dieser Speicherort muss es sich um ein Azure-Blob-Speicherpfad verweisen. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](create-external-data-source-transact-sql.md).

**PLATTFORM = WINDOWS**

Gibt die Plattform für den Inhalt der Bibliothek. Dieser Wert ist erforderlich, wenn eine vorhandene Bibliotheksfreigabe zum Hinzufügen von einer anderen Plattform zu ändern. Windows ist die einzige unterstützte Plattform.

## <a name="remarks"></a>Hinweise

Für die Sprache R-Pakete müssen in Form von ZIP-Archivdateien mit vorbereitet werden die. ZIP-Erweiterung für Windows. Derzeit wird nur die Windows-Plattform unterstützt.  
Die `ALTER EXTERNAL LIBRARY` Anweisung uploads nur die Bits für die Bibliothek mit der Datenbank. Die geänderte Bibliothek ist nicht tatsächlich installiert, bis ein Benutzer ein externes Skript anschließend durch Ausführen ausführt [Sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="permissions"></a>Berechtigungen
Erfordert die `ALTER ANY EXTERNAL LIBRARY` Berechtigung. Benutzer, die eine externe Bibliothek erstellt haben kann, externe Bibliothek geändert werden.

## <a name="examples"></a>Beispiele

Im folgende Beispiel wird eine externe Bibliothek namens CustomPackage geändert.

```sql  
ALTER EXTERNAL LIBRARY customPackage 
SET 
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


## <a name="see-also"></a>Siehe auch  
[Erstellen von EXTERNEN Bibliothek (Transact-SQL)](create-external-library-transact-sql.md)
[löschen externe Bibliothek (Transact-SQL)](drop-external-library-transact-sql.md)  
[Sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[Sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

