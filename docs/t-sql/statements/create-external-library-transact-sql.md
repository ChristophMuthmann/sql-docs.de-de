---
title: CREATE EXTERNAL LIBRARY (Transact-SQL) | Microsoft-Dokumentation
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
manager: craigg
ms.openlocfilehash: e28716314837225586cf4bd1f80a37c5c6b824ab
ms.sourcegitcommit: 6e819406554efbd17bbf84cf210d8ebeddcf772d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="create-external-library-transact-sql"></a>CREATE EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]  

Lädt R-Pakete vom angegebenen Bytedatenstrom oder Dateipfad in eine Datenbank hoch.

Diese Anweisung dient als generischer Mechanismus, mithilfe dessen der Datenbankadministrator Artefakte hochladen kann, die von Runtimes neuer externer Sprachen (R, Python, Java usw.) und Betriebssystemplattformen benötigt werden, die von [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] unterstützt werden. 

Derzeit werden nur die R-Sprache und die Windows-Plattform unterstützt. Die Unterstützung für Python und Linux ist für ein späteres Release eingeplant.

## <a name="syntax"></a>Syntax

```text
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

Bibliotheken werden zu der Datenbank hinzugefügt, die an den Benutzer angepasst ist. Das bedeutet, dass Bibliotheksnamen innerhalb des Kontexts eines bestimmten Benutzers oder Besitzers als eindeutig gelten. Bibliotheksnamen müssen außerdem für jeden Benutzer eindeutig sein. Beispielsweise können zwei Benutzer, **RUser1** und **RUser2**, die R-Bibliothek `ggplot2` individuell und separat hochladen.

Bibliotheksnamen können nicht beliebig zugewiesen werden. Der Bibliotheksname sollte mit dem Namen übereinstimmen, der benötigt wird, um die R-Bibliothek von R zu laden.

**owner_name**

Gibt den Namen eines Benutzers oder einer Rolle an, der oder die die externe Bibliothek besitzt. Wird kein Wert angegeben, wird der aktuelle Benutzer zum Besitzer.

Bibliotheken, die Datenbankbesitzern gehören, gelten als global für die Datenbank und Runtime. Sprich, Datenbankbesitzer können Bibliotheken erstellen, die eine gemeinsame Menge von Bibliotheken oder Paketen enthalten, die von vielen Benutzern geteilt werden. Wenn eine externe Bibliothek von einem anderen Benutzer als dem `dbo`-Benutzer erstellt wurde, ist die externe Bibliothek nur für diesen Benutzer privat.

Wenn der Benutzer **RUser1** ein R-Skript ausführt, kann der Wert von `libPath` mehrere Pfade enthalten. Der erste Pfad ist immer der Pfad zur gemeinsamen Bibliothek, die vom Datenbankbesitzer erstellt wurde. Der zweite Teil von `libPath` gibt den Pfad an, der Pakete enthält, die von **RUser1** individuell hochgeladen wurden.

**file_spec**

Gibt den Inhalt des Pakets für eine bestimmte Plattform an. Nur ein Dateiartefakt pro Plattform wird unterstützt.

Die Datei kann in Form eines lokalen Pfads oder eines Netzwerkpfads angegeben werden.

Optional kann eine Betriebssystemplattform für die Datei angegeben werden. Für jede Betriebssystemplattform für eine bestimmte Sprache oder Runtime ist nur ein Darteiartefakt oder Inhalt erlaubt.

**library_bits**

Gibt den Inhalt des Pakets als Hexadezimalliteral an, vergleichbar mit Assemblys. 

Diese Option ist hilfreich, wenn Sie eine Bibliothek erstellen oder eine bestehende Bibliothek ändern müssen (und über die erforderlichen Berechtigungen dafür verfügen), das Dateisystem auf dem Server jedoch eingeschränkt ist und die Bibliotheksdateien nicht an einen Speicherort kopieren kann, auf den der Server Zugriff hat.

**PLATFORM = WINDOWS**

Gibt die Plattform für den Inhalt der Bibliothek an. Der Standardwert ist die Hostplattform, auf der SQL Server ausgeführt wird. Aus diesem Grund muss der Benutzer den Wert nicht angeben. Dies ist in Fällen erforderlich, in denen mehrere Plattformen unterstützt werden oder in denen der Benutzer eine andere Plattform angeben muss. 

Bei SQL Server 2017 ist Windows die einzig unterstützte Plattform.

## <a name="remarks"></a>Remarks

Bei der R-Sprache müssen bei Verwendung einer Datei Pakete in Form von gezippten Archivdateien mit der Dateiendung .ZIP für Windows vorbereitet werden. Derzeit wird nur die Windows-Plattform unterstützt. 

Die `CREATE EXTERNAL LIBRARY`-Anweisung lädt die Bibliothekbits in die Datenbank hoch. Die Bibliothek wird installiert, wenn ein Benutzer mithilfe von [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ein externes Skript ausführt und das Paket oder die Bibliothek aufruft.

Bibliotheken, die in die Instanz hochgeladen werden, können entweder öffentlich oder privat sein. Wenn die Bibliothek von einem Mitglied von `dbo` erstellt wird, ist sie öffentlich und kann mit allen Benutzern geteilt werden. Andernfalls ist die Bibliothek für diesen Benutzer privat.

Sie können im SQL Server 2017-Release keine Blobs als Datenquelle verwenden.

## <a name="permissions"></a>Berechtigungen

Erfordert die `CREATE ANY EXTERNAL LIBRARY`-Berechtigung.

Zum Bearbeiten einer Bibliothek ist die separate Berechtigung `ALTER ANY EXTERNAL LIBRARY` erforderlich.

## <a name="examples"></a>Beispiele

### <a name="a-add-an-external-library-to-a-database"></a>A. Hinzufügen einer externen Bibliothek zu einer Datenbank  

Im folgenden Beispiel wird eine externe Bibliothek namens `customPackage` zu einer Datenbank hinzugefügt.

```sql
CREATE EXTERNAL LIBRARY customPackage
FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip') WITH (LANGUAGE = 'R');
```  

Nachdem die Bibliothek erfolgreich in die Instanz hochgeladen wurde, führt ein Benutzer den Vorgang `sp_execute_external_script` aus, um die Bibliothek zu installieren.

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
```

### <a name="b-installing-packages-with-dependencies"></a>B. Installieren von Paketen mit Abhängigkeiten

Wenn das Paket, das Sie installieren möchten, Abhängigkeiten aufweist, ist es sehr wichtig, dass Sie sowohl Abhängigkeiten der ersten als auch der zweiten Ebene analysieren und sicherstellen, dass alle erforderlichen Pakete verfügbar sind, _bevor_ Sie versuchen, das Zielpaket zu installieren.

Nehmen wir beispielsweise an, dass Sie ein neues Paket, `packageA`, installieren möchten:

+ `packageA` ist abhängig von `packageB`.
+ `packageB` ist abhängig von `packageC`.

Damit die Installation von `packageA` erfolgreich ist, müssen Sie Bibliotheken für `packageB` und `packageC` zur selben Zeit erstellen, zu der Sie `packageA` zu SQL Server hinzufügen. Achten Sie darauf, dass Sie auch die erforderlichen Paketversionen überprüfen.

In der Praxis sind Paketabhängigkeiten für häufig verwendete Pakete in der Regel viel komplizierter als in diesem einfachen Beispiel. Beispielsweise könnte „ggplot2“ mehr als 30 Pakete erfordern, und diese Pakete könnten zusätzliche Pakete erfordern, die auf dem Server nicht verfügbar sind. Jedes fehlende Paket und jede falsche Paketversion kann zu einem Fehler bei der Installation führen.

Da es schwierig sein kann, alle Abhängigkeiten nur durch Betrachten des Paketmanifests zu bestimmen, empfehlen wir Ihnen, dass Sie ein Paket wie [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) oder [iGraph](http://igraph.org/redirect.html) verwenden, um alle Pakete zu identifizieren, die für eine erfolgreiche Installation erforderlich sein könnten.

+ Laden Sie das Zielpaket und dessen Abhängigkeiten hoch. Alle Dateien müssen sich in einem Ordner befinden, auf den der Server Zugriff hat.

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    GO

    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    GO

    CREATE EXTERNAL LIBRARY packageC FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageC.zip') 
    WITH (LANGUAGE = 'R');
    GO
    ```

+ Installieren Sie zunächst die erforderlichen Pakete.

    Wenn ein erforderliches Paket bereits in die Instanz hochgeladen wurde, müssen Sie dieses nicht erneut hinzufügen. Achten Sie nur darauf, zu überprüfen, ob es sich bei der Version des vorhandenen Pakets um die richtige handelt. 
    
    Die erforderlichen Pakete `packageC` und `packageB` werden beim ersten Ausführen von `sp_execute_external_script` zur Installation des Pakets `packageA` in der richtigen Reihenfolge installiert.

    Wenn ein erforderliches Paket jedoch nicht verfügbar ist, tritt ein Fehler bei der Installation des Zielpakets `packageA` auf.

    ```sql
    EXEC sp_execute_external_script 
    @language =N'R', 
    @script=N'
    # load the desired package packageA
    library(packageA)
    # call function from package
    OutputDataSet <- packageA.function()
    '
    with result sets (([result] int));    
    ```

### <a name="c-create-a-library-from-a-byte-stream"></a>C. Erstellen einer Bibliothek aus einem Bytedatenstrom

Wenn Sie nicht die Möglichkeit haben, die Paketdateien an einem Speicherort auf dem Server zu speichern, können Sie die Paketinhalte auch in einer Variable übergeben. Im folgenden Beispiel wird eine Bibliothek erstellt, indem die Bits als Hexadezimalliteral übergeben werden.

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

Hier wurden die Hexadezimalwerte zur besseren Lesbarkeit abgeschnitten.

### <a name="d-change-an-existing-package-library"></a>D. Löschen einer vorhandenen Paketbibliothek

Die `ALTER EXTERNAL LIBRARY`-DDL-Anweisung kann verwendet werden, um neuen Bibliotheksinhalt hinzuzufügen oder bestehenden Bibliotheksinhalt zu ändern. Zum Bearbeiten einer bestehenden Bibliothek ist die Berechtigung `ALTER ANY EXTERNAL LIBRARY` erforderlich.

Weitere Informationen finden Sie unter [ALTER EXTERNAL LIBRARY](alter-external-library-transact-sql.md).

### <a name="e-delete-a-package-library"></a>E. Löschen einer Paketbibliothek

Um eine Paketbibliothek aus der Datenbank zu löschen, führen Sie die folgende Anweisung aus:

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> Im Gegensatz zu anderen `DROP`-Anweisungen in [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] unterstützt diese Anweisung einen optionalen Parameter, der die Benutzerberechtigung angibt. Durch diese Option können Benutzer mit Besitzrollen Bibliotheken löschen, die von regulären Benutzern hochgeladen wurden.

## <a name="see-also"></a>Siehe auch

[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
