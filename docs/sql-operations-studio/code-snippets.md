---
title: Erstellen von Codeausschnitten in SQL Operations Studio (preview) | Microsoft Docs
description: Informationen Sie zum Erstellen und Verwenden von SQL-Codeausschnitte in SQL Operations Studio (preview)
ms.custom: tools|sos
ms.date: 11/15/2017
ms.reviewer: alayu; erickang; sstein
ms.prod: sql-non-specified
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4670c824b1e52776c3d81d097beeb4ccd9e62e2d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>Erstellen und Verwenden von Codeausschnitten, Transact-SQL (T-SQL)-Skripts in schnell erstellen[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Codeausschnitte in [!INCLUDE[name-sos](../includes/name-sos-short.md)] sind Vorlagen, die erleichtern die Datenbanken und Datenbankobjekte erstellen. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)]bietet mehrere T-SQL-Ausschnitte, um Ihnen zu helfen, schnell generieren die korrekte Syntax. 

Benutzerdefinierte Codeausschnitte können auch erstellt werden.

## <a name="using-built-in-t-sql-code-snippets"></a>Verwenden integrierte T-SQL-Codeausschnitte

1. Geben Sie den Zugriff auf die verfügbaren Ausschnitte *Sql* im Abfrage-Editor, um die Liste zu öffnen:

   ![Ausschnitte](media/code-snippets/sql-snippets.png)

1. Wählen Sie den Ausschnitt, die, den Sie verwenden möchten, und die T-SQL-Skript generiert. Wählen Sie z. B. *SqlCreateTable*:

   ![Tabelle Ausschnitte erstellen](media/code-snippets/create-table.png)

1. Aktualisieren Sie die hervorgehobenen Felder durch die entsprechenden Werte ein. Ersetzen Sie z. B. *TableName* und *Schema* mit den Werten für die Datenbank:

   ![Ersetzen Sie die Vorlagenfeld](media/code-snippets/table-from-snippet.png)

   Wenn das Feld, das Sie ändern möchten, nicht mehr hervorgehoben ist (Dies geschieht, wenn den Cursor, um den Editor zu verschieben), mit der rechten Maustaste des Worts, das Sie ändern möchten, und wählen Sie **ersetzen Sie alle Vorkommen**:

   ![Ersetzen Sie die Vorlagenfeld](media/code-snippets/change-all.png)

1. Aktualisieren Sie, oder fügen Sie alle zusätzlichen T-SQL Sie für den ausgewählten Ausschnitt müssen hinzu. Aktualisieren Sie z. B. *Column1*, *Column2*, und fügen Sie weitere Spalten hinzu.


 
## <a name="creating-sql-code-snippets"></a>Erstellen von SQL-Codeausschnitte 

Sie können eigene Ausschnitte definieren. Um die SQL-Ausschnittdatei für die Bearbeitung zu öffnen:

1. Öffnen der *Befehl Palette* (**UMSCHALT + STRG + P**), und geben *Ausschnitt*, und wählen Sie **Voreinstellungen: Öffnen Benutzer Ausschnitte**:

   ![Ersetzen Sie die Vorlagenfeld](media/code-snippets/user-snippets.png)

1. Wählen Sie **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)]erbt seine Code Snippet-Funktionalität von Visual Studio-Code, damit in diesem Artikel insbesondere erläutert die Verwendung von SQL-Ausschnitten. Ausführlichere Informationen finden Sie unter [eigene Ausschnitte erstellen](https://code.visualstudio.com/docs/editor/userdefinedsnippets) in der Dokumentation zu Visual Studio-Code. 

   ![Ersetzen Sie die Vorlagenfeld](media/code-snippets/select-sql.png)

1. Fügen Sie den folgenden Code in *sql.json*:

   ```sql
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   ```

1. Speichern Sie die sql.json-Datei.
1. Öffnen Sie ein neues Abfrage-Editorfenster, indem Sie auf **STRG + N**.
2. Typ **Sql**, und Sie sehen, dass die zwei Benutzer Ausschnitte, die Sie gerade hinzugefügt; *sqlCreateTable2* und *sqlSelectTop5*.

Wählen Sie eine neue Ausschnitte aus, und geben Sie ihm einen Testlauf!


## <a name="additional-resources"></a>Weitere Ressourcen

Informationen zu den SQL-Editor finden Sie unter [Code-Editor-Lernprogramm](tutorial-sql-editor.md).