---
title: "Beispiele für den Massenimport und -export von XML-Dokumenten (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field terminators [SQL Server]
- bulk importing [SQL Server], data formats
- row terminators [SQL Server]
- OPENROWSET function, XML bulk load
- terminators [SQL Server]
- bulk exporting [SQL Server], data formats
- XML bulk load [SQL Server]
ms.assetid: dff99404-a002-48ee-910e-f37f013d946d
caps.latest.revision: 65
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 17f350c10f32dbd230d7c372820178a3dde081d2
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="examples-of-bulk-import-and-export-of-xml-documents-sql-server"></a>Beispiele für den Massenimport und -export von XML-Dokumenten (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

    
##  <a name="top"></a>
 Sie können XML-Dokumente per Massenimport in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank importieren bzw. aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank exportieren. Dieses Thema bietet Beispiele für diese beiden Situationen.  
  
 Verwenden Sie für den Massenimport von Daten aus einer Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder eine nicht partitionierte Sicht Folgendes:  
  
-   **bcp** (Hilfsprogramm)  
 Sie können das **bcp** -Hilfsprogramm auch verwenden, um Daten von einem beliebigen Speicherort in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank zu exportieren, wo eine SELECT-Anweisung verwendet werden kann, einschließlich partitionierter Sichten.  
  
-   BULK INSERT  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
 **Hinweis:** Weitere Informationen finden Sie in den folgenden Themen 
  - [Importieren und Exportieren von Massendaten mithilfe des Hilfsprogramms bcp (SQL Server).](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
   - [Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET(BULK...) (SQL Server).](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md) 
    - [Importieren von XML in SQL Server mit der Komponente zum XML-Massenladen.](https://support.microsoft.com/en-us/kb/316005)
     - [XML-Schemaauflistungen (SQL Server)](https://msdn.microsoft.com/library/ms187856.aspx)
  
## <a name="examples"></a>Beispiele  
 Es werden folgende Beispiele aufgeführt:  
  
-  [A. Massenimport von XML-Daten als binärer Bytedatenstrom](#binary_byte_stream)  
  
-  [B. Massenimport von XML-Daten in eine vorhandene Zeile](#existing_row)  
  
-  [C. Massenimport von XML-Daten aus einer Datei, die eine DTD enthält](#file_contains_dtd)  
  
- [D. Explizites Angeben des Feldabschlusszeichens mithilfe einer Formatdatei](#field_terminator_in_format_file)  
  
-  [E. Massenexport von XML-Daten](#bulk_export_xml_data)  
  
## <a name="binary_byte_stream"></a>Massenimport von XML-Daten als binärer Bytedatenstrom  
 Geben Sie beim Massenimportieren von XML-Daten aus einer Datei mit einer Codierungsdeklaration, die Sie anwenden möchten, die Option SINGLE_BLOB in der OPENROWSET(BULK...)-Klausel an. Mit der Option SINGLE_BLOB stellen Sie sicher, dass der XML-Parser in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Daten gemäß dem in der XML-Deklaration angegebenen Codierungsschema importiert.  
  
#### <a name="sample-table"></a>Beispieltabelle  
 Zum Testen des unten aufgeführten Beispiels A erstellen Sie die folgende Beispieltabelle `T`.  
  
```  
USE tempdb  
CREATE TABLE T (IntCol int, XmlCol xml);  
GO  
```  
  
#### <a name="sample-data-file"></a>Beispieldatendatei  
 Bevor Sie Beispiel A ausführen können, müssen Sie die UTF-8-codierte Datei (`C:\SampleFolder\SampleData3.txt`) erstellen, die die folgende Beispielinstanz enthält, die das `UTF-8` -Codierungsschema angibt.  
  
```  
\<?xml version="1.0" encoding="UTF-8"?>  
<Root>  
          <ProductDescription ProductModelID="5">  
             <Summary>Some Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-a"></a>Beispiel A  
 In diesem Beispiel wird die `SINGLE_BLOB` -Option in einer `INSERT ... SELECT * FROM OPENROWSET(BULK...)` -Anweisung verwendet, um die Daten aus einer Datei namens `SampleData3.txt` zu importieren und eine XML-Instanz in eine Beispieltabelle mit einer einzelnen Spalte `T`einzufügen.  
  
```  
INSERT INTO T(XmlCol)  
SELECT * FROM OPENROWSET(  
   BULK 'c:\SampleFolder\SampleData3.txt',  
   SINGLE_BLOB) AS x;  
```  
  
#### <a name="remarks"></a>Hinweise  
 Indem Sie SINGLE_BLOB verwenden, können Sie vermeiden, dass die Codierung des XML-Dokuments (wie in der XML-Codierungsdeklaration angegeben) und die Codierung der vom Server implizierten Codepage nicht übereinstimmen.  
  
 Wenn beim Verwenden der Datentypen NCLOB oder CLOB Codepage- oder Codierungskonflikte auftreten, führen Sie einen der folgenden Schritte aus:  
  
-   Entfernen Sie die XML-Deklaration, um den Inhalt der XML-Datendatei erfolgreich zu importieren.  
  
-   Geben Sie eine dem Codierungsschema der XML-Deklaration entsprechende Codepage in der CODEPAGE-Option der Abfrage an.  
  
-   Stellen Sie eine Übereinstimmung oder Auflösung zwischen den Einstellungen der Datenbanksortierung und einem Nicht-Unicode-XML-Codierungsschema her.  
  
 [&#91;Nach oben&#93;](#top)  
  
##  <a name="existing_row"></a> Massenimport von XML-Daten in eine vorhandene Zeile  
 In diesem Beispiel wird der `OPENROWSET` -Massenrowsetanbieter verwendet, um eine XML-Instanz einer vorhandenen Zeile bzw. vorhandenen Zeilen in der Beispieltabelle `T`hinzuzufügen.  
  
> [!NOTE]  
>  Bevor Sie dieses Beispiel ausführen können, müssen Sie zunächst das Testskript aus Beispiel A abschließen. In Beispiel A wird nämlich die `tempdb.dbo.T` -Tabelle erstellt und der Massenimport von Daten aus `SampleData3.txt`durchgeführt.  
  
#### <a name="sample-data-file"></a>Beispieldatendatei  
 In Beispiel B wird eine veränderte Version der Beispieldatendatei `SampleData3.txt` aus dem vorhergehenden Beispiel verwendet. Ändern Sie den Inhalt dieser Datei wie folgt, um dieses Beispiel auszuführen:  
  
```  
<Root>  
          <ProductDescription ProductModelID="10">  
             <Summary>Some New Text</Summary>  
          </ProductDescription>  
</Root>  
```  
  
#### <a name="example-b"></a>Beispiel B  
  
```  
-- Query before update shows initial state of XmlCol values.  
SELECT * FROM T  
UPDATE T  
SET XmlCol =(  
SELECT * FROM OPENROWSET(  
   BULK 'C:\SampleFolder\SampleData3.txt',  
           SINGLE_BLOB  
) AS x  
)  
WHERE IntCol = 1;  
GO  
```  
  
 [&#91;Nach oben&#93;](#top)  
  
## <a name="file_contains_dtd"></a> Massenimport von XML-Daten aus einer Datei, die eine DTD enthält  
  
> [!IMPORTANT]  
>  Es wird nicht empfohlen, die Unterstützung für DTDs (Document Type Definitions) zu aktivieren, es sei denn, dies ist in Ihrer XML-Umgebung erforderlich. Das Aktivieren der DTD-Unterstützung erhöht die Angriffsfläche Ihres Servers, und kann ihn einem Denial-of-Service-Angriff aussetzen. Wenn Sie die Unterstützung von DTDs aktivieren müssen, können Sie dieses Sicherheitsrisiko reduzieren, indem Sie ausschließlich vertrauenswürdige XML-Dokumente verarbeiten.  
  
 Wenn versucht wird, einen [bcp](../../tools/bcp-utility.md) -Befehl zum Importieren von XML-Daten aus einer Datei mit DTD zu verwenden, tritt möglicherweise ein Fehler wie der folgende auf:  
  
 "SQLState = 42000, NativeError = 6359"  
  
 "Error = [Microsoft][SQL Server Native Client][SQL Server]Das Analysieren von XML mit internen Teilmengen-DTDs ist unzulässig. Verwenden Sie CONVERT mit der Formatoption '2', um die begrenzte Unterstützung interner Teilmengen-DTDs zu ermöglichen."  
  
 "Fehler beim Kopieren von %s mit BCP"  
  
 Um dieses Problem zu umgehen, können Sie die XML-Daten aus einer Datendatei mit DTD importieren, indem Sie die `OPENROWSET(BULK...)` -Funktion verwenden und die `CONVERT` -Option in der `SELECT` -Klausel des Befehls angeben. Die Hauptsyntax für diesen Befehl lautet:  
  
 `INSERT ... SELECT CONVERT(…) FROM OPENROWSET(BULK...)`  
  
#### <a name="sample-data-file"></a>Beispieldatendatei  
 Bevor Sie dieses Beispiel für den Massenimport testen, müssen Sie zunächst die Datei`C:\temp\Dtdfile.xml`erstellen, die die folgende Beispielinstanz enthält:  
  
```  
<!DOCTYPE DOC [<!ATTLIST elem1 attr1 CDATA "defVal1">]><elem1>January</elem1>  
```  
  
#### <a name="sample-table"></a>Beispieltabelle  
 In Beispiel C wird die Beispieltabelle `T1` verwendet, die Sie durch die folgende `CREATE TABLE` -Anweisung erstellen:  
  
```  
USE tempdb;  
CREATE TABLE T1(XmlCol xml);  
GO  
```  
  
#### <a name="example-c"></a>Beispiel C  
 In diesem Beispiel wird mit `OPENROWSET(BULK...)` die `CONVERT` -Option in der `SELECT` -Klausel angegeben, um die XML-Daten aus `Dtdfile.xml` in die Beispieltabelle `T1`zu importieren.  
  
```  
INSERT T1  
  SELECT CONVERT(xml, BulkColumn, 2) FROM   
    OPENROWSET(Bulk 'c:\temp\Dtdfile.xml', SINGLE_BLOB) [rowsetresults];  
```  
  
 Nach dem Ausführen der `INSERT` -Anweisung wird die DTD aus der XML-Datei entfernt und in der Tabelle `T1` gespeichert.  
  
 [&#91;Nach oben&#93;](#top)  
  
## <a name="field_terminator_in_format_file"></a> Explizites Angeben des Feldabschlusszeichens mithilfe einer Formatdatei  
 Im folgenden Beispiel wird gezeigt, wie das XML-Dokument `Xmltable.dat`per Massenimport importiert wird.  
  
#### <a name="sample-data-file"></a>Beispieldatendatei  
 Das Dokument in `Xmltable.dat` enthält zwei XML-Werte; einen für jede Zeile. Der erste XML-Wert ist UTF-16-codiert, der zweite ist UTF-8-codiert:  
  
 Der Inhalt dieser Datendatei wird im folgenden Hexadezimalabbild gezeigt:  
  
```  
FF FE 3C 00 3F 00 78 00-6D 00 6C 00 20 00 76 00  *..\<.?.x.m.l. .v.*  
65 00 72 00 73 00 69 00-6F 00 6E 00 3D 00 22 00  *e.r.s.i.o.n.=.".*  
31 00 2E 00 30 00 22 00-20 00 65 00 6E 00 63 00  *1...0.". .e.n.c.*  
6F 00 64 00 69 00 6E 00-67 00 3D 00 22 00 75 00  *o.d.i.n.g.=.".u.*  
74 00 66 00 2D 00 31 00-36 00 22 00 3F 00 3E 00  *t.f.-.1.6.".?.>.*  
3C 00 72 00 6F 00 6F 00-74 00 3E 00 A2 4F 9C 76  *\<.r.o.o.t.>..O.v*  
0C FA 77 E4 80 00 89 00-00 06 90 06 91 2E 9B 2E  *..w.............*  
99 34 A2 34 86 00 83 02-92 20 7F 02 4E C5 E4 A3  *.4.4..... ..N...*  
34 B2 B7 B3 B7 FE F8 FF-F8 00 3C 00 2F 00 72 00  *4.........\<./.r.*  
6F 00 6F 00 74 00 3E 00-00 00 00 00 7A EF BB BF  *o.o.t.>.....z...*  
3C 3F 78 6D 6C 20 76 65-72 73 69 6F 6E 3D 22 31  *\<?xml version="1*  
2E 30 22 20 65 6E 63 6F-64 69 6E 67 3D 22 75 74  *.0" encoding="ut*  
66 2D 38 22 3F 3E 3C 72-6F 6F 74 3E E4 BE A2 E7  *f-8"?><root>....*  
9A 9C EF A8 8C EE 91 B7-C2 80 C2 89 D8 80 DA 90  *................*  
E2 BA 91 E2 BA 9B E3 92-99 E3 92 A2 C2 86 CA 83  *................*  
E2 82 92 C9 BF EC 95 8E-EA 8F A4 EB 88 B4 EB 8E  *................*  
B7 EF BA B7 EF BF B8 C3-B8 3C 2F 72 6F 6F 74 3E  *.........</root>*  
00 00 00 00 7A                                   *....z*  
```  
  
#### <a name="sample-table"></a>Beispieltabelle  
 Beim Massenimport oder -export eines XML-Dokuments sollten Sie ein [Feldabschlusszeichen](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md) verwenden, das keinesfalls in einem der Dokumente auftritt, beispielsweise eine Reihe von vier Nullen (`\0`) gefolgt vom Buchstaben `z`: `\0\0\0\0z`.  
  
 In diesem Beispiel wird gezeigt, wie Sie dieses Feldabschlusszeichen in der Beispieltabelle `xTable` verwenden. Verwenden Sie zum Erstellen dieser Beispieltabelle die folgende `CREATE TABLE` -Anweisung:  
  
```  
USE tempdb;  
CREATE TABLE xTable (xCol xml);  
GO  
```  
  
#### <a name="sample-format-file"></a>Beispielformatdatei  
 Das Feldabschlusszeichen muss in der Formatdatei angegeben werden. In Beispiel D wird eine Nicht-XML-Formatdatei namens `Xmltable.fmt` verwendet, die Folgendes enthält:  
  
```  
9.0  
1  
1       SQLBINARY     0       0       "\0\0\0\0z"    1     xCol         ""  
```  
  
 Sie können diese Formatdatei für den Massenimport von XML-Dokumenten in die `xTable` -Tabelle verwenden und dazu entweder einen `bcp` -Befehl oder eine `BULK INSERT` - oder eine `INSERT ... SELECT * FROM OPENROWSET(BULK...)` -Anweisung verwenden.  
  
#### <a name="example-d"></a>Beispiel D  
 In diesem Beispiel wird die `Xmltable.fmt` -Formatdatei in einer `BULK INSERT` -Anweisung verwendet, um den Inhalt einer XML-Datendatei namens `Xmltable.dat`zu importieren.  
  
```  
BULK INSERT xTable   
FROM 'C:\Xmltable.dat'  
WITH (FORMATFILE = 'C:\Xmltable.fmt');  
GO  
```  
  
 [&#91;Nach oben&#93;](#top)  
  
## <a name="bulk_export_xml_data"></a> Massenexport von XML-Daten  
 Im folgenden Beispiel werden XML-Daten mithilfe von `bcp` per Massenexport aus der im vorherigen Beispiel erstellten Tabelle exportiert. Dabei wird dieselbe XML-Formatdatei verwendet. Im folgenden `bcp` -Befehl stellen `<server_name>` und `<instance_name>` Platzhalter dar, die durch die entsprechenden Werte ersetzt werden müssen:  
  
```  
bcp bulktest..xTable out a-wn.out -N -T -S<server_name>\<instance_name>  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichert die XML-Codierung nicht, wenn XML-Daten in der Datenbank persistent gespeichert werden. Die ursprüngliche Codierung der XML-Felder ist also nicht mehr verfügbar, wenn die XML-Daten exportiert werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet für den Export von XML-Daten die UTF-16-Codierung.  
  

## <a name="see-also"></a>Siehe auch  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  

