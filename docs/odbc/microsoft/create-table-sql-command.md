---
title: Erstellen der Tabelle - SQL-Befehl | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 35a22420b5ecaf21539fd16aecb3870e3f3049dc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="create-table---sql-command"></a>Erstellen der Tabelle - SQL-Befehl
Erstellt eine Tabelle mit den angegebenen Feldern.  
  
 Der Visual FoxPro-ODBC-Treiber unterstützt die systemeigene Visual FoxPro-Sprachsyntax für diesen Befehl an. Treiberspezifische Informationen finden Sie unter **Treiber "Hinweise"**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>Argumente  
 Erstellen von Tabellen &#124; DBF *TableName1*  
 Gibt den Namen der Tabelle zu erstellen. Die Tabelle und die DBF-Optionen sind identisch.  
  
 Namen *LongTableName*  
 Gibt einen langen Namen für die Tabelle. Eine lange Tabellenname kann angegeben werden, nur wenn eine Datenbank geöffnet wird, da lange Tabellennamen, Spaltennamen in Datenbanken gespeichert werden.  
  
 Lange Namen können bis zu 128 Zeichen enthalten und können anstelle von kurzen Dateinamen in der Datenbank verwendet werden.  
  
 KOSTENLOS  
 Gibt an, dass die Tabelle eine geöffnete Datenbank nicht hinzugefügt werden. KOSTENLOS ist nicht erforderlich, wenn eine Datenbank nicht geöffnet ist.  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [, *nPrecision*])]  
 Gibt an die Feldnamen, Feldtyp, Feldbreite und Feld Genauigkeit (Anzahl von Dezimalstellen an).  
  
 *FieldType* ist ein einzelner Buchstabe, der angibt, in des Felds [Datentyp](../../odbc/microsoft/visual-foxpro-field-data-types.md). Einige Felddatentypen erfordern die Angabe *nFieldWidth* oder *nPrecision* oder beides.  
  
 *nFieldWidth* und *nPrecision* D, G, I, L, M, P, T und Y werden ignoriert Typen. *nPrecision* standardmäßig auf 0 (null) (ohne Dezimalstellen) an, wenn *nPrecision* ist nicht für die B, F oder N-Typen enthalten.  
  
 NULL  
 Null-Werte in das Feld zulässt.  
  
 NOT NULL  
 Verhindert, dass null-Werte in das Feld.  
  
 Wenn Sie, NULL weglassen und NOT NULL, bestimmt die aktuelle Einstellung von SET NULL an, ob in das Feld null-Werte zulässig sind. Jedoch wenn Sie, NULL weglassen und NOT NULL und die PRIMARY KEY- oder UNIQUE-Klausel enthalten, die aktuelle Einstellung von SET NULL ignoriert, und das Feld ist standardmäßig auf NOT NULL.  
  
 Überprüfen Sie *lExpression1*  
 Gibt eine Überprüfungsregel für das Feld. *lExpression1* kann eine benutzerdefinierte Funktion sein. Wenn ein leerer Datensatz angefügt wird, wird die Validierungsregel überprüft. Ein Fehler wird generiert, wenn die Überprüfungsregel für ein leeres Feldwert in eine angefügte Datensatz nicht zugelassen wird.  
  
 Fehler beim *cMessageText1*  
 Gibt die Fehlermeldung Visual FoxPro angezeigt werden soll, wenn die Feldregel einen Fehler generiert. Die Nachricht wird nur angezeigt, wenn Daten in einem Durchsuchen-Fenster oder ein Fenster "Bearbeiten" geändert werden.  
  
 Standard *eExpression1*  
 Gibt einen Standardwert für das Feld an. Der Datentyp des *eExpression1* müssen der Datentyp des Felds identisch sein.  
  
 PRIMARY KEY  
 Erstellt einen primären Index für das Feld. Der Primärindex Tag hat den gleichen Namen wie das Feld ein.  
  
 UNIQUE  
 Erstellt einen Index Kandidat für das Feld. Der Indexname Candidate hat den gleichen Namen wie das Feld ein.  
  
> [!NOTE]  
>  Kandidat Indizes (erstellt durch Einschließen der EINDEUTIGEN Option in CREATE TABLE- oder ALTER TABLE - SQL) sind nicht identisch mit Indizes, die mit der EINDEUTIGEN Option in den Befehl "INDEX" erstellt. Ein Index erstellt, mit der EINDEUTIGEN-Option in den INDEX-Befehl kann doppelte Indexschlüssel. Doppelte Indexschlüssel zulassen kandidatenindizes nicht. Finden Sie unter [INDEX](../../odbc/microsoft/index-command.md) zusätzliche Informationen zu dessen EINDEUTIGER Option.  
  
 NULL-Werte und Duplikate sind nicht in eines Felds, das für einen primären oder Kandidatenschlüssel Index zulässig. Visual FoxPro generiert jedoch keinen Fehler, wenn Sie einen primären oder Kandidatenschlüssel Index für ein Feld erstellen, die null-Werte unterstützt werden. Visual FoxPro generiert einen Fehler aus, wenn Sie versuchen, geben Sie null oder einen doppelten Wert in ein Feld für einen primären oder Kandidatenschlüssel Index verwendet.  
  
 Verweise *TableName2*[TAG *TagName1*]  
 Gibt die übergeordnete Tabelle mit der eine persistente Beziehung hergestellt wird. Wenn Sie-Tag weglassen *TagName1*, die Beziehung besteht, mit dem Schlüssel primären Index der übergeordneten Tabelle erstellt. Wenn die übergeordneten Tabelle nicht über einen primären Index verfügt, generiert Visual FoxPro einen Fehler aus.  
  
 Include (Tag) *TagName1* zum Herstellen einer Beziehungs auf Grundlage einer vorhandenen Index Tags für die übergeordnete Tabelle. Index-Tagnamen können bis zu 10 Zeichen enthalten.  
  
 Die übergeordneten Tabelle darf nicht auf eine freie Tabelle sein.  
  
 NOCPTRANS  
 Verhindert die Übersetzung in eine andere Codepage für Zeichen und Memo-Felder. Wenn die Tabelle in einer anderen Codepage konvertiert wird, werden die Felder für die NOCPTRANS angegeben wurde nicht übersetzt. NOCPTRANS können nur für Zeichen- und Memo Felder angegeben werden.  
  
 Das folgende Beispiel erstellt eine Tabelle namens Mytable, zwei Zeichenfelder und zwei Memofelder enthält. Die zweite Zeichenfeld, char2 und das zweite Memofeld memo2, umfassen NOCPTRANS, um zu verhindern, dass bei der Übersetzung.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 PRIMÄRSCHLÜSSEL *eExpression2* TAG *TagName2*  
 Gibt einen primären Index zu erstellen. *eExpression2* gibt ein Feld oder eine Kombination von Feldern in der Tabelle. TAG *TagName2 s*gibt den Namen für den primären Index Transponder, die erstellt wird. Index-Tagnamen können bis zu 10 Zeichen enthalten.  
  
 Da eine Tabelle nur einen primären Index aufweisen darf, können nicht Sie diese Klausel einschließen, wenn Sie einen primären Index für ein Feld bereits erstellt haben. Visual FoxPro generiert einen Fehler, wenn Sie mehr als eine PRIMARY KEY-Klausel in CREATE TABLE.  
  
 EINDEUTIGE *eExpression3*TAG *TagName3*  
 Erstellt einen Index geeignet. *eExpression3* gibt ein Feld oder eine Kombination von Feldern in der Tabelle. Wenn Sie einen primären Index mit einem der PRIMARY KEY-Optionen erstellt haben, können nicht Sie das Feld einschließen, das für den primären Index angegeben wurde. TAG *TagName3 s*gibt einen Tagnamen für die Kandidaten-Indexname, die erstellt wird. Index-Tagnamen können bis zu 10 Zeichen enthalten.  
  
 Eine Tabelle kann mehrere mögliche Indizes enthalten.  
  
 FREMDSCHLÜSSEL *eExpression4*TAG *TagName4*[NODUP]  
 Erstellt einen Fremdschlüssel (nicht primäre) Index und stellt eine Beziehung zu einer übergeordneten Tabelle her. *eExpression4* gibt an, die foreign Key Indexausdruck, und *TagName4* gibt den Namen der foreign Key Indexname, die erstellt wird*.* Index-Tagnamen können bis zu 10 Zeichen enthalten. Umfassen Sie NODUP, um einen Fremdschlüssel Kandidaten-Index erstellen.  
  
 Sie können mehrere Fremdschlüssel Indizes für die Tabelle erstellen, aber die Fremdschlüssel Indexausdrücke müssen verschiedene Felder in der Tabelle angeben.  
  
 Verweise *TableName3*[TAG *TagName5*]  
 Gibt die übergeordnete Tabelle mit der eine persistente Beziehung hergestellt wird. Include (Tag) *TagName5* zum Herstellen einer Beziehungs auf Grundlage einer Index-Tags für die übergeordnete Tabelle. Index-Tagnamen können bis zu 10 Zeichen enthalten. Standardmäßig, wenn Sie-Tag weglassen *TagName5,* der Beziehung besteht, mit der übergeordneten Tabelle Primärindex Schlüssel erstellt.  
  
 Überprüfen Sie *eExpression2*[Fehler *cMessageText2*]  
 Gibt die Validierungsregel für die Tabelle an. Fehler beim *cMessageText2* gibt die Fehlermeldung an, die der Visual FoxPro angezeigt wird, wenn die Validierungsregel für die Tabelle ausgeführt wird. Nur, wenn Daten in einem Durchsuchen-Fenster geändert werden, oder bearbeiten im Fenster die Meldung angezeigt.  
  
 AUS ARRAY *ArrayName*  
 Gibt den Namen eines vorhandenen Arrays, dessen Inhalt Name, Datentyp, Genauigkeit und Skalierung für jedes Feld in der Tabelle ist. Der Inhalt des Arrays können definiert werden, mit der **AFIELDS**()-Funktion.  
  
## <a name="remarks"></a>Hinweise  
 Die neue Tabelle in die niedrigste verfügbare Arbeitsbereich geöffnet ist und über den Alias zugegriffen werden kann. Die neue Tabelle wird ausschließlich, unabhängig von der aktuellen Einstellung der exklusive festlegen geöffnet.  
  
 Wenn eine Datenbank geöffnet ist, und Sie die kostenlose-Klausel nicht einschließen, wird die neue Tabelle in der Datenbank hinzugefügt. Sie können nicht mit dem gleichen Namen wie eine Tabelle in der Datenbank eine neue Tabelle erstellen.  
  
 Wenn eine Datenbank geöffnet ist, erfordert die CREATE TABLE - SQL exklusive Verwendung der Datenbank. Schließen Sie zum Öffnen einer Datenbank für die ausschließliche Verwendung exklusive, in Datenbank öffnen.  
  
 Wenn eine Datenbank geöffnet ist, wenn Sie die neue Tabelle erstellen, generiert das einschließlich der Namen, CHECK, DEFAULT, FOREIGN KEY, PRIMARY KEY- oder Verweise Klauseln einen Fehler aus.  
  
> [!NOTE]  
>  CREATE TABLE-Syntax mithilfe von Kommas trennen Sie bestimmte Optionen für die CREATE TABLE. Darüber hinaus müssen die NULL, nicht NULL, CHECK, Default-, PRIMARY KEY- und UNIQUE-Klausel innerhalb der Klammern, enthält die Spaltendefinitionen platziert werden.  
  
## <a name="driver-remarks"></a>Treiber "Hinweise".  
 Wenn Ihre Anwendung die ODBC-SQL-Anweisung sendet übersetzt CREATE TABLE mit der Datenquelle der Visual FoxPro-ODBC-Treiber den Befehl in der Visual FoxProCREATE TABLE-Befehl, die mit der Syntax in der folgenden Tabelle gezeigt.  
  
|ODBC-syntax|Visual FoxPro-syntax|  
|-----------------|--------------------------|  
|CREATE TABLE *Base Tabellenname*<br /><br /> (*Spaltenbezeichner Datentyp*<br /><br /> [NOT NULL]<br /><br /> [,*Spaltenbezeichner Datentyp*<br /><br /> [NOT NULL]...)|Erstellen der Tabelle *TableName1* [NAME *LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [NOT NULL])|  
  
 Beim Erstellen einer Tabelle mit dem Treiber schließt der Treiber die Tabelle direkt nach dem Erstellen, um Zugriff auf die Tabelle von anderen Benutzern zu ermöglichen. Dies unterscheidet sich vom Visual FoxPro, open ausschließlich bei der Erstellung die Tabelle zu verwerfen. Jedoch wenn eine gespeicherte Prozedur auf die Datenquelle mit einer CREATE TABLE-Anweisung ausführt, die Tabelle bleibt geöffnet.  
  
 Wenn die Datenquelle einer Datenbank (.dbc-Datei) ist, erstellt der Visual FoxPro-ODBC-Treiber eine Tabelle namens *LongTableName* mit dem gleichen Namen wie die *Base Tabellenname*.  
  
### <a name="using-data-definition-language-ddl"></a>Mithilfe der Datendefinitionssprache (DDL)  
 Sie können nicht in den folgenden Stellen DDL einschließen:  
  
-   In einem Batch SQL-Anweisung erfordert, dass eine Transaktion  
  
-   Im Manualcommit-Modus, nach einer Anweisung, die eine Transaktion erforderlich, es sei denn, die Anwendung zuerst ruft **SQLTransact**.  
  
 Z. B. Wenn Sie eine temporäre Tabelle erstellen möchten, sollten Sie die Tabelle erstellen, vor dem Beginn der Anweisung, die eine Transaktion erfordern. Wenn Sie die CREATE TABLE-Anweisung in einem Batch SQL-Anweisung, die eine Transaktion erfordert einschließen, gibt der Treiber eine Fehlermeldung zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER TABLE - SQL-Befehl](../../odbc/microsoft/alter-table-sql-command.md)   
 [Unterstützte Datentypen (Visual FoxPro-ODBC-Treiber)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT - SQL-Befehl](../../odbc/microsoft/insert-sql-command.md)   
 [Wählen Sie-SQL-Befehl](../../odbc/microsoft/select-sql-command.md)

