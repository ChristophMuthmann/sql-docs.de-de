---
title: ALTER externe Bibliothek (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: d0fe9adc1907d773bdfddda38b5900774ec97deb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-external-library-transact-sql"></a>ALTER externe Bibliothek (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Ändert den Inhalt einer vorhandenen externen Paket-Bibliothek.

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

**DATA_SOURCE = external_data_source_name**

Gibt den Namen der externen Datenquelle, die den Speicherort der Bibliotheksdatei enthält. Dieser Speicherort muss es sich um ein Azure-Blob-Speicherpfad verweisen. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](create-external-data-source-transact-sql.md).

> [!IMPORTANT] 
> Blobs sind derzeit nicht als Datenquelle in der SQL Server-2017-Version unterstützt.

**library_bits**

Gibt den Inhalt des Pakets als hexadezimale Literal, wie Assemblys an. Diese Option ermöglicht Benutzern das Erstellen einer Bibliothek, um die Bibliothek zu ändern, wenn sie über die erforderlichen Berechtigungen verfügt, jedoch keine dateipfadzugriff einen beliebigen Ordner aus, auf der Server zugreifen kann.

**PLATTFORM = WINDOWS**

Gibt die Plattform für den Inhalt der Bibliothek. Dieser Wert ist erforderlich, wenn eine vorhandene Bibliotheksfreigabe zum Hinzufügen von einer anderen Plattform zu ändern. Windows ist die einzige unterstützte Plattform.

## <a name="remarks"></a>Hinweise

Für die Sprache R-Pakete müssen in Form von ZIP-Archivdateien mit vorbereitet werden die. ZIP-Erweiterung für Windows. Derzeit wird nur die Windows-Plattform unterstützt.  

Die `ALTER EXTERNAL LIBRARY` Anweisung uploads nur die Bits für die Bibliothek mit der Datenbank. Die geänderte Bibliothek ist nicht tatsächlich installiert, bis ein Benutzer ein externes Skript anschließend durch Ausführen ausführt [Sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="permissions"></a>Berechtigungen

Erfordert die `ALTER ANY EXTERNAL LIBRARY` Berechtigung. Benutzer, die eine externe Bibliothek erstellt haben kann, externe Bibliothek geändert werden.

## <a name="examples"></a>Beispiele

In den folgenden Beispielen wird eine externe Bibliothek namens CustomPackage geändert.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. Ersetzen Sie den Inhalt einer Bibliothek, die mithilfe einer Datei

Im folgende Beispiel ändert eine externe Bibliothek namens CustomPackage, mit einer ZIP-Datei, die die aktualisierte Bits enthält.

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

Um die aktualisierte Bibliothek zu installieren, führen Sie die gespeicherte Prozedur `sp_execute_external_script`.

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
WITH RESULT SETS (([result] int));
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Ändern einer vorhandenen Bibliotheksfreigabe, die unter Verwendung eines Bytestreams

Im folgenden Beispiel wird die vorhandene Bibliothek durch die neue Bits als eine hexadezimale Literale übergeben.

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

## <a name="see-also"></a>Siehe auch  

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
