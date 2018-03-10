---
title: "Überspringen einer Tabellenspalte mithilfe einer Formatdatei (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/15/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ffe13b9772d5c281897fa2e9099060e6858660b6
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/19/2018
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>Überspringen einer Tabellenspalte mithilfe einer Formatdatei (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

In diesem Artikel wird beschrieben, wie eine Formatdatei zum Überspringen des Imports einer Tabellenspalte verwendet wird, wenn die Daten für die übersprungene Spalte nicht in der Quelldatendatei vorhanden sind. Eine Datendatei kann weniger Felder enthalten als Spalten in der Zieltabelle vorhanden sind. Das bedeutet, dass Sie das Importieren einer Spalte überspringen können – allerdings nur, wenn eine der folgenden zwei Bedingungen in der Zieltabelle erfüllt ist:
-   Für die übersprungene Spalte ist NULL zulässig.
-   Die übersprungene Spalte besitzt einen Standardwert.  
  
## <a name="sample-table-and-data-file"></a>Beispieltabelle und Datendatei  
 Die Beispiele in diesem Artikel erwarten eine Tabelle mit der Bezeichnung `myTestSkipCol` unter dem **dbo**-Schema. Sie können diese Tabelle in einer Beispieldatenbank wie *WideWorldImporters* oder *AdventureWorks* oder einer anderen beliebigen Datenbank erstellen. Erstellen Sie diese Tabelle folgendermaßen  
  
```sql
USE WideWorldImporters;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
In den Beispielen in diesem Artikel wird auch eine Beispieldatendatei verwendet: `myTestSkipCol2.dat`. Diese Datendatei enthält nur zwei Felder, obwohl die Zieltabelle drei Spalten enthält.

```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
```  
  
## <a name="basic-steps"></a>Grundlegende Schritte

Sie können eine Nicht-XML-Formatdatei oder eine XML-Formatdatei verwenden, um eine Tabellenspalte auszulassen. In beiden Fällen sind zwei Schritte erforderlich:

1.   Verwenden Sie das **bcp**-Befehlszeilenhilfsprogramm, um eine Standardformatdatei zu erstellen.

2.   Ändern Sie die Standardformatdatei in einem Text-Editor.

Die geänderte Formatdatei muss jedes vorhandene Feld der jeweiligen Spalte in der Zieltabelle zuordnen. Es muss ebenfalls angegeben werden, welche Tabellenspalte oder -spalten übersprungen werden sollen. 

Um beispielsweise einen Massenimport von Daten aus `myTestSkipCol2.dat` in die Tabelle `myTestSkipCol` durchzuführen, muss die Formatdatei das erste Datenfeld `Col1` zuordnen, `Col2` überspringen und das zweite Feld `Col3` zuordnen.  
 
## <a name="option-1---use-a-non-xml-format-file"></a>Option 1: Verwenden einer Nicht-XML-Formatdatei  
  
### <a name="step-1---create-a-default-non-xml-format-file"></a>Schritt 1: Erstellen einer Nicht-XML-Standardformatdatei  
Erstellen Sie eine Nicht-XML-Standardformatdatei für die Beispieltabelle `myTestSkipCol`, indem Sie den folgenden **bcp**-Befehl an der Eingabeaufforderung ausführen:  
  
```cmd
bcp WideWorldImporters..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  

> [!IMPORTANT]  
>  Möglicherweise müssen Sie mit dem `-S`-Argument den Namen der Serverinstanz angeben, mit der Sie eine Verbindung herstellen. Außerdem kann es erforderlich sein, den Benutzernamen und das entsprechende Kennwort mit den Argumenten `-U` und `-P` anzugeben. Weitere Informationen finden Sie unter [bcp Utility](../../tools/bcp-utility.md).  

Mit dem zuvor angeführten Befehl wird die Nicht-XML-Formatdatei `myTestSkipCol_Default.fmt`erstellt: Diese Formatdatei wird auch als *Standardformatdatei* bezeichnet. Es handelt sich hierbei um die Form, in der Dateien von **bcp**generiert werden. Mit einer Standardformatdatei wird eine 1:1-Entsprechung zwischen den Feldern in der Datendatei und den Spalten in der Tabelle beschrieben.  
  
 Im folgenden Screenshot werden Werte in diesen Beispiel-Standardformatzeichendateien gezeigt. 
  
 ![Standardmäßige Nicht-XML-Formatdatei für MyTextSkipCol](../../relational-databases/import-export/media/mytestskipcol-f-c-default-fmt.gif "default non-XML format file for myTestSkipCol")  
  
> [!NOTE]  
>  Weitere Informationen zu Formatdateifeldern finden Sie unter [Nicht-XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
### <a name="step-2---modify-a-non-xml-format-file"></a>Schritt 2: Ändern einer Nicht-XML-Formatdatei  
Um eine Nicht-XML-Standardformatdatei zu ändern, gibt es zwei Alternativen. Beide Alternativen zeigen, dass das Datenfeld in der Datendatei nicht vorhanden ist und dass keine Daten in die entsprechende Tabellenspalte eingefügt werden.

Sie können eine Tabellenspalte auslassen, indem Sie eine standardmäßige Nicht-XML-Formatdatei bearbeiten und die Datei mithilfe einer der folgenden alternativen Methoden ändern:  

#### <a name="option-1---remove-the-row"></a>Option 1: Entfernen der Zeile
Die bevorzugte Methode zum Überspringen einer Spalte umfasst die folgenden drei Schritte:

1.   Löschen Sie zuerst alle Formatdateizeilen, in denen Felder beschrieben werden, die in der Quelldatendatei fehlen.
2.   Ändern Sie anschließend den Wert „Reihenfolge der Felder der Hostdatei“ für die einzelnen Formatdateizeilen, die auf eine gelöschte Zeile folgen. Das Ziel besteht darin, mithilfe der „Host file field order“-Werte (Reihenfolge der Felder der Hostdatei) von 1 bis *n*die eigentliche Position der einzelnen Datenfelder in der Datendatei zu erhalten.
3.   Abschließend muss der Wert im Feld „Spaltenanzahl“ entsprechend der tatsächlichen Anzahl der Felder in der Datendatei verringert werden.  
  
Das folgende Beispiel basiert ebenfalls auf der Standardformatdatei für die Tabelle `myTestSkipCol`. In dieser geänderten Formatdatei wird `Col1`das erste Datenfeld zugeordnet, `Col2`wird ausgelassen, und das zweite Datenfeld wird `Col3`zugeordnet. Die Zeile für `Col2` wurde gelöscht. Das Trennzeichen nach dem ersten Feld wurde ebenfalls von `\t` in `,` geändert.
  
```  
14.0  
2  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
```  
  
#### <a name="option-2---modify-the-row-definition"></a>Option 2: Ändern der Zeilendefinition

Alternativ können Sie eine Tabellenspalte auslassen, indem Sie die Definition der Formatdateizeile ändern, die der Tabellenspalte entspricht. In dieser Formatdateizeile müssen die Werte „prefix length“, „host file data length“ und „server column order“ auf 0 festgelegt werden. Außerdem müssen die Felder „terminator“ und „column collation“ auf „“ (d.h. auf einen leeren oder NULL-Wert) festgelegt werden. Für „server column name“ (Serverspaltenname)muss eine Zeichenfolge eingegeben werden, die nicht leer ist. Dabei muss es sich jedoch auch nicht um den tatsächlichen Spaltennamen handeln. Für die verbleibenden Formatfelder sind die entsprechenden Standardwerte erforderlich.  
  
Das folgende Beispiel wird ebenfalls von der Standardformatdatei der `myTestSkipCol` -Tabelle abgeleitet.  
  
```  
14.0  
3  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       0       ""       0     Col2         ""  
3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
```  
  
### <a name="examples-with-a-non-xml-format-file"></a>Beispiele mit einer Nicht-XML-Formatdatei 
Die folgenden Beispiele basieren auf der Beispieltabelle `myTestSkipCol` und der Beispieldatendatei `myTestSkipCol2.dat`, die weiter oben in diesem Artikel beschrieben wurden.  
  
#### <a name="using-bulk-insert"></a>Verwenden von BULK INSERT  
Dieses Beispiel funktioniert wie im vorherigen Abschnitt beschrieben unter Verwendung einer geänderten erstellten Nicht-XML-Formatdateien. In diesem Beispiel lautet der Name der geänderten Formatdatei `myTestSkipCol2.fmt`. Führen Sie den folgenden Code in SSMS aus, um `BULK INSERT` zum Massenimport der `myTestSkipCol2.dat`-Datendatei zu verwenden. Aktualisieren Sie die Dateisystempfade für den Speicherort der Beispieldateien auf Ihrem Computer.
  
```sql  
USE WideWorldImporters;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="option-2---use-an-xml-format-file"></a>Option 2: Verwenden einer XML-Formatdatei  
  
### <a name="step-1---create-a-default-xml-format-file"></a>Schritt 1: Erstellen einer XML-Standardformatdatei   

Erstellen Sie eine XML-Standardformatdatei für die Beispieltabelle `myTestSkipCol`, indem Sie den folgenden **bcp**-Befehl an der Eingabeaufforderung ausführen:  
  
```cmd
bcp WideWorldImporters..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
> [!IMPORTANT]  
>  Möglicherweise müssen Sie mit dem `-S`-Argument den Namen der Serverinstanz angeben, mit der Sie eine Verbindung herstellen. Außerdem kann es erforderlich sein, den Benutzernamen und das entsprechende Kennwort mit den Argumenten `-U` und `-P` anzugeben. Weitere Informationen finden Sie unter [bcp (Hilfsprogramm)](../../tools/bcp-utility.md).  
 
Mit dem zuvor genannten Befehl wird eine XML-Formatdatei namens `myTestSkipCol_Default.xml` erstellt. Diese Formatdatei wird auch als *Standardformatdatei* bezeichnet. Es handelt sich hierbei um die Form, in der Dateien von **bcp**generiert werden. Mit einer Standardformatdatei wird eine 1:1-Entsprechung zwischen den Feldern in der Datendatei und den Spalten in der Tabelle beschrieben.  
  
```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Informationen zur Struktur von XML-Formatdateien finden Sie unter [XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  

### <a name="step-2---modify-an-xml-format-file"></a>Schritt 2: Ändern einer XML-Formatdatei

Hier ist die geänderte XML-Formatdatei, `myTestSkipCol2.xml`, dargestellt, die `Col2` überspringt. Die Einträge `FIELD` und `ROW` für `Col2` wurden entfernt, und die Einträge wurden neu nummeriert. Das Trennzeichen nach dem ersten Feld wurde ebenfalls von `\t` in `,` geändert.

```xml
<?xml version="1.0"?>  
<BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
 
### <a name="examples-with-an-xml-format-file"></a>Beispiele für eine XML-Formatdatei   
Die folgenden Beispiele basieren auf der Beispieltabelle `myTestSkipCol` und der Beispieldatendatei `myTestSkipCol2.dat`, die weiter oben in diesem Artikel beschrieben wurden.

Zum Importieren der Daten aus `myTestSkipCol2.dat` in die Tabelle `myTestSkipCol` wird in den Beispielen die geänderte XML-Formatdatei `myTestSkipCol2.xml` verwendet.   
  
#### <a name="using-bulk-insert-with-a-view"></a>Verwenden von BULK INSERT mit einer Sicht  

Bei einer XML-Formatdatei ist es nicht möglich, beim direkten Importieren in eine Tabelle mit dem Befehl **bcp** oder der `BULK INSERT`-Anweisung eine Spalte auszulassen. Sie können jedoch Daten in alle Spalten einer Tabelle mit Ausnahme der letzten Spalte importieren. Wenn Sie eine andere Spalte als die letzte auslassen müssen, müssen Sie eine Sicht der Zieltabelle erstellen, die nur die in der Datendatei enthaltenen Spalten enthält. Anschließend können Sie Daten aus dieser Datei in die Sicht massenimportieren.  
  
Im folgenden Beispiel wird für die `myTestSkipCol`-Tabelle die Sicht `v_myTestSkipCol` erstellt. In dieser Sicht wird die zweite Tabellenspalte, `Col2`, ausgelassen. Anschließend wird mit `BULK INSERT` die Datendatei `myTestSkipCol2.dat` in die Sicht importiert.  
  
Führen Sie den folgenden Code in SSMS aus: Aktualisieren Sie die Dateisystempfade für den Speicherort der Beispieldateien auf Ihrem Computer. 
  
```sql  
USE WideWorldImporters;  
GO  

CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  

#### <a name="using-openrowsetbulk"></a>Verwenden von OPENROWSET(BULK...)  

Um eine XML-Formatdatei zu verwenden, die unter Verwendung von `OPENROWSET(BULK...)` eine Tabellenspalte überspringt, muss eine explizite Liste von Spalten in der Auswahlliste und in der Zieltabelle angegeben werden:  
  
    ```sql
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...) 
    ```

Im folgenden Beispiel werden der Massenrowsetanbieter `OPENROWSET` und die Formatdatei `myTestSkipCol2.xml` verwendet. Die Datendatei `myTestSkipCol2.dat` wird per Massenimport in die `myTestSkipCol` -Tabelle übertragen. Die Anweisung enthält anforderungsgemäß eine explizite Liste der Spalten in der Auswahlliste und in der Zieltabelle.  
  
Führen Sie den folgenden Code in SSMS aus: Aktualisieren Sie die Dateisystempfade für den Speicherort der Beispieldateien auf Ihrem Computer.
  
```sql  
USE WideWorldImporters;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Auslassen eines Datenfelds mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
