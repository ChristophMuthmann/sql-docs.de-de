---
title: "Beispiel für SQLXML-Datentyp | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b265d7f16eba8af7ceefd9abea738b0069162f8f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlxml-data-type-sample"></a>SQLXML Datenbeispiel-Typ
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Dies [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] beispielanwendung für veranschaulicht, wie XML-Daten in einer relationalen Datenbank gespeichert, wie XML-Daten aus einer Datenbank abgerufen und das Analysieren von XML-Daten mit den **SQLXML** Java-Datentyp.  
  
 In den Codebeispielen in diesem Abschnitt wird ein SAX (Simple API for XML)-Parser verwendet. SAX ist ein öffentlich entwickelter Standard für die ereignisbasierte Analyse von XML-Dokumenten. Es stellt außerdem eine Anwendungsprogrammierschnittstelle für die Arbeit mit XML-Daten bereit. Beachten Sie, dass in den Anwendungen ebenso jeder andere XML-Parser wie DOM (Document Object Model) oder StAX (Streaming API for XML) usw. verwendet werden kann.  
  
 DOM (Document Object Model) stellt eine programmgesteuerte Darstellung der XML-Dokumente, -Fragmente, -Knoten oder -Knotensätze bereit. Es stellt außerdem eine Anwendungsprogrammierschnittstelle für die Arbeit mit XML-Daten bereit. Entsprechend handelt es sich bei StAX (Streaming API for XML) um eine Java-basierte API für die Pullanalyse von XML.  
  
> [!IMPORTANT]  
>  Um die SAX-Parser-API verwenden zu können, müssen Sie die SAX-Standardimplementierung aus dem Paket "javax.xml" importieren.  
  
 Die Codedatei für dieses Beispiel heißt "sqlxmlExample.java" und befindet sich unter folgendem Pfad:  
  
 \<*Installationsverzeichnis*> \sqljdbc_\<*Version*>\\<*Sprache*> \samples\datatypes  
  
## <a name="requirements"></a>Anforderungen  
 Wenn Sie diese Beispielanwendung ausführen möchten, müssen Sie die Datei "sqljdbc4.jar" in den Klassenpfad aufnehmen. Wenn im Klassenpfad kein Eintrag für "sqljdbc4.jar" vorhanden ist, löst die beispielanwendung die Ausnahme "Klasse nicht gefunden" aus. Weitere Informationen zum Festlegen des Klassenpfads finden Sie unter [mit dem JDBC-Treiber](../../connect/jdbc/using-the-jdbc-driver.md).  
  
 Darüber hinaus benötigen Sie Zugriff auf die [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] Beispieldatenbank, um diese beispielanwendung ausführen.  
  
## <a name="example"></a>Beispiel  
 In der folgende Beispielcode stellt eine Verbindung mit der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] Datenbank und ruft dann die CreateSampleTables-Methode.  
  
 Mit der createSampleTables-Methode werden die Testtabellen TestTable1 und TestTable2 gelöscht, sofern vorhanden. Dann werden zwei Zeilen in TestTable1 eingefügt.  
  
 Darüber hinaus enthält das Codebeispiel die folgenden drei Methoden und eine zusätzliche Klasse mit dem Namen "ExampleContentHandler".  
  
 Die ExampleContentHandler-Klasse implementiert einen benutzerdefinierten Inhaltshandler, der Methoden für Parserereignisse definiert.  
  
 Die showGetters-Methode veranschaulicht das Analysieren der Daten im SQLXML-Objekt mit SAX, ContentHandler und XMLReader. Zunächst erstellt das Codebeispiel eine Instanz eines benutzerdefinierten Inhaltshandlers, dem ExampleContentHandler. Dann wird eine SQL-Anweisung erstellt und ausgeführt, die einen Datensatz aus TestTable1 zurückgibt. Anschließend werden im Codebeispiel ein SAX-Parser abgerufen und die XML-Daten analysiert.  
  
 Die ShowSetters-Methode veranschaulicht das Festlegen der **Xml** -Spalte mit SAX, ContentHandler und ResultSet. Zuerst erstellt ein leeres SQLXML-Objekt mithilfe der [CreateSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Methode der Connection-Klasse. Dann wird eine Instanz eines Inhaltshandlers abgerufen, um die Daten in das SQLXML-Objekt zu schreiben. Anschließend werden die Daten im Codebeispiel in TestTable1 geschrieben. Schließlich der Code durchläuft die Datenzeilen im Resultset enthalten sind, und verwendet die [GetSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) Methode, um die XML-Daten zu lesen.  
  
 Die showTransformer-Methode veranschaulicht das Abrufen von XML-Daten aus der einen Tabelle, die dann mit SAX und Transformer in eine andere Tabelle eingefügt werden. Zunächst wird das SQLXML-Quellobjekt aus TestTable1 abgerufen. Anschließend erstellt er ein leeres SQLXML-Zielobjekt mithilfe der [CreateSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) Methode der Connection-Klasse. Daraufhin wird das SQLXML-Zielobjekt aktualisiert, und die XML-Daten werden in TestTable2 geschrieben. Schließlich der Code durchläuft die Datenzeilen im Resultset enthalten sind, und verwendet die [GetSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) Methode, um die XML-Daten in TestTable2.  
  
 [!code[JDBC#UsingSQLXML1](../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit Datentypen &#40; JDBC &#41;](../../connect/jdbc/working-with-data-types-jdbc.md)  
  
  
