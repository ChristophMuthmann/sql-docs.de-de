---
title: Anzeigen benutzerdefinierter Funktionen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.udfproperties.general.f1
- sql13.swb.functionproperties.general.f1
helpviewer_keywords:
- displaying user-defined functions
- viewing user-defined functions
- user-defined functions [SQL Server], viewing
- status information [SQL Server], user-defined functions
ms.assetid: a45dfab5-6384-4311-b935-2e23a70c5c10
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 16f1c2ed871db93259f87bc2e26dba634a0602d6
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="view-user-defined-functions"></a>Anzeigen benutzerdefinierter Funktionen
  Sie können Informationen zur Definition oder zu den Eigenschaften einer benutzerdefinierten Funktion in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]abrufen. Manchmal ist es erforderlich, die Definition einer Funktion anzuzeigen, um zu verstehen, wie die Daten der Funktion aus den Quelltabellen abgeleitet werden, oder um die durch die Funktion definierten Daten anzuzeigen.  
  
> [!IMPORTANT]  
>  Wenn Sie den Namen eines Objekts ändern, auf das eine Funktion verweist, müssen Sie den Text dieser Funktion mit dem neuen Namen aktualisieren. Bevor Sie ein Objekt umbenennen, sollten Sie daher erst die Abhängigkeiten des Objekts anzeigen, um feststellen zu können, ob Funktionen von der beabsichtigten Änderung betroffen sind.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **Abrufen von Informationen zu einer Funktion mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Das Anzeigen aller Abhängigkeiten einer Funktion mithilfe von **sys.sql_expression_dependencies** erfordert die VIEW DEFINITION-Berechtigung für die Datenbank und die SELECT-Berechtigung für **sys.sql_expression_dependencies** für die Datenbank. Systemobjektdefinitionen, wie die in OBJECT_DEFINITION zurückgegebenen Definitionen, sind öffentlich sichtbar.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-show-a-user-defined-functions-properties"></a>So zeigen Sie die Eigenschaften einer benutzerdefinierten Funktion an  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen neben der Datenbank mit der Funktion, deren Eigenschaften Sie anzeigen möchten, und klicken Sie dann auf das Pluszeichen, um den Ordner **Programmierbarkeit** zu erweitern.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Funktionen** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um den Ordner mit der Funktion zu erweitern, deren Eigenschaften Sie anzeigen möchten:  
  
    -   Table-valued Function  
  
    -   Skalarwertfunktion  
  
    -   Aggregatfunktion  
  
4.  Klicken Sie mit der rechten Maustaste auf die Funktion, deren Eigenschaften Sie anzeigen möchten, und wählen Sie **Eigenschaften**aus.  
  
     Die folgenden Eigenschaften werden im Dialogfeld **Funktionseigenschaften** *function_name* dialog box.  
  
     **Datenbank**  
     Name der Datenbank, die diese Funktion enthält.  
  
     **Server**  
     Name der aktuellen Serverinstanz.  
  
     **Benutzer**  
     Name des Benutzers dieser Verbindung.  
  
     **Erstellt am**  
     Zeigt das Datum an, an dem die Funktion erstellt wurde.  
  
     **Ausführen als**  
     Ausführungskontext für die Funktion.  
  
     **Name**  
     Name der aktuellen Funktion.  
  
     **Schema**  
     Zeigt das Schema an, zu dem die Funktion gehört.  
  
     **Systemobjekt**  
     Gibt an, ob es sich bei der Funktion um ein Systemobjekt handelt. Die Werte sind True und False.  
  
     **ANSI NULLS**  
     Gibt an, ob das Objekt mit der Option ANSI NULLS erstellt wurde.  
  
     **Verschlüsselt**  
     Gibt an, ob die Funktion verschlüsselt ist. Die Werte sind True und False.  
  
     **Funktionstyp**  
     Typ der benutzerdefinierten Funktion.  
  
     **Bezeichner in Anführungszeichen**  
     Gibt an, ob das Objekt mit der Option Bezeichner in Anführungszeichen erstellt wurde.  
  
     **Schema-gebunden**  
     Gibt an, ob die Funktion Schema-gebunden ist. Die Werte sind True und False. Informationen zu schemagebundenen Funktionen finden Sie im Abschnitt SCHEMABINDING von [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-function"></a>So rufen Sie die Definition und die Eigenschaften einer Funktion ab  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie eines der folgenden Beispiele, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the function name, definition, and relevant properties  
    SELECT sm.object_id,   
       OBJECT_NAME(sm.object_id) AS object_name,   
       o.type,   
       o.type_desc,   
       sm.definition,  
       sm.uses_ansi_nulls,  
       sm.uses_quoted_identifier,  
       sm.is_schema_bound,  
       sm.execute_as_principal_id  
    -- using the two system tables sys.sql_modules and sys.objects  
    FROM sys.sql_modules AS sm  
    JOIN sys.objects AS o ON sm.object_id = o.object_id  
    -- from the function 'dbo.ufnGetProductDealerPrice'  
    WHERE sm.object_id = OBJECT_ID('dbo.ufnGetProductDealerPrice')  
    ORDER BY o.type;  
    GO  
  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get the definition of the function dbo.ufnGetProductDealerPrice  
    SELECT OBJECT_DEFINITION (OBJECT_ID('dbo.ufnGetProductDealerPrice')) AS ObjectDefinition;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) und [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md).  
  
#### <a name="to-get-the-dependencies-of-a-function"></a>So rufen Sie die Abhängigkeiten einer Funktion ab  
  
1.  Stellen Sie im Objekt-Explorer **** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Get all of the dependency information  
    SELECT OBJECT_NAME(sed.referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(sed.referencing_id, sed.referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        sed.referencing_class_desc, sed.referenced_class_desc,  
        sed.referenced_server_name, sed.referenced_database_name, sed.referenced_schema_name,  
        sed.referenced_entity_name,   
        COALESCE(COL_NAME(sed.referenced_id, sed.referenced_minor_id), '(n/a)') AS referenced_column_name,  
        sed.is_caller_dependent, sed.is_ambiguous  
    -- from the two system tables sys.sql_expression_dependencies and sys.object  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    -- on the function dbo.ufnGetProductDealerPrice  
    WHERE sed.referencing_id = OBJECT_ID('dbo.ufnGetProductDealerPrice');  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) und [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
  
