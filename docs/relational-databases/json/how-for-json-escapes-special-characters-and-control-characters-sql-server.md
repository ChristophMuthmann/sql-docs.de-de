---
title: Schutz von Sonderzeichen und Steuerzeichen durch FOR JSON (SQL Server) | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1b2a6a10c3aa3ec3caa432a208be4b3023072046
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>Schutz von Sonderzeichen und Steuerzeichen durch FOR JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Dieses Thema beschreibt, wie die **FOR JSON**-Klausel einer **SELECT**-Anweisung von SQL Server Sonderzeichen schützt und Steuerzeichen in der JSON-Ausgabe darstellt.  

> [!IMPORTANT]
> Diese Seite beschreibt die integrierte Unterstützung für JSON in Microsoft SQL Server. Allgemeine Informationen zum Maskieren und Codierung in JSON finden Sie in Abschnitt 2.5 des JSON RFC - [http://www.ietf.org/rfc/rfc4627.txt](http://www.ietf.org/rfc/rfc4627.txt).

## <a name="escaping-of-special-characters"></a>Schutz von Sonderzeichen  
Wenn die Quelldatei Sonderzeichen enthält, umgeht die **FOR JSON**-Klausel diese in der JSON-Ausgabe mit `\`, wie in der folgenden Tabelle dargestellt. Dieser Schutz tritt in den Namen von Eigenschaften und in ihren Werte auf.  
  
|**Sonderzeichen**|**Ausgabe mit Escapezeichen**|  
|---------------------------|--------------------------|  
|Anführungszeichen (")|\\"|  
|Umgekehrter Schrägstrich (\\)|\\\|  
|Schrägstrich (/)|\\/|  
|Rücktaste|\b|  
|Seitenvorschub|\f|  
|Neue Zeile|\n|  
|Wagenrücklauf|\r|  
|Horizontaler Tabstopp|\t|  
  
## <a name="control-characters"></a>Steuerzeichen  
Wenn die Quelldatei Steuerzeichen enthält, kodiert die **FOR JSON**-Klausel diese in der JSON-Ausgabe im `\u<code>`-Format, wie in der folgenden Tabelle dargestellt.  
  
|**Steuerzeichen**|**Codierte Ausgabe**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>Beispiel  
 Hier ist ein Beispiel für die **FOR JSON**-Ausgabe von Quelldaten, die Sonderzeichen und Steuerelement enthält.  
  
 Abfrage:  
  
```tsql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 Ergebnis:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  
  
## <a name="see-also"></a>Siehe auch  
 [Formatieren von Abfrageergebnisse als JSON mit FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR-Klausel](../../t-sql/queries/select-for-clause-transact-sql.md)

