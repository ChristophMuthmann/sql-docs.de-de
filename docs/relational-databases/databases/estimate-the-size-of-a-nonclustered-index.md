---
title: "Schätzen der Größe eines nicht gruppierten Index | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: SQL
ms.prod_service: database-engine, sql-database
ms.component: indexes
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: c183b0e4-ef4c-4bfc-8575-5ac219c25b0a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 03eaa651f6184c9dc1dc53913e1662798664b983
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>Schätzen der Größe eines nicht gruppierten Index

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Befolgen Sie diese Schritte, um abzuschätzen, wie viel Speicherplatz zum Speichern eines nicht gruppierten Index erforderlich ist.  
  
1.  Berechnen Sie die Variablen zur Verwendung in Schritt 2 und 3.  
  
2.  Berechnen Sie den Speicherplatz, der zum Speichern der Indexinformationen in der Blattebene des nicht gruppierten Index verwendet wird.  
  
3.  Berechnen Sie den Speicherplatz, der zum Speichern der Indexinformationen in den inneren Knotenebenen des nicht gruppierten Index verwendet wird.  
  
4.  Addieren Sie die berechneten Werte.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>Schritt 1: Berechnen der zu verwendenden Variablen in Schritt 2 und 3  
 Mit den folgenden Schritten können Sie die Variablen berechnen, mit denen die Größe des Speicherplatzes geschätzt wird, die zum Speichern der oberen Ebenen des Indexes erforderlich ist.  
  
1.  Geben Sie die Anzahl der Zeilen an, die die Tabelle enthalten wird:  
  
     ***Num_Rows***  = Anzahl der Zeilen in der Tabelle  
  
2.  Geben Sie die Anzahl der Spalten mit fester und mit variabler Länge im Indexschlüssel an, und berechnen Sie den Speicherplatz, der für deren Speicherung erforderlich ist:  
  
     Die Schlüsselspalten eines Indexes können Spalten fester und variabler Länge enthalten. Um die Größe der Indexzeilen auf der inneren Ebene zu schätzen, müssen Sie den Speicherplatz berechnen, der von jeder dieser Spaltengruppen innerhalb der Indexzeile belegt wird. Die Größe einer Spalte hängt von der Angabe für Datentyp und -länge ab.  
  
     ***Num_Key_Cols***  = Gesamtanzahl der Schlüsselspalten (fester und variabler Länge)  
  
     ***Fixed_Key_Size***  = Gesamtzahl der Bytes in allen Schlüsselspalten fester Länge  
  
     ***Num_Variable_Key_Cols***  = Anzahl der Schlüsselspalten variabler Länge  
  
     ***Max_Var_Key_Size***  = Maximale Bytegröße aller Schlüsselspalten variabler Länge  
  
3.  Berücksichtigen Sie auch den Datenzeilenlokator, der erforderlich ist, wenn der Index nicht eindeutig ist:  
  
     Wenn der nicht gruppierte Index nicht eindeutig ist, wird der Datenzeilenlokator mit dem Schlüssel des nicht gruppierten Indexes kombiniert, um einen eindeutigen Schlüsselwert für jede Zeile zu erstellen.  
  
     Wenn sich der nicht gruppierte Index über einem Heap befindet, ist der Datenzeilenlokator die Heap-RID. Die Größe beträgt dann 8 Byte.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 8  
  
     Wenn sich der nicht gruppierte Index über einem gruppierten Index befindet, dann ist der Datenzeilenlokator der Gruppierungsschlüssel. Bei den Spalten, die mit dem nicht gruppierten Index kombiniert werden müssen, handelt es sich um die im Gruppierungsschlüssel enthaltenen Spalten, die noch nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + Anzahl der Gruppierungsschlüsselspalten, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind (+ 1, wenn der gruppierte Index nicht eindeutig ist)  
  
     ***Fixed_Key_Size***  = ***Fixed_Key_Size*** + Gesamtanzahl der Bytes in allen Gruppierungsschlüsselspalten fester Länge, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + Anzahl der Gruppierungsschlüsselspalten variabler Länge, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind (+ 1, wenn der gruppierte Index nicht eindeutig ist)  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + maximale Anzahl der Bytes in den Gruppierungsschlüsselspalten variabler Länge, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind (+ 4, wenn der gruppierte Index nicht eindeutig ist)  
  
4.  Ein Teil der Zeile, der als NULL-Bitmuster bezeichnet wird, kann für das Verwalten der NULL-Zulässigkeit der Spalte reserviert sein. Berechnen Sie dessen Größe:  
  
     Wenn der Indexschlüssel Spalten enthält, die NULL-Werte zulassen (einschließlich erforderlicher Gruppierungsschlüsselspalten wie in Schritt 1.3 beschrieben), ist ein Teil der Indexzeile für das NULL-Bitmuster reserviert.  
  
     ***Index_Null_Bitmap***  = 2 + ((Anzahl der Spalten in der Indexzeile + 7) / 8)  
  
     Nur der ganzzahlige Teil des vorherigen Ausdrucks darf verwendet werden. Der Rest wird verworfen.  
  
     Wenn keine Schlüsselspalten vorhanden sind, die NULL-Werte zulassen, legen Sie ***Index_Null_Bitmap*** auf 0 fest.  
  
5.  Berechnen Sie die Größe der Daten variabler Länge:  
  
     Wenn der Indexschlüssel Spalten variabler Länge enthält (einschließlich erforderlicher Schlüsselspalten des gruppierten Indexes), müssen Sie ermitteln, wie viel Speicherplatz zum Speichern der Spalten innerhalb der Indexzeile verwendet wird:  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     Die zu ***Max_Var_Key_Size*** hinzugefügten Bytes dienen der Nachverfolgung jeder einzelnen Variablenspalte. Bei dieser Formel wird angenommen, dass alle Spalten variabler Länge zu 100 Prozent gefüllt sind. Wenn sich abzeichnet, dass ein niedrigerer Prozentsatz des Speicherplatzes für Spalten variabler Länge verwendet wird, können Sie den ***Max_Var_Key_Size*** -Wert mithilfe dieses Prozentsatzes anpassen, um einen genaueren Schätzwert für die Gesamtgröße der Tabelle zu erhalten.  
  
     Wenn keine Spalten variabler Länge vorhanden sind, legen Sie ***Variable_Key_Size*** auf 0 fest.  
  
6.  Berechnen Sie die Länge der Indexzeile:  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (für Zeilenüberschriftenaufwand einer Indexzeile) + 6 (für ID-Zeiger der untergeordneten Seite)  
  
7.  Berechnen Sie die Anzahl der Indexzeilen pro Seite (8096 freie Byte pro Seite):  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     Da sich eine Indexzeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Indexzeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>Schritt 2: Berechnen des Speicherplatzes, der zum Speichern der Indexinformationen in der Blattebene verwendet wird  
 Mit den folgenden Schritten können Sie den Umfang des Speicherplatzes schätzen, der zum Speichern der Blattebene des Indexes erforderlich ist. Sie benötigen die in Schritt 1 aufgezeichneten Werte, um diesen Schritt durchführen zu können.  
  
1.  Geben Sie die Anzahl der Spalten mit fester und mit variabler Länge auf Blattebene an, und berechnen Sie den Speicherplatz, der für deren Speicherung erforderlich ist:  
  
    > [!NOTE]  
    >  Sie können einen nicht gruppierten Index erweitern, indem Nichtschlüsselspalten zusätzlich zu Indexschlüsselspalten eingeschlossen werden. Diese zusätzlichen Spalten werden auf der Blattebene des nicht gruppierten Indexes gespeichert. Weitere Informationen finden Sie unter [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
    > [!NOTE]  
    >  Sie können **varchar**-, **nvarchar**-, **varbinary**- oder **sql_variant** -Spalten kombinieren, mit dem Ergebnis, dass die definierte Tabellengesamtbreite größer als 8060 Bytes ist. Die Länge jeder einzelnen Spalte unterliegt auch weiterhin der Beschränkung von 8.000 Byte für eine **varchar**-, **varbinary**- oder **sql_variant** -Spalte und von 4.000 Byte für **nvarchar** -Spalten. Die kombinierte Breite kann jedoch den Grenzwert von 8.060 Byte in einer Tabelle überschreiten. Dies gilt auch für die Zeilen auf Blattebene eines nicht gruppierten Indexes, die eingeschlossene Spalten enthalten.  
  
     Wenn der nicht gruppierte Index keine eingeschlossenen Spalten besitzt, verwenden Sie die Werte aus Schritt 1 einschließlich aller Änderungen, die ggf. in Schritt 1.3 vorgenommen wurden:  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols***  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size***  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols***  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size***  
  
     Wenn der nicht gruppierte Index keine eingeschlossenen Spalten besitzt, fügen Sie die entsprechenden Werte den Werten aus Schritt 1 einschließlich allen Änderungen, die ggf. in Schritt 1.3 vorgenommen wurden, hinzu. Die Größe einer Spalte hängt von der Angabe für Datentyp und -länge ab. Weitere Informationen finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols*** + Anzahl der enthaltenen Spalten  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size*** + Gesamtzahl der Bytes der enthaltenen Schlüsselspalten fester Länge  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols*** + Anzahl der enthaltenen Spalten variabler Länge  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size*** + Maximale Bytegröße der enthaltenen Spalten variabler Länge  
  
2.  Konto für den Datenzeilenlokator:  
  
     Wenn der nicht gruppierte Index nicht eindeutig ist, wurde der Aufwand für den Datenzeilenlokator bereits in Schritt 1.3 berücksichtigt. In diesem Fall sind keine zusätzlichen Änderungen erforderlich. Fahren Sie mit dem nächsten Schritt fort.  
  
     Wenn der nicht gruppierte Index eindeutig ist, muss der Datenzeilenlokator in allen Zeilen auf der Blattebene berücksichtigt werden.  
  
     Wenn sich der nicht gruppierte Index über einem Heap befindet, ist der Datenzeilenlokator die Heap-RID (Größe 8 Byte).  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 1  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 1  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 8  
  
     Wenn sich der nicht gruppierte Index über einem gruppierten Index befindet, dann ist der Datenzeilenlokator der Gruppierungsschlüssel. Bei den Spalten, die mit dem nicht gruppierten Index kombiniert werden müssen, handelt es sich um die im Gruppierungsschlüssel enthaltenen Spalten, die noch nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + Anzahl der Gruppierungsschlüsselspalten, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind (+ 1, wenn der gruppierte Index nicht eindeutig ist)  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Leaf_Size*** + Anzahl der Bytes in allen Gruppierungsschlüsselspalten fester Länge, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + Anzahl der Gruppierungsschlüsselspalten variabler Länge, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind (+ 1, wenn der gruppierte Index nicht eindeutig ist)  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + Anzahl der Bytes in den Gruppierungsschlüsselspalten variabler Länge, die nicht in der Menge der nicht gruppierten Indexschlüsselspalten vorhanden sind (+ 4, wenn der gruppierte Index nicht eindeutig ist)  
  
3.  Berechnen der Größe des NULL-Bitmusters:  
  
     ***Leaf_Null_Bitmap***  = 2 + ((***Num_Leaf_Cols*** + 7) / 8)  
  
     Nur der ganzzahlige Teil des vorherigen Ausdrucks darf verwendet werden. Der Rest wird verworfen.  
  
4.  Berechnen Sie die Größe der Daten variabler Länge:  
  
     Wenn der Indexschlüssel Spalten variabler Länge enthält (einschließlich erforderlicher Gruppierungsschlüsselspalten wie zuvor in Schritt 2.2 beschrieben), müssen Sie ermitteln, wie viel Speicherplatz zum Speichern der Spalten innerhalb der Indexzeile verwendet wird:  
  
     ***Variable_Leaf_Size***  = 2 + (***Num_Variable_Leaf_Cols*** x 2) + ***Max_Var_Leaf_Size***  
  
     Die zu ***Max_Var_Key_Size*** hinzugefügten Bytes dienen der Nachverfolgung jeder einzelnen Variablenspalte. Bei dieser Formel wird angenommen, dass alle Spalten variabler Länge zu 100 Prozent gefüllt sind. Wenn sich abzeichnet, dass ein niedrigerer Prozentsatz des Speicherplatzes für Spalten variabler Länge verwendet wird, können Sie den ***Max_Var_Leaf_Size*** -Wert mithilfe dieses Prozentsatzes anpassen, um einen genaueren Schätzwert für die Gesamtgröße der Tabelle zu erhalten.  
  
     Wenn keine Spalten variabler Länge vorhanden sind, legen Sie ***Variable_Leaf_Size*** auf 0 fest.  
  
5.  Berechnen Sie die Länge der Indexzeile:  
  
     ***Leaf_Row_Size***  = ***Fixed_Leaf_Size*** + ***Variable_Leaf_Size*** + ***Leaf_Null_Bitmap*** + 1 (für Zeilenüberschriftenaufwand einer Indexzeile)  
  
6.  Berechnen Sie die Anzahl der Indexzeilen pro Seite (8096 freie Byte pro Seite):  
  
     ***Leaf_Rows_Per_Page***  = 8096 / (***Leaf_Row_Size*** + 2)  
  
     Da sich eine Indexzeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Indexzeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
7.  Berechnen Sie die Anzahl der reservierten freien Zeilen pro Seite anhand des angegebenen [Füllfaktors](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) :  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Leaf_Row_Size*** + 2)  
  
     Bei dem in der Berechnung verwendeten Füllfaktor handelt es sich nicht um einen Prozentwert, sondern um einen ganzzahligen Wert. Da sich eine Zeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Zeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Mit ansteigendem Füllfaktor werden mehr Daten auf jeder Seite gespeichert, und die Anzahl der Seiten nimmt ab. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
8.  Berechnen Sie die Anzahl der Seiten, die zum Speichern aller Zeilen benötigt werden:  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Leaf_Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     Die geschätzte Seitenanzahl muss auf die nächste ganze Seite aufgerundet werden.  
  
9. Berechnen Sie die Größe des Indexes (insgesamt 8.192 Byte pro Seite):  
  
     ***Leaf_Space_Used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>Schritt 3: Berechnen des Speicherplatzes, der zum Speichern der Indexinformationen in den inneren Knotenebenen verwendet wird  
 Befolgen Sie diese Schritte, um abzuschätzen, wie viel Speicherplatz zum Speichern der Zwischen- und Stammebenen des Indexes erforderlich ist. Sie benötigen die in Schritt 2 und 3 errechneten Werte, um diesen Schritt durchführen zu können.  
  
1.  Berechnen Sie die Anzahl der inneren Knotenebenen im Index:  
  
     ***Non-leaf Levels***  = 1 + log( Index_Rows_Per_Page) (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     Runden Sie diese Zahl auf die nächste ganze Zahl auf. Dieser Wert schließt die Blattebene des nicht gruppierten Index nicht mit ein.  
  
2.  Berechnen Sie die Anzahl der inneren Knotenseiten im Index:  
  
     ***Num_Index_Pages***  = ∑Level (***Num_Leaf_Pages/Index_Rows_Per_Page***^Level)where 1 <= Level <= ***Levels***  
  
     Runden Sie jeden Summanden auf die nächste ganze Zahl auf. Stellen Sie sich als einfaches Beispiel einen Index vor, bei dem ***Num_Leaf_Pages*** = 1000 und ***Index_Rows_Per_Page*** = 25. gilt. Die erste Indexebene über der Blattebene speichert 1.000 Indexzeilen, dies bedeutet eine Indexzeile pro Blattseite. Dabei passen 25 Indexzeilen auf eine Seite. Dies bedeutet, dass 40 Seiten zum Speichern dieser 1.000 Indexzeilen erforderlich sind. Die nächste Ebene des Indexes muss 40 Zeilen speichern. Dies bedeutet, dass zwei Seiten erforderlich sind. Die letzte Ebene des Indexes muss zwei Zeilen speichern. Dies bedeutet, dass eine Seite erforderlich ist. Daraus ergeben sich 43 innere Knotenseiten im Index. Wenn Sie diese Werte in den oben genannten Formeln verwenden, erhalten Sie folgendes Ergebnis:  
  
     ***Non-leaf_Levels***  = 1 + log(25) (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43, was der Anzahl der Seiten im Beispiel entspricht.  
  
3.  Berechnen Sie die Größe des Indexes (insgesamt 8.192 Byte pro Seite):  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-4-total-the-calculated-values"></a>Schritt 4. Addieren der berechneten Werte  
 Addieren Sie die Werte, die in den beiden vorherigen Schritten erzielt wurden:  
  
 Größe des nicht gruppierten Indexes (in Bytes) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 In dieser Berechnung wird Folgendes nicht berücksichtigt:  
  
-   Partitionierung  
  
     Der Speicherplatzaufwand aus der Partitionierung ist geringfügig, seine Berechnung jedoch komplex. Er muss nicht berücksichtigt werden.  
  
-   Zuordnungsseiten  
  
     Mindestens eine IAM-Seite wird zum Nachverfolgen der für einen Heap zugeordneten Seiten verwendet, der Speicherplatzaufwand ist jedoch nur minimal. Außerdem ist kein Algorithmus verfügbar, um deterministisch genau zu berechnen, wie viele IAM-Seiten verwendet werden.  
  
-   LOB-Werte (Large Object)  
  
     Der Algorithmus zum Berechnen des genauen Speicherplatzes, der zum Speichern der Werte der LOB-Datentypen **varchar(max)**, **varbinary(max)**, **nvarchar(max)**, **text**, **ntext**, **xml**und **image** erforderlich ist, ist komplex. Es ist ausreichend, einfach die durchschnittliche Größe der erwarteten LOB-Werte zu addieren, diese mit ***Num_Rows***zu multiplizieren und das Ergebnis dann zur Gesamtgröße des nicht gruppierten Indexes zu addieren.  
  
-   Komprimierung  
  
     Sie können die Größe eines komprimierten Index nicht im Vorfeld berechnen.  
  
-   Spalten mit geringer Dichte  
  
     Informationen zu den Speicherplatzanforderungen von Sparsespalten finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Beschreibung von gruppierten und nicht gruppierten Indizes](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Erstellen nicht gruppierter Indizes](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Erstellen gruppierter Indizes](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Schätzen der Größe einer Tabelle](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Schätzen der Größe eines gruppierten Indexes](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Schätzen der Größe eines Heaps](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Schätzen der Größe einer Datenbank](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
