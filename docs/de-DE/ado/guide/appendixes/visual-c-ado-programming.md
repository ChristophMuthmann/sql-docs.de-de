---
title: Visual C++-ADO-Programmierung | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO]
ms.assetid: 11233b96-e05c-4221-9aed-5f20944b0f1c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d884f6cdba58b8135ec2dbe4d4eeda852882a065
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="visual-c-ado-programming"></a>Visual C++-ADO-Programmierung
Die ADO-API-Referenz beschreibt die Funktionalität von der ADO-Anwendungsprogrammierschnittstelle (API) eine Microsoft Visual Basic-ähnliche Syntax verwenden. Obwohl die beabsichtigte Zielgruppe alle Benutzer ist, verwendet ADO-Programmierer verschiedene Sprachen wie Visual Basic, Visual C++ (mit und ohne die **#import** Richtlinie), und Visual J++ (mit dem Paket für den ADO/WFC-Klasse).  

> [!NOTE]
> Microsoft Support für Visual J++ 2004 endete.

 Um diese Vielfalt Rechnung zu tragen die [ADO für Visual C++-Syntaxindizes](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) bieten Visual C++ sprachspezifische Syntax mit Links zu allgemeinen Beschreibungen der Funktionen, Parameter und außergewöhnliche Verhaltensweisen sowie usw., in der API Verweis.  
  
 ADO wird mit COM (Component Object Model)-Schnittstellen implementiert. Allerdings ist es einfacher für Programmierer, die zur Bearbeitung von COM in bestimmte Programmiersprachen als andere. Beispielsweise werden nahezu alle Details der Verwendung von COM implizit für Visual Basic-Programmierer behandelt, während Visual C++-Programmierer zu diesen Details selbst kümmern müssen.  
  
 In den folgenden Abschnitten zusammengefasst Details für C- und C++-Programmierer, die mithilfe von ADO und der **#import** Richtlinie. Der Schwerpunkt liegt auf den speziellen Datentypen für COM (**Variant**, **BSTR**, und **SafeArray**), und die Fehlerbehandlung (_com_error).  
  
## <a name="using-the-import-compiler-directive"></a>Verwenden der #import-Compiler-Direktive  
 Die **#import** Visual C++-Compiler-Anweisung vereinfacht die Verwendung mit dem ADO-Methoden und Eigenschaften. Die Direktive nimmt den Namen einer Datei mit einer Typbibliothek, wie z. B. die ADO-DLL-Datei ("MSADO15.dll"), und Headerdateien mit typedef-Deklarationen, intelligente Zeiger für Schnittstellen und Enumerationskonstanten generiert. Jede Schnittstelle ist gekapselt, oder in einer Klasse umschlossen.  
  
 Für jeden Vorgang innerhalb einer Klasse (d. h. eine Methode oder Eigenschaft aufrufen) besteht eine Deklaration zum Aufrufen des Vorgangs direkt (d. h. "unformatiert" Form des Vorgangs), und eine Deklaration, um den unformatierten Vorgang aufrufen und einen COM-Fehler auslösen, wenn der Vorgang nicht Succ ausgeführt essfully. Wenn der Vorgang eine Eigenschaft ist, ist normalerweise eine Compilerdirektive, die eine alternative Syntax für den Vorgang erstellt, die Syntax wie Visual Basic besteht.  
  
 Vorgänge, die den Wert einer Eigenschaft abzurufen haben Namen im Format **abrufen *** Eigenschaft*. Vorgänge, die den Wert einer Eigenschaft festgelegt haben Namen im Format **Put *** Eigenschaft*. Vorgänge, die den Wert einer Eigenschaft mit einem Zeiger auf ein ADO-Objekt festgelegt haben Namen im Format **PutRef *** Eigenschaft*.  
  
 Sie können abrufen oder festlegen eine Eigenschaft durch Aufrufe der folgenden Formen:  
  
```  
variable = objectPtr->GetProperty(); // get property value   
objectPtr->PutProperty(value);       // set property value  
objectPtr->PutRefProperty(&value);   // set property with object pointer  
```  
  
## <a name="using-property-directives"></a>Using-Eigenschaftendirektiven  
 Die **__declspec(property...)**  Compilerdirektive ist eine Erweiterung der Microsoft-spezifischen C-Sprache, die eine Funktion, die als eine Eigenschaft verwendet, um eine alternative Syntax deklariert. Daher können Sie festlegen oder Abrufen der Werte einer Eigenschaft auf eine Weise Visual Basic ähnelt. Sie können z. B. festgelegt und eine Eigenschaft auf diese Weise abrufen:  
  
```  
objectPtr->property = value;        // set property value  
variable = objectPtr->property;     // get property value  
```  
  
 Beachten Sie, dass Sie nicht zu Code verfügen:  
  
```  
objectPtr->PutProperty(value);      // set property value  
variable = objectPtr->GetProperty;  // get property value  
```  
  
 Generiert der Compiler den entsprechenden **Get ***-*, **Put**-, oder **PutRef *** Eigenschaft* Aufruf basierend auf welche alternative Syntax deklariert wird und ob die Eigenschaft ist gelesen oder geschrieben.  
  
 Die **__declspec(property...)**  kann nur die Compilerdirektive deklarieren **abrufen**, **put**, oder **abrufen** und **put** alternative Syntax für eine Funktion. Nur schreibgeschützte Vorgänge haben eine **abrufen** Deklaration; nur-schreiben Vorgänge, die nur eine **put** -Deklaration; Vorgänge, die sind sowohl Lese-als auch haben beide **abrufen** und **put** Deklarationen.  
  
 Es sind nur zwei Deklarationen mit dieser Richtlinie möglich; Allerdings kann jede Eigenschaft drei Eigenschaftenfunktionen aufweisen: **abrufen *** Eigenschaft*, **Put *** Eigenschaft*, und **PutRef *** Eigenschaft*. In diesem Fall ist nur zwei Formen der Eigenschaft, die alternative Syntax.  
  
 Z. B. die **Befehl** Objekt **ActiveConnection** Eigenschaft wird deklariert, wobei eine alternative Syntax für **abrufen *** ActiveConnection* und **PutRef * ** ActiveConnection*. Die **PutRef**-Syntax ist eine gute Wahl, da in der Praxis, Sie in der Regel werden ein offenes aufnehmen möchten **Verbindung** Objekt (d. h. eine **Verbindung** Objektzeiger) in diesem Diese Eigenschaft. Andererseits, die **Recordset** Objekt hat **abrufen**-, **Put**-, und **PutRef *** ActiveConnection* Vorgänge, aber keine Alternative Die Syntax.  
  
## <a name="collections-the-getitem-method-and-the-item-property"></a>Sammlungen, die GetItem-Methode und die Item-Eigenschaft  
 ADO definiert mehrere Auflistungen, einschließlich **Felder**, **Parameter**, **Eigenschaften**, und **Fehler**. In Visual C++ die **GetItem (***Index***)** Methode gibt ein Element der Auflistung zurück. *Index* ist ein **Variant**, dessen Wert der wird entweder einen numerischen Index des Elements in der Auflistung oder eine Zeichenfolge, die mit dem Namen des Elements.  
  
 Die **__declspec(property...)**  Compilerdirektive deklariert die **Element** eine alternative Syntax auf jede Sammlung-Eigenschaft des grundlegenden **'GetItem()'** Methode. Die alternative Syntax eckige Klammern verwendet, und gleicht dem Verweis auf ein Array. Im Allgemeinen werden die beiden Formen wie folgt aussehen:  
  
```  
  
      collectionPtr->GetItem(index);  
collectionPtr->Item[index];  
```  
  
 Z. B. ein Feld einen Wert zuweisen einer **Recordset** Objekt, mit dem Namen ***Rs***, abgeleitet von der **Autoren** Tabelle mit den **Pubs** Datenbank. Verwenden der **Item()** aufzurufende die dritte Eigenschaft **Feld** von der **Recordset** Objekt **Felder** (Sammlungen werden indiziert aus Auflistung 0 (null); Angenommen, das dritte Feld den Namen ***Au_fname***). Rufen Sie anschließend die **Value()** Methode für die **Feld** Objekt, das einen Zeichenfolgenwert zugewiesen.  
  
 Dies kann ausgedrückt werden in Visual Basic in der folgenden vier Methoden (die letzten beiden Formen gelten nur für Visual Basic; anderen Sprachen verfügen nicht über die Entsprechungen):  
  
```  
rs.Fields.Item(2).Value = "value"  
rs.Fields.Item("au_fname").Value = "value"  
rs(2) = "value"  
rs!au_fname = "value"  
```  
  
 In Visual C++ entspricht die ersten beiden oben genannten Formulare:  
  
```  
rs->Fields->GetItem(long(2))->PutValue("value");   
rs->Fields->GetItem("au_fname")->PutValue("value");  
```  
  
 – oder – (die alternative Syntax für die **Wert** Eigenschaft wird ebenfalls angezeigt.)  
  
```  
rs->Fields->Item[long(2)]->Value = "value";  
rs->Fields->Item["au_fname"]->Value = "value";  
```  
  
 Beispiele für das Durchlaufen einer Auflistung finden Sie unter "ADO Reference" Abschnitt "ADO Sammlungen".  
  
## <a name="com-specific-data-types"></a>COM-spezifischen Datentypen  
 Im Allgemeinen haben alle Visual Basic-Datentyp, der in der ADO-API-Referenz Sie finden eine Visual C++-Entsprechung. Dazu gehören z. B. Standarddatentypen **unsigned Char** für eine Visual Basic **Byte**, **kurze** für **Ganzzahl**, und  **lange** für **lang**. Suchen in der Syntax Indexesto finden Sie, was für die Operanden des einer bestimmten Methode oder Eigenschaft benötigt wird.  
  
 Die Ausnahmen von dieser Regel werden die spezifisch für COM-Datentypen: **Variant**, **BSTR**, und **SafeArray**.  
  
### <a name="variant"></a>Variant  
 Ein **Variant** ist ein strukturierten Datentyps, die ein Wertemember und einen Datenmember des Typs enthält. Ein **Variant** kann eine Vielzahl anderer Datentypen, einschließlich einer anderen Variante, BSTR boolescher Wert, IDispatch oder IUnknown-Zeiger, Währung, Datum und usw. enthalten. COM bietet auch Methoden, die zum Vereinfachen eines Datentyps in einen anderen konvertieren.  
  
 Die **_variant_t** -Klasse kapselt und verwaltet die **Variant** -Datentyp.  
  
 Die ADO-API-Referenz besagt, dass eine Methode oder Eigenschaft Operand akzeptiert einen Wert, in der Regel bedeutet dies übergebene Wert ist eine **_variant_t**.  
  
 Mit dieser Regel wird explizit "true", wenn die **Parameter** in den Themen von der ADO-API-Referenz im Abschnitt besagt, dass ein Operand ist ein **Variant**. Eine Ausnahme ist die Dokumentation explizit besagt, dass die Operanden akzeptiert einen standard-Datentyp, wie z. B. **lange** oder **Byte**, oder eine Enumeration. Eine andere Ausnahme ist, wenn der Operand akzeptiert eine **Zeichenfolge**.  
  
### <a name="bstr"></a>BSTR  
 Ein **BSTR** (**B**rswindowsbasic **STR**Ing) ist ein strukturierte Daten-Typ, der eine Zeichenfolge und die Länge der Zeichenfolge enthält. COM stellt Methoden zum reservieren, bearbeiten und Freigeben einer **BSTR**.  
  
 Die **_bstr_t** -Klasse kapselt und verwaltet die **BSTR** -Datentyp.  
  
 Wenn die ADO-API-Referenz auf eine Methode oder Eigenschaft sagt nimmt eine **Zeichenfolge** Wert, es bedeutet, dass der Wert wird in Form von einer **_bstr_t**.  
  
### <a name="casting-variantt-and-bstrt-classes"></a>Umwandeln von _variant_t und _bstr_t-Klasse  
 Häufig ist es nicht notwendig, explizit Code eine **_variant_t** oder **_bstr_t** in einem Argument für einen Vorgang. Wenn die **_variant_t** oder **_bstr_t** -Klasse verfügt über einen Konstruktor, der dem Datentyp des Arguments übereinstimmt, generiert der Compiler den entsprechenden **_variant_t** oder **_bstr_t**.  
  
 Jedoch wenn das Argument nicht eindeutig ist, d. h. der Argumentdatentyp entspricht mehr als einen Konstruktor, müssen Sie das Argument mit dem entsprechenden Datentyp, den richtigen Konstruktor aufrufen eine Umwandlung.  
  
 Z. B. die Deklaration für die **Open** Methode ist:  
  
```  
    HRESULT Open (  
        const _variant_t & Source,  
        const _variant_t & ActiveConnection,  
        enum CursorTypeEnum CursorType,  
        enum LockTypeEnum LockType,  
        long Options );  
```  
  
 Die `ActiveConnection` Argument erfordert einen Verweis auf eine **_variant_t**, den Sie als eine Verbindungszeichenfolge oder ein Zeiger auf ein offenes codieren können **Verbindung** Objekt.  
  
 Die richtige **_variant_t** wird implizit erstellt werden, wenn Sie eine Zeichenfolge, z. B. übergeben "`DSN=pubs;uid=MyUserName;pwd=MyPassword;`", oder ein Zeiger, z. B. "`(IDispatch *) pConn`".  
  
> [!NOTE]
>  Wenn Sie ein Datenquellenanbieter, die Windows-Authentifizierung unterstützt Verbindung, müssen Sie angeben **Trusted_Connection = Yes** oder **Integrated Security = SSPI** anstelle von Benutzer-ID und Kennwort die Informationen in der Verbindungszeichenfolge angegeben.  
  
 Oder Sie können explizit code eine **_variant_t** wie z. B. mit einem Zeiger "`_variant_t((IDispatch *) pConn, true)`". Die Umwandlung `(IDispatch *)`, löst die Mehrdeutigkeit mit einem anderen Konstruktor, der einen Zeiger auf eine IUnknown-Schnittstelle akzeptiert.  
  
 Es ist entscheidend, wenn tatsächlich nur selten erwähnt, ADO eine IDispatch-Schnittstelle ist. Bei jedem muss ein Zeiger auf ein ADO-Objekt übergeben werden, als ein **Variant**, diesen Zeiger als Zeiger auf eine IDispatch-Schnittstelle umgewandelt werden muss.  
  
 Die letzte Anfrage Rückgabecodes explizit das zweite boolesche Argument des Konstruktors mit den optional, Standardwert `true`. Dieses Argument bewirkt, dass die **Variant** Konstruktor aufrufen seiner **AddRef**()-Methode, die ADO automatisch kompensiert die **_variant_t::Release()**()-Methode Wenn die ADO-Methode oder Eigenschaft aufrufen abgeschlossen ist.  
  
### <a name="safearray"></a>SafeArray  
 Ein **SafeArray** ist ein strukturierte Daten-Typ, ein Array von anderen Datentypen enthält. Ein **SafeArray** heißt *sichere* daran, dass es Informationen über die Grenzen der einzelnen Dimensionen des Arrays enthält, und den Zugriff auf Arrayelemente innerhalb dieser Grenzen schränkt.  
  
 Wenn die ADO-API-Referenz besagt, dass eine Methode oder Eigenschaft akzeptiert, oder gibt ein Array zurück, es bedeutet, dass die Methode oder Eigenschaft akzeptiert bzw. zurückgibt eine **SafeArray**, nicht systemeigenen C/C++-Arrays.  
  
 Angenommen, der zweite Parameter von der **Verbindung** Objekt **OpenSchema** Methode erfordert ein Array von **Variant** Werte. Die **Variant** Werte übergeben werden müssen, als Elemente von einer **SafeArray**, und dass **SafeArray** muss festgelegt werden, als der Wert eines anderen **Variant** . Es ist, die andere **Variant** als das zweite Argument der übergebenen **OpenSchema**.  
  
 Als weiteres Beispiel, das erste Argument der der **suchen** Methode ist ein **Variant** , dessen Wert ist ein eindimensionales **SafeArray**; jede der ersten und zweiten optionale Argumente der **AddNew** ist ein eindimensionales **SafeArray**; und der Rückgabewert von der **GetRows** Methode ist ein **Variant** , deren Wert ist ein zweidimensionales **SafeArray**.  
  
## <a name="missing-and-default-parameters"></a>Fehlende und Standardparameter  
 Visual Basic gestattet die fehlende Parameter in Methoden. Z. B. die **Recordset** Objekt **öffnen** Methode über fünf Parameter verfügt, jedoch können Sie überspringen und lassen Sie Weg nachfolgenden Parameter. Eine standardmäßige **BSTR** oder **Variant** wird je nach Datentyp des fehlenden Operanden ersetzt werden.  
  
 In C/C++-müssen alle Operanden angegeben werden. Wenn Sie einen fehlenden Parameter angeben möchten, deren Datentyp eine Zeichenfolge ist, geben Sie einen **_bstr_t** , enthält eine null-Zeichenfolge. Wenn Sie einen fehlenden Parameter angeben, dessen Datentyp, möchten eine **Variant**, geben Sie eine **_variant_t** mit einem Wert von DISP_E_PARAMNOTFOUND und einen Typ von VT_ERROR. Alternativ geben Sie die entsprechende **_variant_t** konstant, **VtMissing**, die angegeben ist, indem Sie die **#import** Richtlinie.  
  
 Drei Methoden sind Ausnahmen von der typischen Verwendung von **VtMissing**. Hierbei handelt es sich die **Execute** Methoden die **Verbindung** und **Befehl** Objekte, und die **NextRecordset** Methode von der **Recordset** Objekt. Im folgenden sind die Signaturen:  
  
```  
_RecordsetPtr <A HREF="mdmthcnnexecute.htm">Execute</A>( _bstr_t CommandText, VARIANT * RecordsAffected,   
        long Options );  // Connection  
_RecordsetPtr <A HREF="mdmthcmdexecute.htm">Execute</A>( VARIANT * RecordsAffected, VARIANT * Parameters,   
        long Options );  // Command  
_RecordsetPtr <A HREF="mdmthnextrec.htm">NextRecordset</A>( VARIANT * RecordsAffected );  // Recordset  
```  
  
 Die Parameter *RecordsAffected* und *Parameter*, sind Zeiger auf eine **Variant**. *Parameter* ist ein Eingabeparameter, der angibt, die Adresse des eine **Variant** mit einem einzelnen Parameter oder Array der Parameter, die den ausgeführte Befehl geändert werden. *RecordsAffected* ist ein Ausgabeparameter, der angibt, die Adresse einer **Variant**, wobei die Anzahl der von der Methode betroffenen Zeilen zurückgegeben wird.  
  
 In der **Befehl** Objekt **Execute** -Methode, um anzugeben, dass keine Parameter, indem Sie festlegen angegeben werden *Parameter* entweder `&vtMissing` (empfohlen) oder auf der null-Zeiger (d. h. **NULL** oder 0 (null)). Wenn *Parameter* festgelegt ist, der null-Zeiger, ersetzt die Methode intern die Entsprechung der **VtMissing**, und schließt dann den Vorgang.  
  
 In allen Methoden anzugeben, dass die Anzahl der betroffenen Datensätze nicht zurückgegeben werden sollen, können Sie durch Festlegen von *RecordsAffected* zum null-Zeiger. In diesem Fall ist der null-Zeiger nicht so viele fehlende Parameter, wie ein Hinweis, dass die Methode die Anzahl der betroffenen Datensätze verwerfen soll.  
  
 Daher ist es für diese drei Methoden, um etwas wie z. B. code gültig:  
  
```  
pConnection->Execute("commandText", NULL, adCmdText);   
pCommand->Execute(NULL, NULL, adCmdText);  
pRecordset->NextRecordset(NULL);  
```  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 In COM geben die meisten Vorgänge einen HRESULT-Rückgabecode, der angibt, ob eine Funktion wurde erfolgreich abgeschlossen. Die **#import** Richtlinie Wrappercode um jede "unformatiert" Methode oder Eigenschaft generiert und überprüft das zurückgegebene HRESULT. Wenn das HRESULT Fehler weist darauf hin, löst der Wrappercode einen COM-Fehler vom aufrufenden _com_issue_errorex() mit dem HRESULT-Rückgabecode als Argument an. COM-Fehlerobjekte abgefangen werden können, einem **versuchen**-**catch** Block. (Aus Gründen der Effizienz catch einen Verweis auf eine **_com_error** Objekt.)  
  
 Beachten Sie, dass dies die ADO-Fehler sind: von der ADO-Vorgangsfehler führt. Der zugrunde liegende Anbieter zurückgegebene Fehler werden als **Fehler** Objekte in der **Verbindung** Objekt **Fehler** Auflistung.  
  
 Die **#import** Richtlinie erstellt nur Fehler Ereignisbehandlungsroutinen für Methoden und Eigenschaften, die in der ADO-DLL deklariert. Allerdings können Sie dieses gleiche Fehlerbehandlungsmechanismus durch Schreiben von eigenen fehlerüberprüfung-Makro oder zur Inlinefunktion nutzen. Finden Sie im Thema [Visual C++-Erweiterungen](../../../ado/guide/appendixes/visual-c-extensions-for-ado.md), oder den Code in den folgenden Abschnitten Beispiele.  
  
## <a name="visual-c-equivalents-of-visual-basic-conventions"></a>Visual C++-Entsprechungen von VB-Konventionen  
 Im folgenden wird ein Überblick über verschiedene Konventionen in der ADO-Dokumentation in Visual Basic sowie ihre Entsprechungen in Visual C++ codiert.  
  
### <a name="declaring-an-ado-object"></a>Deklarieren Sie ein ADO-Objekt  
 In Visual Basic eine ADO-Objektvariable (in diesem Fall für einen **Recordset** Objekt) wie folgt deklariert:  
  
```  
Dim rst As ADODB.Recordset  
```  
  
 Die Klausel "`ADODB.Recordset`", ist die ProgID des der **Recordset** in der Registrierung definiert sind. Eine neue Instanz der eine **Datensatz** Objekt wie folgt deklariert:  
  
```  
Dim rst As New ADODB.Recordset  
```  
  
 -oder-  
  
```  
Dim rst As ADODB.Recordset  
Set rst = New ADODB.Recordset  
```  
  
 In Visual C++ die **#import** -Direktive generiert intelligenten Zeigertyp Deklarationen für die ADO-Objekten. Angenommen, eine Variable, die auf zeigt eine **_Recordset** Objekt ist vom Typ **_RecordsetPtr**, und wie folgt deklariert:  
  
```  
_RecordsetPtr  rs;  
```  
  
 Eine Variable, die auf eine neue Instanz der verweist eine **_Recordset** Objekt wie folgt deklariert:  
  
```  
_RecordsetPtr  rs("ADODB.Recordset");  
```  
  
 -oder-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance("ADODB.Recordset");  
```  
  
 -oder-  
  
```  
_RecordsetPtr  rs;  
rs.CreateInstance(__uuidof(_Recordset));  
```  
  
 Nach der **CreateInstance** -Methode aufgerufen wird, die Variable kann wie folgt verwendet:  
  
```  
rs->Open(...);  
```  
  
 Beachten Sie, dass in einem Fall ist die "`.`"-Operator wird verwendet, als wären die Variable eine Instanz einer Klasse (`rs.CreateInstance`), und in einem anderen Fall der "`->`"-Operator wird verwendet, als wären die Variable ein Zeiger auf eine Schnittstelle (`rs->Open`).  
  
 Eine Variable kann auf zwei Arten verwendet werden, da die "`->`"-Operator ist überladen, sodass um eine Instanz einer Klasse, verhält sich wie ein Zeiger auf eine Schnittstelle zu ermöglichen. Mitglied private Klasse die Instanzvariable enthält einen Zeiger auf die **_Recordset** Schnittstelle; die "`->`" Operator gibt diesen Zeiger; und der zurückgegebene Zeiger greift auf die Mitglieder der **_Recordset**  Objekt.  
  
### <a name="coding-a-missing-parameter--string"></a>Codieren eines fehlenden Parameters – Zeichenfolge  
 Wenn Sie einen fehlenden code müssen **Zeichenfolge** Operanden in Visual Basic, lassen Sie lediglich den Operanden. Sie müssen den Operanden in Visual C++ angeben. Code eine **_bstr_t** , eine leere Zeichenfolge als Wert besitzt.  
  
```  
_bstr_t strMissing(L"");  
```  
  
### <a name="coding-a-missing-parameter--variant"></a>Codieren eines fehlenden Parameters – Variant  
 Wenn Sie einen fehlenden code müssen **Variant** Operanden in Visual Basic, lassen Sie lediglich den Operanden. Sie müssen alle Operanden in Visual C++ angeben. Codieren eines fehlenden **Variant** Parameter mit einem **_variant_t** auf den Spezialwert, die DISP_E_PARAMNOTFOUND und den Typ VT_ERROR festgelegt. Geben Sie alternativ **VtMissing**, die ist eine entsprechende vordefinierte Konstante angegeben, durch die **#import** Richtlinie.  
  
```  
_variant_t  vtMissingYours(DISP_E_PARAMNOTFOUND, VT_ERROR);   
```  
  
 - oder -  
  
```  
...vtMissing...;  
```  
  
### <a name="declaring-a-variant"></a>Deklarieren Sie eine Variante  
 In Visual Basic ein **Variant** wird deklariert, mit der **Dim** Anweisung wie folgt:  
  
```  
Dim VariableName As Variant  
```  
  
 Deklarieren Sie in Visual C++ eine Variable als Typ **_variant_t**. Einige schematische Darstellung **_variant_t** Deklarationen sind unten aufgeführt.  
  
> [!NOTE]
>  Diese Deklarationen geben lediglich eine ungefähre Vorstellung davon, was Sie in der eigenen Anwendung code würde. Weitere Informationen finden Sie unter den Beispielen unten, und der Visual C++-Dokumentation.  
  
```  
_variant_t  VariableName(value);  
_variant_t  VariableName((data type cast) value);  
_variant_t  VariableName(value, VT_DATATYPE);  
_variant_t  VariableName(interface * value, bool fAddRef = true);  
```  
  
### <a name="using-arrays-of-variants"></a>Verwenden von Arrays von Varianten  
 In Visual Basic, Arrays von **Varianten** codiert werden können, mit der **Dim** -Anweisung, oder Sie können die **Array** -Funktion, wie im folgenden Beispielcode gezeigt:  
  
```  
Public Sub ArrayOfVariants  
Dim cn As ADODB.Connection  
Dim rs As ADODB.Recordset  
Dim fld As ADODB.Field  
  
    cn.Open "DSN=pubs"  
    rs = cn.OpenSchema(adSchemaColumns, _  
        Array(Empty, Empty, "authors", Empty))  
    For Each fld in rs.Fields  
        Debug.Print "Name = "; fld.Name  
    Next fld  
    rs.Close  
    cn.Close  
End Sub  
```  
  
 Im folgende Visual C++-Beispiel veranschaulicht die Verwendung einer **SafeArray** mit verwendet eine **_variant_t**.  
  
#### <a name="notes"></a>Hinweise  
 Die folgenden Hinweise entsprechen kommentierten Abschnitten im Codebeispiel.  
  
1.  Noch einmal: wird TESTHR() Inlinefunktion definiert, um die vorhandenen Fehlerbehandlungsmechanismus nutzen.  
  
2.  Sie brauchen nur ein eindimensionales Array, sodass Sie verwenden können **SafeArrayCreateVector**, anstatt das allgemeine **SAFEARRAYBOUND** Deklaration und **SafeArrayCreate** Funktion. Im folgenden finden Sie diesen Code mit aussehen würde **SafeArrayCreate**:  
  
    ```  
       SAFEARRAYBOUND   sabound[1];  
       sabound[0].lLbound = 0;  
       sabound[0].cElements = 4;  
       pSa = SafeArrayCreate(VT_VARIANT, 1, sabound);  
    ```  
  
3.  Das Schema der Enumerationskonstante identifizierten **AdSchemaColumns**, bezieht sich auf vier Einschränkungsspalten: TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME und COLUMN_NAME. Aus diesem Grund wird ein Array von **Variant** Werte mit vier Elementen erstellt wird. Anschließend wird ein Einschränkungswert, der dritten Spalte, TABLE_NAME, entspricht, angegeben.  
  
     Die **Recordset** zurückgegeben wird, besteht aus mehreren Spalten, die eine Teilmenge der besteht aus den Einschränkungsspalten. Die Werte der Einschränkungsspalten für jede zurückgegebene Zeile müssen es sich um die entsprechenden Einschränkungswerte identisch sein.  
  
4.  Die vertraute **SAFEARRAY** möglicherweise überrascht es, dass **SafeArrayDestroy**() wird nicht aufgerufen, bevor das Beenden. In der Tat Aufrufen **SafeArrayDestroy**() in diesem Fall führt dazu, dass eine Laufzeitausnahme. Der Grund ist, dass der Destruktor für `vtCriteria` angerufen **VariantClear**() Wenn die **_variant_t** verlässt den Bereich, der frei wird, die **SafeArray**. Aufrufen von **SafeArrayDestroy**, ohne manuellen Löschen der **_variant_t**, würde dazu führen, dass den Destruktor zu dem Versuch, eine ungültige deaktivieren **SafeArray** Zeiger.  
  
     Wenn **SafeArrayDestroy** wurden aufgerufen wird, würde der Code wie folgt aussehen:  
  
    ```  
          TESTHR(SafeArrayDestroy(pSa));  
       vtCriteria.vt = VT_EMPTY;  
          vtCriteria.parray = NULL;  
    ```  
  
     Allerdings ist es viel einfacher, lassen Sie die **_variant_t** verwalten die **SafeArray**.  
  
```  
// Visual_CPP_ADO_Prog_1.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// Note 1  
inline void TESTHR( HRESULT _hr ) {   
   if FAILED(_hr)   
      _com_issue_error(_hr);   
}  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      _ConnectionPtr pCn("ADODB.Connection");  
      _variant_t vtTableName("authors"), vtCriteria;  
      long ix[1];  
      SAFEARRAY *pSa = NULL;  
  
      pCn->Provider = "sqloledb";  
      pCn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
      // Note 2, Note 3  
      pSa = SafeArrayCreateVector(VT_VARIANT, 1, 4);  
      if (!pSa)   
         _com_issue_error(E_OUTOFMEMORY);  
  
      // Specify TABLE_NAME in the third array element (index of 2).   
      ix[0] = 2;        
      TESTHR(SafeArrayPutElement(pSa, ix, &vtTableName));  
  
      // There is no Variant constructor for a SafeArray, so manually set the   
      // type (SafeArray of Variant) and value (pointer to a SafeArray).  
  
      vtCriteria.vt = VT_ARRAY | VT_VARIANT;  
      vtCriteria.parray = pSa;  
  
      pRs = pCn->OpenSchema(adSchemaColumns, vtCriteria, vtMissing);  
  
      long limit = pRs->GetFields()->Count;  
      for ( long x = 0 ; x < limit ; x++ )  
         printf( "%d: %s\n", x + 1, ((char*) pRs->GetFields()->Item[x]->Name) );  
      // Note 4  
      pRs->Close();  
      pCn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Code meaning = %s\n", (char*) e.ErrorMessage());  
      printf("Source = %s\n", (char*) e.Source());  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   CoUninitialize();  
}  
```  
  
### <a name="using-property-getputputref"></a>Mithilfe der Eigenschaft Get/Put/PutRef  
 In Visual Basic ist der Name einer Eigenschaft nicht qualifiziert, gibt an, ob es abgerufen, zugewiesen oder ein Verweis zugewiesen wird.  
  
```  
Public Sub GetPutPutRef  
Dim rs As New ADODB.Recordset  
Dim cn As New ADODB.Connection  
Dim sz as Integer  
cn.Open "Provider=sqloledb;Data Source=yourserver;" & _  
         "Initial Catalog=pubs;Integrated Security=SSPI;"  
rs.PageSize = 10  
sz = rs.PageSize  
rs.ActiveConnection = cn  
rs.Open "authors",,adOpenStatic  
' ...  
rs.Close  
cn.Close  
End Sub  
```  
  
 Dieses Visual C++-Beispiel zeigt die **abrufen**/**Put**/**PutRef *** Eigenschaft*.  
  
#### <a name="notes"></a>Hinweise  
 Die folgenden Hinweise entsprechen kommentierten Abschnitten im Codebeispiel.  
  
1.  Dieses Beispiel verwendet zwei Arten von fehlenden Zeichenfolgenargument: eine explizite Konstante **StrMissing**, und eine Zeichenfolge, die der Compiler zum Erstellen eines temporären verwendet **_bstr_t** ist, die für den Rahmen der vorhanden **Open** Methode.  
  
2.  Es ist nicht notwendig, die der Operand des umgewandelt `rs->PutRefActiveConnection(cn)` auf `(IDispatch *)` da der Datentyp des Operanden bereits `(IDispatch *)`.  
  
```  
// Visual_CPP_ado_prog_2.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _bstr_t strMissing(L"");  
      long oldPgSz = 0, newPgSz = 5;  
  
      // Note 1  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", strMissing, "", adConnectUnspecified);  
  
      oldPgSz = rs->GetPageSize();  
      // -or-  
      // oldPgSz = rs->PageSize;  
  
      rs->PutPageSize(newPgSz);  
      // -or-  
      // rs->PageSize = newPgSz;  
  
      // Note 2  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockReadOnly, adCmdTable);  
      printf("Original pagesize = %d, new pagesize = %d\n", oldPgSz, rs->GetPageSize());  
      rs->Close();  
      cn->Close();  
  
   }  
   catch (_com_error &e) {  
      printf("Description = %s\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```  
  
### <a name="using-getitemx-and-itemx"></a>Verwenden von GetItem(x)"und Element [X]  
 Diese Visual Basic-Beispiel veranschaulicht die Standard- und alternative Syntax für **Element**().  
  
```  
Public Sub GetItemItem  
Dim rs As New ADODB.Recordset  
Dim name as String  
rs = rs.Open "authors", "DSN=pubs;", adOpenDynamic, _  
         adLockBatchOptimistic, adTable  
name = rs(0)  
' -or-  
name = rs.Fields.Item(0)  
rs(0) = "Test"  
rs.UpdateBatch  
' Restore name  
rs(0) = name  
rs.UpdateBatch  
rs.Close  
End Sub  
```  
  
 Dieses Visual C++-Beispiel zeigt **Element**.  
  
> [!NOTE]
>  Der folgende Hinweis entspricht kommentierten Abschnitten im Codebeispiel wird: Wenn die Auflistung zugegriffen wird, mit **Element**, den Index **2**, umgewandelt werden muss, um **lange** damit ein geeignete Konstruktor wird aufgerufen.  
  
```  
// Visual_CPP_ado_prog_3.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
void main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr cn("ADODB.Connection");  
      _RecordsetPtr rs("ADODB.Recordset");  
      _variant_t vtFirstName;  
  
      cn->Provider = "sqloledb";  
      cn->Open("Data Source='(local)';Initial Catalog=pubs;Integrated Security=SSPI;", "", "", adConnectUnspecified);  
  
      rs->PutRefActiveConnection( cn );  
      rs->Open("authors", vtMissing, adOpenStatic, adLockOptimistic, adCmdTable);  
      rs->MoveFirst();  
  
      // Note 1. Get a field.  
      vtFirstName = rs->Fields->GetItem((long)2)->GetValue();  
      // -or-  
      vtFirstName = rs->Fields->Item[(long)2]->Value;  
  
      printf( "First name = '%s'\n", (char*)( (_bstr_t)vtFirstName) );  
  
      rs->Fields->GetItem((long)2)->Value = L"TEST";  
      rs->Update(vtMissing, vtMissing);  
  
      // Restore name  
      rs->Fields->GetItem((long)2)->PutValue(vtFirstName);  
      // -or-  
      rs->Fields->GetItem((long)2)->Value = vtFirstName;  
      rs->Update(vtMissing, vtMissing);  
      rs->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }  
   ::CoUninitialize();  
}  
```  
  
### <a name="casting-ado-object-pointers-with-idispatch-"></a>Umwandeln von Objektzeigern mit ADO (IDispatch *)  
 Im folgende Visual C++-Beispiel veranschaulicht die Verwendung (IDispatch *), ADO-Objektzeigern Umwandlung.  
  
#### <a name="notes"></a>Hinweise  
 Die folgenden Hinweise entsprechen kommentierten Abschnitten im Codebeispiel.  
  
1.  Geben Sie ein offenes **Verbindung** Objekt in einen codierten explizit **Variant**. Wandeln sie mit (IDispatch \*), damit der richtige Konstruktor aufgerufen wird. Auch explizit festgelegt, die zweite **_variant_t** Parameter auf den Standardwert des **"true"**, sodass den Verweiszählerwert des Objekts richtig, wenn ausgeführt wird die **Open** Vorgang wird beendet.  
  
2.  Der Ausdruck `(_bstr_t)`, wird nicht umgewandelt, aber ein **_variant_t** -Operator, extrahiert eine **_bstr_t** die Zeichenfolge, aus der **Variant** zurückgegebenes **Wert** .  
  
 Der Ausdruck `(char*)`, wird nicht umgewandelt, aber ein **_bstr_t** Operator, der einen Zeiger auf die gekapselte Zeichenfolge in extrahiert eine **_bstr_t** Objekt.  
  
 In diesem Abschnitt des Codes veranschaulicht einige nützliche Verhaltensweisen von **_variant_t** und **_bstr_t** Operatoren.  
  
```  
// Visual_CPP_ado_prog_4.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
int main() {  
   CoInitialize(NULL);  
   try {  
      _ConnectionPtr pConn("ADODB.Connection");  
      _RecordsetPtr pRst("ADODB.Recordset");  
  
      pConn->Provider = "sqloledb";  
      pConn->Open("Data Source='(local)';Initial Catalog='pubs';Integrated Security=SSPI", "", "", adConnectUnspecified);  
  
      // Note 1.  
      pRst->Open("authors", _variant_t((IDispatch *) pConn, true), adOpenStatic, adLockReadOnly, adCmdTable);  
      pRst->MoveLast();  
  
      // Note 2.  
      printf("Last name is '%s %s'\n",   
         (char*) ((_bstr_t) pRst->GetFields()->GetItem("au_fname")->GetValue()),  
         (char*) ((_bstr_t) pRst->Fields->Item["au_lname"]->Value));  
  
      pRst->Close();  
      pConn->Close();  
   }  
   catch (_com_error &e) {  
      printf("Description = '%s'\n", (char*) e.Description());  
   }     
   ::CoUninitialize();  
}  
```
