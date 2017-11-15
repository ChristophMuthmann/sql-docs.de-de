---
title: "Schätzen der Größe eines Heaps | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 8980fc43f62093e3d8821a7725685e8402486485
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="estimate-the-size-of-a-heap"></a>Schätzen der Größe eines Heaps
  Mit den folgenden Schritten können Sie den Umfang des Speicherplatzes schätzen, der zum Speichern von Daten in einem Heap erforderlich ist:  
  
1.  Geben Sie die Anzahl der Zeilen an, die die Tabelle enthalten wird:  
  
     ***Num_Rows***  = Anzahl der Zeilen in der Tabelle  
  
2.  Geben Sie die Anzahl der Spalten mit fester und mit variabler Länge an, und berechnen Sie den Speicherplatz, der für deren Speicherung erforderlich ist:  
  
     Berechnen Sie den Speicherplatz, der zum Speichern jeder dieser Spaltengruppen innerhalb der Datenzeile erforderlich ist. Die Größe einer Spalte hängt von der Angabe für Datentyp und -länge ab.  
  
     ***Num_Cols***  = Gesamtanzahl der Spalten (mit fester und variabler Länge)  
  
     ***Fixed_Data_Size***  = Gesamtzahl der Bytes in allen Spalten fester Länge  
  
     ***Num_Variable_Cols***  = Anzahl der Spalten variabler Länge  
  
     ***Max_Var_Size***  = Maximale gesamte Bytegröße aller Spalten variabler Länge  
  
3.  Ein Teil der Zeile, der als NULL-Bitmuster (Null_Bitmap) bezeichnet wird, wird für das Verwalten der NULL-Zulässigkeit der Spalte reserviert. Berechnen Sie dessen Größe:  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     Nur der ganzzahlige Teil dieses Ausdrucks darf verwendet werden. Der Rest wird verworfen.  
  
4.  Berechnen Sie die Größe der Daten variabler Länge:  
  
     Wenn die Tabelle Spalten variabler Länge enthält, müssen Sie den Speicherplatz ermitteln, der von den Spalten innerhalb der Zeile verwendet wird:  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     Die zu ***Max_Var_Size*** hinzugefügten Bytes dienen der Nachverfolgung jeder einzelnen Spalte mit variabler Länge. Bei dieser Formel wird angenommen, dass alle Spalten variabler Länge zu 100 % gefüllt sind. Wenn sich abzeichnet, dass ein niedrigerer Prozentsatz des Speicherplatzes für Spalten variabler Länge verwendet wird, können Sie den ***Max_Var_Size*** -Wert mithilfe dieses Prozentsatzes anpassen, um einen genaueren Schätzwert für die Gesamtgröße der Tabelle zu erhalten.  
  
    > [!NOTE]  
    >  Sie können **varchar**-, **nvarchar**-, **varbinary**- oder **sql_variant** -Spalten kombinieren, mit dem Ergebnis, dass die definierte Tabellengesamtbreite größer als 8.060 Byte ist. Die Länge jeder einzelnen Spalte unterliegt auch weiterhin der Beschränkung von 8.000 Byte für eine **varchar**-, **nvarchar-,****varbinary**- oder **sql_variant** -Spalte. Die kombinierte Breite kann jedoch den Grenzwert von 8.060 Byte in einer Tabelle überschreiten.  
  
     Wenn keine Spalten variabler Länge vorhanden sind, legen Sie ***Variable_Data_Size*** auf 0 fest.  
  
5.  Berechnen Sie die Gesamtzeilenlänge:  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
     Der Wert 4 in der Formel ist der Zeilenüberschriftenaufwand der Datenzeile.  
  
6.  Berechnen Sie die Anzahl der Zeilen pro Seite (8.096 freie Byte pro Seite):  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     Da sich eine Zeile nicht auf zwei Seiten erstreckt, muss die Anzahl der Zeilen pro Seite auf die nächste ganze Zeile abgerundet werden. Die Angabe 2 in der Formel bezieht sich auf den Eingang der Zeile in das Slotarray der Seite.  
  
7.  Berechnen Sie die Anzahl der Seiten, die zum Speichern aller Zeilen benötigt werden:  
  
     ***Num_Pages***  = ***Num_Rows*** / ***Rows_Per_Page***  
  
     Die geschätzte Seitenanzahl muss auf die nächste ganze Seite aufgerundet werden.  
  
8.  Berechnen Sie den Umfang des Speicherplatzes, der zum Speichern der Daten im Heap erforderlich ist (insgesamt 8.192 Byte pro Seite):  
  
     Heapgröße (Bytes) = 8192 x ***Num_Pages***  
  
 In dieser Berechnung wird Folgendes nicht berücksichtigt:  
  
-   Partitionierung  
  
     Der Speicherplatzaufwand aus der Partitionierung ist geringfügig, seine Berechnung jedoch komplex. Er muss nicht berücksichtigt werden.  
  
-   Zuordnungsseiten  
  
     Mindestens eine IAM-Seite wird zum Nachverfolgen der für einen Heap zugeordneten Seiten verwendet, der Speicherplatzaufwand ist jedoch nur minimal. Außerdem ist kein Algorithmus verfügbar, um deterministisch genau zu berechnen, wie viele IAM-Seiten verwendet werden.  
  
-   LOB-Werte (Large Object)  
  
     Der Algorithmus zum Berechnen des genauen Speicherplatzes, der zum Speichern der Werte der LOB-Datentypen **varchar(max)**, **varbinary(max)**, **nvarchar(max)**, **text**, **ntextxml**und **image** erforderlich ist, ist komplex. Es reicht aus, lediglich die Durchschnittsgröße der erwarteten LOB-Werte zu addieren und diesen Wert zur Heapgesamtgröße zu addieren.  
  
-   Komprimierung  
  
     Sie können die Größe eines komprimierten Heaps nicht im Voraus berechnen.  
  
-   Spalten mit geringer Dichte  
  
     Informationen zu den Speicherplatzanforderungen von Sparsespalten finden Sie unter [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Heaps &#40;Tabellen ohne gruppierte Indizes&#41;](../../relational-databases/indexes/heaps-tables-without-clustered-indexes.md)   
 [Beschreibung von gruppierten und nicht gruppierten Indizes](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Erstellen gruppierter Indizes](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Erstellen nicht gruppierter Indizes](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Schätzen der Größe einer Tabelle](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Schätzen der Größe eines gruppierten Indexes](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Schätzen der Größe eines nicht gruppierten Index](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Schätzen der Größe einer Datenbank](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
