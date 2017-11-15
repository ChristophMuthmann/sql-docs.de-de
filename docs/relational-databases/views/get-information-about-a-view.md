---
title: Abrufen von Informationen zu einer Sicht | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-views
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.viewproperties.general.f1
helpviewer_keywords:
- views [SQL Server], status information
- metadata [SQL Server], views
- dependencies [SQL Server], views
- displaying view information
- views [SQL Server], metadata
- viewing view information
- status information [SQL Server], views
- view dependencies
ms.assetid: 05a73e33-8f85-4fb6-80c1-1b659e753403
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 70db6677328cfb978c7cdda663d56c8fa7332fea
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="get-information-about-a-view"></a>Abrufen von Informationen zu einer Sicht
  Sie erhalten Informationen zur Definition oder den Eigenschaften einer Sicht in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]. Manchmal ist es erforderlich, die Definition einer Sicht anzuzeigen, um zu verstehen, wie die Daten in der Sicht aus den Quelltabellen abgeleitet werden, oder um die durch die Sicht definierten Daten anzuzeigen.  
  
> [!IMPORTANT]  
>  Wenn Sie den Namen eines Objekts ändern, auf das eine Sicht verweist, müssen Sie die Sicht so ändern, dass ihr Text den neuen Namen wiedergibt. Bevor Sie ein Objekt umbenennen, sollten Sie somit erst die Abhängigkeiten des Objekts anzeigen, um feststellen zu können, ob Sichten von der beabsichtigten Änderung betroffen sind.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **Informationen zu einer Sicht rufen Sie ab mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Für die Verwendung von `sp_helptext` zum Zurückgeben der Definition einer Sicht ist die Mitgliedschaft in der Rolle **Öffentlich** erforderlich. Für die Verwendung von `sys.sql_expression_dependencies` zur Suche aller Abhängigkeiten von einer Sicht sind die Berechtigung VIEW DEFINITION für die Datenbank und die Berechtigung SELECT auf `sys.sql_expression_dependencies` für die Datenbank erforderlich. Systemobjektdefinitionen, wie die in SELECT OBJECT_DEFINITION zurückgegebenen Systemobjektdefinitionen, sind öffentlich sichtbar.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="get-view-properties-by-using-object-explorer"></a>Abrufen von Sichteigenschaften mit Objekt-Explorer  
  
1.  Klicken Sie in **Objekt-Explorer**auf das Pluszeichen neben der Datenbank, die die Sicht enthält, deren Eigenschaften Sie anzeigen möchten, und klicken Sie dann auf das Pluszeichen, um den Ordner **Sichten** zu erweitern.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Sicht, deren Eigenschaften Sie anzeigen möchten, und wählen Sie **Eigenschaften**aus.  
  
     Die folgenden Eigenschaften werden im Dialogfeld **Sichteigenschaften** angezeigt.  
  
     **Datenbank**  
     Name der Datenbank, die diese Sicht enthält.  
  
     **Server**  
     Name der aktuellen Serverinstanz.  
  
     **Benutzer**  
     Name des Benutzers dieser Verbindung.  
  
     **Erstellt am**  
     Zeigt das Datum an, an dem die Sicht erstellt wurde.  
  
     **Name**  
     Name der aktuellen Sicht.  
  
     **Schema**  
     Zeigt das Schema an, zu dem die Sicht gehört.  
  
     **Systemobjekt**  
     Gibt an, ob es sich bei der Sicht um ein Systemobjekt handelt. Die Werte sind True und False.  
  
     **ANSI NULLS**  
     Gibt an, ob das Objekt mit der Option ANSI NULLS erstellt wurde.  
  
     **Verschlüsselt**  
     Gibt an, ob die Sicht verschlüsselt ist. Die Werte sind True und False.  
  
     **Bezeichner in Anführungszeichen**  
     Gibt an, ob das Objekt mit der Option Bezeichner in Anführungszeichen erstellt wurde.  
  
     **Schema-gebunden**  
     Gibt an, ob die Sicht Schema-gebunden ist. Die Werte sind True und False. Informationen zu Schema-gebundenen Sichten finden Sie im Abschnitt SCHEMABINDING von [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
#### <a name="getting-view-properties-by-using-the-view-designer-tool"></a>Abrufen von Sichteigenschaften mit dem Tool Sicht-Designer  
  
1.  Erweitern Sie in **Objekt-Explorer**die Datenbank, die die Sicht enthält, deren Eigenschaften Sie anzeigen möchten, und erweitern Sie dann den Ordner **Sichten** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Sicht, deren Eigenschaften Sie anzeigen möchten, und wählen Sie **Entwurf**aus.  
  
3.  Klicken Sie mit der rechten Maustaste in den Leerraum des Diagrammbereichs, und klicken Sie auf **Eigenschaften**.  
  
     Die folgenden Eigenschaften werden im Bereich **Eigenschaften** angezeigt.  
  
     **(Name)**  
     Name der aktuellen Sicht.  
  
     **Datenbankname**  
     Name der Datenbank, die diese Sicht enthält.  
  
     **Beschreibung**  
     Eine kurze Beschreibung der aktuellen Sicht.  
  
     **Schema**  
     Zeigt das Schema an, zu dem die Sicht gehört.  
  
     **Servername**  
     Name der aktuellen Serverinstanz.  
  
     **An Schema binden**  
     Verhindert, dass Benutzer die zugrunde liegenden Objekte ändern, die auf beliebige Weise zu dieser Sicht beitragen, was die Sichtdefinition ungültig machen würde.  
  
     **Deterministisch**  
     Zeigt, ob der Datentyp der ausgewählten Spalte mit Sicherheit bestimmt werden kann  
  
     **Unterschiedliche Werte**  
     Gibt an, dass die Abfrage alle Duplikate in der Sicht herausfiltert. Diese Option ist hilfreich, wenn Sie nur einige Spalten aus einer Tabelle verwenden und diese möglicherweise doppelte Werte enthalten, oder wenn die Verknüpfung von mehreren Tabellen eine Verdopplung von Zeilen im Resultset zur Folge hat. Das Aktivieren dieser Option ist gleichbedeutend mit dem Einfügen des Schlüsselworts DISTINCT in die Anweisung im SQL-Bereich.  
  
     **GROUP BY-Erweiterung**  
     Gibt an, dass zusätzliche Optionen für Sichten verfügbar sind, die auf Aggregatabfragen basieren.  
  
     **Alle Spalten ausgeben**  
     Zeigt an, ob alle Spalten von der ausgewählten Sicht zurückgegeben werden. Dies wird beim Erstellen der Sicht festgelegt.  
  
     **SQL-Kommentar**  
     Zeigt eine Beschreibung der SQL-Anweisungen an. Klicken Sie auf die Beschreibung, und klicken Sie anschließend auf die Auslassungspunkte **(...)** rechts neben der Eigenschaft, um die ganze Beschreibung anzuzeigen oder sie zu bearbeiten. Kommentare können Informationen darüber enthalten, wer die Sicht verwendet und wann sie verwendet wird.  
  
     **Oberste Angabe**  
     Erweitert das Element, um die Eigenschaften für **Oben**, **Ausdruck**, **Prozent**und **WITH TIES** anzuzeigen.  
  
     **(Nach oben)**  
     Gibt an, dass die Sicht eine TOP-Klausel enthält, die bewirkt, dass nur die ersten N Zeilen oder ersten N Prozent der Zeilen im Resultset zurückgegeben werden. In der Standardeinstellung gibt die Sicht die ersten 10 Zeilen im Resultset zurück. Verwenden Sie dies, um die Anzahl der zurückzugebenden Zeilen zu ändern oder einen anderen Prozentwert anzugeben.  
  
     **Ausdruck**  
     Zeigt an, welchen Prozentsatz (wenn **Prozent** auf **Ja**festgelegt ist) oder welche Datensätze (wenn **Prozent** auf **Nein**festgelegt wird) die Sicht zurückgegeben wird.  
  
     **Prozent**  
     Gibt an, dass die Abfrage eine **TOP** -Klausel enthält, von der nur die ersten N Prozent der Zeilen im Resultset zurückgegeben werden.  
  
     **WITH TIES**  
     Gibt an, dass die Sicht eine **WITH TIES** -Klausel enthält. **WITH TIES** ist hilfreich, wenn eine Sicht sowohl eine **ORDER BY** -Klausel als auch eine **TOP** -Klausel mit Prozentangabe enthält. Wenn diese Option festgelegt ist und der Prozentbereich in der Mitte einer Zeilenfolge mit identischen Werten in der **ORDER BY** -Klausel endet, wird die Sicht bis ans Ende der betreffenden Zeilenfolge erweitert.  
  
     **Spezifikation aktualisieren**  
     Erweitert, um Eigenschaften für die Eigenschaften **Aktualisieren mit Sichtregeln** und **Überprüfungsoption** anzuzeigen.  
  
     **(Aktualisieren mit Sichtregeln)**  
     Gibt an, dass alle Updates und Einfügungen für die Sicht von Microsoft Data Access Components (MDAC) in SQL-Anweisungen übersetzt werden, die auf die Sicht verweisen, statt in SQL-Anweisungen, die direkt auf die Basistabellen der Sicht verweisen.  
  
     In einigen Fällen gibt MDAC Sichtaktualisierungen und Sichteinfügevorgänge als Aktualisierungen und Einfügungen für die zugrunde liegenden Basistabellen der Sicht bekannt. Durch Auswahl von **Aktualisieren mit Sichtregeln**wird gewährleistet, dass MDAC Aktualisierungs- und Einfügevorgänge für die Sicht selbst generiert.  
  
     **Überprüfungsoption**  
     Gibt an, dass beim Öffnen dieser Sicht und Ändern des Bereichs **Ergebnisse** die Datenquelle überprüft, ob die hinzugefügten oder geänderten Daten die **WHERE-Klausel** der Sichtdefinition erfüllen. Wenn die Änderung die **WHERE** -Klausel nicht erfüllt, erhalten Sie eine Fehlermeldung mit weiteren Informationen.  
  
#### <a name="to-get-dependencies-on-the-view"></a>So rufen Sie Abhängigkeiten für die Sicht ab  
  
1.  Erweitern Sie in **Objekt-Explorer**die Datenbank, die die Sicht enthält, deren Eigenschaften Sie anzeigen möchten, und erweitern Sie dann den Ordner **Sichten** .  
  
2.  Klicken Sie mit der rechten Maustaste auf die Sicht, deren Eigenschaften Sie anzeigen möchten, und wählen Sie **Abhängigkeiten anzeigen**aus.  
  
3.  Wählen Sie **Objekte, die von [Sichtname] abhängig sind** aus, um die Objekte anzuzeigen, die auf die Sicht verweisen.  
  
4.  Wählen Sie **Objekte, von denen [Sichtname] abhängt** aus, um die Objekte anzuzeigen, auf die von der Sicht verwiesen wird.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-view"></a>So rufen Sie die Definition und die Eigenschaften einer Sicht ab  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie eines der folgenden Beispiele, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition, uses_ansi_nulls, uses_quoted_identifier, is_schema_bound  
    FROM sys.sql_modules  
    WHERE object_id = OBJECT_ID('HumanResources.vEmployee');   
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID('HumanResources.vEmployee')) AS ObjectDefinition;   
    GO  
    ```  
  
    ```  
    EXEC sp_helptext 'HumanResources.vEmployee';  
    ```  
  
 Weitere Informationen finden Sie unter [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md), [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md) und [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
#### <a name="to-get-the-dependencies-of-a-view"></a>So rufen Sie die Abhängigkeiten einer Sicht ab  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) und [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
  
