---
title: "Verwenden von R-Code in Transact-SQL (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# Verwenden von R-Code in Transact-SQL (SQL Server R Services)
Dieses Tutorial zeigt kurze Beispiele der Syntax zum Arbeiten mit R in SQL Server R Services.    
    
    
Dies ist ein guter Ausgangspunkt, wenn Sie noch keine Erfahrung mit SQL Server R Services haben und die Grundlagen kennenlernen möchten, wie ein R-Skript in einer gespeicherten T-SQL-Prozedur definiert wird, wie Daten als Eingabe verwendet werden und wie Ausgaben definiert werden.    
    
**Voraussetzungen:** Sie müssen zum Ausführen von R-Code in SQL Server R Services mit einer SQL Server-Instanz verbunden sein, bei der R Services bereits installiert ist.     
    
## Teil 1 – Grundlegende Vorgänge  

In den folgenden Abschnitten erfahren Sie, wie Sie die gespeicherte Prozedur erweitern, indem Sie Parameter hinzufügen, und wie Sie die Eingaben und Ausgaben konfigurieren.   
  
### 1.1. Überprüfen, ob R in SQL Server funktioniert  

Diese Abfrage verwendet die gespeicherte Systemprozedur, [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx), mit der Sie R im Kontext von SQL Server aufrufen können. In diesem Beispiel wird eine SQL-Abfrage als Input an R übermittelt. R übergibt diesen Datenrahmen anschließend an SQL Server.     
    
1. Suchen Sie Microsoft SQL Server Management Studio im Windows-Startmenü.     
2. Falls Sie es nicht finden können, müssen Sie es möglicherweise zuerst installieren: [Hier können Sie SQL Server Management Studio herunterladen.](https://msdn.microsoft.com/library/mt238290.aspx)    
3. Geben Sie im Dialogfeld **Verbindung mit Server herstellen** den Namen eines Servers oder einer Instanz ein, auf dem bzw. der SQL Server R Services aktiviert ist. Zur Verwendung dieser Beispiele müssen Sie sich mit einem Konto anmelden, das über die Fähigkeit verfügt, eine neue Datenbank zu erstellen, SELECT-Anweisungen auszuführen und Tabellen anzuzeigen.  Öffnen Sie ein neues **Abfrage**-Fenster, und fügen Sie diese Anweisung ein, nur um zu überprüfen, dass alles betriebsbereit ist:    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. Erstellen einiger einfacher Testdaten  
    
Bevor Sie eine komplexe Data Science-Lösung entwickeln, sollten Sie die Unterschiede zwischen SQL Server und R verstehen.    
  
1. Erstellen Sie eine temporäre Tabelle mit Daten, indem Sie die folgende T-SQL-Anweisung ausführen.     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. Wenn die Tabelle erstellt wurde, verwenden Sie die folgende Anweisung zum Abfragen der Tabelle:  
    ```sql  
    SELECT * from #MyData  
    ```  

**Ergebnisse**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. Abrufen der Textdaten mithilfe eines R-Skripts    
  
Führen Sie die folgende Anweisung aus, nachdem die Tabelle erstellt wurde:  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
Es sollten die gleichen Werte zurückgegeben werden, jedoch mit einem neuen Spaltennamen.  
  
**Hinweise**    
- Der Parameter *@language* definiert die aufzurufende Spracherweiterung, was in diesem Fall R ist.    
- Im Parameter *@script* definieren Sie die Befehle, die an die R-Laufzeit als Unicode-Text übergeben wird. Sie können den Text auch einer Variablen des Typs **nvarchar** hinzufügen und die Variable anschließend aufrufen.    
- Die Zeile `N'OutputDataSet <- InputDataSet;'` übergibt die im Standardvariablennamen **InputDataSet** enthaltenen Eingabedaten an R und übermittelt sie anschließend ohne weitere Vorgänge wieder an die Ergebnisse. Beachten Sie, dass bei R die Groß- und Kleinschreibung berücksichtigt wird. Daher muss sowohl für den Variablennamen der Eingabe als auch für den der Ausgabe die richtige Schreibweise verwendet werden, da ansonsten ein Fehler ausgegeben wird.    
   
    
Um eine andere Eingabe- oder Ausgabevariable anzugeben, verwenden Sie den Parameter *@input_data_1_name*, und geben Sie einen gültigen SQL-Bezeichner ein. In diesem Beispiel wurden die Namen der Ausgabe- und der Eingabevariablen in *SQLOut* bzw. *SQLIn* geändert:    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**Hinweise**    
- Die erforderlichen Parameter *@input_data_1* und *@output_data_1* müssen zuerst angegeben werden, um die optionalen Parameter *@input_data_1_name* und *@output_data_1_name* zu verwenden.    
- SQL und R unterstützen nicht die gleichen Datentypen. Daher finden sehr häufig Typumwandlungen statt, wenn Daten von SQL Server an R und umgekehrt gesendet werden. Weitere Informationen finden Sie unter [Arbeiten mit R-Datentypen](../../advanced-analytics/r-services/working-with-r-data-types.md).    
- Nur eine Eingabedataset kann als Parameter übergeben werden, und Sie können nur ein Dataset zurückgeben. Allerdings können Sie andere Datasets innerhalb Ihres R-Codes aufrufen und Ausgaben und andere Typen zusätzlich zum Dataset zurückgeben. Sie können auch das Schlüsselwort OUTPUT zu einem beliebigen Parameter hinzufügen, damit es mit den Ergebnissen zurückgegeben wird.      
- Das Schema für das zurückgegebene Dataset (R data.frame) wird durch die `WITH RESULT SETS`-Anweisung definiert. Versuchen Sie es auszulassen, und beobachten Sie, was passiert.    
- Tabellarische Ergebnisse werden im Bereich **Werte** zurückgegeben. Nachrichten, die von der R-Laufzeit zurückgegeben werden, werden in den **Meldungen** bereitgestellt.     
  
### 1.4. Generieren der Ergebnisse mithilfe von R    
    
Sie können Werte auch nur mit dem R-Skript generieren und die Zeichenfolge der Eingabeabfrage in _@input_data_1_ leer lassen. Alternativ können Sie eine gültige SQL SELECT-Anweisung als Platzhalter verwenden. Sie können die SQL-Ergebnisse jedoch nicht in einem R-Skript verwenden.    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**Ergebnisse**    
    
    
 |*col* |    
 |-----|    
 |*Hello*|    
 |     |    
 |*world*|    
    

Probieren Sie nun eine andere Version des oben aufgeführten „Hello World“-Beispiels.     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**Ergebnisse**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*Hello*|  |*world*|    
    
Beachten Sie, dass beide Anweisungen einen Vektor mit drei Werten erstellen, das zweite Beispiel jedoch drei Spalten mit einer einzelnen Zeile zurückgibt, während das erste eine einzelne Spalte mit drei Zeilen zurückgibt. Warum?
    
R bietet viele Methoden (Vektoren, Matrizen, Arrays und Listen), um mit Wertespalten zu arbeiten. Obwohl diese Vorgänge leistungsstark und flexibel sind, entsprechen sie nicht immer den Erwartungen von SQL-Entwicklern.  Einige R-Funktionen führen implizite Datenobjektkonvertierungen für Listen und Matrizen aus.

> [!TIP] 
> 
> Überprüfen Sie immer Ihre Ergebnisse, und legen Sie fest, wie viele Spalten von Daten Ihr R-Code zurückgeben wird und was die Datentypen sein werden.    
>     
> Unabhängig davon, ob Ihr R-Code Matrizen, Vektoren oder eine andere Datenstruktur verwendet, sollten Sie darauf achten, dass das vom R-Skript an die gespeicherte Prozedur ausgegebene Ergebnis ein **data.frame** sein muss.      
  
  
## Teil 2 – Datenkonvertierung und andere Probleme  
  
Dieser Abschnitt enthält eine kurze Übersicht über einige der Probleme, die bei der Ausführung Ihres R-Codes in SQL Server zu berücksichtigen sind.  
  
+ Datentypen: Verstehen von Umwandlungs- und Konvertierungsoptionen sowie implizierten Konvertierungen  
+ Tabellarische Resultsets: Vorhersehen, wie R Datenspalten und -zeilen verändern kann    
  
### 2.1 Implizierte Koersion von Datentypen  
    
R und SQL Server verwenden nicht die gleichen Datentypen. Sie müssen daher die Einschränkungen beachten, wenn Sie Daten zwischen R und der Datenbank verschieben. Die folgenden Beispiele veranschaulichen einige bekannte Probleme.   
    
    
1. Führen Sie die folgende Anweisung aus, um die Matrixmultiplikation mithilfe von R durchzuführen.In diesem Skript wird die einzelne Spalte mit drei Werten in eine einspaltige Matrix konvertiert.  R wandelt die zweite Variable, `y`, implizit in eine einspaltige Matrix um, sodass die zwei Argumente dieser entsprechen.  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**Ergebnisse**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. Führen Sie nun das nächste Skript aus, das sich ähnlich verhält, und beobachten Sie, was passiert, wenn Sie die Länge des Arrays verändern. 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**Ergebnisse**    
    
|Col1|
|---|    
|1542|    
  
  Dieses Mal gibt R einen einzelnen Wert als Ergebnis zurück. Dieses Ergebnis ist gültig, da die beiden Argumente Vektoren derselben Länge sind. Darum gibt R das innere Produkt als Matrix zurück.    
    
   
  
### 2.2 Zusammenführen oder Multiplizieren von Spalten mit unterschiedlicher Länge    
    
  
Das folgende Skript stellt einige Verhaltensweisen von R dar, die möglicherweise nicht den Erwartungen eines Datenbankentwicklers entsprechen.   
  
Das Skript definiert ein numerisches Array der Länge 6 und speichert es in der R-Variable `df1`. Das numerische Array wird anschließend mit den ganzen Zahlen der #MyData-Tabelle kombiniert, die drei Werte enthält, um einen neuen Datenrahmen, `df2`, zu erstellen.   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**Ergebnisse**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
Es gibt viele Funktionen in R, mit denen eine Tabellenausgabe erstellt werden kann, die jedoch abhängig vom R-Datenobjekt unterschiedliche Vorgänge auf den Werten ausführen können. Da diese gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur erfordert, dass jeweils die Eingaben und Ausgaben als Datenrahmen übergeben werden, werden Sie häufig Funktionen verwenden, um Spalten und Zeilen zu und aus Datenrahmen zu konvertieren.    
    
Wenn Sie jemals Zweifel haben, welches Datenobjekt von R verwendet wird, fügen Sie die Funktion `str()` von R hinzu oder eine der Erkennungsfunktionen (`is.matrix`, `is.vector` usw.), um die Ergebnisse zu überprüfen und das tatsächliche Schema und die Werttypen abzurufen.    
  
  
Weitere Informationen finden Sie in diesem Artikel von Hadley Wickham unter [R Data Structures](http://adv-r.had.co.nz/Data-structures.html) (Datenstrukturen von R).    
    
### 2.3 Identifizieren von Datentypen und Überprüfen von Schemas   
Sie sehen, dass es wichtig ist, genau zu wissen, wie viele Spalten Ihr R-Code zurückgibt und welche Datentypen diese Spalten aufweisen.     
    
  
Sie können die Funktion `str()` in Ihrem R-Skript verwenden, um das Datenschema des R-Objekts als Informationsmeldung in zurückzugeben. 

Die folgende Anweisung gibt z.B. das Schema der Tabelle „#MyData“ zurück.    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**Ergebnisse**    
    
*STDOUT-Meldung(en) aus dem externen Skript:*    
*'data.frame': 3 obs. von 1 Variable:*    
*STDOUT-Meldung(en) aus dem externen Skript:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4 Umwandeln oder Konvertieren von Spalten   
  
Beim Senden von Daten aus SQL Server an R müssen Sie häufig die Datentypen umwandeln oder konvertieren, um sicherzustellen, dass sie ordnungsgemäß verarbeitet werden.    
  
Wenn Sie eine SQL-Abfrage als Eingabe für R-Code verwenden, finden mehrere Datentransformationen statt:    
- SQL Server überträgt die Daten aus der Abfrage an den vom Launchpad-Dienst verwalteten R-Prozess und konvertiert sie in eine interne Darstellung.    
- Die R-Laufzeit lädt die Daten in eine data.frame-Variable und führt ihre eigenen Vorgänge für die Daten aus.    
- Das Datenbankmodul gibt die Daten an Management Studio oder einem anderen Client mithilfe der SQL Server-Datentypen zurück.  
    
1. Führen Sie die folgende Abfrage auf dem Data Warehouse AdventureWorksDW aus. Die Eingabedatenabfrage definiert eine Tabelle mit Umsatzdaten, die für die Erstellung einer Vorhersage verwendet werden.   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. Überprüfen Sie nun die Ergebnisse der `str`-Funktion, um zu sehen, wie R die Eingabedaten verarbeitet hat.
      
**Ergebnisse**    
    
  *STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:*    
  *STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**Hinweise**    
    
- Einige SQL Server-Datentypen werden von R nicht unterstützt. Daher sollten Sie zur Vermeidung von Fehlern die Spalten einzeln angeben und einige Spalten umwandeln.    
- Das Zeichenfolgenprädikat in der WHERE-Klausel muss von jeweils zwei einfachen Anführungszeichen umschlossen sein.    
- Die datetime-Spalte wurde als R-Datentyp **POSIXct** zurückgegeben.    
- Die Spalte [ProductSeries] wurde (richtig) als ein **Faktor** identifiziert.    
     
  
### 2.5 Verwenden mehrerer Eingaben   
Es kann nur ein Eingabedataset als Parameter übergeben werden. Allerdings können Sie andere Datasets innerhalb Ihres R-Codes mithilfe von RODBC aufrufen.     
  
Im folgenden Beispiel wird ein Aufruf an das RODBC-Paket gesendet und gibt die Daten in einer SELECT-Anweisung an.    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

Es wird empfohlen, RODBC zu verwenden, um kleinere Datasets wie Suchvorgänge oder Faktorlisten zu erhalten, und den Parameter „@input_data“ zum Abrufen größerer Datasets von SQL Server zu verwenden, mit denen z.B. ein Modell trainiert wird. 


### 2.6 Generieren mehrerer Ausgaben

In SQL Server 2016 ist die Ausgabe von R aus der gespeicherten Prozedur sp_execute_external_script auf einen einzelnen Datenrahmen oder ein einzelnes Dataset beschränkt. (Diese Einschränkung wird möglicherweise in Zukunft entfernt.)   
Sie können allerdings zusätzlich zum Dataset Ausgaben für andere Typen zurückgeben. Sie können möglicherweise z.B. ein Modell mithilfe eines einzelnen Datasets als Eingabe trainieren, dann jedoch eine Statistiktabelle als Ausgabe und das trainierte Modell als Objekt zurückgeben.    
    
Sie können zudem auch das Schlüsselwort `OUTPUT` zu einem beliebigen Eingabeparameter hinzufügen, damit es mit den Ergebnissen zurückgegeben wird.   
    
### 2.7 Parallelverarbeitung    
    
Wenn Sie mit einem großen Dataset arbeiten und die SQL-Abfrage, die die Daten abruft, einen parallelen Abfrageplan generieren kann, können Sie ein R-Skript parallel ausführen, indem Sie den Parameter *@parallel* auf „1“ festlegen. Dies ist in der Regel hilfreich, wenn Sie ein großes Resultset bewerten. Wenn Sie diese Option verwenden, müssen Sie das Schema der Ausgabeergebnisse im Voraus mithilfe von WITH RESULT SETS angeben.    
    
Allerdings hat dieser Parameter keinerlei Auswirkungen, wenn Sie ein Modell trainieren müssen, das alle Zeilen verwendet. In solchen Fällen empfiehlt es sich, die **ScaleR**-Pakete zu verwenden. Diese Pakete können die Verarbeitung automatisch verteilen, ohne dass *@parallel=1* beim Aufrufen von sp_execute_external_script angegeben werden muss.    
    
      
  
## Teil 3. Umschließen von R-Funktionen in gespeicherten Prozeduren  
  
R kann viele erweiterte statistische Funktionen ausführen, die sich in T-SQL möglicherweise nur mit kompliziertem Code reproduzieren ließen.  Mit R Services können Sie Skripts für R-Hilfsprogramme jedoch in einer gespeicherten Prozedur ausführen, um z.B. folgende Tasks zu unterstützen:   
    
- Anwenden von mathematischen und statistischen Funktionen von R auf SQL Server-Daten    
    
- Erstellen von Tabellenwertfunktionen oder skalaren Funktionen, die R-Code verwenden    
     

 In der Regel würden Sie die Aufrufe dieser R-Funktionen in gespeicherten Prozeduren kapseln, um die Übergabe von Parametern zu vereinfachen. Zur Veranschaulichung dieses Prozesses wird die gleiche Funktion in R-Code, in einem Ad-Hoc-Aufruf der gespeicherten Prozedur „sp_execute_external_script“ und zu guter Letzt in einer gespeicherten Prozedur bereitgestellt, mit der Sie die R-Funktion parametrisieren können.
 
      
### 3.1. Generieren von Zufallszahlen  
  
Die folgende Anweisung verwendet eine der R-Funktionen aus dem `stats`-Paket, das standardmäßig geladen wird, wenn R Services installiert werden. Die hier gezeigte `rnorm`-Funktion generiert 20 Zufallszahlen mit Normalverteilung, deren Mittelwert 100 beträgt.    

Dies ist der R-Code, der die Arbeit übernimmt.

```r
as.data.frame(rnorm(20, mean = 100));
```

Diese Anweisung ruft die Funktion von T-SQL auf und gibt die Ergebnisse an SQL Server aus.  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

Als Nächstes umschließen Sie die gespeicherte Prozedur mit einer anderen gespeicherten Prozedur, um die Übergabe von Parametern zu erleichtern. Definieren Sie jeden Eingabeparameter im Argument _@params_, und ordnen Sie jeden Parameter nach Namen dem entsprechenden R-Parameter zu.

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

Rufen Sie die neue gespeicherte Prozedur auf, und übergeben Sie Werte.

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2. Weitere Verwendungsmöglichkeiten für R-Hilfsfunktionen  
  
In diesem Beispiel wird eines der R-Hilfspakete aufgerufen und dessen `memory.limit()`-Funktion verwendet, um Speicher für die aktuelle Umgebung abzurufen. Das `utils`-Paket wird installiert, jedoch nicht standardmäßig geladen.    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

Im nächsten Beispiel wird mithilfe der R-Funktion „.Machine“ die maximale Länge von ganzen Zahlen abgerufen, die auf dem aktuellen Computer unterstützt werden, und an die Konsole ausgegeben.

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
Allerdings funktioniert R nicht immer besser. Mengenbasierte Vorgänge in SQL Server können für einige Vorgänge wesentlich effizienter sein, die Datenanalysten traditionell in R ausführen würden.Ein Beispiel für einen Leistungsvergleich der R-Funktionen und der benutzerdefinierten Funktionen von T-SQL finden Sie unter [Exemplarische Data Science Ende-zu-Ende-Vorgehensweise](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md). 

Es wird empfohlen, situationsabhängig auszuwerten, ob die Durchführung eines bestimmten Vorgangs mit R, mit T-SQL oder mit einem anderen Tool am sinnvollsten ist.    
    
    
    
### Zusätzliche Ressourcen    
    
[Tieferer Einblick in Data Science: Verwenden des RevoScaleR-Pakets](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md): Diese exemplarische Vorgehensweise bietet praktische Beispiele mit häufigen Data Science-Tasks    
[Data Science End-to-End solution](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) (Data Science Ende-zu-Ende-Lösung): Diese exemplarische Vorgehensweise beschreibt eine Entwicklung und einen Entwicklungsprozess, in der bzw. in dem sowohl SQL als auch R verwendet wird       
[In-Database Advanced Analytics for SQL Developers (Tutorial)](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md) (Datenbankinterne Advanced Analytics für SQL-Entwickler (Tutorial)): Diese exemplarische Vorgehensweise beschreibt die vollständigen Modelloperationalisierung eines SQL-Entwicklers.     
    
    
    
    
