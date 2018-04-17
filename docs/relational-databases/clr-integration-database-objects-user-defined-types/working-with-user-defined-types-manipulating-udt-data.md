---
title: Bearbeiten von UDT-Daten | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- data deletions [CLR integration]
- data insertions [CLR integration]
- CONVERT function
- data updates [CLR integration]
- comparing data
- updating data [CLR integration]
- removing data
- IsByteOrdered property
- variables [CLR integration]
- data manipulation [CLR integration]
- user-defined types [CLR integration], data manipulation
- deleting data
- UDTs [CLR integration], data manipulation
- invoking UDT methods
- inserting data
ms.assetid: 51b1a5f2-7591-4e11-bfe2-d88e0836403f
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f5d5c9dbbf7596f2c3a16d80dcb821e4b75c22f3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-user-defined-types---manipulating-udt-data"></a>Arbeiten mit benutzerdefinierten Typen: Bearbeiten von UDT-Daten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] stellt keine spezialisierte Syntax für INSERT-, UPDATE- oder DELETE-Anweisungen zum Ändern von Daten in Spalten vom benutzerdefinierten Typ (User-defined Type, UDT) bereit. Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen CAST oder CONVERT werden verwendet, um systemeigene Datentypen in den benutzerdefinierten Typ (UDT) umzuwandeln.  
  
## <a name="inserting-data-in-a-udt-column"></a>Einfügen von Daten in eine UDT-Spalte  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen fügen drei Zeilen Beispieldaten in die **Punkte** Tabelle. Die **Punkt** Datentyp besteht aus X- und Y-Ganzzahlwerten, werden als Eigenschaften des UDT verfügbar gemacht. Verwenden Sie entweder die CAST- oder CONVERT-Funktion, um die durch Kommas getrennten X- und Y-Werte in der **Punkt** Typ. Die ersten beiden Anweisungen verwenden die CONVERT-Funktion zum Konvertieren eines Zeichenfolgenwertes in der **Punkt** Typ und die dritte Anweisung verwendet die CAST-Funktion:  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>Auswählen von Daten  
 Die folgende SELECT-Anweisung wählt den Binärwert des UDTs aus.  
  
```  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 Um die Ausgabe in einem lesbaren Format anzuzeigen, rufen die **ToString** Methode der **Punkt** UDT, der den Wert in seine Zeichenfolgendarstellung konvertiert.  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 Hierdurch werden folgende Ergebnisse erzielt.  
  
```  
IDPointValue  
----------  
13,4  
21,5  
31,99  
```  
  
 Sie können auch die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Funktionen CAST und CONVERT verwenden, um dieselben Ergebnisse zu erreichen.  
  
```  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 Die **Punkt** UDT macht seine X- und Y-Koordinaten als Eigenschaften, die Sie dann einzeln auswählen können. Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung wählt die X- und die Y-Koordinate getrennt aus:  
  
```  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 Die X-Eigenschaft und die Y-Eigenschaft geben einen ganzzahligen Wert zurück, der im Resultset angezeigt wird.  
  
```  
IDxValyVal  
----------  
134  
215  
3199  
```  
  
## <a name="working-with-variables"></a>Arbeiten mit Variablen  
 Sie können mit Variablen arbeiten, indem Sie die DECLARE-Anweisung verwenden, um einem UDT eine Variable zuzuweisen. Die folgenden Anweisungen weisen Sie einen Wert unter Verwendung der [!INCLUDE[tsql](../../includes/tsql-md.md)] SET-Anweisung, und zeigen Sie die Ergebnisse durch Aufrufen des UDTS **ToString** -Methode für die Variable:  
  
```  
DECLARE @PointValue Point;  
SET @PointValue = (SELECT PointValue FROM dbo.Points  
    WHERE ID = 2);  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 Das Resultset zeigt den Wert der Variablen an:  
  
```  
PointValue  
----------  
-1,5  
```  
  
 Mit den folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen wird dasselbe Ergebnis erzielt. Dabei wird für die Variablenzuweisung SELECT statt SET verwendet:  
  
```  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 Der Unterschied zwischen der Verwendung von SELECT statt SET für die Variablenzuweisung besteht darin, dass SELECT ermöglicht, mehrere Variable in einer SELECT-Anweisung zuzuweisen, während die SET-Syntax erfordert, dass jede Variable durch eine eigene SET-Anweisung zugewiesen wird.  
  
## <a name="comparing-data"></a>Vergleichen von Daten  
 Sie können Vergleichsoperatoren verwenden, um Werte in Ihrem UDT vergleichen, wenn Sie festgelegt haben die **IsByteOrdered** Eigenschaft **"true"** beim Definieren der Klasse. Weitere Informationen finden Sie unter [erstellen einen benutzerdefinierten Typ](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md).  
  
```  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 Sie können interne Werte des UDTS unabhängig von Vergleichen die **IsByteOrdered** Einstellung aus, wenn die Werte selbst vergleichbar sind. Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung wählt die Zeilen aus, in denen X größer ist als Y:  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 Vergleichsoperatoren können auch mit Variablen verwendet werden, wie in dieser Abfrage gezeigt, in der nach einem übereinstimmenden PointValue gesucht wird.  
  
```  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>Aufrufen von UDT-Methoden  
 Sie können auch Methoden aufrufen, die im UDT in [!INCLUDE[tsql](../../includes/tsql-md.md)] definiert sind. Die **Punkt** Klasse enthält drei Methoden **Abstand**, **DistanceFrom**, und **DistanceFromXY**. Die Codebeispiele, die diese drei Methoden definieren, finden Sie unter [Codieren benutzerdefinierter Typen](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-coding.md).  
  
 Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung ruft die **PointValue.Distance** Methode:  
  
```  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 Die Ergebnisse werden angezeigt, der **Abstand** Spalte:  
  
```  
IDXYDistance  
------------------------  
1345  
2155.09901951359278  
319999.0050503762308  
```  
  
 Die **DistanceFrom** -Methode akzeptiert ein Argument des **zeigen** -Datentyp und zeigt die Entfernung vom angegebenen Punkt zum PointValue:  
  
```  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 Die Ergebnisse zeigen die Ergebnisse von der **DistanceFrom** Methode für jede Zeile in der Tabelle:  
  
```  
ID PntDistanceFromPoint  
---------------------  
13,495.0210502993942  
21,594  
31,990  
```  
  
 Die **DistanceFromXY** -Methode übernimmt die Punkte einzeln als Argumente:  
  
```  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 Das Resultset ist identisch mit der **DistanceFrom** Methode.  
  
## <a name="updating-data-in-a-udt-column"></a>Aktualisieren von Daten in einer UDT-Spalte  
 Verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-UPDATE-Anweisung, um Daten in einer UDT-Spalte zu aktualisieren. Sie können auch eine Methode des UDTs verwenden, um den Status des Objekts zu aktualisieren. Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aktualisiert eine einzelne Zeile in der Tabelle:  
  
```  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 Sie können auch UDT-Elemente getrennt aktualisieren. Die folgende [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung aktualisiert nur die Y-Koordinate:  
  
```  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Wenn der UDT mit Bytereihenfolge auf definiert wurde **"true"**, [!INCLUDE[tsql](../../includes/tsql-md.md)] können die UDT-Spalte in einer WHERE-Klausel ausgewertet.  
  
```  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>Einschränkungen für Updates  
 Mehrere Eigenschaften können mit [!INCLUDE[tsql](../../includes/tsql-md.md)] nicht gleichzeitig aktualisiert werden. Beispielsweise schlägt die folgende UPDATE-Anweisung fehl, und es wird ein Fehler ausgegeben, da Sie denselben Spaltennamen nicht zwei Mal in derselben UPDATE-Anweisung verwenden können.  
  
```  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Um jeden Punkt einzeln zu aktualisieren, müssen Sie in der Point-UDT-Assembly eine Mutatormethode erstellen. Anschließend können Sie die Mutatormethode aufrufen, um das Objekt in einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-UPDATE-Anweisung zu aktualisieren, wie im Folgenden dargestellt:  
  
```  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>Löschen von Daten in einer UDT-Spalte  
 Um Daten in einem UDT zu löschen, verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)]-DELETE-Anweisung. Die folgende Anweisung löscht alle Zeilen in der Tabelle, die den in der WHERE-Klausel angegebenen Kriterien entsprechen. Wenn Sie die WHERE-Klausel einer DELETE-Anweisung weglassen, werden alle Zeilen in der Tabelle gelöscht.  
  
```  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 Sollen die Werte aus einer UDT-Spalte gelöscht werden, andere Zeilenwerte jedoch intakt bleiben, verwenden Sie die UPDATE-Anweisung. In diesem Beispiel wird für PointValue NULL festgelegt.  
  
```  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Arbeiten mit benutzerdefinierten Typen in SQLServer](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
