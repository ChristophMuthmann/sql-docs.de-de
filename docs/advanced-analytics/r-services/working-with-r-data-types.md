---
title: "Arbeiten mit R-Datentypen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Arbeiten mit R-Datentypen
  Während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt mehrere Dutzend Datentypen R hat eine beschränkte Anzahl von skalaren Datentypen (numerisch, Integer, komplexe, logische und Zeichen, Datum/Uhrzeit und raw). Daher bei Verwendung von Daten aus  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in R-Skripts können verschiedene Dinge geschehen:  
  
-   Daten werden implizit in einen kompatiblen Datentyp konvertiert.  
  
-   Daten können nicht implizit konvertiert werden, und ein Fehler wird zurückgegeben.  
  
 Im Allgemeinen verwenden, wenn Sie nicht sicher sind haben, wie eine bestimmte Datenstruktur oder Datentyp in R verwendet wird, der  `str()` Funktion, um die interne Struktur und die Art der R-Objekt abzurufen. Das Ergebnis der Funktion wird in der R-Konsole ausgegeben und steht auch in den Abfrageergebnissen in der **Nachrichten** Registerkarte [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Wenn eine bestimmte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp wird nicht unterstützt, von R, jedoch müssen Sie die Spalten der Daten im R-Skript verwenden, wir empfehlen die Verwendung der [CAST und CONVERT & #40; Transact-SQL & #41;](../../t-sql/functions/cast-and-convert-transact-sql.md) Funktionen, um sicherzustellen, dass der Datentyp Konvertierungen werden durchgeführt, wie beabsichtigt, bevor Sie die Daten in Ihrem R-Skript verwenden.  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentypen finden Sie in [Datentypen & #40; Transact-SQL & #41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
## Datentypenkonvertierung zwischen R und SQL Server  
 In der folgenden Tabelle zeigt die Änderungen in Datentypen und Werte, wenn Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in einem R-Skript verwendet und an Sie zurückgesendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||||  
|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] type|R-Klasse|Geben Sie im **RESULTSET**|Kommentare|  
|**smalldatetime**|`POSIXct`|**Datetime**|Dargestellt als GMT|  
|**smallmoney**|`numeric`|**Float**||  
|**Datetime**|`POSIXct`|**Datetime**|Dargestellt als GMT|  
|**money**|`numeric`|**Float**||  
|**uniqueidentifier**|`character`|**varchar(max)**||  
|**numeric(p,s)**|`numeric`|**Float**||  
|**decimal(p,s)**|`numeric`|**Float**||  
|**Datum**|`POSIXct`|**Datetime**|Dargestellt als GMT|  
|**tinyint**|`integer`|**int**||  
|**bit**|`logical`|**bit**||  
|**smallint**|`integer`|**int**||  
|**int**|`integer`|**int**||  
|**Float**|`numeric`|**Float**||  
|**real**|`numeric`|**Float**||  
|**bigint**|`numeric`|**Float**||  
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Nur als Eingabeparameter und als Ausgabe zulässig|  
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary (n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Nur als Eingabeparameter und als Ausgabe zulässig|  
|**varchar (n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary(max)**|`raw`|**varbinary(max)**|Nur als Eingabeparameter und als Ausgabe zulässig|  
  
## Beispiele für die Datentypenkonvertierung  
 Die folgende Abfrage ruft eine Reihe von Werten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle, und verwendet die gespeicherte Prozedur  [Sp_execute_external_script & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) um die Werte mithilfe der R-Laufzeit auszugeben.  
  
```  
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```  
  
 **Ergebnisse**  
  
||||||  
|-|-|-|-|-|  
||C1|C2|C3|C4|  
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|  
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|  
  
 Beachten Sie, dass die `str` -Funktion in R, um das Schema der Ausgabedaten zu erhalten. Diese Funktion gibt die folgenden Informationen zurück:  
  
```  
'data.frame':2 obs. of  4 variables:   
 $ c1: int  1 -11   
 $ c2: Factor w/ 2 levels "Hello","world": 1 2   
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1   
 $ cR: num  4 2  
```  
  
 Daraus können Sie erkennen, dass die folgenden Datentypenkonvertierungen implizit als Teil der Abfrage durchgeführt wurden:  
  
-   **Spalte C1**. Die Spalte wird als **Int** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `integer` in R und **Int** in das Ergebnis der Ausgabe festlegen.  
  
     Es wurde keine Typenkonvertierung durchgeführt.  
  
-   **Spalte C2**. Die Spalte wird als **varchar(10)** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `factor` in R und **varchar(max)** in der Ausgabe.  
  
     Beachten Sie, wie die Ausgabe ändert. eine beliebige Zeichenfolge aus R (ein Faktor oder eine reguläre Zeichenfolge) wird als dargestellt werden **varchar(max)**, unabhängig von der Länge der Zeichenfolgen.  
  
-   **Spalte C3**.  Die Spalte wird als **Uniqueidentifier** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `character` in R und **varchar(max)** in der Ausgabe.  
  
     Beachten Sie die ausgeführte Datentypenkonvertierung. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die **Uniqueidentifier** jedoch R nicht, daher werden die IDs als Zeichenfolgen dargestellt.  
  
-   **Spalte C4**. Die Spalte enthält Werte, die vom R-Skript generiert wurden und die in den ursprünglichen Daten nicht vorhanden waren.  
 
 ## Siehe auch
 [SQL Server R Services – Features und Aufgaben](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
  
  