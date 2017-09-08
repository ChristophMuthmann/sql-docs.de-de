---
title: Erstellen von VIEW (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
caps.latest.revision: 85
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9c47fbc342ac911cba103f34ccebafd84af8432a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-view-transact-sql"></a>CREATE VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt eine virtuelle Tabelle, deren Inhalt (Spalten und Zeilen) durch eine Abfrage definiert wird. Verwenden Sie diese Anweisung, um in einer oder mehreren Tabellen in der Datenbank eine Sicht der Daten zu erstellen. Eine Sicht kann z. B. für folgende Zwecke verwendet werden:  
  
-   Um die Darstellung einer Datenbank für jeden einzelnen Benutzer einzuschränken, zu vereinfachen und anzupassen.  
  
-   Als Sicherheitsmechanismus, indem Benutzern der Zugriff auf Daten über die Sicht ermöglicht wird, ohne diesen Benutzern jedoch die Berechtigungen für den direkten Zugriff auf die zugrunde liegenden Basistabellen zu gewähren.  
  
-   Um eine abwärtskompatible Schnittstelle zum Emulieren einer Tabelle bereitzustellen, deren Schema geändert wurde.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] VIEW [ schema_name . ] view_name [ (column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ]   
[ ; ]  
  
<view_attribute> ::=   
{  
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE VIEW [ schema_name . ] view_name [  ( column_name [ ,...n ] ) ]   
AS <select_statement>   
[;]  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>Argumente
ODER ÄNDERN  
 **Gilt für**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).   
  
 Bedingt ändert die Ansicht nur, wenn sie bereits vorhanden ist. 
 
 *schema_name*  
 Ist der Name des Schemas, zu dem die Sicht gehört.  
  
 *view_name*  
 Ist der Name der Sicht. Sichtnamen müssen den Regeln für Bezeichner entsprechen. Das Angeben des Sichtbesitzernamens ist optional.  
  
 *Spalte*  
 Der Name, den eine Spalte in einer Sicht erhalten soll. Das Angeben eines Spaltennamens ist nur erforderlich, wenn eine Spalte von einem arithmetischen Ausdruck, einer Funktion oder einer Konstanten abgeleitet wird oder wenn zwei oder mehr Spalten sonst denselben Namen haben können (gewöhnlich aufgrund eines Joins) oder aber wenn für die Spalte in einer Sicht ein anderer Name angegeben ist als die Spalte, von der sie abgeleitet wurde. Spaltennamen können auch in der SELECT-Anweisung zugewiesen werden.  
  
 Wenn *Spalte* nicht angegeben ist, werden die Spalten der Sicht abzurufen, die gleichen Namen wie die Spalten in der SELECT-Anweisung.  
  
> [!NOTE]  
>  In den Spalten für die Sicht gelten die Berechtigungen für einen Spaltennamen über eine CREATE VIEW- oder ALTER VIEW-Anweisung hinaus, unabhängig von der Quelle der zugrunde liegenden Daten. Z. B. Berechtigungen für die **SalesOrderID** Spalte in einer CREATE VIEW-Anweisung, eine ALTER VIEW-Anweisung können Sie benennen die **SalesOrderID** Spalte mit einem anderen Spaltennamen, z. B. **OrderRef**, und die Ansicht mit zugeordneten Berechtigungen haben weiterhin **SalesOrderID**.  
  
 AS  
 Gibt die Aktionen an, die die Sicht ausführen soll.  
  
 *select_statement*  
 Die SELECT-Anweisung, die die Sicht definiert. In der Anweisung dürfen mehrere Tabellen und andere Sichten angegeben werden. Sie müssen über die entsprechenden Berechtigungen verfügen, um aus den Objekten auszuwählen, auf die in der SELECT-Klausel der erstellten Sicht verwiesen wird.  
  
 Eine Sicht muss nicht unbedingt eine einfache Teilmenge der Zeilen und Spalten einer bestimmten Tabelle sein. Mithilfe einer SELECT-Klausel beliebiger Komplexität kann auch eine Sicht erstellt werden, die mehr als eine Tabelle oder andere Sichten verwendet.  
  
 In einer indizierten Sichtdefinition muss die SELECT-Anweisung aus einer nur eine Tabelle betreffenden Anweisung oder aus einer sich über mehrere Tabellen erstreckenden JOIN-Anweisung mit optionaler Aggregation bestehen.  
  
 In der SELECT-Klausel einer Sichtdefinition darf Folgendes nicht enthalten sein:  
  
-   Eine ORDER BY-Klausel, es sei denn, eine TOP-Klausel ist in der Auswahlliste der SELECT-Anweisung vorhanden  
  
    > [!IMPORTANT]  
    >  Die ORDER BY-Klausel wird lediglich zur Ermittlung der Zeilen verwendet, die von der TOP- oder OFFSET-Klausel in der Sichtdefinition zurückgegeben werden. Durch die ORDER BY-Klausel wird keine bestimmte Ergebnisreihenfolge bei der Abfrage der Sicht sichergestellt, es sei denn, in der Abfrage selbst ist ebenfalls ORDER BY angegeben.  
  
-   Das INTO-Schlüsselwort  
  
-   Die OPTION-Klausel  
  
-   Ein Verweis auf eine temporäre Tabelle oder auf eine Tabellenvariable  
  
 Da *Select_statement* verwendet die SELECT-Anweisung, es ist zulässig, verwenden Sie \<Join_hint > und \<Table_hint > Hinweise, wie in der FROM-Klausel angegeben. Weitere Informationen finden Sie unter [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md) und [SELECT &#40; Transact-SQL &#41; ](../../t-sql/queries/select-transact-sql.md). 
  
 Funktionen und mehrere SELECT-Anweisungen, die durch UNION oder UNION ALL getrennt in verwendet werden können *Select_statement*.  
  
 CHECK OPTION  
 Erzwingt, dass alle datenänderungsanweisungen, die für die Sicht, die innerhalb von festgelegten Kriterien folgen ausgeführten *Select_statement*. Wenn durch eine Sicht eine Zeile geändert wird, stellt WITH CHECK OPTION sicher, dass die Daten nach dem Ausführen eines Commits für die Änderung in der Sicht weiterhin angezeigt werden.  
  
> [!NOTE]  
>  Alle Updates, die direkt für die zugrunde liegenden Tabellen einer Sicht durchgeführt werden, werden nicht anhand der Sicht geprüft, auch wenn CHECK OPTION angegeben ist.  
  
 ENCRYPTION  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Verschlüsselt die Einträge in [sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md) , die den Text der CREATE VIEW-Anweisung enthalten. Mit WITH ENCRYPTION kann verhindert werden, dass die Sicht als Teil der SQL Server-Replikation veröffentlicht wird.  
  
 SCHEMABINDING  
 Bindet die Sicht an das Schema der zugrunde liegenden Basistabellen. Wenn SCHEMABINDING angegeben ist, können an der/den Basistabelle(n) keine Änderungen vorgenommen werden, die die Sichtdefinition betreffen können. Zunächst muss die Sichtdefinition selbst geändert oder gelöscht werden, um Abhängigkeiten in der zu ändernden Tabelle zu entfernen. Wenn Sie SCHEMABINDING verwenden die *Select_statement* umfasst die mit dem zweiteiligen Namen (*Schema***.** *Objekt*) von Tabellen, Sichten oder benutzerdefinierten Funktionen, auf die verwiesen werden. Alle Objekte, auf die verwiesen wird, müssen in derselben Datenbank vorhanden sein.  
  
 Sichten oder Tabellen, die Bestandteil einer mit der SCHEMABINDING-Klausel erstellten Sicht sind, können erst dann gelöscht werden, wenn diese Sicht gelöscht oder geändert wurde, sodass keine Schemabindung mehr vorhanden ist. Andernfalls löst [!INCLUDE[ssDE](../../includes/ssde-md.md)] einen Fehler aus. Darüber hinaus schlagen ALTER TABLE-Anweisungen für Tabellen fehl, die Bestandteil von Sichten mit Schemabindung sind, wenn diese Anweisungen die Sichtdefinition betreffen.  
  
 VIEW_METADATA  
 Gibt an, dass die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Metadateninformationen der Sicht anstelle der Basistabelle(n) an die DB-Library-, ODBC- und OLE DB-APIs zurückgibt, wenn Metadaten des Durchsuchenmodus für eine Abfrage angefordert werden, die auf die Sicht verweist. Bei Metadaten des Durchsuchenmodus handelt es sich um zusätzliche Metadaten, die von der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an diese clientseitigen APIs zurückgegeben werden. Mithilfe dieser Metadaten können die clientbasierten APIs aktualisierbare clientbasierte Cursors implementieren. Metadaten des Durchsuchenmodus enthalten Informationen zu der Basistabelle, zu der die Spalten im Resultset gehören.  
  
 Bei Sichten, die mit VIEW_METADATA erstellt wurden, geben die Metadaten des Durchsuchenmodus den Sichtnamen anstelle der Basistabellennamen zurück, wenn Spalten aus der Sicht im Resultset beschrieben werden.  
  
 Wenn eine Sicht erstellt wird, mithilfe von WITH VIEW_METADATA alle enthaltenen Spalten außer einem **Zeitstempel** Spalte, aktualisierbar, falls die Sicht INSTEAD OF INSERT hat oder INSTEAD OF UPDATE-Trigger sind. Weitere Informationen zu aktualisierbaren Sichten finden Sie unter Hinweise.  
  
## <a name="remarks"></a>Hinweise  
 Eine Sicht kann nur in der aktuellen Datenbank erstellt werden. Bei CREATE VIEW muss es sich um die erste Anweisung in einem Abfragebatch handeln. Für eine Sicht sind maximal 1.024 Spalten zulässig.  
  
 Bei der Abfrage über eine Sicht der [!INCLUDE[ssDE](../../includes/ssde-md.md)] überprüft, um sicherzustellen, dass alle Datenbankobjekte, die an einer beliebigen Stelle in der Anweisung verwiesen vorhanden sind und dass sie im Kontext der Anweisung gültig sind, und Anweisungen zur Datenänderung keinen Daten verletzen Regeln der Datenintegrität. Schlägt eine Überprüfung fehl, wird eine Fehlermeldung zurückgegeben. Andernfalls wird die Aktion in eine Aktion für die zugrunde liegende Tabelle bzw. Tabellen übersetzt.  
  
 Wenn eine Sicht von einer Tabelle oder Sicht abhängt, die gelöscht wurde, erzeugt [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Fehlermeldung, wenn jemand versucht, die Sicht zu verwenden. Wenn eine neue Tabelle oder Sicht, deren Struktur sich nicht von der vorherigen Basistabelle unterscheidet, erstellt wird, um die gelöschte zu ersetzen, wird die Sicht wieder verwendbar. Wenn sich die Struktur der neuen Tabelle oder Sicht ändert, muss die Sicht gelöscht und neu erstellt werden.  
  
 Wenn eine Sicht nicht mit der SCHEMABINDING-Klausel erstellt wird [Sp_refreshview](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md) sollte ausgeführt werden, wenn Änderungen an den der Sicht zugrunde liegenden Objekten vorgenommen werden, die die Definition der Sicht betreffen. Andernfalls liefert die Abfrage der Sicht möglicherweise unerwartete Ergebnisse.  
  
 Wenn eine Sicht erstellt wird, wird der Informationen über die Ansicht in den folgenden Katalogsichten gespeichert: [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md), [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), und [Sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md). Der Text der CREATE VIEW-Anweisung befindet sich in der [sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) -Katalogsicht angezeigt.  
  
 Eine Abfrage, die einen Index für eine Sicht verwendet, die mit definierten **numerischen** oder **"float"** Ausdrücke möglicherweise als Ergebnis einer ähnlichen Abfrage unterscheiden, die den Index für die Sicht nicht verwendet. Dieser Unterschied kann durch Rundungsfehler während INSERT-, DELETE- oder UPDATE-Aktionen in den zugrunde liegenden Tabellen verursacht werden.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] speichert die Einstellungen für SET QUOTED_IDENTIFIER und SET ANSI_NULLS, wenn eine Sicht erstellt wird. Diese Originaleinstellungen werden zum Analysieren der Sicht wiederhergestellt, wenn die Sicht verwendet wird. Deshalb haben alle Clientsitzungseinstellungen für SET QUOTED_IDENTIFIER und SET ANSI_NULLS keine Auswirkungen auf die Sichtdefinition, wenn auf die Sicht zugegriffen wird.  
  
## <a name="updatable-views"></a>Aktualisierbare Sichten  
 Sie können die Daten einer zugrunde liegenden Basistabelle über eine Sicht ändern, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Alle Änderungen, einschließlich UPDATE-, INSERT- und DELETE-Anweisungen, dürfen nur von einer Basistabelle aus auf Spalten verweisen.  
  
-   Die Spalten, die in der Sicht geändert werden, müssen direkt auf die zugrunde liegenden Daten der Tabellenspalten verweisen. Die Spalten können nicht auf andere Art abgeleitet werden, wie etwa über:  
  
    -   Eine Aggregatfunktion: AVG, COUNT, SUM, MIN, MAX, GROUPING, STDEV, STDEVP, VAR und VARP.  
  
    -   Eine Berechnung. Die Spalte kann mit einem Ausdruck, der andere Spalten verwendet, nicht berechnet werden. Spalten, die mithilfe der Mengenoperatoren UNION, UNION ALL, CROSSJOIN, EXCEPT und INTERSECT erstellt werden, werden berechnet und sind daher auch nicht aktualisierbar.  
  
-   Die geänderten Spalten sind von den GROUP BY-, HAVING- oder DISTINCT-Klauseln nicht betroffen.  
  
-   Nach oben werden nicht an einer beliebigen Stelle in der *Select_statement* der Sicht zusammen mit der WITH CHECK OPTION-Klausel.  
  
 Die vorigen Einschränkungen gelten, so wie für die Sicht selbst, für alle Unterabfragen in der FROM-Klausel der Sicht. Im Allgemeinen muss [!INCLUDE[ssDE](../../includes/ssde-md.md)] Änderungen von der Sichtdefinition an einer Basistabelle eindeutig nachverfolgen können. Weitere Informationen finden Sie unter [Ändern von Daten über eine Sicht](../../relational-databases/views/modify-data-through-a-view.md).  
  
 Wenn Sie aufgrund der vorigen Einschränkungen die Daten nicht direkt über eine Sicht ändern können, sollten Sie die folgenden Optionen berücksichtigen:  
  
-   **INSTEAD OF-Trigger**  
  
     Für eine Sicht können INSTEAD OF-Trigger erstellt werden, um sie aktualisierbar zu machen. Der INSTEAD OF-Trigger wird anstelle der Datenänderungsanweisung ausgeführt, für die der Trigger definiert ist. Mithilfe dieses Triggers kann der Benutzer die Gruppe von Aktionen angeben, die erforderlich sind, um die Datenänderungsanweisung zu verarbeiten. Wenn also ein INSTEAD OF-Trigger einer Sicht für eine angegebene Datenänderungsanweisung (INSERT, UPDATE oder DELETE) vorhanden ist, ist die entsprechende Sicht über diese Anweisung aktualisierbar. Weitere Informationen zu INSTEAD OF-Trigger finden Sie unter [DML-Triggern](../../relational-databases/triggers/dml-triggers.md).  
  
-   **Partitionierte Sichten**  
  
     Wenn es sich bei der Sicht um eine partitionierte Sicht handelt, ist sie mit gewissen Einschränkungen aktualisierbar. Bei Bedarf unterscheidet [!INCLUDE[ssDE](../../includes/ssde-md.md)] zwischen lokalen partitionierten Sichten (als Sichten, bei denen sich alle beteiligten Tabellen und die jeweilige Sicht selbst auf derselben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz befinden) und verteilten partitionierten Sichten (als Sichten, bei denen sich mindestens eine der Tabellen auf einem anderen Server oder Remoteserver befindet).  
  
## <a name="partitioned-views"></a>Partitionierte Sichten  
 Bei einer partitionierten Sicht handelt es sich um eine Sicht, die durch eine UNION ALL-Anweisung von Mitgliedstabellen definiert ist, die dieselbe Struktur aufweisen, jedoch getrennt voneinander in mehreren Tabellen entweder in derselben Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder in einer Gruppe von eigenständigen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Servern gespeichert sind, die vereinte Datenbankserver genannt werden.  
  
> [!NOTE]  
>  Die bevorzugte Methode zum lokalen Partitionieren von Daten auf einem Server ist die mithilfe partitionierter Tabellen. Weitere Informationen finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Beim Entwurf eines Partitionierungsschemas muss offensichtlich sein, welche Daten zu den einzelnen Partitionen gehören. Die Daten der `Customers`-Tabelle sind beispielsweise auf drei Mitgliedstabellen an drei Serverstandorten verteilt: `Customers_33` auf `Server1`, `Customers_66` auf `Server2` und `Customers_99` auf `Server3`.  
  
 Eine partitionierte Sicht auf `Server1` wird wie folgt definiert:  
  
```  
--Partitioned view as defined on Server1  
CREATE VIEW Customers  
AS  
--Select from local member table.  
SELECT *  
FROM CompanyData.dbo.Customers_33  
UNION ALL  
--Select from member table on Server2.  
SELECT *  
FROM Server2.CompanyData.dbo.Customers_66  
UNION ALL  
--Select from mmeber table on Server3.  
SELECT *  
FROM Server3.CompanyData.dbo.Customers_99;  
```  
  
 Im Allgemeinen gilt eine Sicht als partitioniert, wenn sie die folgende Form aufweist:  
  
```  
SELECT <select_list1>  
FROM T1  
UNION ALL  
SELECT <select_list2>  
FROM T2  
UNION ALL  
...  
SELECT <select_listn>  
FROM Tn;  
```  
  
## <a name="conditions-for-creating-partitioned-views"></a>Bedingungen für das Erstellen von partitionierten Sichten  
  
1.  Die SELECT-`list`  
  
    -   In der Spaltenliste der Sichtdefinition sollten alle Spalten der Mitgliedstabellen aufgeführt sein.  
  
    -   Die Spalten an derselben Ordnungsposition jeder `select list` sollten denselben Typ haben, einschließlich Sortierungen. Es ist nicht ausreichend, wenn die Spalten implizit konvertierbar sind, wie dies für UNION generell der Fall ist.  
  
         Demnach muss mindestens eine Spalte (z. B. `<col>`) in allen SELECT-Listen an derselben Ordnungsposition vorhanden sein. Diese `<col>`-Spalte sollte so definiert sein, dass die Mitgliedstabellen `T1, ..., Tn` über CHECK-Einschränkungen `C1, ..., Cn` verfügen, die entsprechend in `<col>` definiert sind.  
  
         Die für `C1` definierte Einschränkung `T1` muss die folgende Form haben:  
  
        ```  
        C1 ::= < simple_interval > [ OR < simple_interval > OR ...]  
        < simple_interval > :: =   
        < col > { < | > | \<= | >= | = < value >}   
        | < col > BETWEEN < value1 > AND < value2 >  
        | < col > IN ( value_list )  
        | < col > { > | >= } < value1 > AND  
        < col > { < | <= } < value2 >  
        ```  
  
    -   Die Einschränkungen müssen so festgelegt sein, dass jeder angegebene Wert von `<col>` höchstens eine der Einschränkungen `C1, ..., Cn` erfüllt, sodass die Einschränkungen eine Gruppe von getrennten oder nicht überlappenden Intervallen bilden. Die `<col>`-Spalte, für die die getrennten Einschränkungen definiert sind, wird Partitionierungsspalte genannt. Beachten Sie, dass die Partitionierungsspalte in den zugrunde liegenden Tabellen unterschiedliche Namen haben kann. Die Einschränkungen sollten sich im enabled- und trusted-Status befinden, damit sie die zuvor genannten Bedingungen für die Partitionierungsspalte erfüllen. Ist die Einschränkungen deaktiviert sind, erneut aktivieren, die einschränkungsüberprüfung mithilfe der CHECK-Einschränkung *Constraint_name* -Option von ALTER TABLE, und verwenden die WITH CHECK Option um zu überprüfen.  
  
         Die folgenden Beispiele zeigen gültige Einschränkungsgruppen:  
  
        ```  
        { [col < 10], [col between 11 and 20] , [col > 20] }  
        { [col between 11 and 20], [col between 21 and 30], [col between 31 and 100] }  
        ```  
  
    -   Die mehrfache Verwendung einer Spalte in der Auswahlliste ist nicht zulässig.  
  
2.  Partitionierungsspalte  
  
    -   Die Partitionierungsspalte ist Teil der PRIMARY KEY-Einschränkung der Tabelle.  
  
    -   Eine Identitätspalte, in der Standardeinstellung kann nicht mehr oder **Zeitstempel** Spalte.  
  
    -   Wenn es für eine Spalte einer Mitgliedstabelle mehrere Einschränkungen gibt, ignoriert das Datenbankmodul alle diese Einschränkungen und berücksichtigt sie nicht, wenn ermittelt wird, ob die Sicht eine partitionierte Sicht ist. Damit die Bedingungen für partitionierte Sichten erfüllt werden, sollte es für die Partitionierungsspalte nur eine Partitionierungseinschränkung geben.  
  
    -   Für Partitionierungsspalten gelten keine Einschränkungen hinsichtlich der Aktualisierbarkeit.  
  
3.  Mitgliedstabellen oder zugrunde liegende Tabellen `T1, ..., Tn`  
  
    -   Bei den Tabellen kann es sich entweder um lokale Tabellen oder um Tabellen von anderen Computern handeln, auf denen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, auf die entweder über einen vierteiligen Namen oder einen OPENDATASOURCE- oder OPENROWSET-basierten Namen verwiesen wird. Die OPENDATASOURCE- und OPENROWSET-Syntax kann zwar einen Tabellennamen angeben, nicht jedoch eine Pass-Through-Abfrage. Weitere Informationen finden Sie unter [OPENDATASOURCE &#40; Transact-SQL &#41; ](../../t-sql/functions/opendatasource-transact-sql.md) und [OPENROWSET &#40; Transact-SQL &#41; ](../../t-sql/functions/openrowset-transact-sql.md).  
  
         Falls eine oder mehrere Mitgliedstabellen Remotetabellen sind, wird die Sicht verteilte partitionierte Sicht genannt, und es gelten zusätzliche Bedingungen. Diese werden weiter unten in diesem Abschnitt beschrieben.  
  
    -   Eine Tabelle darf nicht zweimal in der Tabellengruppe enthalten sein, die mithilfe der UNION ALL-Anweisung kombiniert werden.  
  
    -   Die Mitgliedstabellen dürfen nicht über Indizes verfügen, die für berechnete Spalten der Tabelle erstellt werden.  
  
    -   Für alle Mitgliedstabellen sollte gelten, dass ihre PRIMARY KEY-Einschränkungen auf gleich vielen Spalten basieren.  
  
    -   Alle Mitgliedstabellen einer Sicht sollten dieselbe Einstellung für die ANSI-Auffüllung aufweisen. Dies kann festgelegt werden, indem Sie entweder die **Benutzeroptionen** option **Sp_configure** oder SET-Anweisung.  
  
## <a name="conditions-for-modifying-data-in-partitioned-views"></a>Bedingungen für das Ändern von Daten in partitionierten Sichten  
 Die folgenden Einschränkungen gelten für Anweisungen, die Daten in partitionierten Sichten ändern:  
  
-   Die INSERT-Anweisung muss für alle Spalten in der Sicht Werte bereitstellen, auch wenn die zugrunde liegenden Mitgliedstabellen über eine DEFAULT-Einschränkung für diese Spalten verfügen oder NULL-Werte zulassen. Für diese Spalten in der Mitgliedstabelle, die über DEFAULT-Definitionen verfügen, können die Anweisungen nicht explizit das DEFAULT-Schlüsselwort verwenden.  
  
-   Der in die Partitionierungsspalte eingefügte Wert sollte mindestens eine der zugrunde liegenden Einschränkungen erfüllen. Andernfalls schlägt die INSERT-Aktion mit einer Einschränkungsverletzung fehl.  
  
-   In einer UPDATE-Anweisung darf das Schlüsselwort DEFAULT nicht als Wert in der SET-Klausel angegeben werden. Dies gilt selbst dann, wenn in der entsprechenden Mitgliedstabelle ein DEFAULT-Wert definiert ist.  
  
-   Die in der Sicht enthaltenen Spalten, bei denen es sich um eine IDENTITY-Spalte in einer oder mehreren Mitgliedstabellen handelt, können nicht mit der INSERT- oder UPDATE-Anweisung geändert werden.  
  
-   Wenn eine der Mitgliedstabellen enthält eine **Zeitstempel** Spalte, die Daten können nicht mithilfe einer INSERT- oder UPDATE-Anweisung geändert werden.  
  
-   Wenn eine der Mitgliedstabellen einen Trigger oder eine ON UPDATE CASCADE/SET NULL/SET DEFAULT- oder ON DELETE CASCADE/SET NULL/SET DEFAULT-Einschränkung hat, kann die Sicht nicht geändert werden.  
  
-   INSERT-, UPDATE- und DELETE-Aktionen für eine partitionierte Sicht sind nicht zulässig, wenn ein Selbstjoin mit derselben Sicht oder mit einer der Mitgliedstabelle in der Anweisung vorhanden ist.  
  
-   Massenimport von Daten in eine partitionierte Sicht wird nicht unterstützt, **Bcp** BULK INSERT oder INSERT... SELECT * FROM OPENROWSET(BULK...)-Anweisungen per Massenimport übertragen werden. Sie können jedoch mehrere Zeilen in eine partitionierte Sicht einfügen, mit der [einfügen](../../t-sql/statements/insert-transact-sql.md) Anweisung.  
  
    > [!NOTE]  
    >  Zum Aktualisieren einer partitionierten Sicht benötigt der Benutzer INSERT-, UPDATE- und DELETE-Berechtigungen für die Mitgliedstabellen.  
  
## <a name="additional-conditions-for-distributed-partitioned-views"></a>Zusätzliche Bedingungen für verteilte partitionierte Sichten  
 Für verteilte partitionierte Sichten (bei denen eine oder mehrere Mitgliedstabellen Remotetabellen sind), gelten zusätzlich die folgenden Bedingungen:  
  
-   Eine verteilte Transaktion wird in allen Knoten, die vom Update betroffenen Unteilbarkeit garantieren gestartet werden.  
  
-   Die Option XACT_ABORT SET sollte auf ON festgelegt werden, damit INSERT-, UPDATE- oder DELETE-Anweisungen funktionieren.  
  
-   Alle Spalten in Remotetabellen vom Typ **Smallmoney** verwiesen wird, werden in einer partitionierten Sicht zugeordnet sind, als **Money**. Aus diesem Grund müssen die entsprechenden Spalten (in derselben Ordnungsposition in der Auswahlliste) in den lokalen Tabellen auch werden vom Typ **Money**.  
  
-   Unter Datenbank-Kompatibilitätsgrad 110 und höher werden alle Spalten in Remotetabellen vom Typ **Smalldatetime** verwiesen wird, werden in einer partitionierten Sicht zugeordnet sind, als **Smalldatetime**. Entsprechende Spalten (in derselben Ordnungsposition in der Auswahlliste) in den lokalen Tabellen muss **Smalldatetime**. Dies ist eine Änderung im Verhalten unterscheidet sich von früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in dem alle Spalten in Remotetabellen vom Typ **Smalldatetime** verwiesen wird, werden in einer partitionierten Sicht zugeordnet sind, als **"DateTime"** und entsprechende Spalten in lokalen Tabellen muss vom Typ **"DateTime"**. Weitere Informationen finden Sie unter [ALTER DATABASE-Kompatibilitätsgrad &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
-   Ein an der partitionierten Sicht beteiligter Verbindungsserver kann kein Loopback-Verbindungsserver sein. Dies ist ein Verbindungsserver, der auf dieselbe Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verweist.  
  
 Die Einstellung der Option SET ROWCOUNT wird für INSERT-, UPDATE- und DELETE-Aktionen ignoriert, die aktualisierbare partitionierte Sichten und Remotetabellen betreffen.  
  
 Wenn die Mitgliedstabellen und die partitionierte Sichtdefinition vorhanden sind, erstellt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageoptimierer intelligente Pläne, die Abfragen zum effizienten Zugriff auf Daten in den Mitgliedstabellen verwenden. Mit den CHECK-Einschränkungsdefinitionen kann der Abfrageprozessor die Verteilung der Schlüsselwerte den Mitgliedstabellen zuordnen. Wenn ein Benutzer eine Abfrage ausgibt, vergleicht der Abfrageprozessor die Zuordnung mit den in der WHERE-Klausel angegebenen Werten und erstellt einen Ausführungsplan, für den nur eine minimale Menge an Daten zwischen den Mitgliedsservern übertragen werden muss. Obwohl einige Mitgliedstabellen möglicherweise auf Remoteservern gespeichert sind, löst die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] daher verteilte Abfragen so auf, dass nur eine minimale Menge von verteilten Daten übertragen werden muss.  
  
## <a name="considerations-for-replication"></a>Überlegungen zur Replikation  
 Die folgenden Überlegungen sind erforderlich, wenn Sie partitionierte Sichten für Mitgliedstabellen erstellen, die an der Replikation beteiligt sind:  
  
-   Wenn die zugrunde liegenden Tabellen Merge- oder Transaktionsreplikation mit updateabonnements beteiligt sind die **"uniqueidentifier"** Spalte auch in der select-Liste eingeschlossen werden soll.  
  
     Alle INSERT-Aktionen in der partitionierten Sicht müssen einen NEWID()-Wert für Bereitstellen der **"uniqueidentifier"** Spalte. UPDATE-Aktionen für die **"uniqueidentifier"** -Spalte muss NEWID() als Wert angeben, da das DEFAULT-Schlüsselwort verwendet werden kann.  
  
-   Die Replikation von Updates, die mithilfe der Sicht ausgeführt werden, entspricht der Replikation von Tabellen in zwei verschiedenen Datenbanken: Die Tabellen werden von unterschiedlichen Replikations-Agents bedient, und die Reihenfolge der Updates ist nicht sichergestellt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE VIEW-Berechtigung in der Datenbank und die ALTER-Berechtigung für das Schema, in dem die Sicht erstellt wird.  
  
## <a name="examples"></a>Beispiele  

Die folgenden Beispiele verwenden die AdventureWorks 2012 oder AdventureWorksDW-Datenbank.  

### <a name="a-using-a-simple-create-view"></a>A. Verwenden einer einfachen CREATE VIEW-Anweisung  
 Im folgenden Beispiel wird mithilfe einer einfachen `SELECT`-Anweisung eine Sicht erstellt. Eine einfache Sicht ist hilfreich, wenn eine Kombination mehrerer Spalten häufig abgefragt wird. Die Daten dieser Sicht stammen aus den `HumanResources.Employee`- und `Person.Person`-Tabellen der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank. Mit diesen Daten werden Name und Einstellungsdatum der Mitarbeiter von [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] bereitgestellt. Die Sicht könnte für die Person erstellt werden, die für die Nachverfolgung von Jubiläen verantwortlich ist. Dabei wird dieser Person nicht der Zugriff auf alle Daten dieser Tabellen gewährt.  
  
```  
CREATE VIEW hiredate_view  
AS   
SELECT p.FirstName, p.LastName, e.BusinessEntityID, e.HireDate  
FROM HumanResources.Employee e   
JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
### <a name="b-using-with-encryption"></a>B. Verwenden von WITH ENCRYPTION  
 Das folgende Beispiel verwendet die Option `WITH ENCRYPTION` und zeigt berechnete, umbenannte und mehrfache Spalten.  
  
**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] über [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
CREATE VIEW Purchasing.PurchaseOrderReject  
WITH ENCRYPTION  
AS  
SELECT PurchaseOrderID, ReceivedQty, RejectedQty,   
    RejectedQty / ReceivedQty AS RejectRatio, DueDate  
FROM Purchasing.PurchaseOrderDetail  
WHERE RejectedQty / ReceivedQty > 0  
AND DueDate > CONVERT(DATETIME,'20010630',101) ;  
GO  
  
```  
  
### <a name="c-using-with-check-option"></a>C. Verwenden von WITH CHECK OPTION  
 Im folgenden Beispiel wird die Sicht mit dem Namen `SeattleOnly` gezeigt, die auf fünf Tabellen verweist und Datenänderungen nur bei Mitarbeitern zulässt, die in Seattle leben.  
  
```  
CREATE VIEW dbo.SeattleOnly  
AS  
SELECT p.LastName, p.FirstName, e.JobTitle, a.City, sp.StateProvinceCode  
FROM HumanResources.Employee e  
INNER JOIN Person.Person p  
ON p.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN Person.BusinessEntityAddress bea   
    ON bea.BusinessEntityID = e.BusinessEntityID   
    INNER JOIN Person.Address a   
    ON a.AddressID = bea.AddressID  
    INNER JOIN Person.StateProvince sp   
    ON sp.StateProvinceID = a.StateProvinceID  
WHERE a.City = 'Seattle'  
WITH CHECK OPTION ;  
GO  
```  
  
### <a name="d-using-built-in-functions-within-a-view"></a>D. Verwenden integrierter Funktionen innerhalb einer Sicht  
 Das folgende Beispiel zeigt die Definition einer Sicht, die eine integrierte Funktion enthält. Wenn Sie Funktionen verwenden, müssen Sie für die abgeleitete Spalte einen Spaltennamen angeben.  
  
```  
CREATE VIEW Sales.SalesPersonPerform  
AS  
SELECT TOP (100) SalesPersonID, SUM(TotalDue) AS TotalSales  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > CONVERT(DATETIME,'20001231',101)  
GROUP BY SalesPersonID;  
GO  

```  
  
### <a name="e-using-partitioned-data"></a>E. Verwenden von partitionierten Daten  
 Das folgende Beispiel verwendet Tabellen mit den Namen `SUPPLY1`, `SUPPLY2`, `SUPPLY3` und `SUPPLY4`. Diese Tabellen entsprechen den Lieferantentabellen von vier Büros in verschiedenen Ländern/Regionen.  
  
```  
--Create the tables and insert the values.  
CREATE TABLE dbo.SUPPLY1 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 1 and 150),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY2 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 151 and 300),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY3 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 301 and 450),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY4 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 451 and 600),  
supplier CHAR(50)  
);  
GO  
INSERT dbo.SUPPLY1 VALUES ('1', 'CaliforniaCorp'), ('5', 'BraziliaLtd')  
, ('231', 'FarEast'), ('280', 'NZ')  
, ('321', 'EuroGroup'), ('442', 'UKArchip')  
, ('475', 'India'), ('521', 'Afrique');  
GO  
--Create the view that combines all supplier tables.  
CREATE VIEW dbo.all_supplier_view  
WITH SCHEMABINDING  
AS  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY1  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY2  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY3  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY4;  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-creating-a-simple-view"></a>F. Erstellen eine einfache Sicht  
 Im folgende Beispiel erstellt eine Ansicht, indem Sie nur einige Spalten aus der Quelltabelle auswählen.  
  
```  
CREATE VIEW DimEmployeeBirthDates AS  
SELECT FirstName, LastName, BirthDate   
FROM DimEmployee;  
```  
  
### <a name="g-create-a-view-by-joining-two-tables"></a>G. Erstellen Sie eine Ansicht, indem Sie zwei Tabellen verknüpfen  
 Das folgende Beispiel erstellt eine Sicht mit einem `SELECT` -Anweisung mit einer `OUTER JOIN`. Die Ergebnisse der Abfrage Joins füllen Sie die Ansicht.  
  
```  
CREATE VIEW view1  
AS 
SELECT fis.CustomerKey, fis.ProductKey, fis.OrderDateKey, 
  fis.SalesTerritoryKey, dst.SalesTerritoryRegion  
FROM FactInternetSales AS fis   
LEFT OUTER JOIN DimSalesTerritory AS dst   
ON (fis.SalesTerritoryKey=dst.SalesTerritoryKey);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP VIEW &#40; Transact-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [Sp_refreshview &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Sys.Views &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


