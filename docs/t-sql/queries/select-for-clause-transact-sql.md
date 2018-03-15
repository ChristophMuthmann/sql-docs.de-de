---
title: FOR-Klausel (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 085a9c7f6422c70cc43086d2174a5c7aa485040e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="select---for-clause-transact-sql"></a>SELECT – FOR Clause (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Mit der FOR-Klausel können Sie eine der folgenden Optionen für Abfrageergebnisse angeben.  
  
-   Zulassen von Updates durch Angabe von **FOR BROWSE**, während Abfrageergebnisse in einem Cursor im Durchsuchenmodus angezeigt werden.  
  
-   Formatieren von Abfrageergebnissen als XML durch Angabe von **FOR XML**.  
  
-   Formatieren von Abfrageergebnissen als JSON durch Angabe von **FOR JSON**.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}  
```  
  
## <a name="for-browse"></a>FOR BROWSE  
 BROWSE  
 Gibt an, dass Updates zulässig sind, während Daten in einem DB-Library-Cursor im Durchsuchenmodus angezeigt werden. Eine Tabelle kann in einer Anwendung durchsucht werden, wenn sie eine **timestamp**-Spalte enthält, über einen eindeutigen Index verfügt und sich die FOR BROWSE-Option am Ende der an eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz gesendeten SELECT-Anweisungen befindet.  
  
> [!NOTE]  
>  \<lock_hint> HOLDLOCK kann nicht in einer SELECT-Anweisung mit der FOR BROWSE-Option verwendet werden.
  
 FOR BROWSE kann nicht in SELECT-Anweisungen verwendet werden, die durch den UNION-Operator miteinander verknüpft sind.  
  
> [!NOTE]  
>  Wenn die eindeutigen Indexschlüsselspalten einer Tabelle NULL-Werte zulassen und sich die Tabelle auf der Innenseite eines äußeren Joins befindet, wird der Durchsuchenmodus vom Index nicht unterstützt.  
  
 Mit dem Durchsuchenmodus können Sie die Zeilen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle scannen und die Daten in der Tabelle zeilenweise aktualisieren. Sie sollten für den Zugriff im Durchsuchenmodus auf eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle in der Anwendung eine der beiden folgenden Optionen verwenden:  
  
-   Die von Ihnen für den Zugriff auf die Daten Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle verwendete SELECT-Anweisung muss mit den Schlüsselwörtern **FOR BROWSE** enden. Wenn Sie die Option **FOR BROWSE** für die Verwendung des Durchsuchenmodus aktivieren, werden temporäre Tabellen erstellt.  
  
-   Sie müssen die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ausführen, um den Durchsuchenmodus mit der Option **NO_BROWSETABLE** zu aktivieren:  
  
    ```  
    SET NO_BROWSETABLE ON  
    ```  
  
     Wenn Sie die Option **NO_BROWSETABLE** aktivieren, verhalten sich alle SELECT-Anweisungen so, als würde die Option **FOR BROWSE** an die Anweisungen angefügt. Die Option **NO_BROWSETABLE** erstellt jedoch nicht die temporären Tabellen, welche die Option **FOR BROWSE** im Allgemeinen verwendet, um die Ergebnisse an Ihre Anwendung zu senden.  
  
 Wenn Sie versuchen, im Durchsuchenmodus auf die Daten aus den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabellen mit einer SELECT-Abfrage zuzugreifen, die eine äußere Verknüpfungsanweisung enthält, und wenn ein eindeutiger Index für die Tabelle definiert ist, die sich innerhalb der äußeren Verknüpfungsanweisung befindet, unterstützt der Durchsuchenmodus den eindeutigen Index nicht. Der eindeutige Index wird durch den Durchsuchenmodus nur dann unterstützt, wenn alle eindeutigen Indexschlüsselspalten NULL-Werte annehmen können. Der eindeutige Index wird durch den Durchsuchenmodus nicht unterstützt, wenn die folgenden Bedingungen zutreffen:  
  
-   Sie versuchen, im Durchsuchenmodus auf die Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabellen mit einer SELECT-Anweisung zuzugreifen, die eine äußere Verknüpfungsanweisung enthält.  
  
-   Es ist ein eindeutiger Index für die Tabelle definiert, die sich innerhalb eines äußeren Joins befindet.  
  
 Um dieses Verhalten im Durchsuchenmodus zu reproduzieren, führen Sie folgende Schritte aus:  
  
1.  Erstellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eine Datenbank mit der Bezeichnung SampleDB.  
  
2.  Erstellen Sie in der SampleDB-Datenbank eine Tabelle tlinks und eine Tabelle trechts, die beide eine einzelne Spalte mit der Bezeichnung c1 enthalten. Definieren Sie für die c1-Spalte in der Tabelle tlinks einen eindeutigen Index, und legen Sie fest, dass die Spalte NULL-Werte annehmen kann. Führen Sie hierzu die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem entsprechenden Abfragefenster aus:  
  
    ```  
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  Fügen Sie mehrere Werte in die Tabelle tlinks und die Tabelle trechts ein. Stellen Sie sicher, dass Sie einen NULL-Wert in die Tabelle tlinks einfügen. Führen Sie hierzu die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in dem Abfragefenster aus:  
  
    ```  
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  Aktivieren Sie die Option **NO_BROWSETABLE**. Führen Sie hierzu die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in dem Abfragefenster aus:  
  
    ```  
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  Greifen Sie mit einem äußeren Join in der SELECT-Abfrage auf die Daten in der Tabelle tlinks und der Tabelle trechts zu. Stellen Sie sicher, dass sich die Tabelle tlinks innerhalb der äußeren Joinanweisung befindet. Führen Sie hierzu die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in dem Abfragefenster aus:  
  
    ```  
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;  
  
    ```  
  
     Beachten Sie die folgende Ausgabe im Ergebnisbereich:  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 Nach dem Ausführen der SELECT-Abfrage zum Zugreifen auf die Tabellen im Durchsuchenmodus, enthält das Resultset der SELECT-Abfrage aufgrund der Definition der rechten äußeren Joinanweisung zwei Nullwerte für die Spalte c1 in der Tabelle tlinks. Daher können Sie im Resultset nicht zwischen den Nullwerten, die aus der Tabelle stammen, und den Nullwerten, die durch die rechte äußere Joinanweisung eingebracht wurden, unterscheiden. Sie könnten falsche Ergebnisse erhalten, wenn Sie die Nullwerte aus dem Resultset ignorieren müssen.  
  
> [!NOTE]  
>  Wenn die Spalten, die in dem eindeutigen Index enthalten sind, keine Nullwerte annehmen können, wurden alle Nullwerte im Ergebnis durch die rechte äußere Joinanweisung eingebracht.  
  
## <a name="for-xml"></a>FOR XML  
 XML  
 Gibt an, dass die Ergebnisse einer Abfrage als XLM-Dokument zurückgegeben werden. Einer der folgenden XML-Modi muss angegeben werden: RAW, AUTO oder EXPLICIT. Weitere Informationen zu XML-Daten und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 RAW [ **('***ElementName***')** ]  
 Verwendet das Abfrageergebnis und transformiert jede Zeile des Resultsets in ein XML-Element mit dem generischen Bezeichner \<row /> als Elementtag. Sie können optional einen Namen für das Zeilenelement angeben. Die resultierende XML-Ausgabe verwendet den angegebenen *ElementName* als das für jede Zeile generierte Zeilenelement. Weitere Informationen finden Sie unter [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md) und unter [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 AUTO  
 Gibt Abfrageergebnisse in einer einfachen, geschachtelten XML-Struktur zurück. Jede Tabelle in der FROM-Klausel, aus der mindestens eine Spalte in der SELECT-Klausel aufgeführt ist, wird als XML-Element dargestellt. Die in der SELECT-Klausel aufgelisteten Spalten werden den entsprechenden Elementattributen zugeordnet. Weitere Informationen finden Sie unter [Verwenden des AUTO-Modus mit FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md).  
  
 EXPLICIT  
 Gibt an, dass die Form der sich ergebenden XML-Struktur explizit definiert wird. In diesem Modus müssen die Abfragen auf eine bestimmte Weise geschrieben werden, sodass zusätzliche Informationen zur gewünschten Schachtelung explizit angegeben werden. Weitere Informationen finden Sie unter [Verwenden des EXPLICIT-Modus mit FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md).  
  
 XMLDATA  
 Gibt das XDR-Inlineschema zurück, fügt jedoch das Stammelement dem Ergebnis nicht hinzu. Wenn XMLDATA angegeben ist, wird das XDR-Schema an das Dokument angefügt.  
  
> [!IMPORTANT]  
>  Die XMLDATA-Anweisung ist veraltet. Verwenden Sie XSD-Generierung für RAW- und AUTO-Modus. Es gibt keinen Ersatz für die XMLDATA-Direktive im EXPLICIT-Modus. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 XMLSCHEMA [ **('***TargetNameSpaceURI***')** ]  
 Gibt das XSD-Inlineschema zurück. Beim Angeben dieser Direktive können Sie optional einen Zielnamespace-URI angeben, der den angegebenen Namespace im Schema zurückgibt. Weitere Informationen finden Sie unter [Generieren eines XSD-Inlineschemas](../../relational-databases/xml/generate-an-inline-xsd-schema.md).  
  
 ELEMENTS  
 Gibt an, dass die Spalten als Unterelemente zurückgegeben werden. Andernfalls werden sie XML-Attributen zugeordnet. Diese Option wird nur in den Modi RAW, AUTO und PATH unterstützt. Weitere Informationen finden Sie unter [Verwenden des RAW-Modus mit FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 XSINIL  
 Gibt an, dass ein Element, dessen Attribut **xsi:nil** auf **TRUE** festgelegt ist, für NULL-Spaltenwerte erstellt wird. Diese Option kann nur mit der ELEMENTS-Anweisung angegeben werden. Weitere Informationen finden Sie unter [Generieren von Elementen für NULL-Werte mithilfe des XSINIL-Parameters](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md).  
  
 ABSENT  
 Gibt an, dass dem XML-Ergebnis für NULL-Spaltenwerte keine entsprechenden XML-Elemente hinzugefügt werden. Diese Option kann nur mit der ELEMENTS-Direktive angegeben werden.  
  
 PATH [ **('***ElementName***')** ]  
 Generiert für jede Zeile im Resultset einen \<row>-Elementwrapper. Sie können optional einen Elementnamen für den \<row>-Elementwrapper angeben. Bei einer leeren Zeichenfolge, wie z.B. FOR XML PATH (**''**) ), wird kein Wrapperelement generiert. Die Verwendung von PATH kann eine einfachere Alternative zu mithilfe der EXPLICIT-Direktive geschriebenen Abfragen darstellen. Weitere Informationen finden Sie unter [Verwenden des PATH-Modus mit FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md).  
  
 BINARY BASE64  
 Gibt an, dass die Abfrage die Binärdaten im BINARY BASE64-Format codiert zurückgibt. Zum Abrufen von Binärdaten im RAW- oder EXPLICIT-Modus muss diese Option angegeben werden. Im AUTO-Modus ist sie die Standardeinstellung.  
  
 TYPE  
 Gibt an, dass die Abfrage Ergebnisse als **XML**-Typ zurückgibt. Weitere Informationen finden Sie unter [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md).  
  
 ROOT [ **('***RootName***')** ]  
 Gibt an, dass ein einzelnes Element der obersten Ebene dem als Ergebnis zurückgegebenen XML-Dokument hinzugefügt wird. Optional können Sie den zu generierenden Stammelementnamen angeben. Wenn der optionale Stammelementname angegeben wird, wird das \<root>-Standardelement hinzugefügt.  
  
 Weitere Informationen finden Sie unter [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **Beispiel für FOR XML**  
  
 Im folgenden Beispiel wird `FOR XML AUTO` mit den Optionen `TYPE` und `XMLSCHEMA` angegeben. Aufgrund der `TYPE`-Option wird das Resultset als **XML**-Typ an den Client zurückgegeben. Die `XMLSCHEMA`-Option gibt an, dass das XSD-Inlineschema in den zurückgegebenen XML-Daten enthalten ist, während die `ELEMENTS`-Option angibt, dass das XML-Ergebnis elementzentriert ist.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>FOR JSON  
 JSON  
 Geben Sie FOR JSON an, um die Ergebnisse einer als JSON-Text formatierten Abfrage zurückzugeben. Zudem müssen Sie einen der folgenden JSON-Modi angeben: AUTO oder PATH. Weitere Informationen zur **FOR JSON**-Klausel finden Sie unter [Formatieren von Abfrageergebnissen als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 Formatieren Sie die JSON-Ausgabe automatisch basierend auf der Struktur der **SELECT**-Anweisung,  
            indem Sie **FOR JSON AUTO** angeben. Weitere Informationen und Beispiele finden Sie unter [Automatisches Formatieren von JSON-Ausgaben &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).  
  
 PATH  
 Gewinnen Sie vollständige Kontrolle über das Format der JSON-Ausgabe durch Angabe von   
            **FOR JSON PATH**. Im**PATH** -Modus können Sie Wrapper-Objekte erstellen und komplexe Eigenschaften schachteln. Weitere Informationen und Beispiele finden Sie unter [Formatieren einer geschachtelten JSON-Ausgabe im PATH-Modus &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).  
  
 INCLUDE_NULL_VALUES  
 Schließen Sie NULL-Werte in die JSON-Ausgabe ein, indem Sie die Option **INCLUDE_NULL_VALUES** mit der **FOR JSON**-Klausel angeben. Wenn Sie diese Option nicht angeben, enthält die Ausgabe in den Abfrageergebnissen keine JSON-Eigenschaften für NULL-Werte. Weitere Informationen und Beispiele finden Sie unter[Include Null Values in JSON Output with the INCLUDE_NULL_VALUES Option &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md) (Einschließen von NULL-Werten in die JSON-Ausgabe mit der Option INCLUDE_NULL_VALUES (SQL Server)).  
  
 ROOT [ **('***RootName***')** ]  
 Fügen Sie ein einzelnes Element der obersten Ebene zur JSON-Ausgabe hinzu, indem Sie die Option **ROOT** mit der **FOR JSON**-Klausel angeben. Wenn Sie die Option **ROOT** nicht angeben, besitzt die JSON-Ausgabe kein Stammelement. Weitere Informationen und Beispiele finden Sie unter [Add a Root Node to JSON Output with the ROOT Option &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md) (Hinzufügen eines Stammknotens zur JSON-Ausgabe mithilfe der ROOT-Option (SQL Server)).  
  
 WITHOUT_ARRAY_WRAPPER  
 Entfernen Sie die rechteckigen Klammern, welche die JSON-Ausgabe standardmäßig umgeben, indem Sie die Option **WITHOUT_ARRAY_WRAPPER** mit der **FOR JSON**-Klausel angeben. Wenn Sie diese Option nicht angeben, wird die JSON-Ausgabe in eckige Klammern eingeschlossen. Verwenden Sie die Option **WITHOUT_ARRAY_WRAPPER**, um ein einzelnes JSON-Objekt als Ausgabe zu generieren.  Weitere Informationen finden Sie unter [Remove Square Brackets from JSON Output with the WITHOUT_ARRAY_WRAPPER Option &#40;SQL Server&#41; (Entfernen von rechteckigen Klammern von JSON-Ausgabe mit der Option WITHOUT_ARRAY_WRAPPER (SQL Server))](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md).  
  
 Weitere Informationen finden Sie unter [Formatieren von Abfrageergebnissen als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
