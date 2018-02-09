---
title: Einfache Microsoft OLE DB-Anbieter | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae0672fc209e2a31608a36fdef6757bef8d60cf6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Microsoft OLE DB-einfachen Anbieter (Übersicht)
Der Microsoft OLE DB-einfachen Anbieter (OSP) können auf alle Daten zugreifen, für die ein Anbieter geschrieben wurde mithilfe von, ADO der [OLE DB-einfachen Anbieter (OSP) Toolkit](http://msdn.microsoft.com/en-us/6e7b7931-9e4a-4151-ae51-672abd3f84a6). Einfache Anbieter dienen dem Zugriff auf Datenquellen, die nur grundlegende OLE DB-Unterstützung, z. B. in-Memory-Arrays oder XML-Dokumenten erforderlich ist.

## <a name="connection-string-parameters"></a>Parameter für Verbindungszeichenfolgen
 Legen Sie zur Verbindung mit der OLE DB-einfachen Anbieter-DLL der *Anbieter* Argument an die ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft, um:

```
MSDAOSP
```

 Dieser Wert kann auch festlegen oder lesen, mit der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft.

 Sie können auf einfachen Anbieter verbinden, die mit dem registrierten Anbieternamen, der bestimmt, indem die Anbieterwriter als vollständige OLE DB-Anbieter registriert wurden.

## <a name="typical-connection-string"></a>Typische Verbindungszeichenfolge
 Eine typische Verbindungszeichenfolge für diesen Anbieter ist:

```
"Provider=MSDAOSP;Data Source=serverName"
```

 Die Zeichenfolge, die dieser Schlüsselwörter besteht aus:

|Schlüsselwort|Description|
|-------------|-----------------|
|**Provider**|Gibt die OLE DB-Anbieter für SQL Server an.|
|**Datenquelle**|Gibt den Namen eines Servers.|

## <a name="xml-document-example"></a>XML-Dokument (Beispiel)
 Der OLE DB-einfachen Anbieter (OSP) in MDAC 2.7 oder höher und Windows Data Access Components (Windows DAC) wurde verbessert, um das Öffnen von hierarchischen ADO unterstützt **Recordsets** über beliebige XML-Dateien. Diese XML-Dateien können das ADO-XML-Persistenz-Schema enthalten, aber es ist nicht erforderlich. Dies wurde durch Herstellen einer Verbindung das OSP, implementiert die **"Msxml2.dll"**daher **"Msxml2.dll"** oder höher erforderlich.

 Die **portfolio.xml** -Datei verwendet, die im folgenden Beispiel enthält die folgende Struktur:

```
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 Die XML-DSO anhand der integrierten Heuristik, konvertieren die Knoten in einer XML-Struktur in Kapitel in einer hierarchischen **Recordset**.

 Verwenden diese integrierten Heuristiken, die XML-Struktur in eine hierarchische zweistufige konvertiert **Recordset** der folgenden Form:

```
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Beachten Sie, dass die Tags Portfolio und Informationen nicht in der hierarchischen dargestellt werden **Recordset**. Eine Erläuterung, wie die XML-DSO XML-Strukturen in hierarchischen konvertiert **Recordsets**, finden Sie unter den folgenden Regeln. Die Spalte $Text wird im folgenden Abschnitt erläutert.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Regeln zum Zuweisen von XML-Elementen und-Attributen zu Zeilen und Spalten
 Die XML-DSO folgt ein Verfahren zum Zuweisen von Elementen und-Attribute verwenden, um Zeilen und Spalten in datengebundenen Anwendungen. XML ist als eine Struktur mit einem Tag modelliert, die die gesamte Hierarchie enthält. Eine XML-Beschreibung eines Buchs kann z. B. Kapitel Tags, Abbildung und Abschnitt Tags enthalten. Auf der höchsten Ebene wäre das Buch-Tag, mit der Unterelemente Kapitel, Abbildung, und dem Abschnitt. Wenn die XML-DSO-XML-Elemente in Zeilen und Spalten zugeordnet werden, werden die Teilelemente fest, nicht das oberste Element konvertiert.

 Die XML-DSO greift auf dieses Verfahren zum Konvertieren von Unterelemente:

-   Jede-Unterelement und ein Attribut entspricht einer Spalte in einigen **Recordset** in der Hierarchie.

-   Der Name der Spalte ist identisch mit den Namen des Unterelements oder Attributs, es sei denn, das übergeordnete Element eines Attributs und ein Unterelement mit dem gleichen Namen in diesem Fall verfügt ein "!" wird an das Unterelement Spaltennamen vorangestellt.

-   Jede Spalte handelt es sich um eine *einfache* Spalte mit skalaren Werten (in der Regel Zeichenfolgen) oder ein **Recordset** Spalte, die untergeordnete enthält **Recordsets**.

-   Spalten, die Attribute sind stets einfach.

-   Spalten, die entspricht Teilelemente sind **Recordset** Spalten zurück, wenn das Teilelement verfügt über einen eigenen untergeordneten Elemente oder Attribute (oder beides) oder das Unterelement übergeordnetes Element mehr als eine Instanz des Unterelements als untergeordnetes Element besitzt. Andernfalls ist die Spalte einfach.

-   Wenn mehrere Instanzen des ein Unterelement (unter verschiedenen übergeordneten Elementen) vorhanden sind, wird die Spalte ist eine **Recordset** Spalte Wenn *alle* implizieren die Instanzen einer **Recordset** Spalte; die Spalte ist einfach nur, wenn *alle* Instanzen implizieren, eine einfache Spalte.

-   Alle **Recordsets** haben eine weitere Spalte namens $Text.

 Der Code, der erforderlich ist, zum Erstellen einer **Recordset** lautet wie folgt:

```
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "http://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  Der Pfad der Datendatei kann mithilfe von vier unterschiedlichen Benennungskonventionen angegeben werden.

```
'HTTP://
adoRS.Open "http://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 Sobald die **Recordset** geöffnet wurde, den übliche ADO **Recordset** Navigationsbefehle verwendet werden können.

 **Recordsets** durch das OSP generiert einige Einschränkungen:

-   Clientcursor (**AdUseClient**) werden nicht unterstützt.

-   Hierarchische **Recordsets** für beliebige erstellt XML kann nicht persistent sein mit **Recordset.Save**.

-   **Recordsets** erstellt, mit der OSP sind schreibgeschützt.

-   Die XMLDSO Fügt eine zusätzliche Spalte mit Daten ($Text) auf die einzelnen **Recordset** in der Hierarchie.

 Weitere Informationen zum OLE DB-Simple-Anbieter finden Sie unter [Erstellen eines einfachen Anbieters](http://msdn.microsoft.com/en-us/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Codebeispiel
 Die folgenden Visual Basic-Code wird veranschaulicht, öffnen eine beliebige XML-Datei, erstellen eine hierarchische **Recordset**, und jeder Datensatz für jede schreiben rekursiv **Recordset** an das Debugfenster.

 Hier ist eine einfache XML-Datei, die Aktienkurse enthält. Der folgende Code verwendet diese Datei zum Erstellen einer hierarchischen zweistufige **Recordset**.

```
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>http://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>http://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>http://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>http://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 Es folgen zwei Visual Basic-Sub-Prozeduren. Die erste erstellt die **Recordset** und übergibt es an die *WalkHier* sub-Prozedur, welche rekursiv in der Hierarchie durchläuft, Schreiben jede **Feld** in jedem Datensatz in den einzelnen **Recordset** an das Debugfenster.

```
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "http://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
