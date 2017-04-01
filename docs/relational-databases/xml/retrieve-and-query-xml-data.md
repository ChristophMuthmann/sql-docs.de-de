---
title: "Abrufen und Abfragen von XML-Daten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XML-Daten [SQL Server], abrufen"
  - "XML-Instanzabruf"
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Abrufen und Abfragen von XML-Daten
  In diesem Thema werden die Abfrageoptionen beschrieben, die für die Abfrage von XML-Daten anzugeben sind. Es beschreibt auch die Teile der XML-Instanzen, die nicht beibehalten werden, wenn sie in Datenbanken gespeichert werden.  
  
##  <a name="features"></a> Funktionen einer XML-Instanz, die nicht beibehalten werden  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] behält den Inhalt der XML-Instanz bei. Allerdings werden die Aspekte der XML-Instanz nicht beibehalten, die im Hinblick auf das XML-Datenmodell als nicht signifikant betrachtet werden. Das bedeutet, dass eine abgerufene XML-Instanz möglicherweise nicht mit der Instanz identisch ist, die auf dem Server gespeichert wurde, aber die gleichen Informationen enthält.  
  
### XML-Deklaration  
 Die XML-Deklaration in einer Instanz wird nicht beibehalten, wenn die Instanz in der Datenbank gespeichert wird. Beispiel:  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 Das Ergebnis ist `<doc/>`.  
  
 Die XML-Deklaration, z. B. `<?xml version='1.0'?>`, wird nicht beibehalten, wenn die XML-Daten in einer **xml** -Datentypinstanz gespeichert werden. Dies ist beabsichtigt. Die XML-Deklaration () und die Attribute (Version/Codierung/Eigenständigkeit) gehen bei der Konvertierung in den Typ **xml** verloren. Die XML-Deklaration wird als Direktive für den XML-Parser behandelt. Die XML-Daten werden intern als ucs-2 gespeichert. Alle anderen PIs in der XML-Instanz werden beibehalten.  
  
 [In diesem Thema](#top)  
  
### Reihenfolge von Attributen  
 Die Reihenfolge der Attribute in einer XML-Instanz wird nicht erhalten. Bei einer Abfrage der in der **xml** -Typspalte gespeicherten XML-Instanz kann die Reihenfolge der Attribute in der resultierenden XML von der der ursprünglichen XML-Instanz abweichen.  
  
 [In diesem Thema](#top)  
  
### Anführungszeichen um Attributwerte  
 Einfache Anführungszeichen und doppelte Anführungszeichen um Attributwerte werden nicht erhalten. Die Attributwerte werden in der Datenbank als Name/Wert-Paar gespeichert. Die Anführungszeichen werden nicht gespeichert. Wenn eine XQuery-Abfrage für eine XML-Instanz ausgeführt wird, wird die resultierende XML mit doppelten Anführungszeichen um die Attributwerte serialisiert.  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 Für beide Abfragen wird Folgendes zurückgeben: = `<root a="1" />`.  
  
 [In diesem Thema](#top)  
  
### Namespacepräfixe  
 Namespacepräfixe werden nicht erhalten. Wenn Sie eine XQuery-Abfrage für eine **xml** -Typspalte angeben, werden vom serialisierten XML-Ergebnis möglicherweise andere Namespacepräfixe zurückgeben.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 Das Namespacepräfix des Ergebnisses kann unterschiedlich sein. Beispiel:  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
 [In diesem Thema](#top)  
  
##  <a name="query"></a> Festlegen der erforderlichen Abfrageoptionen  
 Beim Abfragen von Spalten oder Variablen des **xml** -Datentyps mithilfe von **xml** -Datentypmethoden müssen die folgenden Optionen wie dargestellt festgelegt werden.  
  
|SET-Optionen|Erforderliche Werte|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 Wenn die Optionen nicht wie dargestellt festgelegt sind, schlagen Abfragen und Änderungen für **xml** -Datentypmethoden fehl.  
  
 [In diesem Thema](#top)  
  
## Siehe auch  
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  