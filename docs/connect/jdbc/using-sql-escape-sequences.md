---
title: Verwenden von SQL-Escapesequenzen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00f9e25a-088e-4ac6-aa75-43eacace8f03
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: edf033fd91ecdd9ddd5ad33ce9a19e32f58b8bba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="using-sql-escape-sequences"></a>Verwenden von SQL-Escapesequenzen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] unterstützt die Verwendung von SQL-Escapesequenzen, wie von der JDBC-API definiert. Mithilfe von Escapesequenzen wird in einer SQL-Anweisung für den Treiber angegeben, dass der Teil der SQL-Zeichenfolge mit Escapezeichen anders behandelt werden soll. Wenn der JDBC-Treiber den Teil einer SQL-Anweisung mit Escapezeichen verarbeitet, wird dieser Teil der Zeichenfolge in SQL-Code übersetzt, den SQL Server verwenden kann.  
  
 Es gibt fünf Arten von Escapesequenzen, die für die JDBC-API erforderlich sind. Alle werden vom JDBC-Treiber unterstützt:  
  
-   LIKE-platzhalterliterale  
  
-   Funktionsbehandlung  
  
-   Datums- und Zeitliterale  
  
-   Gespeicherte Prozeduraufrufe  
  
-   Äußere joins  
  
-   LIMIT-Escapesyntax  
  
 JDBC-Treiber verwendet die folgende Escapesequenzsyntax:  
  
 `{keyword ...parameters...}`  
  
> [!NOTE]  
>  Die SQL-Escapeverarbeitung ist für den JDBC-Treiber immer aktiviert.  
  
 In den folgenden Abschnitten werden die fünf Arten von Escapesequenzen und ihre Unterstützung durch den JDBC-Treiber beschrieben.  
  
## <a name="like-wildcard-literals"></a>LIKE-Platzhalterliterale  
 Der JDBC-Treiber unterstützt die `{escape 'escape character'}` Syntax für das Verwenden von LIKE-klauselplatzhaltern als Literale. Der folgende Code gibt beispielsweise Werte für „col3“ zurück, wenn der Wert von „col2“ wirklich mit einem Unterstrich beginnt (und nicht mit dem Platzhalter).  
  
```  
ResultSet rst = stmt.executeQuery("SELECT col3 FROM test1 WHERE col2   
LIKE '\\_%' {escape '\\'}");  
```  
  
> [!NOTE]  
>  Die Escapesequenz muss sich am Ende der SQL-Anweisung befinden. Bei mehreren SQL-Anweisungen in einer Befehlszeichenfolge muss sich die Escapesequenz am Ende jeder relevanten SQL-Anweisung befinden.  
  
## <a name="function-handling"></a>Funktionsbehandlung  
 Der JDBC-Treiber unterstützt Funktionsescapesequenzen in SQL-Anweisungen mit der folgenden Syntax:  
  
```  
{fn functionName}  
```  
  
 wobei `functionName` ist eine Funktion, die vom JDBC-Treiber unterstützt. Beispiel:  
  
```  
SELECT {fn UCASE(Name)} FROM Employee  
```  
  
 In der folgenden Tabelle werden die unterschiedlichen Funktionen aufgeführt, die der JDBC-Treiber bei der Verwendung einer Funktionsescapesequenz unterstützt.  
  
|Zeichenfolgenfunktionen|Numerische Funktionen|datetime-Funktionen|Systemfunktionen|  
|----------------------|-----------------------|------------------------|----------------------|  
|ASCII<br /><br /> CHAR<br /><br /> CONCAT<br /><br /> DIFFERENCE<br /><br /> INSERT<br /><br /> LCASE<br /><br /> LEFT<br /><br /> LENGTH<br /><br /> LOCATE<br /><br /> LTRIM<br /><br /> REPEAT<br /><br /> REPLACE<br /><br /> RIGHT<br /><br /> RTRIM<br /><br /> SOUNDEX<br /><br /> SPACE<br /><br /> SUBSTRING<br /><br /> UCASE|ABS<br /><br /> ACOS<br /><br /> ASIN<br /><br /> ATAN<br /><br /> ATAN2<br /><br /> CEILING<br /><br /> COS<br /><br /> COT<br /><br /> DEGREES<br /><br /> EXP<br /><br /> FLOOR<br /><br /> LOG<br /><br /> LOG10<br /><br /> MOD<br /><br /> PI<br /><br /> POWER<br /><br /> RADIANS<br /><br /> RAND<br /><br /> ROUND<br /><br /> SIGN<br /><br /> SIN<br /><br /> SQRT<br /><br /> TAN<br /><br /> TRUNCATE|CURDATE<br /><br /> CURTIME<br /><br /> DAYNAME<br /><br /> DAYOFMONTH<br /><br /> TAGDERWOCHE<br /><br /> TAGDESJAHRES<br /><br /> EXTRACT<br /><br /> HOUR<br /><br /> MINUTE<br /><br /> MONTH<br /><br /> MONTHNAME<br /><br /> NOW<br /><br /> QUARTER<br /><br /> SECOND<br /><br /> TIMESTAMPADD<br /><br /> TIMESTAMPDIFF<br /><br /> WEEK<br /><br /> YEAR|DATABASE<br /><br /> IFNULL<br /><br /> Benutzer|  
  
> [!NOTE]  
>  Wenn Sie versuchen, eine von der Datenbank nicht unterstützte Funktion zu verwenden, tritt ein Fehler auf.  
  
## <a name="date-and-time-literals"></a>Datum und Uhrzeit-Literale  
 Die Escapesyntax für Datums-, Zeit- und Timestampliterale lautet wie folgt:  
  
```  
{literal-type 'value'}  
```  
  
 wobei `literal-type` ist eines der folgenden:  
  
|Literaltyp|Description|Wertformat|  
|------------------|-----------------|------------------|  
|d|Datum|yyyy-mm-dd|  
|t|Zeit|hh:mm:ss [1]|  
|ts|Zeitstempel|yyyy-mm-dd hh:mm:ss[.f...]|  
  
 Beispiel:  
  
```  
UPDATE Orders SET OpenDate={d '2005-01-31'}   
WHERE OrderID=1025  
```  
  
## <a name="stored-procedure-calls"></a>Aufrufe gespeicherter Prozeduren  
 Der JDBC-Treiber unterstützt die `{? = call proc_name(?,...)}` und `{call proc_name(?,...)}` Escapesyntax für Aufrufe gespeicherter Prozeduren, abhängig davon, ob ein Rückgabeparameter verarbeitet werden muss.  
  
 Bei einer Prozedur handelt es sich um ein in der Datenbank gespeichertes, ausführbares Objekt. In der Regel handelt es sich dabei um eine oder mehrere vorkompilierte SQL-Anweisungen. Die Escapesequenzsyntax zum Aufrufen einer gespeicherten Prozedur lautet wie folgt:  
  
```  
{[?=]call procedure-name[([parameter][,[parameter]]...)]}  
```  
  
 wobei `procedure-name` gibt den Namen einer gespeicherten Prozedur und `parameter` Parameter einer gespeicherten Prozedur angibt.  
  
 Weitere Informationen zum Verwenden der `call` Escapesequenz mit gespeicherten Prozeduren, finden Sie unter [Using-Anweisungen mit gespeicherten Prozeduren](../../connect/jdbc/using-statements-with-stored-procedures.md).  
  
## <a name="outer-joins"></a>Äußere Joins  
 Der JDBC-Treiber unterstützt die linke, rechte und vollständige äußere SQL92-Joinsyntax. Die Escapesequenz für äußere Joins lautet wie folgt:  
  
```  
{oj outer-join}  
```  
  
 Dabei lautet der äußere Join:  
  
```  
table-reference {LEFT | RIGHT | FULL} OUTER JOIN    
{table-reference | outer-join} ON search-condition  
```  
  
 wobei `table-reference` ist ein Tabellenname und `search-condition` ist die Joinbedingung, die für die Tabellen verwendet werden sollen.  
  
 Beispiel:  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status   
   FROM {oj Customers LEFT OUTER JOIN   
      Orders ON Customers.CustID=Orders.CustID}   
   WHERE Orders.Status='OPEN'  
```  
  
 Die folgenden Escapesequenzen für äußere Joins werden vom JDBC-Treiber unterstützt:  
  
-   Linke äußere Verknüpfungen  
  
-   Rechte äußere Joins  
  
-   Vollständige äußere Joins  
  
-   Geschachtelte äußere Joins  
  
## <a name="limit-escape-syntax"></a>Limit-Escapesyntax  
  
> [!NOTE]  
>  Die LIMIT-Escapesyntax wird nur von Microsoft JDBC Driver 4.2 (oder höher) für SQL Server bei unterstützt JDBC 4.1 oder höher verwenden.  
  
 Die Escapesyntax für LIMIT ist wie folgt:  
  
```  
LIMIT <rows> [OFFSET <row offset>]  
```  
  
 Die Escapesyntax besteht aus zwei Teilen: \< *Zeilen*> ist obligatorisch und gibt die Anzahl der zurückzugebenden Zeilen. OFFSET und \< *Zeilenoffset*> sind optional, und geben Sie die Anzahl der zu überspringenden Zeilen vor Zeilen. Der JDBC-Treiber unterstützt nur den obligatorischen Teil, indem er die Abfrageklausel von LIMIT in TOP umwandelt. SQL Server unterstützt die LIMIT-Klausel nicht. **Der JDBC-Treiber unterstützt nicht das optionale \<Zeilenoffset > und der Treiber löst eine Ausnahme aus, wenn er dient**.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Anweisungen mit dem JDBC-Treiber](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
