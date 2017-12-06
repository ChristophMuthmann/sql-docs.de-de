---
title: "\"true\"-Funktion (XQuery) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f38cd50748b59b2a0cf32e5a7e9ab0a28f7e396b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="boolean-constructor-functions---true-xquery"></a>Boolesche Konstruktorfunktionen - "true" (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den xs:boolean-Wert True zurück. Dieser entspricht `xs:boolean("1")`.  
  
## <a name="syntax"></a>Syntax  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>Beispiele  
 Dieses Thema stellt XQuery-Beispiele für XML-Instanzen, die in verschiedenen gespeichert sind **Xml** -Typspalten in der AdventureWorks-Datenbank.  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. Verwenden der XQuery Boolean-Funktion true()  
 Das folgende Beispiel fragt eine nicht typisierte **Xml** Variable. Der Ausdruck in der **value()** Methodenrückgabe Boolean **true()** ist "aaa" den Wert des Attributs. Die **value()** Methode der **Xml** -Datentyp konvertiert den booleschen Wert in einen Bitwert und gibt ihn zurück.  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 Im folgenden Beispiel wird die Abfrage angegeben für eine typisierte **Xml** Spalte. Der `if`-Ausdruck überprüft den typisierten booleschen Wert des <`ROOT`>-Elements und gibt den konstruierten XML-Code entsprechend zurück. Das Beispiel führt die folgenden Aktionen aus:  
  
-   Erstellt eine XML-Schemaauflistung, die das <`ROOT`>-Element des xs:boolean-Typs definiert.  
  
-   Erstellt eine Tabelle mit typisierter **Xml** Spalte, indem Sie die XML-schemaauflistung.  
  
-   Speichert eine XML-Instanz in der Spalte und fragt sie ab.  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Boolesche Konstruktorfunktionen &#40; XQuery &#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
