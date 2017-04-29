---
title: "Heraufstufen häufig verwendeter XML-Werte mit berechneten Spalten | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc333316c144154f0f06d4f8f9ae0a2887660700
ms.lasthandoff: 04/11/2017

---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>Heraufstufen häufig verwendeter XML-Werte mit berechneten Spalten
  Wenn Abfragen in erster Linie nur für eine geringe Anzahl von Element- und Attributwerten ausgeführt werden, kann es sinnvoll sein, diese Mengen in relationale Spalten heraufzustufen. Dies ist nützlich, wenn Abfragen für einen kleinen Teil der XML-Daten ausgegeben werden, während die gesamte XML-Instanz abgerufen wird. Das Erstellen eines XML-Indexes für die XML-Spalte ist nicht erforderlich. Stattdessen kann die heraufgestufte Spalte indiziert werden. Um die heraufgestufte Spalte zu verwenden, müssen Abfragen geschrieben werden. Das heißt, der Abfrageoptimierer richtet die Abfragen für die XML-Spalte nicht erneut an die heraufgestufte Spalte aus.  
  
 Die heraufgestufte Spalte kann entweder eine berechnete Spalte in derselben Tabelle oder eine getrennte, benutzerverwaltete Spalte in einer Tabelle sein. Dies ist ausreichend, wenn Singleton-Werte aus jeder XML-Instanz heraufgestuft werden. Allerdings müssen Sie für mehrwertige Eigenschaften eine getrennte Tabelle für die Eigenschaft erstellen, was im folgenden Abschnitt beschrieben wird.  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>Berechnete Spalte auf der Basis des xml-Datentyps  
 Eine berechnete Spalte kann mithilfe einer benutzerdefinierten Funktion erstellt werden, die **xml** -Datentypmethoden aufruft. Der Typ der berechneten Spalte kann jeder SQL-Typ sein, einschließlich XML. Dies wird im folgenden Beispiel veranschaulicht.  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>Beispiel: Berechnete Spalte auf der Basis der xml-Datentypmethode  
 Erstellen Sie die benutzerdefinierte Funktion für die ISBN-Nummer eines Buchs:  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 Fügen Sie der Tabelle eine berechnete Spalte für die ISBN hinzu:  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 Die berechnete Spalte kann auf gewöhnliche Weise indiziert werden.  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>Beispiel: Abfragen für eine berechnete Spalte auf der Basis der xml-Datentypmethoden  
 So erhalten Sie das <`book`>-Element, dessen ISBN 0-7356-1588-2 ist:  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 Die Abfrage für die XML-Spalte kann so umgeschrieben werden, dass sie die berechnete Spalte verwendet:  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 Sie können eine benutzerdefinierte Funktion erstellen, die den **xml** -Datentyp zurückgibt, und eine berechnete Spalte mithilfe dieser benutzerdefinierten Funktion. Allerdings können Sie keinen XML-Index für die berechnete XML-Spalte erstellen.  
  
## <a name="creating-property-tables"></a>Erstellen von Eigenschaftentabellen  
 Wenn Sie einige der mehrwertigen Eigenschaften aus Ihren XML-Daten in eine oder mehrere Tabellen heraufstufen möchten, erstellen Sie Indizes für diese Tabellen und richten Sie Ihre Abfrage erneut so aus, dass sie diese Indizes verwenden. Ein typisches Szenario hierfür ist eine Situation, in der eine kleine Anzahl von Eigenschaften den Großteil Ihrer Abfragearbeitsauslastung abdeckt. Sie können folgendermaßen vorgehen:  
  
-   Erstellen Sie eine oder mehrere Tabellen, die die mehrwertigen Eigenschaften aufnehmen. Sie könnten praktischerweise so vorgehen, dass Sie eine Eigenschaft pro Tabelle speichern und den Primärschlüssel der Basistabelle in den Eigenschaftentabellen speichern, um einen Rückwärtsjoin mit der Basistabelle zu erreichen.  
  
-   Wenn Sie die relative Reihenfolge der Eigenschaften beibehalten möchten, müssen Sie eine getrennte Spalte für die relative Reihenfolge einführen.  
  
-   Erstellen Sie Trigger für die XML-Spalte, um die Eigenschaftentabellen zu verwalten. Führen Sie innerhalb der Trigger einen der folgenden Schritte aus:  
  
    -   Verwenden Sie **xml** -Datentypmethoden, z.B. **nodes()** und **value()**, um Zeilen der Eigenschaftentabellen einzufügen oder zu löschen.  
  
    -   Erstellen Sie Streaming-Tabellenwertfunktionen in CLR (Common Language Runtime), um Zeilen der Eigenschaftentabellen einzufügen oder zu löschen.  
  
    -   Schreiben Sie Abfragen für den SQL-Zugriff auf die Eigenschaftentabellen und für den XML-Zugriff auf die XML-Spalte in der Basistabelle, wodurch Joins zwischen den Tabellen mithilfe ihres Primärschlüssels erstellt werden.  
  
### <a name="example-create-a-property-table"></a>Beispiel: Erstellen einer Eigenschaftentabelle  
 Angenommen, Sie wollen den ersten Vornamen des Autors heraufstufen. Bücher weisen einen oder mehrere Autoren auf, sodass der Vorname eine mehrwertige Eigenschaft ist. Jeder Vorname ist in einer getrennten Zeile einer Eigenschaftentabelle gespeichert. Der Primärschlüssel der Basistabelle wird in die Eigenschaftentabelle dupliziert, um einen Rückwärtsjoin zu erstellen.  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>Beispiel: Erstellen einer benutzerdefinierten Funktion zum Generieren eines Rowsets aus einer XML-Instanz  
 Die folgende Tabellenwertfunktion (udf_XML2Table) akzeptiert einen Primärschlüsselwert und eine XML-Instanz. Sie ruft den Vornamen aller Autoren aus den <`book`>-Elementen ab und gibt ein Rowset mit Paaren aus Primärschlüssel und Vorname zurück.  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>Beispiel: Erstellen von Triggern zum Auffüllen einer Eigenschaftentabelle  
 Der insert-Trigger bewirkt das Einfügen von Zeilen in die Eigenschaftentabelle:  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 Der delete-Trigger löscht die Zeilen aus der Eigenschaftentabelle und richtet sich dabei nach dem Primärschlüsselwert der gelöschten Zeilen.  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 Der update-Trigger löscht die vorhandenen Zeilen in der Eigenschaftentabelle entsprechend der aktualisierten XML-Instanz und fügt neue Zeilen in die Eigenschaftentabelle ein:  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>Beispiel: Suchen nach XML-Instanzen, deren Autoren denselben Vornamen haben  
 Die Abfrage kann für die XML-Spalte geformt werden. Alternativ kann sie die Eigenschaftentabelle nach dem Vornamen "David" durchsuchen und einen Rückwärtsjoins mit der Basistabelle ausführen, um die XML-Instanz zurückzugeben: Zum Beispiel:  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>Beispiel: Projektmappe mit Verwendung der Streaming-Tabellenwertfunktion in CLR  
 Diese Projektmappe umfasst die folgenden Schritte:  
  
1.  Definieren Sie eine CLR-Klasse (SqlReaderBase), die ISqlReader implementiert und eine Tabellenwert-Streaming-Ausgabe generiert, indem ein Pfadausdruck auf eine XML-Instanz angewendet wird.  
  
2.  Erstellen Sie ein Assembly und eine benutzerdefinierte Transact-SQL-Funktion, um die CLR-Klasse zu starten.  
  
3.  Definieren Sie die insert-, update- und delete-Trigger, indem Sie die benutzerdefinierte Funktion zum Verwalten einer Eigenschaftentabelle verwenden.  
  
 Dazu erstellen Sie zuerst die Streaming-CLR-Funktion. Der **xml** -Datentyp wird als eine verwaltete SqlXml-Klasse in ADO.NET verfügbar gemacht und unterstützt die **CreateReader()** -Methode, die einen XmlReader zurückgibt.  
  
> [!NOTE]  
>  Der Beispielcode in diesem Abschnitt verwendet XPathDocument und XPathNavigator. Diese zwingen Sie, alle XML-Dokumente in den Arbeitsspeicher zu laden. Wenn Sie ähnlichen Code in Ihrer Anwendung verwenden, um mehrere große XML-Dokumente zu verarbeiten, ist dieser Code nicht skalierbar. Halten Sie stattdessen die Speicherbelegung gering, und verwenden Sie wenn möglich Streaming-Schnittstellen. Weitere Informationen zur Leistung finden Sie unter [Architektur der CLR-Integration](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9).  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 Erstellen Sie als Nächstes eine Assembly und eine benutzerdefinierte [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktion – SQL_streaming_xml_tvf (nicht dargestellt) –, die der CLR-Funktion streaming_xml_tvf entspricht. Die benutzerdefinierte Funktion wird zum Definieren der Tabellenwertfunktion CLR_udf_XML2Table verwendet, mit der das Rowset generiert wird:  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 Definieren Sie schließlich die Trigger wie im Beispiel "Erstellen von Triggern zum Auffüllen einer Eigenschaftentabelle", ersetzen Sie dabei jedoch udf_XML2Table durch die CLR_udf_XML2Table-Funktion. Der insert-Trigger ist im folgenden Beispiel dargestellt:  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 Der delete-Trigger ist identisch mit der Nicht-CLR-Version. Dagegen ist beim update-Trigger lediglich die Funktion udf_XML2Table() durch CLR_udf_XML2Table() ersetzt.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von XML in berechneten Spalten](../../relational-databases/xml/use-xml-in-computed-columns.md)  
  
  
