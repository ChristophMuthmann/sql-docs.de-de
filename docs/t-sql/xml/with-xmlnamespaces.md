---
title: WITH XMLNAMESPACES (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs:
- TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 57874942a62d1a63b6ea22adf0bfa6bdb932f3de
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Deklariert mindestens einen XML-Namespace.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>Argumente  
 *xml_namespace_uri*  
 Ein URI (Uniform Resource Identifier), der den zu deklarierenden XML-Namespace identifiziert. *xml_namespace_uri* ist eine SQL-Zeichenfolge.  
  
 *xml_namespace_prefix*  
 Gibt ein Präfix an, das dem in *xml_namespace_uri* angegebenen Wert vom Namespace-URI zugeordnet werden soll. *xml_namespace_prefix* muss ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner sein.  
  
## <a name="remarks"></a>Remarks  
 Wenn Sie die WITH XMLNAMESPACES-Klausel in einer Anweisung verwenden, die außerdem einen allgemeinen Tabellenausdruck enthält, muss die WITH XMLNAMESPACES-Klausel vor dem allgemeinen Tabellenausdruck in der Anweisung stehen.  
  
 Es folgen allgemeine Syntaxregeln, die beim Verwenden der WITH XMLNAMESPACES-Klausel angewendet werden.  
  
-   Jede XML-Namespacedeklaration muss mindestens ein Element der XML-Standardnamespacedeklaration enthalten.  
  
-   Jedes verwendete XML-Namespacepräfix muss ein nicht kolonisierter Name (NCName) sein, bei dem der Doppelpunkt (:) nicht Teil des Namens ist.  
  
-   Ein Namespacepräfix kann nicht zweimal definiert werden.  
  
-   XML-Namespacepräfixe und URIs berücksichtigen die Groß-/Kleinschreibung.  
  
-   Das XML-Namespacepräfix `xmlns` kann nicht deklariert werden.  
  
-   Das XML-Namespacepräfix `xml` kann nur mit dem URI `'http://www.w3.org/XML/1998/namespace'` des Namespaces überschrieben werden, und dieser URI kann keinem anderen Präfix zugeordnet werden.  
  
-   Das XML-Namespacepräfix `xsi` kann nicht erneut deklariert werden, wenn die ELEMENTS XSINIL-Direktive für die Abfrage verwendet wird.  
  
-   URI-Zeichenfolgenwerte werden gemäß der aktuellen Datenbanksortierungs-Codepage verschlüsselt und intern in Unicode übersetzt.  
  
-   Die Leerzeichen des XML-Namespace-URIs werden gemäß den für **xs:anyURI** verwendeten XSD-Leerzeichenreduzierungsregeln reduziert. Darüber hinaus werden keine Entitäten für XML-Namespace-URI-Werte ausgeführt oder aufgelöst.  
  
-   Der XML-Namespace-URI wird auf ungültige XML 1.0-Zeichen überprüft. Wird ein solches Zeichen gefunden, wird ein Fehler ausgelöst (z. B. U+0007).  
  
-   Der XML-Namespace-URI (nach der Reduzierung aller Leerzeichen) kann keine leere Zeichenfolge sein, da sonst ein Fehler vom Typ "ungültiger leerer Namespace-URI" ausgelöst wird.  
  
-   Das Schlüsselwort XMLNAMESPACES ist im Kontext der WITH-Klausel reserviert.  
  
## <a name="examples"></a>Beispiele  
 Beispiele finden Sie unter [Hinzufügen von Namespaces zu Abfragen mit WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
