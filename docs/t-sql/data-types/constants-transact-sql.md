---
title: Konstanten (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aae955a177f637e3c359eabf02679025cbecdb3a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="constants-transact-sql"></a>Konstanten (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine Konstante, gelegentlich auch als Literal- oder Skalarwert bezeichnet, ist ein Symbol, das einen bestimmten Datenwert repräsentiert. Das Format einer Konstante ist abhängig vom Datentyp des Werts, den sie repräsentiert.
  
## <a name="character-string-constants"></a>Zeichenfolgenkonstanten
Zeichenfolgenkonstanten werden in einfache Anführungszeichen eingeschlossen und enthalten alphanumerische Zeichen (a-z, A-Z und 0-9) sowie Sonderzeichen, wie z. B. Ausrufezeichen (!), @-Zeichen und Nummernzeichen (#). Zeichenfolgenkonstanten wird die Standardsortierung der aktuellen Datenbank zugewiesen, es sei denn, mit der COLLATE-Klausel wird eine Sortierung angegeben. Vom Benutzer eingegebene Zeichenfolgen werden durch die Codepage auf dem Computer ausgewertet und ggf. in die Standardcodepage der Datenbank übersetzt.
  
Wurde für die QUOTED_IDENTIFIER-Option für eine Verbindung OFF festgelegt, können Zeichenfolgen auch in doppelte Anführungszeichen eingeschlossen werden; allerdings verwenden der Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Anbieter und der ODBC-Treiber automatisch SET QUOTED_IDENTIFIER ON. Es wird die Verwendung einfacher Anführungszeichen empfohlen.
  
Enthält eine in einfache Anführungszeichen eingeschlossene Zeichenfolge ein eingeschlossenes Anführungszeichen, muss das eingeschlossene Anführungszeichen durch zwei einfache Anführungszeichen ersetzt werden. Bei Zeichenfolgen, die in doppelten Anführungszeichen stehen, ist dies nicht erforderlich.
  
Nachfolgend finden Sie Beispiele für Zeichenfolgen:
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
Leere Zeichenfolgen werden als zwei einzelne Anführungszeichen ohne Inhalt dargestellt. Im 6.x-Kompatibilitätsmodus wird eine leere Zeichenfolge als einzelnes Leerzeichen interpretiert.
  
Zeichenfolgenkonstanten unterstützen erweiterte Sortierungen.
  
> [!NOTE]  
>  Zeichenkonstanten, die größer als 8000 Bytes typisiert werden **varchar(max)** Daten.  
  
## <a name="unicode-strings"></a>Unicode-Zeichenfolgen
Unicode-Zeichenfolgen besitzen ein ähnliches Format wie Zeichenfolgen, werden aber mit einem N-Bezeichner eingeleitet (N steht für Landessprache (National Language) im SQL-92-Standard). Das Präfix N muss ein Großbuchstabe sein. Beispielsweise ist 'Michél' eine Zeichenkonstante, während N 'Michél' eine Unicode-Konstante ist. Unicode-Konstanten werden als Unicode-Daten interpretiert und nicht mithilfe einer Codepage ausgewertet. Unicode-Konstanten verfügen über eine Sortierung. Diese Sortierung steuert in erster Linie Vergleiche und die Unterscheidung nach Groß- und Kleinschreibung. Unicode-Konstanten wird die Standardsortierung der aktuellen Datenbank zugewiesen, es sei denn, mit der COLLATE-Klausel wird eine Sortierung angegeben. Unicode-Daten werden mithilfe von 2 Byte pro Zeichen anstelle von 1 Byte pro Zeichen bei Zeichendaten gespeichert. Weitere Informationen finden Sie unter [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).
  
Unicode-Zeichenfolgenkonstanten unterstützen erweiterte Sortierungen.
  
> [!NOTE]  
>  Unicode-Konstanten, die größer als 8000 Bytes typisiert werden **nvarchar(max)** Daten.  
  
## <a name="binary-constants"></a>Binäre Konstanten
Binäre Konstanten besitzen das Präfix `0x` und bestehen aus einer Zeichenfolge von hexadezimalen Zahlen. Sie werden nicht in Anführungszeichen eingeschlossen.
  
Nachfolgend finden Sie Beispiele für Binärzeichenfolgen:
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  Binäre Konstanten, die größer als 8000 Bytes typisiert werden **varbinary(max)** Daten.  
  
## <a name="bit-constants"></a>Bit-Konstanten
**Bit** Konstanten werden durch die Zahlen 0 oder 1 dargestellt und nicht in Anführungszeichen eingeschlossen sind. Wird eine größere Zahl als eins verwendet, wird diese in eins umgewandelt.
  
## <a name="datetime-constants"></a>Konstanten "DateTime"
**"DateTime"** -Konstanten werden durch Datumszeichenfolgen in bestimmten Formaten, eingeschlossen in einfache Anführungszeichen dargestellt.
  
Im folgenden sind Beispiele für **"DateTime"** Konstanten:
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Beispiele für "DateTime" Konstanten sind:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>integer-Konstanten
**ganze Zahl** -Konstanten werden durch eine Folge von Ziffern, die nicht in Anführungszeichen eingeschlossen und enthalten keine Dezimaltrennzeichen dargestellt. **ganze Zahl** -Konstanten müssen ganze Zahlen sein; sie können keinen Dezimalstellen enthalten.
  
Im folgenden sind Beispiele für **Ganzzahl** Konstanten:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>decimal-Konstanten
**Decimal** -Konstanten werden durch eine Folge von Ziffern, die nicht in Anführungszeichen eingeschlossen und enthalten ein Dezimaltrennzeichen dargestellt.
  
Im folgenden sind Beispiele für **decimal** Konstanten:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>float- und Real-Konstanten
**"float"** und **echte** -Konstanten wird die wissenschaftliche Schreibweise verwendet.
  
Im folgenden sind Beispiele für **"float"** oder **echte** Werte:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>Money-Konstanten
**Money** -Konstanten werden als Folge von Ziffern mit einem optionalen Dezimaltrennzeichen und einem optionalen Währungssymbol als Präfix dargestellt. **Money** -Konstanten werden nicht in Anführungszeichen eingeschlossen.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erzwingt keine Gruppierungsregeln, wie etwa das Einfügen eines Kommas (,) nach jeder dritten Ziffer in Währungszeichenfolgen.
  
> [!NOTE]  
>  Kommas werden an einer beliebigen Stelle in der angegebenen ignoriert **Money** literal.  
  
Im folgenden sind Beispiele für **Money** Konstanten:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>Uniqueidentifier-Konstanten
**"uniqueidentifier"** -Konstanten sind eine Zeichenfolge, die eine GUID darstellt. Sie können entweder im Binär- oder Zeichenfolgenformat angegeben werden.
  
In den beiden folgenden Beispielen wird dieselbe GUID angegeben:
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Angeben von negativen und positiven Zahlen  
Um anzugeben, ob eine Zahl positiv oder negativ ist, gelten die  **+**  oder  **-**  unäre Operatoren auf eine numerische Konstante. Dadurch wird ein numerischer Ausdruck erstellt, der den numerischen, vorzeichenbehafteten Wert darstellt. Numerische Konstanten verwenden positiv, wenn die  **+**  oder  **-**  unäre Operatoren werden nicht angewendet.
  
Signiert **Ganzzahl** Ausdrücke:  
  
```sql
+145345234
-2147483648
```
Signiert **decimal** Ausdrücke:  
  
```sql
+145345234.2234
-2147483648.10
```
  
Signiert **"float"** Ausdrücke:  
  
```sql
+123E-3
-12E5
```
  
Signiert **Money** Ausdrücke:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Erweiterte Sortierungen  
SQL Server unterstützt Zeichen- und Unicode-Zeichenfolgenkonstanten, die erweiterte Sortierungen unterstützen. Weitere Informationen finden Sie unter der [COLLATE &#40; Transact-SQL &#41; ](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) Klausel.
  
## <a name="see-also"></a>Siehe auch
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operatoren &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  
