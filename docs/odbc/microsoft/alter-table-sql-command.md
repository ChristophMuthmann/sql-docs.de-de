---
title: ALTER TABLE - SQL-Befehl | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9897be4d0e594c82aa872f904d500bd1216d40f0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL-Befehl
Programmgesteuertes Ändern der Struktur einer Tabelle.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>Argumente  
 *TableName1*  
 Gibt den Namen der Tabelle, dessen Struktur geändert wird.  
  
 ADD [Spalte] *FieldName1*  
 Gibt den Namen des Felds hinzufügen.  
  
 ALTER [Spalte] *FieldName1*  
 Gibt den Namen eines vorhandenen Felds zu ändern.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Gibt den Feldtyp Feldbreite und Feld-Genauigkeit (Anzahl der Dezimalstellen) für eine neue oder geänderte Feld an.  
  
 *FieldType* ist ein einzelner Buchstabe, der des Felds angibt [Datentyp](../../odbc/microsoft/visual-foxpro-field-data-types.md). Einige Felddatentypen erfordern die Angabe *nFieldWidth* oder *nPrecision* oder beides.  
  
 *nFieldWidth* und *nPrecision* D, G, I, L, M, P, T und Y werden ignoriert Typen. Standardmäßig *nPrecision* ist 0 (null) (ohne Dezimalstellen) an, wenn *nPrecision* nicht für die Typen B, F oder N enthalten ist.  
  
 NULL &#124; NOT NULL  
 Ermöglicht oder verhindert, dass null-Werte in das Feld.  
  
 Wenn Sie, NULL weglassen und NOT NULL, bestimmt die aktuelle Einstellung von SET NULL an, ob in das Feld null-Werte zulässig sind. Jedoch wenn Sie, NULL weglassen und NOT NULL und die PRIMARY KEY- oder UNIQUE-Klausel enthalten, die aktuelle Einstellung von SET NULL ignoriert, und das Feld wird nicht standardmäßig NULL.  
  
 Überprüfen Sie *lExpression1*  
 Gibt eine Überprüfungsregel für das Feld. *lExpression1* müssen mit einem logischen Ausdruck ausgewertet und kann eine benutzerdefinierte Funktion oder eine gespeicherte Prozedur sein. Wenn ein leerer Datensatz angefügt wird, wird die Validierungsregel überprüft. Ein Fehler wird generiert, wenn die Überprüfungsregel für ein leeres Feldwert in eine angefügte Datensatz nicht zulässig ist.  
  
 Fehler beim *cMessageText1*  
 Gibt an, die Fehlermeldung angezeigt, wenn das Feld Validierungsregel einen Fehler generiert.  
  
 Standard *eExpression1*  
 Gibt einen Standardwert für das Feld an. Der Datentyp des *eExpression1* muss den Datentyp für das Feld identisch sein.  
  
 PRIMARY KEY  
 Erstellt ein Primärindex-Tag. Der Indexname hat den gleichen Namen wie das Feld ein.  
  
 UNIQUE  
 Erstellt ein Kandidat Index Tag mit dem gleichen Namen wie das Feld an.  
  
> [!NOTE]  
>  Kandidat Indizes (einschließlich der EINDEUTIGEN Möglichkeit, ANSI-Kompatibilität in ALTER TABLE oder CREATE TABLE erstellt) unterscheiden sich von Indizes, die mit der EINDEUTIGEN Option in den Befehl "INDEX" erstellt. Ein Index erstellt, in dem Befehl "INDEX" mithilfe von UNIQUE kann doppelte Indexschlüssel. Doppelte Indexschlüssel zulassen kandidatenindizes nicht.  
  
 NULL-Werte und Duplikate sind nicht in einem Feld zulässig, die für einen primären oder Kandidatenschlüssel Index verwendet wird.  
  
 Wenn Sie mithilfe der Spalte hinzufügen ein neues Feld erstellen, generiert Visual FoxPro keine Fehler, wenn Sie einen primären oder Kandidatenschlüssel Index für ein Feld erstellen, die null-Werte unterstützt. Visual FoxPro wird jedoch einen Fehler generiert, wenn Sie versuchen, null oder einen doppelten Wert in ein Feld eingeben, die für einen primären oder Kandidatenschlüssel Index verwendet wird.  
  
 Wenn Sie ein vorhandenes Feld, und der Primärschlüssel ändern oder Indexausdruck Candidate besteht aus Feldern in der Tabelle, überprüft Visual FoxPro die Felder, um festzustellen, ob sie null-Werte oder doppelte Datensätze enthalten. Wenn dies der Fall ist, wird Visual FoxPro generiert einen Fehler, und die Tabelle nicht geändert wird.  
  
 Verweise *TableName2* TAG *TagName1*  
 Gibt die übergeordnete Tabelle mit der eine persistente Beziehung hergestellt wird. TAG *TagName1* gibt an, der übergeordneten Tabelle Indexname auf der die Beziehung basiert. Index-Tagnamen können bis zu 10 Zeichen enthalten.  
  
 NOCPTRANS  
 Verhindert die Übersetzung in eine andere Codepage für Zeichen und Memo-Felder. Wenn die Tabelle in einer anderen Codepage konvertiert wird, werden die Felder für die NOCPTRANS angegeben wurde nicht übersetzt. NOCPTRANS können nur für Zeichen- und Memo Felder angegeben werden.  
  
 Das folgende Beispiel erstellt eine Tabelle namens Mytable, die zwei Zeichenfelder und zwei Memofelder enthält. Die zweite Zeichenfeld, char2 und das zweite Memofeld memo2, umfassen NOCPTRANS, um zu verhindern, dass bei der Übersetzung.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [Spalte] *FieldName2*  
 Gibt den Namen eines vorhandenen Felds zu ändern.  
  
 Standard festlegen *eExpression2*  
 Gibt einen neuen Standardwert für ein vorhandenes Feld. Der Datentyp des *eExpression2* muss den Datentyp für das Feld identisch sein.  
  
 SET-Kontrollkästchen *lExpression2*  
 Gibt einen neuen Überprüfungsregel für ein vorhandenes Feld. *lExpression2* müssen mit einem logischen Ausdruck ausgewertet und eine benutzerdefinierte Funktion oder eine gespeicherte Prozedur sein.  
  
 Fehler beim *cMessageText2*  
 Gibt an, die Fehlermeldung angezeigt, wenn das Feld Validierungsregel einen Fehler generiert. Die Nachricht wird nur angezeigt, wenn Daten in einem Fenster "Durchsuchen" oder Bearbeiten geändert werden.  
  
 DROP DEFAULT  
 Der Standardwert für ein vorhandenes Feld wird entfernt.  
  
 LÖSCHEN VON KONTROLLKÄSTCHEN  
 Entfernt die Überprüfungsregel für ein vorhandenes Feld.  
  
 DROP [Spalte] *FieldName3*  
 Gibt ein Feld aus der Tabelle entfernen. Entfernen eines Felds aus der Tabelle entfernt Standardwert für das Feld und Validierungsregel Feld.  
  
 Wenn der Schlüssel oder einem Trigger Indexausdrücke Feld verweisen, werden die Ausdrücke ungültig, wenn das Feld entfernt wird. In diesem Fall wird ein Fehler nicht generiert, wenn das Feld entfernt, aber die ungültige Index-Schlüssel oder einem Trigger Ausdrücke werden zur Laufzeit Fehler generiert.  
  
 SET-Kontrollkästchen *lExpression3*  
 Gibt die Validierungsregel für die Tabelle an. *lExpression3* müssen mit einem logischen Ausdruck ausgewertet und eine benutzerdefinierte Funktion oder eine gespeicherte Prozedur sein.  
  
 Fehler beim *cMessageText3*  
 Gibt an, die Fehlermeldung angezeigt, wenn die Validierungsregel für die Tabelle einen Fehler generiert. Die Nachricht wird nur angezeigt, wenn Daten in einem Fenster "Durchsuchen" oder Bearbeiten geändert werden.  
  
 LÖSCHEN VON KONTROLLKÄSTCHEN  
 Validierungsregel für die Tabelle wird entfernt.  
  
 ADD PRIMARY KEY *eExpression3*TAG *TagName2*  
 Fügt einen primären Index der Tabelle an. *eExpression3* gibt an, der Primärindex-Schlüsselausdruck und *TagName2* gibt den Namen des primären Indexes Tags. Index-Tagnamen können bis zu 10 Zeichen enthalten. Wenn TAG *TagName2* fehlt und *eExpression3* ist ein einzelnes Feld der Primärindex Tag hat den gleichen Namen wie das im angegebenen Feld *eExpression3*.  
  
 LÖSCHEN VON PRIMÄRSCHLÜSSEL  
 Der Primärindex und Tag Index entfernt. Da eine Tabelle nur einen Primärschlüssel enthalten kann, ist es nicht notwendig, dass der Name des primären Schlüssels angeben. Der primären Index entfernt werden auch alle persistenten Beziehungen, die basierend auf dem primären Schlüssel gelöscht.  
  
 ADD UNIQUE *eExpression4*[TAG *TagName3*]  
 Die Tabelle hinzugefügt einen Index Candidate. *eExpression4* gibt die möglichen Schlüssel Indexausdruck, und *TagName3* gibt den Namen des Tags Index geeignet. Index-Tagnamen können bis zu 10 Zeichen enthalten. Wenn Sie-Tag weglassen *TagName3* und *eExpression4* ist ein einzelnes Feld der Indexname Candidate hat den gleichen Namen wie das im angegebenen Feld *eExpression4*.  
  
 DROP EINDEUTIGES TAG *TagName4*  
 Entfernt die Candidate Index und der Indexname. Da eine Tabelle mehrere Kandidatenschlüssel enthalten kann, müssen Sie den Namen des Tags Candidate Index angeben.  
  
 ADD FOREIGN KEY [ *eExpression5*] TAG *TagName4*  
 Die Tabelle hinzugefügt einen foreign (nicht primäre) Index. *eExpression5* gibt an, die foreign Key Indexausdruck, und *TagName4* gibt den Namen des Tags foreign Index. Index-Tagnamen können bis zu 10 Zeichen enthalten.  
  
 Verweise *TableName2*[TAG *TagName5*]  
 Gibt die übergeordnete Tabelle mit der eine persistente Beziehung hergestellt wird. Include (Tag) *TagName5* zum Herstellen einer Beziehungs auf Grundlage einer vorhandenen Index Tags für die übergeordnete Tabelle. Index-Tagnamen können bis zu 10 Zeichen enthalten. Wenn Sie-Tag weglassen *TagName5*, die Beziehung wird mit der übergeordneten Tabelle Primärindex Tag festgelegt.  
  
 DROP FOREIGN KEY-TAG *TagName6*[speichern]  
 Löscht einen Fremdschlüssel, dessen Index Tag ist *TagName6*. Wenn Sie auf "Speichern" weglassen, wird der Indexname aus der strukturellen Index gelöscht. Schließen Sie speichern, um zu verhindern, dass das Löschen des Index Tags aus der strukturellen Index ein  
  
 RENAME-Spalte *FieldName4*TO *FieldName5*  
 Können Sie den Namen eines Felds in der Tabelle ändern. *FieldName4* gibt den Namen des Felds, das umbenannt wird. *FieldName5* gibt den neuen Namen des Felds.  
  
> [!CAUTION]  
>  Lassen Sie Sorgfalt walten, wenn Tabellenfelder umbenannt werden, da Indizieren von Ausdrücken, Feld- und Validierungsregeln, Befehle und Funktionen die ursprüngliche Feldnamen verweisen können.  
  
 NOVALIDATE  
 Gibt an, dass Visual FoxPro Änderungen an der Struktur der Tabelle vorgenommen werden können. diese Änderungen können die Integrität der Daten in der Tabelle verletzt. Standardmäßig verhindert, dass Visual FoxPro ALTER TABLE vornehmen von Änderungen, die die Integrität der Daten in der Tabelle zu verletzen. Schließen Sie NOVALIDATE, um dieses Standardverhalten zu überschreiben.  
  
## <a name="remarks"></a>Hinweise  
 ALTER TABLE kann verwendet werden, um die Struktur einer Tabelle ändern, die nicht in einer Datenbank hinzugefügt wurde. Visual FoxPro generiert jedoch einen Fehler aus, enthalten die STANDARDMÄßIGE FOREIGN KEY, PRIMARY KEY-, Verweise oder SET-Klauseln für eine kostenlose Tabelle zu ändern.  
  
 ALTER TABLE kann die Tabelle neu erstellen, indem Sie einen neuen Header für die Tabelle erstellen und Anfügen von Datensätzen, die dem Tabellenheader. Typ oder die Breite des Felds ändern würde z. B. möglicherweise die Tabelle neu erstellt werden.  
  
 Nachdem eine Tabelle neu erstellt wird, werden die Überprüfungsregeln für alle Felder ausgeführt, deren Typ oder Breite geändert wird. Wenn Sie den Typ oder die Breite eines Felds in der Tabelle ändern, wird die Regel für die Tabelle ausgeführt.  
  
 Wenn Sie Feld oder eine Tabelle Validierungsregeln für eine Tabelle, die Einträge besitzt ändern, wird Visual FoxPro testet das neue Feld oder eine Tabelle Validierungsregeln für die vorhandenen Daten und gibt eine Warnung auf das erste Vorkommen einer Validierungsregel Feld oder eine Tabelle oder eines Triggers Verstoßes.  
  
 Wenn die Tabelle, die Sie ändern in einer Datenbank, die ALTER TABLE - erfordert SQL die exklusive Verwendung der Datenbank. Schließen Sie zum Öffnen einer Datenbank für die ausschließliche Verwendung exklusive, in Datenbank öffnen.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen der Tabelle - SQL-Befehl](../../odbc/microsoft/create-table-sql-command.md)   
 [Befehl INDEX](../../odbc/microsoft/index-command.md)
