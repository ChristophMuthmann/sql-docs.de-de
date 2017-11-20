---
title: "Wählen Sie-SQL-Befehl | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3604d435a8a95e3690d335e25e1a94b3bbb0b1a1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="select---sql-command"></a>Wählen Sie-SQL-Befehl
Ruft Daten aus einer oder mehreren Tabellen ab.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt die systemeigene Visual FoxPro-Sprachsyntax für diesen Befehl an. Treiberspezifische Informationen finden Sie unter **Treiber "Hinweise"**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
…]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>Argumente  
  
> [!NOTE]  
>  Ein *Unterabfrage*, in der folgenden Argumente bezeichnet werden, wird eine SELECT-Anweisung in eine SELECT-Anweisung und muss in Klammern eingeschlossen werden. Sie können bis zu zwei Unterabfragen auf derselben Ebene haben (nicht geschachtelt) in der WHERE-Klausel. (Siehe dieser Abschnitt der Argumente.) Unterabfragen können mehrere Joinbedingungen enthalten.  
  
 [Alle &#124; DISTINCT] [*Alias*.] *Select_Item* [AS *Column_Name*] [, [*Alias*.] *Select_Item* [AS *Column_Name*]...]  
 Die SELECT-Klausel gibt an, die Felder, Konstanten und Ausdrücke, die in den Abfrageergebnissen angezeigt werden.  
  
 Standardmäßig alle zeigt alle Zeilen in den Abfrageergebnissen angezeigt.  
  
 DISTINCT schließt Duplikate von Zeilen aus den Abfrageergebnissen.  
  
> [!NOTE]  
>  Sie können nur einmal DISTINCT pro SELECT-Klausel verwenden.  
  
 *Alias*. qualifiziert die entsprechenden Elementnamen. Jedes Element, das Sie angeben, mit *Select_Item* generiert eine Spalte der Ergebnisse der Abfrage. Wenn zwei oder mehr Elemente den gleichen Namen enthalten Sie sind Tabellenalias und einen Punkt vor der Elementname, um zu verhindern, dass Spalten dupliziert wird.  
  
 *Select_Item* gibt ein Element, in die Abfrageergebnisse eingeschlossen werden sollen. Ein Element kann einer der folgenden sein:  
  
-   Der Name eines Felds aus einer Tabelle in der FROM-Klausel.  
  
-   Eine Konstante, die angeben, dass denselben Konstante Wert in jeder Zeile der Abfrageergebnisse angezeigt.  
  
-   Ein Ausdruck, der den Namen einer benutzerdefinierten Funktion sein kann.  
  
 **Benutzerdefinierte Funktionen mit SELECT**  
  
 Obwohl durch die Verwendung von benutzerdefinierten Funktionen in der SELECT-Klausel hat offensichtliche Vorteile, sollten Sie auch die folgenden Einschränkungen:  
  
-   Die Geschwindigkeit von Operationen mit SELECT möglicherweise durch die Geschwindigkeit eingeschränkt werden, an dem eine solche benutzerdefinierte Funktionen ausgeführt werden. Hohes Volumen Manipulationen im Zusammenhang mit benutzerdefinierten Funktionen können besser erfüllt werden, mithilfe der API und benutzerdefinierte Funktionen, die in C oder Assemblysprache geschrieben.  
  
-   Die einzig zuverlässige Möglichkeit zum Übergeben von Werten für benutzerdefinierte Funktionen, die aus SELECT aufgerufen wurde, ist durch die Argumentliste enthalten, die an die Funktion übergeben wird, wenn er aufgerufen wird.  
  
-   Auch wenn Sie experimentieren und ermitteln eine eigentlich unzulässige Manipulation, die in einer bestimmten Version eines FoxPro ordnungsgemäß funktioniert, besteht keine Garantie, die sie in höheren Versionen können auch weiterhin.  
  
 Abgesehen von diesen Einschränkungen werden von benutzerdefinierten Funktionen in der SELECT-Klausel zulässig. Beachten Sie jedoch, dass das Verwenden von SELECT die Leistung beeinträchtigen kann.  
  
 Die folgenden Feld Funktionen stehen für die Verwendung mit einer select-Element, das ein Feld oder ein Ausdruck, der ein Feld ist:  
  
-   AVG (*Select_Item*) – eine Spalte mit numerischen Daten ermittelt.  
  
-   COUNT (*Select_Item*) – zählt die Anzahl der Elemente in einer Spalte auswählen. Count(*) zählt die Anzahl der Zeilen in der Ausgabe einer Abfrage.  
  
-   MIN (*Select_Item*) – ermittelt den kleinsten Wert der *Select_Item* in einer Spalte.  
  
-   MAX (*Select_Item*) – ermittelt den größten Wert der *Select_Item* in einer Spalte.  
  
-   SUM (*Select_Item*) – eine Spalte mit numerischen Daten summiert.  
  
 Feld-Funktionen können nicht geschachtelt werden.  
  
 AS *Column_Name*  
 Gibt den Spaltenüberschrift, um eine Spalte in der Ausgabe einer Abfrage an. Dies ist hilfreich, wenn *Select_Item* ist ein Ausdruck oder ein Feld enthält-Funktion, und Sie auf der Spalte einen aussagekräftigen Namen geben möchten. *Column_name* kann kein Ausdruck sein, jedoch können keine Zeichen enthalten (z. B. Leerzeichen), die im Feldnamen für die Tabelle nicht zulässig sind.  
  
 AUS [*DatabaseName*!] *Tabelle* [*Local_Alias*] [, [*DatabaseName*!] *Tabelle* [*Local_Alias*]...]  
 Listet die Tabellen, die Daten enthalten, die die Abfrage abruft. Wenn keine Tabelle geöffnet ist, zeigt Visual FoxPro der **öffnen** Dialogfeld, sodass Sie den Dateispeicherort angeben können. Nachdem er geöffnet wurde, bleibt die Tabelle geöffnet, nachdem die Abfrage abgeschlossen ist.  
  
 *DatabaseName*! Gibt den Namen einer Datenbank als dem mit der Datenquelle angegeben. Sie müssen den Namen der Datenbank enthalten, die die Tabelle enthält, wenn die Datenbank nicht mit der Datenquelle angegeben wird. Schließen Sie das Ausrufezeichen (!)-Trennzeichen an, nach dem Datenbanknamen und vor dem Tabellennamen.  
  
 *Local_Alias* gibt einen temporären Namen für die Tabelle mit dem Namen im *Tabelle*. Wenn Sie einen lokalen Alias angeben, müssen Sie den lokalen Alias statt des Tabellennamens in der SELECT-Anweisung verwenden. Der lokale Alias wirkt sich nicht auf die Visual FoxPro-Umgebung aus.  
  
 WOBEI *JoinCondition* [AND *JoinCondition* ...]    [Und &#124; ODER *FilterCondition* [AND &#124; ODER *FilterCondition* ...]]  
 Weist Visual FoxPro und nur bestimmte Datensätze in den Abfrageergebnissen anzuzeigen. Wenn zum Abrufen von Daten aus mehreren Tabellen erforderlich ist.  
  
 *JoinCondition* gibt Felder, die die Tabellen in der FROM-Klausel verknüpft sind. Wenn Sie mehr als eine Tabelle in einer Abfrage einschließen, sollten Sie nach dem ersten eine Join-Bedingung für jede Tabelle angeben.  
  
> [!IMPORTANT]  
>  Betrachten Sie die folgende Informationen ein, bei der Erstellung von Join-Bedingungen:  
  
-   Wenn Sie zwei Tabellen in einer Abfrage enthalten, und Sie eine Joinbedingung nicht geben, wird jeder Datensatz in der ersten Tabelle mit jeder Datensatz in der zweiten Tabelle verknüpft, solange der filterbedingungen erfüllt sind. Eine solche Abfrage kann längere Ergebnislisten zu erzeugen.  
  
-   Seien Sie vorsichtig beim Verknüpfen von Tabellen mit leeren Feldern, da Visual FoxPro leere Feldern entspricht. Angenommen, Sie auf die Kunden zu verknüpfen. ZIP und Rechnung. ZIP, und wenn Kunden 100 leere Postleitzahlen enthält und Rechnung 400 leere Postleitzahlen, enthält der Abfrageausgabe 40.000 zusätzliche Datensätze infolge der leeren Felder. Verwenden der **(leer)** Funktion leere Datensätze aus der Abfrageausgabe entfernen.  
  
-   Sie müssen den AND-Operator verwenden, die Verbindung mehrere Joinbedingungen. Jede Join-Bedingung weist folgende Form:  
  
     *FieldName1 Vergleich FieldName2*  
  
     *FieldName1* ist der Name eines Felds aus einer Tabelle *FieldName2* ist der Name eines Felds aus einer anderen Tabelle und *Vergleich* ist einer der Operatoren in der folgenden Tabelle beschrieben.  
  
|Operator|Vergleich|  
|--------------|----------------|  
|=|Gleich|  
|==|Genau gleich.|  
|LIKE|SQL-ORIENTIERTE|  
|<>, !=, #|Ist ungleich|  
|>|Mehr als|  
|>=|Größer als oder gleich|  
|<|Kleiner als|  
|<=|Kleiner als oder gleich|  
  
 Bei Verwendung der =-Operator mit Zeichenfolgen, sie fungiert jedoch unterschiedlich, abhängig von der Einstellung von SET ANSI. Wenn SET ANSI auf OFF festgelegt ist, behandelt der Visual FoxPro Zeichenfolgenvergleiche in einer Weise Xbase Benutzern vertraut. Wenn SET ANSI auf ON festgelegt ist, folgt Visual FoxPro ANSI-Standards für Zeichenfolgenvergleiche an. Finden Sie unter [SET ANSI](../../odbc/microsoft/set-ansi-command.md) und [SET EXACT](../../odbc/microsoft/set-exact-command.md) für Weitere Informationen darüber, wie der Visual FoxPro Zeichenfolgenvergleiche durchführt.  
  
 *FilterCondition* gibt die Kriterien, die Datensätze erfüllen muss, damit Sie in die Abfrageergebnisse eingeschlossen werden. Sie können so viele Bedingungen in einer Abfrage filtern, wie Sie möchten das Verbinden mit den AND-Operator, einschließen oder OR-Operator. Sie können auch den NOT-Operator verwenden, um den Wert eines logischen Ausdrucks umzukehren, oder Sie können **(leer)** für ein leeres Feld zu überprüfen. *FilterCondition* kann wie die Formulare in den folgenden Beispielen:  
  
 **Beispiel 1** *FieldName1 Vergleich FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Beispiel 2** *FieldName Vergleichsausdruck*  
  
 `payments.amount >= 1000`  
  
 **Beispiel 3** *FieldName Vergleich* alle (*Unterabfrage*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Wenn die filterbedingung alle enthält, muss das Feld für alle Werte, die von der Unterabfrage generiert werden, bevor der Datensatz in die Ergebnisse der Abfrage enthalten ist der Vergleich-Bedingung erfüllen.  
  
 **Beispiel 4** *FieldName Vergleich* alle &#124; Einige (*Unterabfrage*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Wenn die filterbedingung alle oder einige enthält, muss das Feld die Bedingung Vergleich für mindestens einen der Werte, die von der Unterabfrage generiert erfüllen.  
  
 Im folgenden Beispiel wird überprüft, ob die Werte in das Feld innerhalb eines bestimmten Bereichs von Werten sind:  
  
 **Beispiel 5** *FieldName* [NOT] zwischen *Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 Im folgenden Beispiel wird überprüft, ob mindestens eine Zeile in der Unterabfrage Kriterien erfüllt. Wenn die filterbedingung EXISTS enthält, wertet die filterbedingung auf "true" (. T.), wenn die Unterabfrage auf die leere Menge ausgewertet wird.  
  
 **Beispiel 6** [NOT] vorhanden ist (*Unterabfrage*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Beispiel 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Wenn die filterbedingung IN enthält, muss das Feld enthalten einen der Werte, bevor der Datensatz in die Ergebnisse der Abfrage enthalten ist.  
  
 **Beispiel 8** *FieldName* [NOT] IN (*Unterabfrage*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 Hier muss das Feld enthalten die Werte, die von der Unterabfrage zurückgegeben wird, bevor der Datensatz in die Ergebnisse der Abfrage enthalten ist.  
  
 **Beispiel 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Die filterbedingung für jedes Feld, das entspricht sucht *cExpression*. Sie können das Prozentzeichen (%) und Unterstrich (_)-Platzhalterzeichen als Teil des *cExpression*. Der Unterstrich stellt ein unbekanntes einzelnes Zeichen in der Zeichenfolge dar.  
  
 GROUP BY *GroupColumn* [, *GroupColumn* ...]  
 Gruppen von Zeilen in der Abfrage, die basierend auf Werten in einer oder mehreren Spalten. *GroupColumn* kann eines der folgenden sein:  
  
-   Der Name eines Felds normale Tabelle.  
  
-   Ein Feld, das eine SQL-Feld-Funktion enthält.  
  
-   Ein numerischer Ausdruck, der die Position der Spalte in der Ergebnistabelle angibt. (Die am weitesten links stehende Spaltennummer ist 1.)  
  
 MIT *FilterCondition*  
 Gibt eine filterbedingung, die Gruppen erfüllen muss, damit Sie in die Abfrageergebnisse eingeschlossen werden. HAVING mit GROUP BY verwendet werden soll, und können so viele Bedingungen filtern, wie durch den AND-Operator verbunden werden sollen, einschließen oder OR-Operator. Sie können auch nicht, um den Wert eines logischen Ausdrucks umzukehren.  
  
 *FilterCondition* eine Unterabfrage kann nicht enthalten.  
  
 Eine HAVING-Klausel ohne eine GROUP BY-Klausel verhält sich wie eine WHERE-Klausel. Sie können lokale Aliase und Feld-Funktionen in der HAVING-Klausel verwenden. Verwenden Sie eine WHERE-Klausel für eine bessere Leistung, wenn die HAVING-Klausel keine Feld Funktionen enthält.  
  
 [[ALL] UNION *SELECTCommand*]  
 Kombiniert die Endergebnisse der eine SELECT-Anweisung mit die Endergebnisse von einer anderen SELECT. Standardmäßig werden UNION das kombinierte Ergebnis überprüft und entfernt mehrfach auftretende Zeilen. Verwenden Sie Klammern, um mehrere UNION-Klauseln zu kombinieren.  
  
 Alle wird verhindert, dass UNION Eliminieren von doppelten Zeilen aus den kombinierten Ergebnissen.  
  
 UNION-Klauseln entsprechen diesen Regeln:  
  
-   UNION können keine Unterabfragen kombinieren.  
  
-   Beide SELECT-Befehlen müssen die gleiche Anzahl von Spalten in ihre Ausgabe einer Abfrage verfügen.  
  
-   Jede Spalte in den Abfrageergebnissen eine SELECT muss den gleichen Datentyp und die Breite der entsprechenden Spalte in der anderen SELECT verfügen.  
  
-   Nur die letzte SELECT-Anweisung kann eine ORDER BY-Klausel haben Ausgabespalten durch Anzahl verweisen muss. Wenn eine ORDER BY-Klausel enthalten ist, wirkt sich dieser auf das vollständige Ergebnis.  
  
 Die UNION-Klausel können auch um ein äußeren Joins zu simulieren.  
  
 Wenn Sie zwei Tabellen in einer Abfrage verbinden, sind nur Datensätze mit übereinstimmenden Werten in den Hinzufügen von Feldern in der Ausgabe enthalten. Wenn ein Datensatz in der übergeordneten Tabelle nicht über einen entsprechenden Datensatz in der untergeordneten Tabelle verfügt, wird der Datensatz in der übergeordneten Tabelle nicht in der Ausgabe enthalten. Ein äußerer Join können Sie alle Datensätze in der übergeordneten Tabelle in der Ausgabe zusammen mit den übereinstimmenden Datensätzen in der untergeordneten Tabelle einschließen. Zum Erstellen eines äußeren Joins in der Visual FoxPro müssen Sie einen geschachtelte SELECT-Befehl aus, wie im folgenden Beispiel gezeigt verwenden:  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  Stellen Sie sicher, dass Sie ein Leerzeichen einfügen kann, die jedem Semikolon unmittelbar vorausgeht. Andernfalls erhalten Sie einen Fehler.  
  
 Der Abschnitt des Befehls vor die UNION-Klausel Datensätze aus beiden Tabellen auswählt, die übereinstimmende Werte enthalten. Die Customer-Unternehmen, die keine zugehörige Rechnungen sind nicht eingeschlossen. Der Abschnitt des Befehls nach der UNION-Klausel wählt die Datensätze in der Customer-Tabelle, die keine übereinstimmenden Datensätzen in der Orders-Tabelle.  
  
 Zu den zweiten Abschnitt des Befehls ist Folgendes zu beachten:  
  
-   Die SELECT-Anweisung innerhalb der Klammern wird zuerst verarbeitet. Diese Anweisung erstellt eine Auswahl von Zahlen für alle Kunden in der Orders-Tabelle.  
  
-   Die WHERE-Klausel sucht alle Kundennummern in der Customer-Tabelle, die nicht in der Orders-Tabelle enthalten sind. Da der erste Abschnitt des Befehls alle Unternehmen, die in der Tabelle Orders eine Kundennummer hatten bereitgestellt, werden alle Unternehmen in der Customer-Tabelle nun in den Abfrageergebnissen enthalten.  
  
-   Da die Strukturen in einer UNION enthaltenen Tabellen identisch sein müssen, müssen Sie zwei Platzhalter vorhanden sind, in der zweiten SELECT-Anweisung zur Darstellung *Customer* und *orders.emp_id* aus der ersten SELECT-Anweisung -Anweisung.  
  
    > [!NOTE]  
    >  Die Platzhalter muss denselben Typ wie die Felder, die sie darstellen. Wenn das Feld einen Date-Datentyp ist, muss der Platzhalter {/ /}. Wenn das Feld ein Zeichenfeld ist, muss der Platzhalter die leere Zeichenfolge ("").  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC]...]  
 Sortiert die Ergebnisse der Abfrage anhand der Daten in einer oder mehreren Spalten an. Jede *Order_Item* muss auf eine Spalte in die Ergebnisse der Abfrage entsprechen und kann einen der folgenden:  
  
-   Ein Feld in einer FROM-Tabelle, die auch eine select-Element in der wichtigsten SELECT-Klausel (nicht in einer Unterabfrage) ist.  
  
-   Ein numerischer Ausdruck, der die Position der Spalte in der Ergebnistabelle angibt. (Die am weitesten links stehende Spalte die Zahl ist 1.)  
  
 ASC gibt eine aufsteigende Reihenfolge für Abfrageergebnisse, gemäß der Reihenfolge Element bzw. die Elemente, und ist die Standardeinstellung für die ORDER BY.  
  
 "DESC" gibt eine absteigende Sortierreihenfolge für Abfrageergebnisse an.  
  
 Abfrageergebnisse werden nicht sortiert angezeigt, wenn Sie eine Bestellung nicht mit ORDER BY angeben.  
  
## <a name="remarks"></a>Hinweise  
 Wählen Sie ist ein SQL‑Befehl, der in der Visual FoxPro wie andere Visual FoxPro-Befehl erstellt wird. Bei Verwendung von auswählen, um eine Abfrage darstellen, Visual FoxPro, interpretiert die Abfrage, und die angegebenen Daten aus Tabellen abgerufen. Sie können eine SELECT-Abfrage in das Eingabeaufforderungsfenster oder ein Visual FoxPro-Programm (mit einem beliebigen anderen Visual FoxPro--Befehl) erstellen.  
  
> [!NOTE]  
>  Wählen Sie berücksichtigt nicht die aktuellen filterbedingung angegeben mit FILTER festlegen.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Ihre Anwendung die ODBC-SQL-Anweisung SELECT an die Datenquelle gesendet wird, konvertiert der Visual FoxPro-ODBC-Treiber den Befehl in der Visual FoxPro-wählen-Befehl ohne Übersetzung, wenn der Befehl eine ODBC-Escapesequenz enthält. In einer ODBC-Escapesequenz eingeschlossenen Elemente werden in der Visual FoxPro-Syntax konvertiert. Weitere Informationen zur Verwendung von ODBC-Escapesequenzen, finden Sie unter [Zeit- und Datumsfunktionen](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) und klicken Sie in der *Microsoft ODBC Programmer's Reference*, finden Sie unter [in ODBC-Escapesequenzen](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) .  
  
## <a name="see-also"></a>Siehe auch  
 [ERSTELLEN DER TABELLE - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [LEGEN SIE GENAUE](../../odbc/microsoft/set-exact-command.md)

