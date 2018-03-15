---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 02/25/2018
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
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: 0581957db73b82b9486f938d17b4c8938e20258d
ms.sourcegitcommit: 6e819406554efbd17bbf84cf210d8ebeddcf772d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Ändert den Inhalt einer vorhandenen externen Paketbibliothek.

## <a name="syntax"></a>Syntax

```text
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

Gibt den Namen einer vorhandenen Paketbibliothek an. Bibliotheken umfassen nur den Benutzer. D.h., Bibliotheksnamen gelten innerhalb des Kontexts eines bestimmten Benutzers oder Besitzers als eindeutig.

Der Bibliotheksname kann nicht nach dem Zufallsprinzip zugewiesen werden. D.h., Sie müssen den Namen verwenden, den die aufrufende Runtime beim Laden des Pakets erwartet.

**owner_name**

Gibt den Namen eines Benutzers oder einer Rolle an, der oder die die externe Bibliothek besitzt.

**file_spec**

Gibt den Inhalt des Pakets für eine bestimmte Plattform an. Nur ein Dateiartefakt pro Plattform wird unterstützt.

Die Datei kann in Form eines lokalen Pfads oder eines Netzwerkpfads angegeben werden. Wenn die Datenquellenoption angegeben ist, kann der Dateiname ein relativer Pfad zu dem Container sein, auf den in `EXTERNAL DATA SOURCE` verwiesen wird.

Optional kann eine Betriebssystemplattform für die Datei angegeben werden. Für jede Betriebssystemplattform für eine bestimmte Sprache oder Runtime ist nur jeweils ein Darteiartefakt oder Inhalt erlaubt.

**DATA_SOURCE = external_data_source_name**

Gibt den Namen der externen Datenquelle an, die den Speicherort der Bibliotheksdatei enthält. Dieser Speicherort sollte auf einen Azure Blob Storage-Pfad verweisen. Verwenden Sie zum Erstellen einer externen Datenquelle [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](create-external-data-source-transact-sql.md).

> [!IMPORTANT] 
> Blobs werden derzeit im SQL Server 2017-Release nicht als Datenquelle unterstützt.

**library_bits**

Gibt ähnlich wie bei Assemblys den Inhalt des Pakets als Hexadezimalliteral an. 

Diese Option ist nützlich, wenn Sie die erforderliche Berechtigung zum Ändern einer Bibliothek haben. Jedoch ist der Zugriff auf Daten auf dem Server beschränkt, und Sie können die Inhalte nicht in einem Pfad speichern, auf den der Server zugreifen kann.

Stattdessen können Sie den Paketinhalt als Variable im Binärformat übergeben.

**PLATFORM = WINDOWS**

Gibt die Plattform für den Inhalt der Bibliothek an. Dieser Wert ist erforderlich, wenn eine vorhandene Bibliothek geändert wird, um eine andere Plattform hinzuzufügen. Windows ist die einzige unterstützte Plattform.

## <a name="remarks"></a>Remarks

Bei der R-Sprache müssen Pakete in Form von gezippten Archivdateien mit der Dateiendung .zip für Windows vorbereitet werden. Derzeit wird nur die Windows-Plattform unterstützt.  

Die `ALTER EXTERNAL LIBRARY`-Anweisung lädt nur die Bibliothekbits in die Datenbank hoch. Die geänderte Bibliothek wird installiert, wenn ein Benutzer Code in [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ausführt, der die Bibliothek aufruft.

## <a name="permissions"></a>Berechtigungen

Erfordert die `ALTER ANY EXTERNAL LIBRARY`-Berechtigung. Benutzer, die eine externe Bibliothek erstellt haben, können diese ändern.

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird eine externe Bibliothek namens `customPackage` geändert.

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. Ersetzen des Inhalts einer Bibliothek mithilfe einer Datei

Im folgenden Beispiel wird eine externe Bibliothek mit dem Namen `customPackage` mithilfe einer ZIP-Datei geändert, die die aktualisierten Bits enthält.

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```

Führen Sie die gespeicherte Prozedur `sp_execute_external_script` aus, um die aktualisierte Bibliothek zu installieren.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
;
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Ändern einer vorhandenen Bibliothek mithilfe eines Bytedatenstroms

Im folgenden Beispiel wird die vorhandene Bibliothek geändert, indem die neuen Bits als ein Hexadezimalliteral übergeben werden.

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

In diesem Codebeispiel werden die Inhalte der Variablen aus Gründen der Lesbarkeit abgeschnitten.

## <a name="see-also"></a>Siehe auch

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
