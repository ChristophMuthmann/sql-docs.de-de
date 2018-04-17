---
title: Schreiben von Code von benutzerdefinierten Typen | Microsoft Docs
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
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d39df3bcadebc8c6433d11563c6d628ca439f061
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="creating-user-defined-types---coding"></a>Erstellen von benutzerdefinierten Typen - Codierung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn Sie die Definition eines benutzerdefinierten Typs (UDT) schreiben, müssen Sie verschiedene Funktionen implementieren, abhängig davon, ob Sie den UDT als Klasse oder als Struktur implementieren, sowie abhängig von den von Ihnen gewählten Format- und Serialisierungsoptionen.  
  
 Im Beispiel in diesem Abschnitt veranschaulicht die Implementierung einer **Punkt** UDT als eine **Struktur** (oder **Struktur** in Visual Basic). Die **Punkt** UDT besteht aus X- und Y-Koordinaten als implementiert Eigenschaftenprozeduren.  
  
 Beim Definieren eines UDTs sind die folgenden Namespaces erforderlich:  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 Die **Microsoft.SqlServer.Server** -Namespace enthält die Objekte, die für verschiedene Attribute des UDT, erforderlich sind und die **System.Data.SqlTypes** -Namespace enthält Klassen, die darstellen, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]systemeigenen Datentypen, die auf die Assembly zur Verfügung. Es kann natürlich zusätzliche Namespaces geben, die eine Assembly erfordert, um ordnungsgemäß zu funktionieren. Die **Punkt** UDT verwendet überdies die **System.Text** Namespace zum Arbeiten mit Zeichenfolgen.  
  
> [!NOTE]  
>  Visual C++-Datenbankobjekte, z. B. UDTs, kompiliert mit **/CLR: pure** werden für die Ausführung nicht unterstützt.  
  
## <a name="specifying-attributes"></a>Angeben von Attributen  
 Attribute bestimmen, wie die Serialisierung verwendet wird, um die Speicherdarstellung von UDTs zu erstellen und um UDTs durch Werte an den Client zu übertragen.  
  
 Die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** ist erforderlich. Die **Serializable** Attribut ist optional. Sie können auch angeben, die **Microsoft.SqlServer.Server.SqlFacetAttribute** um Informationen über den Rückgabetyp eines UDTs bereitzustellen. Weitere Informationen finden Sie unter [Benutzerdefinierte Attribute für CLR-Routinen](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Attribute des Point-UDT  
 Die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** legt das Speicherformat für die **Punkt** UDT **systemeigene**. **IsByteOrdered** festgelegt ist, um **"true"**, dies garantiert, dass die Ergebnisse der Vergleiche in SQL Server identisch sind, als ob Sie denselben Vergleich in verwaltetem Code stattgefunden hat. Der UDT implementiert die **System.Data.SqlTypes.INullable** Schnittstelle, um der UDT Null aufmerksam zu machen.  
  
 Das folgende Codefragment zeigt die Attribute für die **Punkt** UDT.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Implementieren von NULL-Zulässigkeit  
 Zusätzlich zum ordnungsgemäßen Angeben der Attribute für die Assemblys muss der UDT auch die NULL-Zulässigkeit unterstützen. UDTs geladenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind Nullwerte, aber in der Reihenfolge der UDT einen Nullwert erkennt, muss der UDT implementieren die **System.Data.SqlTypes.INullable** Schnittstelle.  
  
 Sie müssen eine Eigenschaft namens erstellen **IsNull**, das erforderlich ist, um festzustellen, ob ein Wert von CLR-Code null ist. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine NULL-Instanz eines UDTs findet, wird der UDT mit normalen Behandlungsmethoden für NULL-Werte persistent gespeichert. Der Server vergeudet keine Zeit mit dem Serialisieren oder Deserialisieren des UDTs, wenn dies nicht erforderlich ist, und er verschwendet keinen Platz zum Speichern des NULL-UDTs. Diese Überprüfung auf NULL wird jedes Mal durchgeführt, wenn ein UDT von der CLR übernommen wird. Das heißt, dass mit dem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Konstrukt immer überprüft werden kann, ob UDTs NULL sind. Die **IsNull** Eigenschaft wird auch vom Server verwendet, um zu testen, ob eine Instanz null ist. Sobald der Server bestimmt, dass der UDT NULL ist, kann er seine systemeigene NULL-Behandlung verwenden.  
  
 Die **get()** Methode **IsNull** ist nicht in keiner Weise Sonderfall. Wenn eine **Punkt** Variable **@p** ist **Null**, klicken Sie dann **@p.IsNull** , standardmäßig als ausgewertet "NULL", nicht "1". Grund hierfür ist die **SqlMethod(OnNullCall)** Attribut von der **IsNull get()** Methode der Standardwert ist "false". Da das Objekt ist **Null**, wenn die Eigenschaft angefordert wird, nicht das Objekt deserialisiert wird, die Methode wird nicht aufgerufen und der Standardwert "NULL" wird zurückgegeben.  
  
### <a name="example"></a>Beispiel  
 Im folgenden Beispiel ist die `is_Null`-Variable privat und enthält für die Instanz des UDT den Status NULL. Im Code muss ein entsprechender Wert für `is_Null` verwaltet werden. Der UDT benötigen auch eine statische Eigenschaft namens **Null** , die null-Wertinstanz des UDTS zurückgibt. Dadurch kann der UDT einen NULL-Wert zurückgeben, wenn die Instanz auch in der Datenbank tatsächlich NULL ist.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL und IsNull  
 Betrachten Sie die Tabelle, die das Schema Points (Id Int, einen Punkt darstellt), wobei enthält **Punkt** ist eine CLR-UDT und die folgenden Abfragen:  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 Beide Abfragen zurückgeben, die IDs von Punkten mit nicht-**Null** Speicherorte. In Abfrage 1 wird die normale NULL-Behandlung verwendet, und dort ist keine Deserialisierung von UDTs erforderlich. Abfrage 2, andererseits, muss jedes nicht - deserialisieren**Null** Objekt, und rufen Sie in die CLR zum Abrufen des Werts, der die **IsNull** Eigenschaft. Es ist offensichtlich, verwenden **IS NULL** wird eine bessere Leistung aufweisen, und es darf nie ein Grund zum Lesen der **IsNull** Eigenschaft eines UDT über [!INCLUDE[tsql](../../includes/tsql-md.md)] Code.  
  
 Wozu dient also die Verwendung der **IsNull** Eigenschaft? Es wird zunächst erforderlich, um zu bestimmen, ob ein Wert ist **Null** im CLR-code. Zweitens: der Server benötigt eine Möglichkeit zum Testen, ob eine Instanz **Null**, sodass diese Eigenschaft vom Server verwendet wird. Sobald der Server bestimmt ist **Null**, dann er seine systemeigene null-Behandlung verwenden kann, um ihn zu beheben.  
  
## <a name="implementing-the-parse-method"></a>Implementieren der Parse-Methode  
 Die **analysieren** und **ToString** Methoden für Konvertierungen in und aus der UDT in zeichenfolgendarstellungen zu ermöglichen. Die **analysieren** -Methode ermöglicht es, eine Zeichenfolge in einen UDT konvertiert werden. Es muss deklariert werden, als **statische** (oder **Shared** in Visual Basic), und nehmen einen Versionsparameter vom Typ **System.Data.SqlTypes.SqlString**.  
  
 Der folgende code implementiert die **analysieren** Methode für die **Punkt** UDT, der aus den X- und Y-Koordinaten trennt. Die **analysieren** Methode verfügt über ein einzelnes Argument vom Typ **System.Data.SqlTypes.SqlString**, wird davon ausgegangen, dass die X- und Y-Werte als eine durch Trennzeichen getrennte Zeichenfolge angegeben werden. Festlegen der **Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall** -Attribut **"false"** wird verhindert, dass die **analysieren** Methode aufgerufen wird, von einer null-Instanz von Punkt.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>Implementieren der ToString-Methode  
 Die **ToString** -Methode konvertiert die **Punkt** UDT in einen Zeichenfolgenwert. In diesem Fall wird die Zeichenfolge "NULL" zurückgegeben, für eine Null-Instanz, von der **Punkt** Typ. Die **ToString** -Methode kehrt das Ergebnis der **analysieren** -Methode mithilfe einer **System.Text.StringBuilder** zurückzugebenden eine durch Trennzeichen getrennte **System.String**bestehend aus den X- und Y-Koordinatenwerte. Da **InvokeIfReceiverIsNull** der Standardwert ist "false", die Prüfung auf eine null-Instanz des **Punkt** ist nicht erforderlich.  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>Bereitstellen der UDT-Eigenschaften  
 Die **Punkt** UDT macht die X- und Y-Koordinaten, die als öffentlichen Lese-/ Schreibzugriff Eigenschaften vom Typ implementiert werden **System. Int32**.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>Überprüfen von UDT-Werten  
 Beim Verarbeiten von UDT-Daten konvertiert [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] automatisch Binärwerte in UDT-Werte. Im Rahmen dieses Konvertierungsprozesses muss überprüft werden, ob sich die Werte für das Serialisierungsformat des Typs eignen, und sichergestellt werden, dass die Werte ordnungsgemäß deserialisiert werden können. Dadurch wird sichergestellt, dass der Wert in das binäre Format konvertiert werden kann. Bei UDTs, deren Sortierreihenfolge eine Bytereihenfolge ist, wird dadurch auch sichergestellt, dass der resultierende Binärwert dem ursprünglichen Binärwert entspricht. So wird verhindert, dass ungültige Werte in der Datenbank persistent gespeichert werden. In einigen Fällen ist diese Art der Überprüfung möglicherweise unzulänglich. Eine zusätzliche Überprüfung kann erforderlich sein, wenn UDT-Werte in einer bestimmten Domäne oder einem Bereich liegen müssen. Ein UDT beispielsweise, der ein Datum implementiert, kann erfordern, dass der Wert für den Tag eine positive Zahl ist, die in einem bestimmten zulässigen Wertebereich liegt.  
  
 Die **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName** Eigenschaft von der **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute** können Sie den Namen angeben eine Validierungsmethode, dass der Server ausgeführt, wenn wird Daten einem UDT zugewiesen oder in einen UDT konvertiert. **ValidationMethodName** wird auch während der Ausführung der Bcp-Hilfsprogramm, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, verteilte Abfrage und tabular Data Stream (TDS) Remoteprozeduraufruf Remoteprozeduraufruf (RPC) Vorgänge bezeichnet. Der Standardwert für **ValidationMethodName** ist null, womit angegeben, dass keine Validierungsmethode vorhanden ist.  
  
### <a name="example"></a>Beispiel  
 Das folgende Codefragment zeigt die Deklaration für die **Punkt** -Klasse, der angibt, eine **ValidationMethodName** von **ValidatePoint**.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 Wenn eine Validierungsmethode angegeben wird, muss diese eine Signatur aufweisen, die etwa folgendem Codefragment entspricht:  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 Die Validierungsmethode kann einen beliebigen Gültigkeitsbereich haben und sollte zurückgeben **"true"** Wenn der Wert gültig ist und **"false"** andernfalls. Wenn die-Methode zurückgibt **"false"** oder eine Ausnahme auslöst, wird der Wert als behandelt ist ungültig, und es wird ein Fehler ausgelöst wird.  
  
 Im nachstehenden Beispiel lässt der Code für die X- und Y-Koordinaten nur Werte zu, die größer oder gleich Null sind.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>Einschränkungen von Validierungsmethoden  
 Der Server ruft die Validierungsmethode auf, wenn er Konvertierungen durchführt, nicht wenn Daten durch das Festlegen einzelner Eigenschaften oder mithilfe der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung INSERT eingefügt werden.  
  
 Sie müssen die Validierungsmethode explizit aufrufen, von Settern für Eigenschaften und die **analysieren** Methode, wenn die Validierungsmethode in allen Situationen ausgeführt werden soll. Dies ist keine Voraussetzung, und in einigen Fällen ist es möglicherweise nicht einmal wünschenswert.  
  
### <a name="parse-validation-example"></a>Beispiel für die Validierung in der Parse-Methode  
 Um sicherzustellen, dass die **ValidatePoint** Methode wird aufgerufen, der **Punkt** -Klasse, Sie müssen ihn aufrufen aus der **analysieren** Methode und von den Eigenschaftenprozeduren, die die X- und Y festlegen Koordinatenwerte. Das folgende Codefragment zeigt, wie die **ValidatePoint** Validierungsmethode aus der **analysieren** Funktion.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Beispiel für die Validierung von Eigenschaften  
 Das folgende Codefragment zeigt, wie die **ValidatePoint** Validierungsmethode von den Eigenschaftenprozeduren, die die X- und Y-Koordinaten festgelegt.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>Codieren von UDT-Methoden  
 Bei Codieren von UDT-Methoden müssen Sie berücksichtigen, ob sich der verwendete Algorithmus möglicherweise im Lauf der Zeit ändern könnte. Wenn dem so ist, sollten Sie erwägen, eine separate Klasse für die vom UDT verwendeten Methoden zu erstellen. Wenn sich der Algorithmus ändert, können Sie die Klasse mit dem neuen Code erneut kompilieren und die Assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] laden, ohne den UDT dadurch zu beeinflussen. In vielen Fälle können UDTs mithilfe der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung ALTER ASSEMBLY erneut geladen werden, dies könnte jedoch potenziell zu Problemen mit vorhandenen Daten führen. Z. B. die **Währung** UDT enthalten, mit der **AdventureWorks** -Beispiel Datenbank verwendet ein **ConvertCurrency** -Funktion zum Konvertieren von Währungswerten, die implementiert in einer separaten Klasse. Es ist möglich, dass sich die Konvertierungsalgorithmen in der Zukunft auf unvorhersehbare Weise ändern oder dass eine neue Funktionalität erforderlich wird. Trennen der **ConvertCurrency** -Funktion von der **Währung** UDT-Implementierung bietet größere Flexibilität bei der Planung künftiger Änderungen.  
  
### <a name="example"></a>Beispiel  
 Die **Punkt** Klasse enthält drei einfache Methoden zum Berechnen von Entfernung: **Abstand**, **DistanceFrom** und **DistanceFromXY**. Jede gibt zurück, eine **doppelte** Berechnung der Entfernung von **zeigen** auf 0 (null), der den Abstand zwischen einem angegebenen Punkt zu **zeigen**, und die Entfernung von den angegebenen X- und Y-Koordinaten um **Punkt**. **Abstand** und **DistanceFrom** bei jedem Aufruf **DistanceFromXY**, und veranschaulichen, wie Sie für jede Methode andere Argumente verwenden.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>Verwenden von SqlMethod-Attributen  
 Die **Microsoft.SqlServer.Server.SqlMethodAttribute** -Klasse stellt benutzerdefinierte Attribute, die zum Kennzeichnen von Methodendefinitionen verwendet werden können, um Determinismus, auf null Aufruf Verhalten anzugeben und um anzugeben, ob eine Methode eine Mutatormethode ist. Bei diesen Eigenschaften werden die Standardwerte vorausgesetzt, und das benutzerdefinierte Attribut wird nur verwendet, wenn ein anderer Wert als der Standardwert erforderlich ist.  
  
> [!NOTE]  
>  Die **SqlMethodAttribute** Klasse erbt von der **"SqlFunctionAttribute"** Klasse, daher **SqlMethodAttribute** erbt die **FillRowMethodName** und **TableDefinition** Felder aus **"SqlFunctionAttribute"**. Dies impliziert, dass es möglich ist, eine Tabellenwertmethode zu schreiben. Dies ist jedoch nicht der Fall. Die Methode kompiliert, und die Assembly wird bereitgestellt, aber ein Fehler über die **IEnumerable** zurück zur Laufzeit mit der folgenden Meldung ausgelöst: "Methoden-, Eigenschafts- oder Feldinformationen"\<Name > "in Klasse\<Klasse >' in Assembly "\<Assembly >' hat ungültige Rückgabetyp."  
  
 Die folgende Tabelle beschreibt einige der relevanten **Microsoft.SqlServer.Server.SqlMethodAttribute** Eigenschaften, die in UDT-Methoden verwendet werden können, und die zugehörigen Standardwerte aufgeführt.  
  
 DataAccess  
 Gibt an, ob die Funktion auf die in der lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherten Benutzerdaten zugreift. Standardmäßig wird **DataAccessKind**. **Keine**.  
  
 IsDeterministic  
 Gibt an, ob die Funktion bei denselben Eingabewerten und demselben Datenbankzustand auch immer dieselben Ausgabewerte erzeugt. Standardmäßig wird **"false"**.  
  
 IsMutator  
 Gibt an, ob die Methode eine Statusänderung in der UDT-Instanz verursacht. Standardmäßig wird **"false"**.  
  
 IsPrecise  
 Gibt an, ob die Funktion ungenaue Berechnungen beinhaltet, z. B. Gleitkommaoperationen. Standardmäßig wird **"false"**.  
  
 OnNullCall  
 Gibt an, ob die Methode aufgerufen wird, wenn als Eingabeargumente NULL-Verweise angegeben werden. Standardmäßig wird **"true"**.  
  
### <a name="example"></a>Beispiel  
 Die **Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator** -Eigenschaft können Sie eine Methode markieren, die eine Änderung in den Zustand einer Instanz eines UDTs ermöglicht. Mit [!INCLUDE[tsql](../../includes/tsql-md.md)] ist es nicht möglich, zwei UDT-Eigenschaften in der SET-Klausel einer UPDATE-Anweisung festzulegen. Sie können jedoch eine Methode als Mutator markieren, die zwei Elemente ändert.  
  
> [!NOTE]  
>  In Abfragen sind Mutatormethoden nicht zulässig. Sie können nur in Zuweisungsanweisungen oder Datenänderungsanweisungen aufgerufen werden. Wenn eine Methode markiert, als Mutator keinen zurückgibt **"void"** (oder keine **Sub** in Visual Basic), schlägt CREATE TYPE fehl.  
  
 Die folgende Anweisung setzt die Existenz des eine **Dreiecke** UDT, der verfügt über eine **Drehen** Methode. Die folgenden [!INCLUDE[tsql](../../includes/tsql-md.md)] Update-Anweisung ruft die **Drehen** Methode:  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 Die **Drehen** Methode ergänzt wird, mit der **SqlMethod** -Attribut **IsMutator** auf **"true"** , damit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können markieren die Methode als Mutatormethode. Der Code setzt auch **OnNullCall** auf **"false"**, die an den Server angibt, dass die Methode gibt einen null-Verweis zurück (**nichts** in Visual Basic), wenn die Eingabe Parameter sind null-Verweise.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>Implementieren eines UDTs mit einem benutzerdefinierten Format  
 Wenn Sie einen UDT mit einem benutzerdefinierten Format zu implementieren, müssen Sie implementieren **lesen** und **schreiben** Methoden, die zum Serialisieren von behandeln die Microsoft.SqlServer.Server.IBinarySerialize-Schnittstelle implementieren und Deserialisieren UDT-Daten. Sie müssen auch angeben, die **MaxByteSize** Eigenschaft der **Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute**.  
  
### <a name="the-currency-udt"></a>Der UDT Currency  
 Die **Währung** UDT ist im Lieferumfang der CLR-Beispiele, die installiert werden können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Die **Währung** UDT unterstützt Behandlung Datenmengen Money im Währungssystem einer bestimmten Kultur. Müssen Sie zwei Felder definieren: eine **Zeichenfolge** für **CultureInfo**, die angibt, wer die Währung ausgegeben (En-us, z. B.) und ein **decimal** für  **CurrencyValue**, des Geldbetrags.  
  
 Obwohl sie nicht vom Server, zum Durchführen von Vergleichen verwendet wird, die **Währung** UDT implementiert die **System.IComparable** -Schnittstelle, die eine einzelne Methode verfügbar macht,  **System.IComparable.CompareTo**. Diese Methode wird auf Clientseite in Situationen verwendet, in denen Currency-Werte genau verglichen oder geordnet werden sollen.  
  
 Im Code, der in der CLR ausgeführt wird, wird die Länderangabe getrennt vom Währungswert verglichen. Im [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code bestimmen die folgenden Aktionen den Vergleich:  
  
1.  Legen Sie die **IsByteOrdered** -Attribut auf "true", die mitteilt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] persistent gespeicherte binäre Darstellung auf dem Datenträger für Vergleiche zu verwenden.  
  
2.  Verwenden der **schreiben** Methode für die **Währung** UDT, um zu bestimmen, wie der UDT beibehalten wird auf dem Datenträger und daher wie UDT-Werte verglichen und sortiert zur [!INCLUDE[tsql](../../includes/tsql-md.md)] Vorgänge.  
  
3.  Speichern Sie die **Währung** UDT mit dem folgenden binären Format:  
  
    1.  Speichern Sie die Länderangabe als UTF-16-codierte Zeichenfolge für die Bytes 0 bis 19, wobei die Zeichenfolge rechts mit NULL-Zeichen aufgefüllt werden soll.  
  
    2.  Verwenden Sie Bytes 20 und nachfolgende Bytes zum Speichern des Dezimalwerts der Währungsbetrags.  
  
 Durch die Auffüllung wird gewährleistet, dass die Länderangabe vollständig vom Währungsbetrag getrennt ist, sodass beim Vergleich zweier UDT-Werte im [!INCLUDE[tsql](../../includes/tsql-md.md)]-Code jeweils die Bytes mit den Länderangaben und die Bytes mit den Währungsbeträgen miteinander verglichen werden.  
  
 Für die vollständige codeauflistung für die **Währung** UDT, führen Sie die Anleitungen zur Installation der CLR-Beispiele in [Beispiele für SQL Server Database Engine](http://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Currency-Attribute  
 Die **Währung** UDT mit den folgenden Attributen definiert ist.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>Erstellen von Read- und Write-Methoden mit IBinarySerialize  
 Bei Auswahl **UserDefined** Serialisierungsformat, außerdem müssen Sie implementieren die **IBinarySerialize** Schnittstelle, und erstellen Sie einen eigenen **lesen** und **schreiben**  Methoden. Die folgenden Prozeduren aus der **Währung** UDT verwenden die **System.IO.BinaryReader** und **System.IO.BinaryWriter** zum Lesen und Schreiben von UDT.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 Für die vollständige codeauflistung für die **Währung** UDT, finden Sie unter [Beispiele für SQL Server Database Engine](http://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines benutzerdefinierten Typs](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
