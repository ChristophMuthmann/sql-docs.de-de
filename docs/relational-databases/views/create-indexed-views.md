---
title: Erstellen von indizierten Sichten | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
caps.latest.revision: "79"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e72f863a4746bf091c15e48349943906e172c616
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-indexed-views"></a>Erstellen von indizierten Sichten
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)] In diesem Thema wird beschrieben, wie eine indizierte Sicht in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] erstellt wird. Der erste Index, der für eine Sicht erstellt wird, muss ein eindeutiger gruppierter Index sein. Nachdem der eindeutige gruppierte Index erstellt wurde, können Sie weitere nicht gruppierte Indizes erstellen. Das Erstellen eines eindeutigen gruppierten Indexes für eine Sicht verbessert die Abfrageleistung, da die Sicht wie eine Tabelle mit einem gruppierten Index in der Datenbank gespeichert wird. Der Abfrageoptimierer kann indizierte Sichten verwenden, um die Abfrageausführung zu beschleunigen. Es ist nicht erforderlich, dass in der Abfrage auf die jeweilige Sicht verwiesen wird, damit der Optimierer diese Sicht als Ersatz berücksichtigt.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
 Die folgenden Schritte sind zum Erstellen einer indizierten Sicht erforderlich und wichtig für eine erfolgreiche Implementierung der indizierten Sicht:  
  
1.  Stellen Sie sicher, dass die SET-Optionen für alle vorhandenen Tabellen korrekt sind, auf die in der Sicht verwiesen wird.  
  
2.  Stellen Sie sicher, dass die SET-Optionen für die Sitzung richtig festgelegt sind, bevor Sie Tabellen und die Sicht erstellen.  
  
3.  Stellen Sie sicher, dass die Sichtdefinition deterministisch ist.  
  
4.  Erstellen Sie die Sicht mithilfe der Option WITH SCHEMABINDING.  
  
5.  Erstellen Sie den eindeutigen gruppierten Index für die Sicht.  
  
###  <a name="Restrictions"></a> Erforderliche SET-Optionen für indizierte Sichten  
 Das Auswerten desselben Ausdrucks kann im [!INCLUDE[ssDE](../../includes/ssde-md.md)] zu unterschiedlichen Ergebnissen führen, wenn bei der Ausführung der Abfrage unterschiedliche SET-Optionen aktiviert sind. Wenn die SET-Option CONCAT_NULL_YIELDS_NULL auf ON festgelegt ist, gibt beispielsweise der Ausdruck **'**abc**'** + NULL den Wert NULL zurück. Wenn die Option CONCAT_NULL_YIEDS_NULL allerdings auf OFF festgelegt ist, ergibt derselbe Ausdruck **'**abc**'**.  
  
 Um sicherzustellen, dass die Sichten ordnungsgemäß verwaltet werden können und konsistente Ergebnisse zurückgeben, sind für indizierte Sichten feste Werte für mehrere SET-Optionen erforderlich. Die SET-Optionen in der folgenden Tabelle müssen auf die in der Spalte **Erforderlicher Wert** angezeigten Werte festgelegt werden, wenn eine der folgenden Bedingungen zutrifft:  
  
-   Die Sicht und nachfolgende Indizes für die Sicht werden erstellt.  
  
-   Die Basistabellen, auf die beim Erstellen der Tabelle in der Sicht verwiesen wird.  
  
-   Für eine Tabelle, die Teil der indizierten Sicht ist, wird ein Einfüge-, Update- oder Löschvorgang durchgeführt. Dazu gehören Vorgänge wie Massenkopieren, Replikation und verteilte Abfragen.  
  
-   Die indizierte Sicht wird vom Abfrageoptimierer verwendet, um den Abfrageplan zu erstellen.  
  
    |SET-Optionen|Erforderlicher Wert|Standardserverwert|Standardwert<br /><br /> OLE DB- und ODBC-Wert|Standardwert<br /><br /> DB-Library-Wert|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *Wenn Sie ANSI_WARNINGS auf ON festlegen, wird ARITHABORT implizit auf ON festgelegt.  
  
 Wenn Sie eine OLE DB- oder ODBC-Serververbindung verwenden, müssen Sie nur den Wert der ARITHABORT-Einstellung ändern. Alle DB-Library-Werte müssen entweder auf Serverebene mithilfe von **sp_configure** oder über die Anwendung mithilfe des SET-Befehls ordnungsgemäß festgelegt werden.  
  
> [!IMPORTANT]  
>  Es wird dringend empfohlen, die Benutzeroption ARITHABORT serverweit auf ON festzulegen, sobald in einer Datenbank auf dem Server die erste indizierte Sicht oder der erste Index für eine berechnete Spalte erstellt wird.  
  
### <a name="deterministic-views"></a>Deterministische Sichten  
 Die Definition einer indizierten Sicht muss deterministisch sein. Eine Sicht ist deterministisch, wenn alle Ausdrücke in der Auswahlliste sowie die WHERE-Klausel und die GROUP BY-Klausel deterministisch sind. Deterministische Ausdrücke geben stets dasselbe Ergebnis zurück, wenn sie mit einer bestimmten Gruppe von Eingabewerten ausgewertet werden. Nur deterministische Funktionen können Teil von deterministischen Ausdrücken sein. Beispielsweise ist die DATEADD-Funktion deterministisch, weil sie für eine bestimmte Gruppe von Argumentwerten stets dasselbe Ergebnis für die drei Parameter zurückgibt. GETDATE ist nicht deterministisch, da diese Funktion immer mit demselben Argument aufgerufen wird, der zurückgegebene Wert jedoch bei jeder Ausführung unterschiedlich ist.  
  
 Um zu bestimmen, ob eine Sichtspalte deterministisch ist, verwenden Sie die **IsDeterministic** -Eigenschaft der [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) -Funktion. Mithilfe der **IsPrecise** -Eigenschaft der COLUMNPROPERTY-Funktion können Sie bestimmen, ob eine deterministische Spalte in einer Sicht mit Schemabindung präzise ist. COLUMNPROPERTY gibt den Wert 1 für TRUE, den Wert 0 für FALSE und NULL für ungültige Eingaben zurück. Dies bedeutet, dass die Spalte nicht deterministisch oder nicht präzise ist.  
  
 Auch wenn ein Ausdruck deterministisch ist, kann das exakte Ergebnis von der Prozessorarchitektur oder der Version des Microcodes abhängen, wenn dieser Ausdruck float-Ausdrücke enthält. Um die Datenintegrität sicherzustellen, können solche Ausdrücke nur als Nichtschlüsselspalten von indizierten Sichten verwendet werden. Deterministische Ausdrücke, die keine float-Ausdrücke enthalten, werden als präzise bezeichnet. Nur präzise deterministische Ausdrücke können in indizierten Sichten Teile von Schlüsselspalten und von WHERE-Klauseln oder GROUP BY-Klauseln sein.  
  
> [!NOTE]  
>  Indizierte Sichten, die temporale Abfragen (Abfragen, die die **FOR SYSTEM_TIME** -Klausel verwenden) überlagern, werden nicht unterstützt.  
  
### <a name="additional-requirements"></a>Zusätzliche Anforderungen  
 Zusätzlich zu den Anforderungen bzgl. SET-Optionen und deterministischen Funktionen müssen die folgenden Anforderungen erfüllt werden:  
  
-   Der Benutzer, der die CREATE INDEX-Anweisung ausführt, muss der Besitzer der Sicht sein.  
  
-   Wenn Sie den Index erstellen, muss die Option IGNORE_DUP_KEY auf OFF (Standardeinstellung) festgelegt sein.  
  
-   Auf Tabellen muss in der Sichtdefinition mit dem zweiteiligen Namen *Schema***.***Tabellenname* verwiesen werden.  
  
-   Benutzerdefinierte Funktionen, auf die in der Sicht verwiesen wird, müssen mit der Option WITH SCHEMABINDING erstellt werden.  
  
-   Auf benutzerdefinierte Funktionen, auf die in der Sicht verwiesen wird, muss mit dem zweiteiligen Namen *Schema***.***Funktion*verwiesen werden.  
  
-   Die Datenzugriffseigenschaft einer benutzerdefinierten Funktion muss NO SQL lauten, und die Eigenschaft für den externen Zugriff muss NO lauten.  
  
-   CLR-Funktionen (Common Language Runtime) können in der SELECT-Liste der Sicht angezeigt werden, können aber nicht Teil der Definition des gruppierten Indexschlüssels sein. CLR-Funktionen können nicht in der WHERE-Klausel der Sicht oder in der ON-Klausel einer JOIN-Operation in der Sicht auftreten.  
  
-   Für CLR-Funktionen und -Methoden der CLR-benutzerdefinierten Typen, die in der Sichtdefinition verwendet werden, müssen die in der folgenden Tabelle dargestellten Eigenschaften festgelegt werden.  
  
    |Eigenschaft|Hinweis|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Muss explizit als ein Attribut der Microsoft .NET Framework-Methode deklariert werden.|  
    |PRECISE = TRUE|Muss explizit als ein Attribut der .NET Framework-Methode deklariert werden.|  
    |DATA ACCESS = NO SQL|Wird durch Festlegen des DataAccess-Attributs auf DataAccessKind.None und des SystemDataAccess-Attributs auf SystemDataAccessKind.None bestimmt.|  
    |EXTERNAL ACCESS = NO|Diese Eigenschaft ist für CLR-Routinen standardmäßig auf NO festgelegt.|  
  
-   Die Sicht muss mithilfe der Option WITH SCHEMABINDING erstellt werden.  
  
-   Die Sicht darf nur auf Basistabellen in derselben Datenbank wie die Sicht verweisen. Die Sicht kann nicht auf andere Sichten verweisen.  
  
-   Die SELECT-Anweisung in der Sichtdefinition darf die folgenden Transact-SQL-Elemente nicht enthalten:  
  
    ||||  
    |-|-|-|  
    |COUNT|ROWSET-Funktionen (OPENDATASOURCE, OPENQUERY, OPENROWSET UND OPENXML)|OUTER-Joins (LEFT, RIGHT oder FULL)|  
    |Abgeleitete Tabelle (durch Angabe einer SELECT-Anweisung in der FROM-Klausel definiert)|Selbstjoins|Durch Angeben von Spalten mit SELECT \* oder SELECT *Tabellenname*.*|  
    |DISTINCT|STDEV, STDEVP, VAR, VARP oder AVG|Allgemeine Tabellenausdrücke (CTE, Common Table Expression)|  
    |**float**\*-, **text**-, **ntext**-, **image**-, **XML**- oder **filestream** -Spalten|Unterabfrage|Die OVER-Klausel, die Fensterrang- oder Fensteraggregatfunktionen enthält.|  
    |Volltextprädikate (CONTAIN, FREETEXT)|Eine SUM-Funktion, die auf einen Ausdruck verweist, der NULL zulässt.|ORDER BY|  
    |CLR-benutzerdefinierte Aggregatfunktion|NACH OBEN|Die Operatoren CUBE, ROLLUP oder GROUPING SETS|  
    |MIN, MAX|Die Operatoren UNION, EXCEPT oder INTERSECT|TABLESAMPLE|  
    |Tabellenvariablen|OUTER APPLY oder CROSS APPLY|PIVOT, UNPIVOT|  
    |Spaltensätze mit geringer Dichte|Tabellenwertfunktionen mit Inlinefunktionen oder Funktionen mit mehreren Anweisungen|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*Die indizierte Sicht kann Spalten mit dem Datentyp **float** enthalten. Allerdings dürfen solche Spalten nicht im Schlüssel des gruppierten Indexes enthalten sein.  
  
-   Wenn GROUP BY vorhanden ist, muss die VIEW-Definition COUNT_BIG(*) enthalten, während HAVING nicht enthalten sein darf. Diese GROUP BY-Einschränkungen gelten nur für die indizierte Sichtdefinition. Im Ausführungsplan einer Abfrage kann eine indizierte Sicht auch dann verwendet werden, wenn sie diese GROUP BY-Einschränkungen nicht erfüllt.  
  
-   Wenn die Sichtdefinition eine GROUP BY-Klausel enthält, kann der Schlüssel des eindeutigen gruppierten Index nur auf die Spalten verweisen, die in der GROUP BY-Klausel angegeben sind.  
  
###  <a name="Recommendations"></a> Empfehlungen  
 Wenn Sie in indizierten Sichten auf **datetime** - und **smalldatetime** -Zeichenfolgenliterale verweisen, wird empfohlen, das Literal mithilfe eines deterministischen Datenformats explizit in den gewünschten Datentyp zu konvertieren. Eine Liste der deterministischen Datenformatstile finden Sie unter [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md). Ausdrücke, die eine implizite Konvertierung von Zeichenfolgen in **datetime** oder **smalldatetime** umfassen, werden als nicht deterministisch angesehen. Der Grund hierfür ist, dass die Ergebnisse von den LANGUAGE- und DATEFORMAT-Einstellungen der Serversitzung abhängen. Die Ergebnisse des Ausdrucks `CONVERT (datetime, '30 listopad 1996', 113)` hängen beispielsweise von der LANGUAGE-Einstellung ab, da die Zeichenfolge '`listopad`' für verschiedene Monate in verschiedenen Sprachen steht. In ähnlicher Weise interpretiert `DATEADD(mm,3,'2000-12-01')`in dem Ausdruck [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Zeichenfolge `'2000-12-01'` basierend auf der DATEFORMAT-Einstellung.  
  
 Die implizierte Konvertierung von Nicht-Unicode-Zeichendaten zwischen Sortierungen wird auch als nicht deterministisch angesehen.  
  
###  <a name="Considerations"></a> Weitere Überlegungen  
 Die Einstellung der Option **large_value_types_out_of_row** der Spalten in einer indizierten Sicht wird von der Einstellung für die entsprechende Spalte in der Basistabelle vererbt. Dieser Wert wird mithilfe von [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)festgelegt. Die Standardeinstellung für Spalten, die auf Grundlage von Ausdrücken erstellt werden, ist 0. Das bedeutet, dass umfangreiche Werte innerhalb der Zeile gespeichert werden.  
  
 Indizierte Sichten können für eine partitionierte Tabelle erstellt werden und selbst partitioniert werden.  
  
 Wenn Sie verhindern möchten, dass [!INCLUDE[ssDE](../../includes/ssde-md.md)] indizierte Sichten verwendet, schließen Sie den OPTION (EXPAND VIEWS)-Hinweis in die Abfrage ein. Außerdem kann der Optimierer die Indizes für die Sichten nicht verwenden, wenn eine der aufgeführten Optionen falsch festgelegt ist. Weitere Informationen zum OPTION (EXPAND VIEWS)-Hinweis finden Sie unter [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
 Wenn eine Sicht gelöscht wird, werden alle Indizes für diese Sicht gelöscht. Wird der gruppierte Index einer Sicht gelöscht, werden alle nicht gruppierten Indizes und alle automatisch erstellten Statistiken der Sicht gelöscht. Vom Benutzer erstellte Statistiken zur Sicht werden beibehalten. Nicht gruppierte Indizes können einzeln gelöscht werden. Durch das Löschen des gruppierten Index der Sicht wird das gespeicherte Resultset entfernt, und der Optimierer verarbeitet die Sicht von nun an wieder wie eine Standardsicht.  
  
 Indizes für Tabellen und Sichten können deaktiviert werden. Wenn ein gruppierter Index für eine Tabelle deaktiviert wird, werden Indizes für die den Tabellen zugeordneten Sichten auch deaktiviert.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CREATE VIEW-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Sicht erstellt wird.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-an-indexed-view"></a>So erstellen Sie eine indizierte Sicht  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. Im Beispiel werden eine Sicht und ein Index für diese Sicht erstellt. Dies beinhaltet zwei Abfragen, in denen die indizierte Sicht verwendet wird.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
