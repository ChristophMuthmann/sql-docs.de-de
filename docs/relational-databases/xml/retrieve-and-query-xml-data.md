---
title: Abrufen und Abfragen von XML-Daten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 842569318daf32cb0bedfea0d15e099f05cf73b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="retrieve-and-query-xml-data"></a>Abrufen und Abfragen von XML-Daten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  In diesem Thema werden die Abfrageoptionen beschrieben, die für die Abfrage von XML-Daten anzugeben sind. Es beschreibt auch die Teile der XML-Instanzen, die nicht beibehalten werden, wenn sie in Datenbanken gespeichert werden.  
  
##  <a name="features"></a> Funktionen einer XML-Instanz, die nicht beibehalten werden  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] behält den Inhalt der XML-Instanz bei. Allerdings werden die Aspekte der XML-Instanz nicht beibehalten, die im Hinblick auf das XML-Datenmodell als nicht signifikant betrachtet werden. Das bedeutet, dass eine abgerufene XML-Instanz möglicherweise nicht mit der Instanz identisch ist, die auf dem Server gespeichert wurde, aber die gleichen Informationen enthält.  
  
### <a name="xml-declaration"></a>XML-Deklaration  
 Die XML-Deklaration in einer Instanz wird nicht beibehalten, wenn die Instanz in der Datenbank gespeichert wird. Zum Beispiel:  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 Das Ergebnis ist `<doc/>`.  
  
 Die XML-Deklaration, z. B. `<?xml version='1.0'?>`, wird nicht beibehalten, wenn die XML-Daten in einer **xml** -Datentypinstanz gespeichert werden. Dies ist beabsichtigt. Die XML-Deklaration () und die Attribute (Version/Codierung/Eigenständigkeit) gehen bei der Konvertierung in den Typ **xml**verloren. Die XML-Deklaration wird als Direktive für den XML-Parser behandelt. Die XML-Daten werden intern als ucs-2 gespeichert. Alle anderen PIs in der XML-Instanz werden beibehalten.  
  
  
### <a name="order-of-attributes"></a>Reihenfolge von Attributen  
 Die Reihenfolge der Attribute in einer XML-Instanz wird nicht erhalten. Bei einer Abfrage der in der **xml** -Typspalte gespeicherten XML-Instanz kann die Reihenfolge der Attribute in der resultierenden XML von der der ursprünglichen XML-Instanz abweichen.  
  
  
### <a name="quotation-marks-around-attribute-values"></a>Anführungszeichen um Attributwerte  
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
  
  
### <a name="namespace-prefixes"></a>Namespacepräfixe  
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
  
 Das Namespacepräfix des Ergebnisses kann unterschiedlich sein. Zum Beispiel:  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
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
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen von Instanzen der XML-Daten](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
