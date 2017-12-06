---
title: "Schätzen der Größe eines gruppierten Indexes | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
caps.latest.revision: "49"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3a25804d6bb1769d785e53e0790dff994a528d92
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="estimate-the-size-of-a-clustered-index"></a>Schätzen der Größe eines gruppierten Indexes
  Mit den folgenden Schritten können Sie den Umfang des Speicherplatzes schätzen, der zum Speichern eines gruppierten Indexes erforderlich ist:  
  
1.  Berechnen des Speicherplatzes, der zum Speichern der Daten in der Blattebene des gruppierten Indexes erforderlich ist.  
  
2.  Berechnen des Speicherplatzes, der zum Speichern von Indexinformationen für den gruppierten Index verwendet wird.  
  
3.  Addieren Sie die berechneten Werte.  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>Schritt 1: Berechnen des Speicherplatzes, der zum Speichern der Daten in der Blattebene verwendet wird  
  
1.  Geben Sie die Anzahl der Zeilen an, die die Tabelle enthalten wird:  
  
     ***Num_Rows***  = Anzahl der Zeilen in der Tabelle  
  
2.  Geben Sie die Anzahl der Spalten mit fester und mit variabler Länge an, und berechnen Sie den Speicherplatz, der für deren Speicherung erforderlich ist:  
  
     Berechnen Sie den Speicherplatz, der zum Speichern jeder dieser Spaltengruppen innerhalb der Datenzeile erforderlich ist. Die Größe einer Spalte hängt von der Angabe für Datentyp und -länge ab.  
  
     ***Num_Cols***  = Gesamtanzahl der Spalten (mit fester und variabler Länge)  
  
     ***Fixed_Data_Size***  = Gesamtzahl der Bytes in allen Spalten fester Länge  
  
     ***Num_Variable_Cols***  = Anzahl der Spalten variabler Länge  
  
     ***Max_Var_Size***  = Maximale Bytegröße aller Spalten variabler Länge  
  
3.  Wenn der gruppierte Index nicht eindeutig ist, berücksichtigen Sie die *uniqueifier* -Spalte:  
  
     Die Uniqueifier-Spalte ist eine Spalte variabler Länge mit NULL-Zulässigkeit. Sie ist in Spalten Nicht-NULL und 4 Byte lang, deren Schlüsselwerte nicht eindeutig sind. Dieser Wert ist Teil des Indexschlüssels und für die Sicherstellung erforderlich, dass jede Zeile über einen eindeutigen Schlüsselwert verfügt.  
  
     ***Num_Cols***  = ***Num_Cols*** + 1  
  
     ***Num_Variable_Cols***  = ***Num_Variable_Cols*** + 1  
  
     ***Max_Var_Size***  = ***Max_Var_Size*** + 4  
  
     Diese Änderungen gehen davon aus, dass alle Werte nicht eindeutig sind.  
  
4.  Ein Teil der Zeile, der als NULL-Bitmuster (Null_Bitmap) bezeichnet wird, wird für das Verwalten der NULL-Zulässigkeit der Spalte reserviert. Berechnen Sie dessen Größe:  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     Nur der ganzzahlige Teil des oben aufgeführten Ausdrucks sollte verwendet werden; verwerfen Sie den Nachkommateil.  
  
5.  Berechnen Sie die Größe der Daten variabler Länge:  
  
     Wenn die Tabelle Spalten variabler Länge enthält, müssen Sie den Speicherplatz ermitteln, der von den Spalten innerhalb der Zeile verwendet wird:  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     Die zu ***Max_Var_Size*** hinzugefügten Bytes dienen der Nachverfolgung jeder einzelnen variablen Spalte. Bei dieser Formel wird angenommen, dass alle Spalten variabler Länge zu 100 % gefüllt sind. Wenn sich abzeichnet, dass ein niedrigerer Prozentsatz des Speicherplatzes für Spalten variabler Länge verwendet wird, können Sie den ***Max_Var_Size*** -Wert mithilfe dieses Prozentsatzes anpassen, um einen genaueren Schätzwert für die Gesamtgröße der Tabelle zu erhalten.  
  
    > [!NOTE]  
    >  Sie können **varchar**-, **nvarchar**-, **varbinary**- oder **sql_variant** -Spalten kombinieren, mit dem Ergebnis, dass die definierte Tabellengesamtbreite größer als 8.060 Byte ist. Die Länge jeder einzelnen Spalte unterliegt auch weiterhin der Beschränkung von 8.000 Byte für eine **varchar**-, **varbinary**- oder **sql_variant** -Spalte und von 4.000 Byte für **nvarchar** -Spalten. Die kombinierte Breite kann jedoch den Grenzwert von 8.060 Byte in einer Tabelle überschreiten.  
  
     Wenn keine Spalten variabler Länge vorhanden sind, legen Sie ***Variable_Data_Size*** auf 0 fest.  
  
6.  Berechnen Sie die Gesamtzeilenlänge:  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     Der Wert 4 ist der Zeilenüberschriftenaufwand der Datenzeile.  
  
7.  Berechnen Sie die Anzahl der Zeilen pro Seite (8.096 freie Byte pro Seite):  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     Da sich eine Zeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Zeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
8.  Berechnen Sie die Anzahl der reservierten freien Zeilen pro Seite anhand des angegebenen [Füllfaktors](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) :  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Row_Size*** + 2)  
  
     Bei dem in der Berechnung verwendeten Füllfaktor handelt es sich nicht um einen Prozentwert, sondern um einen ganzzahligen Wert. Da sich eine Zeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Zeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Mit ansteigendem Füllfaktor werden mehr Daten auf jeder Seite gespeichert, und die Anzahl der Seiten nimmt ab. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
9. Berechnen Sie die Anzahl der Seiten, die zum Speichern aller Zeilen benötigt werden:  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     Die geschätzte Seitenanzahl muss auf die nächste ganze Seite aufgerundet werden.  
  
10. Berechnen Sie den Umfang des Speicherplatzes, der zum Speichern der Daten in der Blattebene erforderlich ist (insgesamt 8192 Byte pro Seite):  
  
     ***Leaf_space_used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>Schritt 2: Berechnen des Speicherplatzes, der zum Speichern der Indexinformationen verwendet wird  
 Mit den folgenden Schritten können Sie den Umfang des Speicherplatzes schätzen, der zum Speichern der oberen Ebenen des Indexes erforderlich ist:  
  
1.  Geben Sie die Anzahl der Spalten mit fester und mit variabler Länge im Indexschlüssel an, und berechnen Sie den Speicherplatz, der für deren Speicherung erforderlich ist:  
  
     Die Schlüsselspalten eines Indexes können Spalten fester und variabler Länge enthalten. Um die Größe der Indexzeilen auf der inneren Ebene zu schätzen, müssen Sie den Speicherplatz berechnen, der von jeder dieser Spaltengruppen innerhalb der Indexzeile belegt wird. Die Größe einer Spalte hängt von der Angabe für Datentyp und -länge ab.  
  
     ***Num_Key_Cols***  = Gesamtanzahl der Schlüsselspalten (fester und variabler Länge)  
  
     ***Fixed_Key_Size***  = Gesamtzahl der Bytes in allen Schlüsselspalten fester Länge  
  
     ***Num_Variable_Key_Cols***  = Anzahl der Schlüsselspalten variabler Länge  
  
     ***Max_Var_Key_Size***  = Maximale Bytegröße aller Schlüsselspalten variabler Länge  
  
2.  Berücksichtigen Sie ggf. den Uniqueifier, der erforderlich ist, wenn der Index nicht eindeutig ist:  
  
     Die Uniqueifier-Spalte ist eine Spalte variabler Länge mit NULL-Zulässigkeit. Sie ist in Spalten Nicht-NULL und 4 Byte lang, deren Indexschlüsselwerte nicht eindeutig sind. Dieser Wert ist Teil des Indexschlüssels und für die Sicherstellung erforderlich, dass jede Zeile über einen eindeutigen Schlüsselwert verfügt.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 4  
  
     Diese Änderungen gehen davon aus, dass alle Werte nicht eindeutig sind.  
  
3.  Berechnen der Größe des NULL-Bitmusters:  
  
     Wenn der Index Spalten mit NULL-Zulässigkeit enthält, ist ein Teil der Indexzeile dem NULL-Bitmuster zugeordnet. Berechnen Sie dessen Größe:  
  
     ***Index_Null_Bitmap***  = 2 + ((Anzahl der Spalten in der Indexzeile + 7) / 8)  
  
     Nur der ganzzahlige Teil des vorherigen Ausdrucks darf verwendet werden. Der Rest wird verworfen.  
  
     Wenn keine Schlüsselspalten vorhanden sind, die NULL-Werte zulassen, legen Sie ***Index_Null_Bitmap*** auf 0 fest.  
  
4.  Berechnen Sie die Größe der Daten variabler Länge:  
  
     Wenn der Index Spalten variabler Länge enthält, müssen Sie den Speicherplatz ermitteln, der von den Spalten innerhalb der Indexzeile verwendet wird:  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     Die zu ***Max_Var_Key_Size*** hinzugefügten Bytes dienen der Nachverfolgung der einzelnen Spalten variabler Länge. Bei dieser Formel wird angenommen, dass alle Spalten variabler Länge zu 100 % gefüllt sind. Wenn sich abzeichnet, dass ein niedrigerer Prozentsatz des Speicherplatzes für Spalten variabler Länge verwendet wird, können Sie den ***Max_Var_Key_Size*** -Wert mithilfe dieses Prozentsatzes anpassen, um einen genaueren Schätzwert für die Gesamtgröße der Tabelle zu erhalten.  
  
     Wenn keine Spalten variabler Länge vorhanden sind, legen Sie ***Variable_Key_Size*** auf 0 fest.  
  
5.  Berechnen Sie die Länge der Indexzeile:  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (für Zeilenüberschriftenaufwand einer Indexzeile) + 6 (für ID-Zeiger der untergeordneten Seite)  
  
6.  Berechnen Sie die Anzahl der Indexzeilen pro Seite (8096 freie Byte pro Seite):  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     Da sich eine Indexzeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Indexzeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
7.  Berechnen Sie die Anzahl der Ebenen im Index:  
  
     ***Non-leaf_Levels***  = 1 + log (Index_Rows_Per_Page) (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     Runden Sie diese Zahl auf die nächste ganze Zahl auf. Dieser Wert schließt die Blattebene des gruppierten Index nicht mit ein.  
  
8.  Berechnen Sie die Anzahl der inneren Knotenseiten im Index:  
  
     ***Num_Index_Pages =*** ∑Level ***(Num_Leaf_Pages / (Index_Rows_Per_Page***^Level***))***  
  
     wobei 1 <= Level <= ***Non-leaf_Levels***  
  
     Runden Sie jeden Summanden auf die nächste ganze Zahl auf. Stellen Sie sich als einfaches Beispiel einen Index vor, bei dem ***Num_Leaf_Pages*** = 1000 und ***Index_Rows_Per_Page*** = 25. gilt. Die erste Indexebene über der Blattebene speichert 1.000 Indexzeilen, dies bedeutet eine Indexzeile pro Blattseite. Dabei passen 25 Indexzeilen auf eine Seite. Dies bedeutet, dass 40 Seiten zum Speichern dieser 1.000 Indexzeilen erforderlich sind. Die nächste Ebene des Indexes muss 40 Zeilen speichern. Dies bedeutet, dass 2 Seiten erforderlich sind. Die letzte Ebene des Indexes muss zwei Zeilen speichern. Dies bedeutet, dass eine Seite erforderlich ist. Daraus ergeben sich 43 innere Knotenseiten im Index. Wenn Sie diese Werte in den oben genannten Formeln verwenden, ergibt sich Folgendes:  
  
     ***Non-leaf_Levels***  = 1 + log(25) (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43, was der Anzahl der Seiten im Beispiel entspricht.  
  
9. Berechnen Sie die Größe des Indexes (insgesamt 8.192 Byte pro Seite):  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-3-total-the-calculated-values"></a>Schritt 3: Addieren der berechneten Werte  
 Addieren Sie die Werte, die in den beiden vorherigen Schritten erzielt wurden:  
  
 Größe des gruppierten Indexes (in Bytes) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 In dieser Berechnung wird Folgendes nicht berücksichtigt:  
  
-   Partitionierung  
  
     Der Speicherplatzaufwand aus der Partitionierung ist geringfügig, seine Berechnung jedoch komplex. Er muss nicht berücksichtigt werden.  
  
-   Zuordnungsseiten  
  
     Mindestens eine IAM-Seite wird zum Nachverfolgen der für einen Heap zugeordneten Seiten verwendet, der Speicherplatzaufwand ist jedoch nur minimal. Außerdem ist kein Algorithmus verfügbar, um deterministisch genau zu berechnen, wie viele IAM-Seiten verwendet werden.  
  
-   LOB-Werte (Large Object)  
  
     Der Algorithmus zum Berechnen des genauen Speicherplatzes, der zum Speichern der Werte der LOB-Datentypen **varchar(max)**, **varbinary(max)**, **nvarchar(max)**, **text**, **ntext**, **xml**, and **image** erforderlich ist, ist komplex. Es ist ausreichend, einfach die durchschnittliche Größe der erwarteten LOB-Werte zu addieren, diese mit ***Num_Rows***zu multiplizieren und das Ergebnis dann zur Gesamtgröße des gruppierten Indexes zu addieren.  
  
-   Komprimierung  
  
     Sie können die Größe eines komprimierten Index nicht im Vorfeld berechnen.  
  
-   Spalten mit geringer Dichte  
  
     Informationen zu den Speicherplatzanforderungen von Sparsespalten finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Beschreibung von gruppierten und nicht gruppierten Indizes](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Schätzen der Größe einer Tabelle](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Erstellen gruppierter Indizes](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Erstellen nicht gruppierter Indizes](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Schätzen der Größe eines nicht gruppierten Index](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Schätzen der Größe eines Heaps](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Schätzen der Größe einer Datenbank](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
