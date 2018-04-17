---
title: CLR-Skalarwertfunktionen | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
caps.latest.revision: 81
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 250b86d882caab50c5c7862ee55c358f4ff06c2e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="clr-scalar-valued-functions"></a>CLR-Skalarwertfunktionen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Eine Skalarwertfunktion gibt einen einzelnen Wert wie eine Zeichenfolge, eine ganze Zahl oder einen Bitwert zurück. Außerdem können Sie mithilfe einer beliebigen .NET Framework-Programmiersprache benutzerdefinierte Skalarwertfunktionen in verwaltetem Code erstellen. Auf diese Funktionen kann über [!INCLUDE[tsql](../../includes/tsql-md.md)] oder anderen verwalteten Code zugegriffen werden. Weitere Informationen zu den Vorteilen von CLR-Integration und Auswählen zwischen verwaltetem Code und [!INCLUDE[tsql](../../includes/tsql-md.md)], finden Sie unter [Overview of CLR Integration](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>Anforderungen für CLR-Skalarwertfunktionen  
 .NET Framework-Skalarwertfunktionen werden als Methoden einer Klasse in einer .NET Framework-Assembly implementiert. Die Eingabeparameter und der Rückgabetyp einer Skalarwertfunktion kann eine der skalaren Datentypen von unterstützten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mit Ausnahme von **Varchar**, **Char**, **Rowversion**, **Text**, **Ntext**, **Image**, **Zeitstempel**, **Tabelle**, oder **Cursor** . Skalarwertfunktionen müssen sicherstellen, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentyp und der Rückgabedatentyp der Implementierungsmethode übereinstimmen. Weitere Informationen zu typkonvertierungen finden Sie unter [Zuordnen von CLR-Parameterdaten](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Bei der Implementierung einer .NET Framework-Skalarwertfunktion in eine .NET Framework-Sprache, die **SqlFunction** benutzerdefiniertes Attribut angegeben werden, um zusätzliche Informationen zur Funktion enthalten. Die **SqlFunction** Attribut gibt an, ob die Funktion greift auf oder Daten verändert, ob sie deterministisch ist, und wenn die Funktion gleitkommaberechnungen beinhaltet.  
  
 Benutzerdefinierte Skalarwertfunktionen können deterministisch oder nicht deterministisch sein. Eine deterministische Funktion gibt immer dieselben Ergebnisse zurück, wenn sie mit einem bestimmten Satz an Eingabeparametern aufgerufen wird. Eine nicht deterministische Funktion kann unterschiedliche Ergebnisse zurückgeben, wenn sie mit einem bestimmten Satz an Eingabeparametern aufgerufen wird.  
  
> [!NOTE]  
>  Markieren Sie eine benutzerdefinierte Funktion nicht als deterministisch, wenn die Funktion bei denselben Eingabewerten und demselben Datenbankzustand nicht immer dieselben Ausgabewerte erzeugt. Markieren eine Funktion als deterministisch, kann Wenn die Funktion nicht wirklich deterministisch ist zu beschädigten indizierten Sichten und berechneten Spalten führen. Sie eine Funktion als deterministisch markieren, durch Festlegen der **IsDeterministic** Eigenschaft auf "true".  
  
### <a name="table-valued-parameters"></a>Tabellenwertparameter  
 Tabellenwertparameter (Table Valued Parameters, TVPs), benutzerdefinierte Tabellentypen, die an eine Prozedur oder Funktion übergeben werden, bieten eine effiziente Methode zum Übergeben mehrerer Datenzeilen an den Server. TVPs verfügen über eine ähnliche Funktionalität wie Parameterarrays, bieten aber größere Flexibilität und engere Integration mit [!INCLUDE[tsql](../../includes/tsql-md.md)]. Außerdem verfügen sie auch über ein besseres Leistungspotenzial. TVPs helfen auch, die Anzahl von Roundtrips zum Server zu reduzieren. Anstatt mehrere Anforderungen an den Server zu senden, z. B. mit einer Liste von skalaren Parametern, können Daten als TVP an den Server gesendet werden. Ein benutzerdefinierter Tabellentyp kann nicht als Tabellenwertparameter an eine verwaltete gespeicherte Prozedur oder Funktion übergeben werden, die im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Prozess ausgeführt wird, oder von einer solchen Prozedur oder Funktion zurückgegeben werden. Weitere Informationen zu TVPs finden Sie unter [Tabellenwertparametern & #40; Datenbankmodul & #41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>Beispiel für eine CLR-Skalarwertfunktion  
 Es folgt eine einfache Skalarwertfunktion, die auf Daten zugreift und einen ganzzahligen Wert zurückgibt:  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 Die erste Codezeile verweist auf **Microsoft.SqlServer.Server** um auf Attribute zuzugreifen und **System.Data.SqlClient** auf den ADO.NET-Namespace zuzugreifen. (Dieser Namespace enthält **SqlClient**, die .NET Framework-Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
 Als Nächstes die Funktion empfängt die **SqlFunction** benutzerdefiniertes Attribut, die im ist die **Microsoft.SqlServer.Server** Namespace. Das benutzerdefinierte Attribut gibt an, ob die benutzerdefinierte Funktion (UDF) den prozessinternen Anbieter verwendet, um Daten im Server zu lesen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lässt nicht zu, dass UDFs Daten aktualisieren, einfügen oder löschen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann die Ausführung einer UDF optimieren, die den prozessinternen Anbieter nicht verwendet. Dies wird durch Festlegen von angegeben **DataAccessKind** auf **DataAccessKind.None**. Die Zielmethode in der nächsten Zeile ist eine öffentliche statische Methode (shared in Visual Basic .NET).  
  
 Die **SqlContext** Klasse, die der **Microsoft.SqlServer.Server** Namespace kann zugegriffen werden eine **"SqlCommand"** Objekt eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Instanz, die bereits eingerichtet wurde. Obwohl hier nicht verwendet, ist der aktuelle Transaktionskontext auch verfügbar durch die **System.Transactions** -Anwendungsprogrammierschnittstelle (API).  
  
 Die meisten Codezeilen im Funktionsrumpf aussehen vertraut für Entwickler, die Clientanwendungen geschrieben haben, verwendet werden, die Typen aus, den **System.Data.SqlClient** Namespace.  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 Der entsprechende Befehlstext wird angegeben, durch die Initialisierung der **"SqlCommand"** Objekt. Im vorherige Beispiel zählt die Anzahl der Zeilen in Tabelle **SalesOrderHeader**. Als Nächstes wird die **ExecuteScalar** Methode der **Cmd** -Objekts aufgerufen wird. Dies gibt einen Wert vom Typ **Int** basierend auf der Abfrage. Abschließend wird die Anzahl der Bestellungen an den Aufrufer zurückgegeben.  
  
 Wenn dieser Code in einer Datei namens FirstUdf.cs gespeichert wird, kann er wie folgt als Assembly kompiliert werden:  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library` gibt an, dass eine Bibliothek und keine ausführbare Datei erzeugt werden soll. Ausführbare Dateien können nicht in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert werden.  
  
> [!NOTE]  
>  Visual C++-Datenbankobjekte mit kompiliert **/CLR: pure** können nicht für die Ausführung auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Zu solchen Datenbankobjekten gehören beispielsweise Skalarwertfunktionen.  
  
 Die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Abfrage und ein Beispielaufruf zum Registrieren der Assembly und der UDF folgen:  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 Beachten Sie, dass der Funktionsname, der in [!INCLUDE[tsql](../../includes/tsql-md.md)] angegeben wird, nicht mit dem Namen der öffentlichen statischen Zielmethode übereinstimmen muss.  
  
## <a name="see-also"></a>Siehe auch  
 [Zuordnen von CLR-Parameterdaten](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [Übersicht über benutzerdefinierte Attribute von CLR-Integration](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [Benutzerdefinierte Funktionen](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [Datenzugriff von CLR-Datenbankobjekten aus](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
