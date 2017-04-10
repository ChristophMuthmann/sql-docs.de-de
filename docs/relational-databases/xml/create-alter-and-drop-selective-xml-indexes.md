---
title: "Erstellen, &#196;ndern und L&#246;schen selektiver XML-Indizes | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c398f396-f630-4a2d-a264-f243c5346de1
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# Erstellen, &#196;ndern und L&#246;schen selektiver XML-Indizes
  Beschreibt, wie ein neuer selektiver XML-Index erstellt bzw. ein vorhandener selektiver XML-Index geändert oder gelöscht wird.  
  
 Weitere Informationen über selektive XML-Indizes finden Sie unter [Selektive XML-Indizes &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
##  <a name="create"></a> Erstellen eine selektiven XML-Indexes  
  
### Vorgehensweise: Erstellen eines selektiven XML-Indexes  
 **Erstellen eines selektiven XML-Indexes mit Transact-SQL**  
 Erstellen Sie einen selektiven XML-Index, indem Sie die CREATE SELECTIVE XML INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird die Syntax zum Erstellen eines selektiven XML-Indexes veranschaulicht. Zudem werden mehrere Variationen der Syntax, die die zu indizierenden Pfade beschreibt, mit optionalen Optimierungshinweisen angegeben.  
  
```tsql  
CREATE SELECTIVE XML INDEX sxi_index  
ON Tbl(xmlcol)  
  
FOR(  
    pathab   = '/a/b' as XQUERY 'node()'  
    pathabc  = '/a/b/c' as XQUERY 'xs:double',   
    pathdtext = '/a/b/d/text()' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
    pathabe = '/a/b/e' as SQL NVARCHAR(100)  
)  
```  
  
 [In diesem Thema](#top)  
  
##  <a name="alter"></a> Ändern eines selektiven XML-Indexes  
  
### Vorgehensweise: Ändern eines selektiven XML-Indexes  
 **Ändern eines selektiven XML-Indexes mit Transact-SQL**  
 Ändern Sie einen vorhandenen selektiven XML-Index, indem Sie die ALTER INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [ALTER INDEX &#40;selektive XML-Indizes&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md).  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird eine ALTER INDEX-Anweisung veranschaulicht. Mit dieser Anweisung wird der Pfad `'/a/b/m'` dem XQuery-Teil des Indexes hinzugefügt und der Pfad `'/a/b/e'` vom SQL-Teil des Indexes, der im Beispiel im Thema [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md) erstellt wurde, gelöscht. Der zu löschende Pfad ist anhand des Namens zu erkennen, der ihm bei der Erstellung zugewiesen wurde.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
)  
```  
  
 [In diesem Thema](#top)  
  
##  <a name="drop"></a> Löschen eines selektiven XML-Indexes  
  
### Vorgehensweise: Löschen eines selektiven XML-Indexes  
 **Löschen eines selektiven XML-Indexes mit Transact-SQL**  
 Löschen Sie einen selektiven XML-Index, indem Sie die DROP INDEX-Anweisung aufrufen. Weitere Informationen finden Sie unter [DROP INDEX &#40;selektive XML-Indizes&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md).  
  
 **Beispiel**  
  
 Im folgenden Beispiel wird eine DROP INDEX-Anweisung veranschaulicht.  
  
```tsql  
DROP INDEX sxi_index ON tbl  
```  
  
 [In diesem Thema](#top)  
  
  