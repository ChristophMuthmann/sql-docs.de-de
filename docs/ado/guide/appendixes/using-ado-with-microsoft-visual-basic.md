---
title: Mithilfe von ADO mit Microsoft Visual Basic | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c88dbb57318fe960eab28c463b8c46a5546ffd5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Verwenden von ADO mit Microsoft Visual Basic und Visual Basic für Applikationen
Einrichten eines ADO-Projekts und Schreiben von Code für ADO gleicht gibt an, ob Sie Visual Basic oder Visual Basic für Applikationen verwenden. In diesem Thema behandelt wird, mithilfe von ADO mit Visual Basic und Visual Basic für Applikationen und Anmerkungen dieser Unterschiede.

## <a name="referencing-the-ado-library"></a>Verweis auf die ADO-Bibliothek
 Die ADO-Bibliothek muss vom Projekt verwiesen werden.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>In ADO-Verweis aus Microsoft Visual Basic

1.  In Visual Basic aus der **Projekt** klicken Sie im Menü **Verweise... **.

2.  Wählen Sie **Microsoft ActiveX Data Objects x.x Library** aus der Liste. Überprüfen Sie, dass mindestens die folgenden Bibliotheken ebenfalls ausgewählt sind:

    -   Visual Basic for Applications

    -   Visual Basic-Runtime-Objekte und Prozeduren

    -   Visual Basic-Objekte und Prozeduren

    -   OLE-Automatisierung

3.  Klicken Sie auf **OK**.

 ADO können genauso leicht mit Visual Basic für Applikationen, mit Microsoft Access, zum Beispiel.

#### <a name="to-reference-ado-from-microsoft-access"></a>In ADO-Verweis aus Microsoft Access

1.  Klicken Sie in Microsoft Access wählen, oder erstellen Sie ein Modul aus der **Module** Registerkarte der **Datenbank** Fenster.

2.  Auf der **Tools** klicken Sie im Menü **Verweise... **.

3.  Wählen Sie **Microsoft ActiveX Data Objects x.x Library** aus der Liste. Überprüfen Sie, dass mindestens die folgenden Bibliotheken ebenfalls ausgewählt sind:

    -   Visual Basic for Applications

    -   Microsoft Access 8.0-Objektbibliothek (oder höher)

    -   Microsoft DAO 3.5-Objektbibliothek (oder höher)

4.  Klicken Sie auf **OK**.

## <a name="creating-ado-objects-in-visual-basic"></a>Erstellen von ADO-Objekten in Visual Basic
 Um ein Automation-Variablen und einer Instanz eines Objekts für die Variable zu erstellen, können Sie zwei Methoden verwenden: **Dim** oder **CreateObject**.

### <a name="dim"></a>Dim
 Sie können die **neu** Schlüsselwort mit **Dim** deklarieren und Erstellen von Instanzen von ADO-Objekten in einem Schritt:

```
Dim conn As New ADODB.Connection
```

 Alternativ können Sie die **Dim** Anweisung Deklaration und Objekt Instanziierung kann auch zwei Schritte:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  Es ist nicht erforderlich, explizit mithilfe der `ADODB` progid mit der **Dim** -Anweisung, vorausgesetzt, Sie haben die ADO-Bibliothek ordnungsgemäß in Ihrem Projekt referenziert. Verwenden sie wird jedoch sichergestellt, dass Sie keinen Namenskonflikte mit anderen Bibliotheken.

> [!NOTE]
>  Angenommen, wenn Sie Verweise auf ADO und DAO im gleichen Projekt enthalten, Sie sollten enthalten einen Qualifizierer ein, um anzugeben, welche das Objektmodell verwenden, bei der Instanziierung **Recordset** Objekte, wie im folgenden Code:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 Mit der **CreateObject** -Methode, die Deklaration und das Objekt Instanziierung muss zwei separate Schritte aus:

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 Instanziieren von Objekten mit **CreateObject** sind spät gebunden, d. h., die sie nicht stark typisiert und Befehlszeilen Abschluss ist deaktiviert. Allerdings lässt zu überspringen, Verweis auf die ADO-Bibliothek aus Ihrem Projekt und ermöglicht es Ihnen, bestimmte Versionen von Objekten zu instanziieren. Beispiel:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 Sie können dies auch erreichen, indem speziell erstellen einen Verweis auf die Typbibliothek von ADO, Version 2.0, und beim Erstellen des Objekts.

 Instanziieren von Objekten mithilfe der **CreateObject** Methode ist normalerweise langsamer als die Verwendung der **Dim** Anweisung.

## <a name="handling-events"></a>Behandlung von Ereignissen
 Damit ADO-Ereignisse in Microsoft Visual Basic zu behandeln, müssen Sie deklarieren, einer auf Modulebene Variable mit dem **WithEvents** Schlüsselwort. Die Variable kann nur als Teil eines Moduls Klasse deklariert werden und muss auf der Modulebene deklariert werden. Eine ausführlichere Erläuterung zur Behandlung von ADO-Ereignisse, finden Sie unter [ADO-Ereignisse behandeln](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Visual Basic-Beispiele
 Viele Visual Basic-Beispiele sind in der ADO-Dokumentation enthalten. Weitere Informationen finden Sie unter [ADO-Codebeispiele in Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Siehe auch
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [mithilfe von ADO mit Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [mithilfe von ADO mit Skriptsprachen](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)

