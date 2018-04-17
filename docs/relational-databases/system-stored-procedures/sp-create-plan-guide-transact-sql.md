---
title: Sp_create_plan_guide (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide
- sp_create_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide
ms.assetid: 5a8c8040-4f96-4c74-93ab-15bdefd132f0
caps.latest.revision: 82
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d213b79938f0856d9e17b36366958a89e7ecd2be
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spcreateplanguide-transact-sql"></a>sp_create_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Planhinweisliste für die Zuordnung von Abfragehinweisen oder tatsächlichen Abfrageplänen zu Abfragen in einer Datenbank. Weitere Informationen zu Planhinweislisten finden Sie unter [Planhinweislisten](../../relational-databases/performance/plan-guides.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_create_plan_guide [ @name = ] N'plan_guide_name'  
    , [ @stmt = ] N'statement_text'  
    , [ @type = ] N'{ OBJECT | SQL | TEMPLATE }'  
    , [ @module_or_batch = ]  
      {   
                    N'[ schema_name. ] object_name'  
        | N'batch_text'  
        | NULL  
      }  
    , [ @params = ] { N'@parameter_name data_type [ ,...n ]' | NULL }   
    , [ @hints = ] { N'OPTION ( query_hint [ ,...n ] )'   
                 | N'XML_showplan'  
                 | NULL }  
```  
  
## <a name="arguments"></a>Argumente  
 [ @name =] N'*Plan_guide_name*"  
 Der Name der Planhinweisliste. Die Gültigkeit der Namen von Planhinweislisten beschränkt sich auf die aktuelle Datenbank. *Plan_guide_name* muss den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md) und kann nicht gestartet werden mit dem Nummernzeichen (#). Die maximale Länge des *Plan_guide_name* beträgt 124 Zeichen.  
  
 [ @stmt =] N'*Statement_text*"  
 Ist eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung, für die eine Planhinweisliste erstellt werden soll. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abfrageoptimierer erkennt eine Abfrage, die entspricht *Statement_text*, *Plan_guide_name* tritt in Kraft. Für die Erstellung einer Planhinweisliste erfolgreich ausgeführt werden kann *Statement_text* muss angezeigt werden, in dem durch angegebenen Kontext den @type, @module_or_batch, und @params Parameter.  
  
 *Statement_text* muss angegeben werden, auf eine Weise, die für die Übereinstimmung mit der entsprechenden Anweisung im Batch oder Modul, das durch den Abfrageoptimierer ermöglicht @module_or_batch und @params. Weitere Informationen finden Sie unter dem Abschnitt "Hinweise". Die Größe des *Statement_text* wird nur durch den verfügbaren Arbeitsspeicher des Servers beschränkt.  
  
 [@type =] N'{OBJECT | SQL | VORLAGE} "  
 Ist der Typ der Entität, in der *Statement_text* angezeigt wird. Dies gibt den Kontext für den Abgleich *Statement_text* auf *Plan_guide_name*.  
  
 OBJECT  
 Gibt an, *Statement_text* angezeigt wird, im Rahmen einer [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur, Skalarfunktion, aus mehreren Anweisungen bestehenden Funktion mit Tabellenrückgabe oder [!INCLUDE[tsql](../../includes/tsql-md.md)] DML-Trigger in der aktuellen Datenbank.  
  
 SQL  
 Gibt an, *Statement_text* wird im Kontext einer eigenständigen Anweisung oder eines Batches, die an gesendet werden kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf beliebige Weise. [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die durch die common Language Runtime (CLR)-Objekte oder erweiterte gespeicherte Prozeduren oder mithilfe von EXEC N vorgelegt "*Sql_string*", werden als Batches auf dem Server verarbeitet und aus diesem Grund sollte identifiziert werden, als @type **=** 'SQL'. Wenn SQL angegeben, der Abfragehinweis PARAMETERIZATION {FORCED | EINFACHE} kann nicht angegeben werden, der @hints Parameter.  
  
 TEMPLATE  
 Gibt an, die Planhinweisliste angewendet wird, um jede Abfrage, die auf die im angegebenen Format parametrisiert *Statement_text*. Wenn TEMPLATE angegeben ist, nur der PARAMETERIZATION {FORCED | EINFACHE}-Abfragehinweis kann angegeben werden, der @hints Parameter. Weitere Informationen zu TEMPLATE-Planhinweislisten finden Sie unter [angeben des Abfrageparametrisierungsverhaltens mithilfe von Planhinweislisten](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md).  
  
 [@module_or_batch =]{ N'[ *schema_name*. ] *Object_name*"| N'*Batch_text*"| NULL}  
 Gibt entweder den Namen des Objekts in der *Statement_text* angezeigt wird, oder den Batchtext ein, in dem *Statement_text* angezeigt wird. Der Batchtext kann nicht umfassen eine Verwendung*Datenbank* Anweisung.  
  
 Damit eine Planhinweisliste entsprechend einen Batch zugeordnet, die von einer Anwendung übermittelt *Batch_tex*t muss angegeben werden, im gleichen Format, Zeichen für Zeichen, wie beim Übermitteln an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es findet keine interne Konvertierung zur Vereinfachung dieses Abgleichs statt. Weitere Informationen finden Sie im Abschnitt mit Hinweisen.  
  
 [*Schema_name*.] *Object_name* gibt den Namen des eine [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur, Skalarfunktion, aus mehreren Anweisungen bestehenden Funktion mit Tabellenrückgabe oder [!INCLUDE[tsql](../../includes/tsql-md.md)] DML-Trigger, enthält *Statement_text*. Wenn *Schema_name* nicht angegeben ist, *Schema_name* verwendet das Schema des aktuellen Benutzers. Wenn NULL angegeben wird und @type = 'SQL', den Wert der @module_or_batch festgelegt ist, auf den Wert des @stmt. Wenn @type = "Vorlage**"**, @module_or_batch muss NULL sein.  
  
 [ @params =] {N' *@parameter_name Data_type* [,*.. ...n* ] "| NULL}  
 Gibt an, die Definitionen aller Parameter, die in eingebetteten *Statement_text*. @params gilt nur, wenn eines der folgenden Aussagen zutrifft:  
  
-   @type = 'SQL' oder 'TEMPLATE'. Wenn 'TEMPLATE' @params darf nicht NULL sein.  
  
-   *Statement_text* übermittelt wird, mithilfe von Sp_executesql und einen Wert für die @params Parameter angegeben wird, oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intern übermittelt eine Anweisung, nachdem Sie parametrisiert wurde. Die Übermittlung parametrisierter Abfragen von Datenbank-APIs (einschließlich ODBC, OLE DB und ADO.NET) werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als Aufrufe von sp_executesql oder von API-Servercursorroutinen angezeigt; deshalb können Übereinstimmungen auch von SQL- oder TEMPLATE-Planhinweislisten festgestellt werden.  
  
 *@parameter_name Data_type* muss im exakt gleichen Format angegeben werden, wie beim Übermitteln an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entweder mithilfe von Sp_executesql oder durch interne Übermittelung nach der Parametrisierung. Weitere Informationen finden Sie im Abschnitt mit Hinweisen. Wenn der Batch keine Parameter enthält, muss NULL angegeben werden. Die Größe des @params wird nur durch den verfügbaren Arbeitsspeicher des Servers beschränkt.  
  
 [@hints =] {N ' Option (*Query_hint* [,*.. ...n* ]) "| N'*XML_showplan*"| NULL}  
 N ' Option (*Query_hint* [,*.. ...n* ])  
 Gibt eine OPTION-Klausel einer Abfrage an, die entspricht @stmt. @hints muss syntaktisch identisch sein als eine OPTION-Klausel in einer SELECT-Anweisung, und kann eine beliebige gültige Sequenz von Abfragehinweisen enthalten.  
  
 N'*XML_showplan*'  
 Dies ist der Abfrageplan im XML-Format, der als Hinweis angewendet werden soll.  
  
 Es wird empfohlen, den XML-Showplan einer Variable zuzuweisen; andernfalls müssen Sie alle einfachen Anführungszeichen im Showplan abgrenzen, indem Sie ihnen ein weiteres einfaches Anführungszeichen voranstellen. Siehe Beispiel E.  
  
 NULL  
 Gibt an, dass ein vorhandener Hinweis, der in der OPTION-Klausel angegeben ist, nicht auf die Abfrage angewendet wird. Weitere Informationen finden Sie unter [OPTION-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md).  
  
## <a name="remarks"></a>Hinweise  
 Die Argumente für sp_create_plan_guide müssen in der angezeigten Reihenfolge bereitgestellt werden. Wenn Sie Werte für die Parameter von **sp_create_plan_guide**angeben, müssen entweder alle oder überhaupt keine Parameternamen explizit angegeben werden. Wird z.B. **@name =** angegeben, müssen auch **@stmt =** , **@type =** usw. angegeben werden. Ebenso dürfen, wenn **@name =** nicht angegeben und nur der Parameterwert bereitgestellt wird, die übrigen Parameterwerte ebenfalls nicht angegeben und nur ihre Werte bereitgestellt werden. Argumentnamen dienen nur zu Beschreibungszwecken, zum besseren Verständnis der Syntax. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überprüft nicht, ob der angegebene Parametername mit dem Namen des Parameters an der Position übereinstimmt, an der der Name verwendet wird.  
  
 Sie können mehr als eine Planhinweisliste des Typs OBJECT oder SQL für dieselbe Abfrage und den Batch oder das Modul erstellen. Es kann jedoch nur jeweils eine Planhinweisliste aktiviert sein.  
  
 Planhinweislisten vom Typ OBJECT können nicht für einen @module_or_batch-Wert erstellt werden, der auf eine gespeicherte Prozedur, Funktion oder einen DML-Trigger verweist, in der bzw. dem die WITH ENCRYPTION-Klausel angegeben wird oder die bzw. der temporär ist.  
  
 Das Löschen oder Ändern einer Funktion, einer gespeicherten Prozedur oder eines DML-Triggers, auf die bzw. den in einer Planhinweisliste verwiesen wird, verursacht einen Fehler. Auch der Versuch, eine Tabelle mit einem Trigger zu löschen, auf den eine Planhinweisliste verweist, führt zu einem Fehler.  
  
> [!NOTE]  
>  Planhinweislisten können nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md). Planhinweislisten sind in jeder Edition sichtbar. Sie können auch in allen Versionen eine Datenbank anfügen, die Planhinweislisten enthält. Planhinweislisten bleiben beim Wiederherstellen oder Anfügen einer Datenbank in einer aktualisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erhalten. Nach dem Serverupgrade sollten Sie in jeder Datenbank prüfen, ob die Planhinweislisten wirklich erwünscht sind.  
  
## <a name="plan-guide-matching-requirements"></a>Voraussetzungen für den Planhinweislistenabgleich  
 Für Planhinweislisten, die angeben, @type = 'SQL' oder @type = 'TEMPLATE', um erfolgreich eine Abfrage, die Werte für entsprechen *Batch_text* und  *@parameter_name Data_type* [,*.. ...n* ] müssen in genau das gleiche Format wie von der Anwendung übermittelten Gegenstücke bereitgestellt werden. Das bedeutet, dass Sie den Batchtext genau so bereitstellen müssen, wie er vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Compiler empfangen wird. Mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] können Sie den eigentlichen Batch- und Parametertext erfassen. Weitere Informationen finden Sie unter [Verwenden von SQL Server Profiler zum Erstellen und Testen von Planhinweislisten](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md).  
  
 Wenn @type = 'SQL' und @module_or_batch auf NULL gesetzt wird, wird der Wert von @module_or_batch auf den Wert von @stmt festgelegt. Dies bedeutet, dass den Wert für *Statement_text* muss angegeben werden, in genau demselben Format, Zeichen für Zeichen, wie beim Übermitteln an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es findet keine interne Konvertierung zur Vereinfachung dieses Abgleichs statt.  
  
 Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht dem Wert *Statement_text* auf *Batch_text* und  *@parameter_name Data_type* [,*.. ...n* ], oder Wenn @type = **"**Objekt", um den Text der entsprechenden Abfrage in *Object_name*, die folgenden Zeichenfolgenelemente nicht berücksichtigt:  
  
-   Leerzeichen (Tabstopps, Leerzeichen, Wagenrücklauf oder Zeilenvorschub) innerhalb der Zeichenfolge.  
  
-   Kommentare (**--** oder **/ \* \* /**).  
  
-   Nachfolgende Semikolons  
  
 Beispielsweise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann entsprechen den *Statement_text* Zeichenfolge `N'SELECT * FROM T WHERE a = 10'` , der dem folgenden *Batch_text*:  
  
 `N'SELECT *`  
  
 `FROM T`  
  
 `WHERE a=10'`  
  
 Allerdings die gleiche Zeichenfolge nicht zu diesem abgeglichen werden würden *Batch_text*:  
  
 `N'SELECT * FROM T WHERE b = 10'`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignoriert die Zeichen Wagenrücklauf und Zeilenvorschub sowie Leerzeichen in der ersten Abfrage. In der zweiten Abfrage wird die Sequenz `WHERE b = 10` nicht auf die gleiche Art interpretiert wie `WHERE a = 10`. Bei der Feststellung der Übereinstimmung wird nach Groß- und Kleinschreibung sowie nach Akzenten unterschieden (selbst wenn die Sortierung der Datenbank die Groß-/Kleinschreibung nicht berücksichtigt), mit Ausnahme von Schlüsselwörtern, bei denen keine Unterscheidung nach Groß-/Kleinschreibung stattfindet. Bei der Feststellung der Übereinstimmung wird nicht nach verkürzten Formen von Schlüsselwörtern unterschieden. So werden beispielsweise die Schlüsselwörter `EXECUTE`, `EXEC` und `execute` als gleichwertig angesehen.  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>Auswirkungen von Planhinweislisten auf den Plancache  
 Wenn Sie eine Planhinweisliste für ein Modul erstellen, wird der Abfrageplan für dieses Modul aus dem Plancache entfernt. Wenn Sie eine Planhinweisliste des Typs OBJECT oder SQL für einen Batch erstellen, wird der Abfrageplan für einen Batch mit demselben Hashwert entfernt. Wenn Sie eine Planhinweisliste des Typs TEMPLATE erstellen, werden alle Batches mit einer Anweisung aus dem Plancache in dieser Datenbank entfernt.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Erstellen einer Planhinweisliste vom Typ OBJECT wird die ALTER-Berechtigung für das Objekt benötigt, auf das verwiesen wird. Zum Erstellen einer Planhinweisliste vom Typ SQL oder TEMPLATE wird die ALTER-Berechtigung für die aktuelle Datenbank benötigt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-plan-guide-of-type-object-for-a-query-in-a-stored-procedure"></a>A. Erstellen einer Planhinweisliste vom Typ OBJECT für eine Abfrage in einer gespeicherten Prozedur  
 Im folgenden Beispiel wird eine Planhinweisliste erstellt, die einer im Kontext einer anwendungsbasierten gespeicherten Prozedur ausgeführten Abfrage zugeordnet wird, und der `OPTIMIZE FOR`-Hinweis auf die Abfrage angewendet.  
  
 Dies ist die gespeicherte Prozedur:  
  
```  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t   
        ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country_region;  
END  
GO  
```  
  
 Dies ist die für die Abfrage in der gespeicherten Prozedur erstellte Planhinweisliste:  
  
```  
EXEC sp_create_plan_guide   
    @name =  N'Guide1',  
    @stmt = N'SELECT *  
              FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.Customer AS c   
                 ON h.CustomerID = c.CustomerID  
              INNER JOIN Sales.SalesTerritory AS t   
                 ON c.TerritoryID = t.TerritoryID  
              WHERE t.CountryRegionCode = @Country_region',  
    @type = N'OBJECT',  
    @module_or_batch = N'Sales.GetSalesOrderByCountry',  
    @params = NULL,  
    @hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
### <a name="b-creating-a-plan-guide-of-type-sql-for-a-stand-alone-query"></a>B. Erstellen einer Planhinweisliste vom Typ SQL für eine eigenständige Abfrage  
 Im folgenden Beispiel wird eine Planhinweisliste erstellt, die einer Abfrage in einem Batch zugeordnet wird, der von einer Anwendung übermittelt wird, die die gespeicherte Systemprozedur sp_executesql verwendet.  
  
 Dies ist der Batch:  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 Erstellen Sie die folgende Planhinweisliste, damit kein zweiter Plan für die parallele Ausführung für diese Abfrage generiert wird:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'Guide1',   
    @stmt = N'SELECT TOP 1 *   
              FROM Sales.SalesOrderHeader   
              ORDER BY OrderDate DESC',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = N'OPTION (MAXDOP 1)';  
```  
  
### <a name="c-creating-a-plan-guide-of-type-template-for-the-parameterized-form-of-a-query"></a>C. Erstellen einer Planhinweisliste vom Typ TEMPLATE für die parametrisierte Form einer Abfrage  
 Im folgenden Beispiel wird eine Planhinweisliste erstellt, die mit einer beliebigen Abfrage übereinstimmt, die in einer bestimmten Form parametrisiert wird. Außerdem wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angewiesen, die Parametrisierung der Abfrage zu erzwingen. Die folgenden beiden Abfragen sind syntaktisch gleichwertig, unterscheiden sich jedoch in ihren konstanten Literalwerten.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 Dies ist die Planhinweisliste für die parametrisierte Form der Abfrage:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Im vorhergehenden Beispiel entspricht der Wert des `@stmt` -Parameters der parametrisierten Form der Abfrage. Die einzig zuverlässige Möglichkeit, diesen Wert für die Verwendung in sp_create_plan_guide abzurufen, ist die gespeicherte Systemprozedur [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) . Mithilfe des folgenden Skripts können Sie die parametrisierte Abfrage abrufen und anschließend eine Planhinweisliste für die Abfrage erstellen.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  Der Wert der konstanten Literale in dem an sp_get_query_template übergebenen `@stmt`-Parameter kann sich auf den Datentyp auswirken, der für den Parameter, der das Literal ersetzt, gewählt wird. Dies wiederum beeinflusst den Planhinweislistenabgleich. Möglicherweise müssen mehrere Planhinweislisten für verschiedene Parameterwertbereiche erstellt werden.  
  
### <a name="d-creating-a-plan-guide-on-a-query-submitted-by-using-an-api-cursor-request"></a>D. Erstellen einer Planhinweisliste für eine Abfrage, die über eine API-Cursoranforderung übermittelt wird  
 Planhinweislisten können Übereinstimmungen für Abfragen feststellen, die von API-Servercursorroutinen übermittelt werden. Zu diesen Routinen gehören sp_cursorprepare, sp_cursorprepexec und sp_cursoropen. Anwendungen, die ADO-, OLE DB- und ODBC-APIs verwenden, arbeiten häufig mithilfe von API-Servercursorn mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zusammen. Das Aufrufen von API-Servercursorroutinen in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]-Ablaufverfolgungen kann mithilfe des RPC:Starting-Ablaufverfolgungsereignisses angezeigt werden.  
  
 Angenommen, die folgenden Daten werden in einem RPC:Starting-Ablaufverfolgungsereignis für eine Abfrage angezeigt, die mithilfe einer Planhinweisliste optimiert werden soll:  
  
```  
DECLARE @p1 int;  
SET @p1=-1;  
DECLARE @p2 int;  
SET @p2=0;  
DECLARE @p5 int;  
SET @p5=4104;  
DECLARE @p6 int;  
SET @p6=8193;  
DECLARE @p7 int;  
SET @p7=0;  
EXEC sp_cursorprepexec @p1 output,@p2 output,N'@P1 varchar(255),@P2 varchar(255)',N'SELECT * FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID WHERE h.OrderDate BETWEEN @P1 AND @P2',@p5 OUTPUT,@p6 OUTPUT,@p7 OUTPUT,'20040101','20050101'  
SELECT @p1, @p2, @p5, @p6, @p7;  
```  
  
 Sie stellen fest, dass im Plan für die `SELECT`-Abfrage im Aufruf von `sp_cursorprepexec` ein Mergejoin verwendet wird, Sie möchten jedoch ein Hashjoin verwenden. Die mithilfe von `sp_cursorprepexec` übermittelte Abfrage ist parametrisiert, einschließlich einer Abfragezeichenfolge und einer Parameterzeichenfolge. Sie können die folgende Planhinweisliste erstellen, um die Wahl des Plans zu ändern, indem die Abfrage- und Parameterzeichenfolgen, Zeichen für Zeichen, so wie sie angezeigt werden, im Aufruf von `sp_cursorprepexec` verwendet werden.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'APICursorGuide',  
    @stmt = N'SELECT * FROM Sales.SalesOrderHeader AS h   
              INNER JOIN Sales.SalesOrderDetail AS d   
                ON h.SalesOrderID = d.SalesOrderID   
              WHERE h.OrderDate BETWEEN @P1 AND @P2',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = N'@P1 varchar(255),@P2 varchar(255)',  
    @hints = N'OPTION(HASH JOIN)';  
```  
  
 Diese Planhinweisliste wirkt sich auf nachfolgende Ausführungen dieser Abfrage durch die Anwendung aus, und ein Hashjoin wird zur Verarbeitung der Abfrage verwendet.  
  
### <a name="e-creating-a-plan-guide-by-obtaining-the-xml-showplan-from-a-cached-plan"></a>E. Erstellen einer Planhinweisliste durch Abrufen des XML-Showplans aus einem zwischengespeicherten Plan  
 Im folgenden Beispiel wird eine Planhinweisliste für eine einfache Ad-hoc-SQL-Anweisung erstellt. Der gewünschte Abfrageplan für diese Anweisung wird in der Planhinweisliste durch die direkte Angabe des XML-Showplans für die Abfrage im `@hints` -Parameter bereitgestellt. Im Beispiel wird zunächst die SQL-Anweisung ausgeführt, um einen Plan im Plancache zu erzeugen. Dabei wird davon ausgegangen, dass der erzeugte Plan dem gewünschten Plan entspricht und keine weitere Optimierung der Abfrage erforderlich ist. Der XML-Showplan wird durch eine Abfrage der dynamischen Verwaltungssichten `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`und `sys.dm_exec_text_query_plan` sys.dm_exec_query_stats abgerufen und der Variablen `@xml_showplan` zugewiesen. Die `@xml_showplan` -Variable wird dann im `sp_create_plan_guide` -Parameter an die `@hints` -Anweisung übergeben. Alternativ können Sie die gespeicherte Prozedur [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) verwenden, um eine Planhinweisliste aus einem Abfrageplan im Plancache zu erstellen.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints =@xml_showplan;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Planhinweislisten](../../relational-databases/performance/plan-guides.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [Gespeicherte Datenbankmodulprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [dm_exec_cached_plans & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_get_query_template &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md)  
  
  
