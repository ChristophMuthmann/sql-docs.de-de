---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs: TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 79bf3115ef4e1d929e3e4a1b3ff731a1977ba28e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Definiert die Attribute eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursors, wie z. B. dessen Scrollverhalten, sowie die Abfrage, die zum Erstellen des Resultsets verwendet wird, auf das der Cursor ausgeführt wird. DECLARE CURSOR unterstützt sowohl die Syntax basierend auf dem ISO-Standard als auch eine Syntax, für die eine Teilmenge der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Erweiterungen verwendet wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *cursor_name*  
 Der Name des der [!INCLUDE[tsql](../../includes/tsql-md.md)] Servercursor definiert. *Cursor_name* muss den Regeln für Bezeichner entsprechen.  
  
 INSENSITIVE  
 Definiert einen Cursor, der eine temporäre Kopie der von ihm zu verwendenden Daten erzeugt. Alle Anforderungen an den Cursor werden von dieser temporären Tabelle in beantwortet **Tempdb**; deshalb Änderungen an den Basistabellen werden nicht wiedergegeben, in den Daten, die durch Abrufoperationen an diesem Cursor zurückgegeben, und lässt dieser Cursor keine Änderungen. Bei Verwendung der ISO-Syntax ohne die Option INSENSITIVE werden ausgeführte Löschvorgänge und Updates an den zugrunde liegenden Tabellen (von einem beliebigen Benutzer) in späteren Abrufvorgängen wiedergegeben.  
  
 SCROLL  
 Gibt an, dass alle Abrufoptionen (FIRST, LAST, PRIOR, NEXT, RELATIVE, ABSOLUTE) zur Verfügung stehen. Wird SCROLL in einer ISO-DECLARE CURSOR-Anweisung nicht angegeben, wird nur die Abrufoption NEXT unterstützt. Führen Sie einen Bildlauf nicht angegeben oder FAST_FORWARD angegeben wird.  
  
 *select_statement*  
 Eine standardmäßige SELECT-Anweisung, die das Resultset des Cursors definiert. Die Schlüsselwörter FOR BROWSE und INTO sind nicht zulässig in *Select_statement* der Deklaration eines Cursors.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Konvertiert den Cursor implizit in einen anderen Typ aus, wenn die Klauseln in *Select_statement* Konflikt mit der Funktionalität des angeforderten Cursortyps.  
  
 READ ONLY  
 Verhindert, dass über diesen Cursor Updates vorgenommen werden. Auf den Cursor kann nicht in einer WHERE CURRENT OF-Klausel in einer UPDATE- oder DELETE-Anweisung verwiesen werden. Diese Option überschreibt die Standardeinstellung, nach der ein Cursor aktualisiert werden kann.  
  
 UPDATE [OF *Column_name* [**,**... *n*]]  
 Definiert aktualisierbare Spalten innerhalb des Cursors. Wenn OF *Column_name* [**,**... *...n*] angegeben wird, können Änderungen nur die Spalten aufgeführt. Wenn UPDATE ohne Spaltenliste angegeben wird, können alle Spalten aktualisiert werden.  
  
 *cursor_name*  
 Der Name des der [!INCLUDE[tsql](../../includes/tsql-md.md)] Servercursor definiert. *Cursor_name* muss den Regeln für Bezeichner entsprechen.  
  
 LOCAL  
 Gibt an, dass der Gültigkeitsbereich des Cursors lokal zu dem Batch, der gespeicherten Prozedur oder dem Trigger ist, in dem bzw. in der er erstellt wurde. Der Cursorname ist nur innerhalb dieses Bereichs gültig. Auf den Cursor kann durch lokale Cursorvariablen im Batch, in der gespeicherten Prozedur, im Trigger oder im OUTPUT-Parameter einer gespeicherten Prozedur verwiesen werden. Ein OUTPUT-Parameter kann den lokalen Cursor an den aufrufenden Batch, die aufrufende gespeicherte Prozedur oder den aufrufenden Trigger zurückgeben. Diese können den Parameter einer Cursorvariablen zuweisen, um nach dem Beenden der gespeicherten Prozedur auf den Cursor zu verweisen. Die Zuordnung des Cursors wird implizit aufgehoben, wenn der Batch, die gespeicherte Prozedur oder der Trigger beendet wird, es sei denn, der Cursor wurde in einem OUTPUT-Parameter zurückgegeben. Wenn sie in einer OUTPUT-Parameter übergeben wird, wird der Cursor Zuordnung aufgehoben werden, wenn die letzten auf ihn verweisenden Variablen aufgehoben wird oder den Gültigkeitsbereich verlässt.  
  
 GLOBAL  
 Gibt an, dass der Bereich des Cursors global zur Verbindung ist. Auf den Cursornamen kann in jeder gespeicherten Prozedur und in jedem Batch verwiesen werden, die bzw. der von der Verbindung ausgeführt wird. Die Zuordnung des Cursors wird nur implizit aufgehoben, wenn die Verbindung getrennt wird.  
  
> [!NOTE]  
>  Wenn weder GLOBAL noch LOCAL angegeben wird, wird die Standardeinstellung gesteuert, von der Einstellung der der **standardmäßig die lokalen Cursor** -Datenbankoption.  
  
 FORWARD_ONLY  
 Gibt an, dass innerhalb des Cursors die Zeilen nur nacheinander von der ersten bis zur letzten Zeile gelesen werden können. FETCH NEXT ist die einzige unterstützte Abrufoption. Wenn FORWARD_ONLY ohne eines der Schlüsselwörter STATIC, KEYSET oder DYNAMIC angegeben wird, arbeitet der Cursor mit der Option DYNAMIC. Wenn weder FORWARD_ONLY noch SCROLL angegeben wird, wird standardmäßig FORWARD_ONLY verwendet, es sei denn, die Schlüsselwörter STATIC, KEYSET oder DYNAMIC werden angegeben. STATISCHE, KEYSETGESTEUERTE und dynamische Cursor standardmäßig, Bildlauf. Anders als bei Datenbank-APIs, wie z. B. ODBC und ADO, wird FORWARD_ONLY für STATIC-, KEYSET- und DYNAMIC-[!INCLUDE[tsql](../../includes/tsql-md.md)]-Cursor unterstützt.  
  
 STATIC  
 Definiert einen Cursor, der eine temporäre Kopie der von ihm zu verwendenden Daten erzeugt. Alle Anforderungen an den Cursor werden von dieser temporären Tabelle in beantwortet **Tempdb**; deshalb Änderungen an den Basistabellen werden nicht wiedergegeben, in den Daten, die durch Abrufoperationen an diesem Cursor zurückgegeben, und lässt dieser Cursor keine Änderungen.  
  
 KEYSET  
 Gibt an, dass im Cursor die Mitgliedschaft und Reihenfolge der Zeilen fest ist, wenn der Cursor geöffnet wird. Die Menge der Schlüssel, die Zeilen eindeutig identifiziert wird erstellt, in eine Tabelle in **Tempdb** bekannt als die **Keyset**.  
  
> [!NOTE]  
>  Wenn die Abfrage auf mindestens eine Tabelle ohne einen eindeutigen Index verweist, wird der Keysetcursor in einen statischen Cursor konvertiert.  
  
 Änderungen an Nichtschlüsselwerten in den Basistabellen, die vom Cursorbesitzer oder durch Ausführen eines Commits von anderen Benutzern vorgenommen wurden, werden sichtbar, wenn der Besitzer im Cursor einen Bildlauf durch den Cursor durchführt. Von anderen Benutzern vorgenommene Einfügungen sind nicht sichtbar (Einfügevorgänge können nicht über einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursor durchgeführt werden). Wenn eine Zeile gelöscht wird, gibt ein Versuch zum Abrufen der Zeile ein @@FETCH_STATUS -2. Updates von Schlüsselwerten von außerhalb des Cursors sind vergleichbar mit einem Löschen der alten Zeile, gefolgt von einem Einfügen der neuen Zeile. Die Zeile mit den neuen Werten ist nicht sichtbar, und versuchen, die Zeile mit den alten Werten abzurufen zurückgegeben ein @@FETCH_STATUS -2. Die neuen Werte sind sichtbar, wenn das Update über den Cursor durch Angeben der WHERE CURRENT OF-Klausel durchgeführt wird.  
  
 DYNAMIC  
 Definiert einen Cursor, der alle in den Zeilen vorgenommen Datenänderungen in seinem Resultset widerspiegelt, wenn Sie im Cursor einen Bildlauf durchführen. Datenwerte, Reihenfolge und Mitgliedschaft der Zeilen können sich bei jedem Abrufvorgang ändern. Die Abrufoption ABSOLUTE wird für dynamische Cursor nicht unterstützt.  
  
 FAST_FORWARD  
 Gibt einen FORWARD_ONLY-, READ_ONLY-Cursor mit aktivierter Leistungsoptimierung an. FAST_FORWARD kann nur angegeben werden, wenn weder SCROLL noch FOR UPDATE angegeben ist.  
  
> [!NOTE]  
>  Sowohl FAST_FORWARD als auch FORWARD_ONLY können in derselben DECLARE CURSOR-Anweisung verwendet werden.  
  
 READ_ONLY  
 Verhindert, dass über diesen Cursor Updates vorgenommen werden. Auf den Cursor kann nicht in einer WHERE CURRENT OF-Klausel in einer UPDATE- oder DELETE-Anweisung verwiesen werden. Diese Option überschreibt die Standardeinstellung, nach der ein Cursor aktualisiert werden kann.  
  
 SCROLL_LOCKS  
 Gibt an, dass positionierte Updates oder Löschungen durch den Cursor garantiert erfolgreich sind. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Sperrt die Zeilen, die in den Cursor, um deren Verfügbarkeit für spätere Änderungen sicherzustellen gelesen werden. SCROLL_LOCKS kann nicht angegeben werden, wenn FAST_FORWARD oder STATIC ebenfalls angegeben wird.  
  
 OPTIMISTIC  
 Gibt an, dass positionierte Updates oder Löschungen durch den Cursor nicht erfolgreich sind, wenn die Zeile seit dem letzten Einlesen in den Cursor aktualisiert wurde. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sperrt keine Zeilen, während sie in den Cursor eingelesen werden. Stattdessen wird durch Vergleiche von **Zeitstempel** Spaltenwerte oder einen Prüfsummenwert, wenn die Tabelle keine **Zeitstempel** -Spalte, um zu bestimmen, ob die Zeile nach dem Einlesen in den Cursor geändert wurde. Wurde die Zeile geändert, so schlägt der versuchte positionierte Update- oder Löschvorgang fehl. OPTIMISTISCHE kann nicht angegeben werden, oder FAST_FORWARD angegeben wird.  
  
 TYPE_WARNING  
 Gibt an, dass dem Client eine Warnmeldung gesendet wird, wenn der Cursor vom angeforderten Typ in einen anderen Typ implizit konvertiert wird.  
  
 *select_statement*  
 Eine standardmäßige SELECT-Anweisung, die das Resultset des Cursors definiert. Die Schlüsselwörter COMPUTE, COMPUTE BY, FOR BROWSE und INTO sind nicht zulässig in *Select_statement* der Deklaration eines Cursors.  
  
> [!NOTE]  
>  Sie können einen Abfragehinweis in einer Cursordeklaration verwenden. Wenn Sie auch die FOR UPDATE OF-Klausel verwenden, geben jedoch OPTION (*Query_hint*) nach FOR UPDATE OF.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Konvertiert den Cursor implizit in einen anderen Typ aus, wenn die Klauseln in *Select_statement* Konflikt mit der Funktionalität des angeforderten Cursortyps. Weitere Informationen finden Sie unter Implizite Cursorkonvertierungen.  
  
 FÜR das UPDATE [OF *Column_name* [**,**... *n*]]  
 Definiert aktualisierbare Spalten innerhalb des Cursors. Wenn OF *Column_name* [**,**...  *n* ] angegeben wird, können Änderungen nur die Spalten aufgeführt. Wenn UPDATE ohne Spaltenliste angegeben wird, können alle Spalten aktualisiert werden, sofern nicht die Parallelitätsoption READ_ONLY angegeben wurde.  
  
## <a name="remarks"></a>Hinweise  
 DECLARE CURSOR definiert die Attribute eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Servercursors, wie z. B. dessen Scrollverhalten, sowie die Abfrage, die zum Erstellen des Resultsets verwendet wird, auf das der Cursor ausgeführt wird. Die OPEN-Anweisung füllt das Resultset auf, und FETCH gibt eine Zeile aus dem Resultset zurück. Die CLOSE-Anweisung gibt das aktuelle Resultset frei, das dem Cursor zugeordnet ist. Die DEALLOCATE-Anweisung gibt die vom Cursor verwendeten Ressourcen frei.  
  
 Die erste Form der DECLARE CURSOR-Anweisung verwendet zum Deklarieren des Cursorverhaltens die ISO-Syntax. Die zweite Form der DECLARE CURSOR-Anweisung verwendet [!INCLUDE[tsql](../../includes/tsql-md.md)]-Erweiterungen, die die Definition von Cursorn mithilfe der gleichen Cursortypen zulassen, die in den Datenbank-API-Cursor-Funktionen von ODBC oder ADO verwendet werden.  
  
 Die beiden Formen können nicht gleichzeitig verwendet werden. Wenn Sie das Schlüsselwort SCROLL oder INSENSITIVE vor dem Schlüsselwort CURSOR angeben, können keine zwischen den CURSOR und FOR keine Schlüsselwörter *Select_statement* Schlüsselwörter. Wenn Sie zwischen den CURSOR und FOR keine Schlüsselwörter angeben *Select_statement* Keywords-Eigenschaft, können Sie SCROLL oder INSENSITIVE nicht vor dem Schlüsselwort CURSOR angeben.  
  
 Wird in einer DECLARE CURSOR-Anweisung mit der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Syntax weder READ_ONLY, OPTIMISTIC noch SCROLL_LOCKS angegeben, ist der Standard folgendermaßen:  
  
-   Unterstützt die SELECT-Anweisung keine Updates (wegen fehlender Berechtigungen, Zugriff auf Remotetabellen, die keine Updates unterstützen usw.), ist der Cursor READ_ONLY.  
  
-   STATIC- und FAST_FORWARD-Cursor sind standardmäßig READ_ONLY.  
  
-   DYNAMIC- und KEYSET-Cursor sind standardmäßig OPTIMISTIC.  
  
 Ein Verweis auf Cursornamen ist nur von anderen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen aus möglich. Auf sie kann nicht von Datenbank-API-Funktionen verwiesen werden. Nach der Deklaration eines Cursors besteht beispielsweise keine Möglichkeit, in einer OLE DB-, ODBC- oder ADO-Funktion oder -Methode auf den Cursornamen zu verweisen. Die Zeilen des Cursors können nicht mithilfe von API-Funktionen oder API-Methoden abgerufen werden. Ein Abrufen der Zeilen ist lediglich mit den FETCH-Anweisungen von [!INCLUDE[tsql](../../includes/tsql-md.md)] möglich.  
  
 Nach der Deklaration eines Cursors können die Eigenschaften des Cursors mithilfe der folgenden gespeicherten Systemprozeduren bestimmt werden:  
  
|Gespeicherte Systemprozeduren|Description|  
|------------------------------|-----------------|  
|**sp_cursor_list**|Gibt eine Liste der in der Verbindung aktuell sichtbaren Cursor und ihrer Attribute zurück.|  
|**sp_describe_cursor**|Beschreibt die Attribute eines Cursors, z. B. ob es sich um einen Vorwärtscursor oder einen Scrollcursor handelt.|  
|**sp_describe_cursor_columns**|Beschreibt die Spaltenattribute im Resultset des Cursors.|  
|**sp_describe_cursor_tables**|Beschreibt die Basistabellen, auf die der Cursor zugreift.|  
  
 Variablen können verwendet werden, als Teil der *Select_statement* , die einen Cursor deklariert. Die Werte von Cursorvariablen ändern sich nach dem Deklarieren eines Cursors nicht.  
  
## <a name="permissions"></a>Berechtigungen  
 In der Standardeinstellung haben alle Benutzer die DECLARE CURSOR-Berechtigung, wenn sie über die SELECT-Berechtigungen für die im Cursor verwendeten Sichten, Tabellen und Spalten verfügen.
 
## <a name="limitations-and-restrictions"></a>Einschränkungen

Sie können keine Cursor oder Trigger für eine Tabelle mit einem gruppierten columnstore-Index verwenden. Diese Einschränkung gilt nicht für nicht gruppierte columnstore-Indizes; Sie können den Cursor und Trigger für eine Tabelle mit einem nicht gruppierten columnstore-Index verwenden. 
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. Verwenden des einfachen Cursors und der einfachen Syntax  

Das beim Öffnen dieses Cursors generierte Resultset enthält alle Zeilen und Spalten in der Tabelle. Dieser Cursor kann aktualisiert werden. Alle Updates und Löschungen werden in Abrufen dieses Cursors dargestellt. `FETCH NEXT` ist der einzige verfügbare Abruf, da die `SCROLL`-Option nicht angegeben worden ist.  

  
```  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. Verwenden von geschachtelten Cursorn, um eine Berichtsausgabe zu erzeugen  
 Im folgenden Beispiel wird gezeigt, wie Cursor zum Erzeugen komplexer Berichte geschachtelt werden können. Der innere Cursor wird für jeden Anbieter deklariert.  
  
```  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursors &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
