---
title: SQLXML-Schnittstelle | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c636345439175c516b647a2951ac3bfa8824b06
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlxml-interface"></a>SQLXML-Schnittstelle
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC Driver bietet Unterstützung für die JDBC 4.0-API, in der die java.sql.SQLXML-Schnittstelle eingeführt wird. Die SQLXML-Schnittstelle definiert Methoden zum interagieren und Bearbeiten von XML-Daten. Die **SQLXML** -Datentyp zugeordnet, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Xml** -Datentyp.  
  
 Die SQLXML-Schnittstelle bietet Methoden für den Zugriff auf den XML-Wert als eine **Zeichenfolge**, **Reader** oder **Writer**, oder als eine **Stream**. Der XML-Wert kann auch durch zugegriffen werden eine **Quelle** oder legen Sie als eine **Ergebnis**, dem dienen mit XML-Parser-APIs wie z. B. (DOKUMENTOBJEKTMODELL), Simple API für XML (SAX) und Streaming API for XML-StAX (), als sowie mit XSLT transformiert und XPath.  
  
## <a name="remarks"></a>Hinweise  
 In der folgenden Tabelle werden die in der SQLXML-Schnittstelle definierten Methoden beschrieben:  
  
|Methodensyntax|Methodenbeschreibung|  
|-------------------|------------------------|  
|["void" free()](http://go.microsoft.com/fwlink/?LinkId=131685)|Mit dieser Methode werden das SQLXML-Objekt und die von diesem verwendeten Ressourcen freigegeben.|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|Gibt einen Eingabedatenstrom zum Lesen von Daten aus dem SQLXML zurück.|  
|[Reader getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|Gibt die **XML** Daten als java.io.Reader-Objekt oder als zeichendatenstrom.|  
|[T erweitert Quelle T GetSource (Klasse\<T > SourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|Gibt eine **Quelle** zum Lesen der **XML** Wert angegeben, die von diesem **SQLXML** Objekt.<br /><br /> **Hinweis:** die GetSource-Methode unterstützt die folgenden Quellen: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource und java.io.InputStream.|  
|[Zeichenfolge GetString() zu](http://go.microsoft.com/fwlink/?LinkId=131757)|Gibt eine Zeichenfolgendarstellung der **XML** Wert festgelegt, die von diesem SQLXML-Objekt.|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|Ruft einen Stream, der zum Schreiben verwendet werden kann die **XML** Wert, der diesem SQLXML-Objekt darstellt.|  
|[Writer setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|Gibt einen Stream zum Schreiben zu verwendende der **XML** Wert, der diesem SQLXML-Objekt darstellt.|  
|[T erweitert Ergebnis T z. B. SetResult (Klasse\<T > ResultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|Gibt eine **Ergebnis** für die Einstellung der **XML** Wert angegeben, die von diesem **SQLXML** Objekt.<br /><br /> **Hinweis:** z. B. SetResult-Methode unterstützt die folgenden Quellen: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult und java.io.OutputStream.|  
|["void" setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|Legt den XML-Wert, der von diesem SQLXML-Objekt in den angegebenen benannten **Zeichenfolge** Darstellung.|  
  
 Die Anwendungen können XML-Werte nur einmal aus einem SQLXML-Objekt lesen bzw. in dieses schreiben.  
  
 Wenn die free()-Methode aufgerufen wird, wird ein SQLXML-Objekt wird ungültig und wird weder gelesen noch geschrieben werden. Wenn die Anwendung versucht, eine Methode auf das SQLXML-Objekt als die free()-Methode aufrufen, wird eine Ausnahme ausgelöst.  
  
 Die SQLXML-Objekt nicht mehr gelesen oder geschrieben beim Aufrufen einer der folgenden Abrufmethoden: GetSource, GetCharacterStream, GetBinaryStream, und GetString.  
  
 Das SQLXML-Objekt nicht mehr weder beschreibbaren gelesen oder geschrieben werden beim Aufrufen einer der folgenden festlegungsmethoden: z. B. SetResult, SetCharacterStream, SetBinaryStream, und SetString.  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützung von XML-Daten](../../connect/jdbc/supporting-xml-data.md)  
  
  
