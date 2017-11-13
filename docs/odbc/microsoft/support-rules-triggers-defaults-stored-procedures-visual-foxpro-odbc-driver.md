---
title: "Unterstützung für Regeln, Trigger, Standardwerte und gespeicherten Prozeduren | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e11b18afb96c7e5c1dc6ef6c23fc56cd3a75548e
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Unterstützung für Regeln, Trigger, Standardwerte und gespeicherte Prozeduren (Visual FoxPro-ODBC-Treiber)
Sie können keine Visual FoxPro-Regeln, Trigger, Standardwerte oder gespeicherte Prozeduren mithilfe der Visual FoxPro-ODBC-Treiber erstellen. Allerdings kann die Anwendung interagiert vorhandenen Regeln, Trigger, Standardwerte oder gespeicherte Prozeduren, wie eingefügt, aktualisiert oder Visual FoxPro-Daten in einer Datenbank gespeichert löscht.  
  
 Die folgende Tabelle enthält die Visual FoxPro-Befehle und Funktionen, die von der Visual FoxPro-ODBC-Treiber unterstützt werden, wenn die Befehle oder Funktionen an, die in Regeln, Trigger, Standardwerte oder gespeicherten Prozeduren vorhanden sind.  
  
 Wenn Ihre Anwendung mit Daten, deren Regeln, Trigger, Standardwerte kommuniziert oder gespeicherte Prozeduren, keine weiteren Visual FoxPro-Befehle oder Funktionen aufrufen, generiert der Treiber einen Fehler aus. Finden Sie unter [nicht unterstützte Visual FoxPro-Befehle und Funktionen](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) eine Liste von Befehlen und Funktionen, die vom Treiber nicht unterstützt.  
  
> [!TIP]  
>  Wenn Sie die Regeln, Trigger oder gespeicherte Prozeduren, die bestimmt, die Befehle ausführen, wenn vom Treiber aufgerufen bedingten Code einfügen möchten, können Sie mithilfe der **VERSION ()** Funktion. Die **VERSION ()** -Funktion gibt "Visual FoxPro-ODBC-Treiber  *\<Version >*" beim Aufruf durch den Treiber.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Visual FoxPro-Befehlen und Funktionen, die in Regeln, Trigger, Standardwerte und gespeicherten Prozeduren unterstützt  
  
||||  
|-|-|-|  
|$-Operator|%-Operator|& Befehl|  
|& & Befehl|*-Befehl|=-Befehl|  
  
## <a name="a"></a>Ein  
  
||||  
|-|-|-|  
|ABS ()-Funktion|ACOPY ()-Funktion|Befehl "TABLE" hinzufügen|  
|ADATABASES ()-Funktion|ADBOBJECTS ()-Funktion|AERROR ()-Funktion|  
|ADEL ()-Funktion|AELEMENT ()-Funktion|ALEN ()-Funktion|  
|AFIELDS ()-Funktion|Des Anbieters AINS ()-Funktion|ALTER TABLE - SQL-Befehl|  
|ALIAS-Funktion|ALLTRIM ()-Funktion|ANFÜGEN von ARRAY-Befehl|  
|AND -Operator|APPEND (Befehl)|ANFÜGEN von MEMO-Befehl|  
|ANFÜGEN von Befehl|Fügen Sie allgemeine-Befehl|KANN ()-Funktion|  
|ANFÜGEN von PROZEDUREN-Befehl|ASC ()-Funktion|ASUBSCRIPT ()-Funktion|  
|ASIN-Funktion|ASORT ()-Funktion|ATAN-Funktion|  
|()-Funktion|AT_C ()-Funktion|ATCLINE ()-Funktion|  
|ATC ()-Funktion|ATCC ()-Funktion|AUSED ()-Funktion|  
|ATLINE ()-Funktion|ATN2-Funktion||  
|Durchschnittliche-Befehl|ACOS-Funktion||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BEGIN TRANSACTION-Befehl|ZWISCHEN ()-Funktion|BITNOT-Funktion|  
|BITCLEAR ()-Funktion|BITLSHIFT ()-Funktion|BITSET-Funktion|  
|BITOR-Funktion|BITRSHIFT ()-Funktion|LEER-Befehl|  
|BITTEST ()-Funktion|BITXOR-Funktion||  
|BOF ()-Funktion|BITAND-Funktion||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Berechnen der Befehl|KANDIDAT ()-Funktion|CHR ()-Funktion|  
|CDX ()-Funktion|CEILING-Funktion|CLOSE-Befehle|  
|CHRTRAN ()-Funktion|CHRTRANC ()-Funktion|Kopieren Sie INDIZES-Befehl|  
|CMONTH ()-Funktion|Befehl zu fortfahren|Erweiterte von Kopierbefehl-Struktur|  
|Kopieren Sie PROZEDUREN-Befehl|COPY-Struktur-Befehl|Kopieren auf einen Menübefehl|  
|Kopieren Sie die TAG-Befehl|ARRAY-Befehl Kopieren|CPCONVERT ()-Funktion|  
|COS-Funktion)|COUNT-Befehl|CTOD ()-Funktion|  
|CPCURRENT ()-Funktion|CPDBF ()-Funktion|CURSORSETPROP ()-Funktion|  
|CTOT ()-Funktion|CURSORGETPROP ()-Funktion||  
|CURVAL ()-Funktion|CDOW ()-Funktion||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Datum ()-Funktion|"DateTime" ()-Funktion|DAY ()-Funktion|  
|Datenbank ()-Funktion|DBF-Funktion|DBGETPROP ()-Funktion|  
|DBUSED ()-Funktion|Löschen - SQL-Befehl|DELETE-Befehl|  
|Löschen Sie die TAG-Befehl|Gelöschte ()-Funktion|ABSTEIGEND ()-Funktion|  
|DIFFERENCE ()-Funktion|DIMENSION-Befehl|Speicherplatz ()-Funktion|  
|DMY ()-Funktion|FÜHREN SIE FALL... ENDCASE-Befehl|Führen Sie-Befehl|  
|FÜHREN SIE DAGEGEN... ENDDO-Befehl|TICHTAG ()-Funktion|DTOC ()-Funktion|  
|DTOR ()-Funktion|DTOS ()-Funktion|DTOT ()-Funktion|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|(Leer)-Funktion|Auswerten von ()-Funktion|EXIT-Befehl|  
|Fehler ()-Funktion|EXP ()-Funktion||  
|Befehl "END TRANSACTION"|EOF-Funktion||  
  
## <a name="f"></a>V  
  
||||  
|-|-|-|  
|FCOUNT ()-Funktion|FDATE ()-Funktion|Feld ()-Funktion|  
|Datei ()-Funktion|FILTER ()-Funktion|FLDLIST ()-Funktion|  
|Bestand ()-Funktion|FLOOR ()-Funktion|FLUSH-Befehl|  
|FOR... ENDFOR-Befehl|FÜR ()-Funktion|()-Funktion gefunden|  
|KOSTENLOSE TABLE-Befehl|FSIZE ()-Funktion|FTIME-Funktion|  
|Vollständiger Pfad ()-Funktion|Funktion-Befehl|ZW ()-Funktion|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Befehl sammeln|GETNEXTMODIFIED ()-Funktion|Befehl GEHE/GOTO|  
|Und übergibt ihr ()-Funktion|GOMONTH ()-Funktion||  
|GETCP ()-Funktion|GETENV-Funktion||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|HEADER ()-Funktion|Stunde ()-Funktion|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE ()-Funktion|IF... ENDIF-Befehl|IIF ()-Funktion|  
|INDBC ()-Funktion|Befehl "INDEX"|InList-Prozedur ()-Funktion|  
|INSERT-SQL-Befehl|INT ()-Funktion|ISALPHA-Funktion|  
|ISBLANK-Funktion|ISDIGIT-Funktion|ISEXCLUSIVE ()-Funktion|  
|ISLEADBYTE-Funktion|ISLOWER-Funktion|ISNULL ()-Funktion|  
|ISREADONLY-Funktion|ISUPPER-Funktion||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Schlüssel ()-Funktion|KEYMATCH ()-Funktion||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|LEFT ()-Funktion|LEFTC ()-Funktion|LIKEC ()-Funktion|  
|LENC ()-Funktion|WIE ()-Funktion|LOCK-Funktion|  
|LOKALE-Befehl|Suchen-Befehl|Suche ()-Funktion|  
|LOG ()-Funktion|LOG10-Funktion|LTRIM ()-Funktion|  
|LOWER ()-Funktion|LPARAMETERS-Befehl||  
|LUPDATE ()-Funktion|LEN ()-Funktion||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _MLINE|MAX ()-Funktion|MDX-Funktion|  
|MDY ()-Funktion|MEMLINES ()-Funktion|Nachricht ()-Funktion|  
|MIN ()-Funktion|MINUTE-Funktion|MLINE ()-Funktion|  
|MOD-Funktion|MONTH ()-Funktion|MTON ()-Funktion|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX ()-Funktion|NORMALISIEREN ()-Funktion|NOT-Operator|  
|Hinweis-Befehl|NTOM ()-Funktion|NVL ()-Funktion|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Tritt auf, ()-Funktion|OLDVAL ()-Funktion|ZUM Befehl "Fehler"|  
|AUF Tastaturbefehl|()-Funktion|OPEN DATABASE-Befehl|  
|OR -Operator|ORDER ()-Funktion|OS ()-Funktion|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK-Befehl|Parameter ()-Funktion|PAYMENT ()-Funktion|  
|Parameter-Befehl|PRIMÄRE Funktion|PRIVATE-Befehl|  
|PI-Funktion|Programm-Funktion|RICHTIGE ()-Funktion|  
|PROCEDURE-Befehl|PV ()-Funktion||  
|PUBLIC-Befehl|PADL () &#124; PADR () &#124; PADC ()-Funktionen||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND ()-Funktion|RATTE ()-Funktion|RATC ()-Funktion|  
|RATLINE ()-Funktion|Denken Sie daran Befehl|RECCOUNT ()-Funktion|  
|RECNO ()-Funktion|RECSIZE ()-Funktion|Land/Region-Befehl|  
|Beziehung ()-Funktion|Befehl "TABLE" entfernen|Befehl "ersetzen"|  
|ARRAY-Befehl ersetzen|REPLICATE-Funktion)|Wiederholen Sie den Befehl|  
|Zurückgeben der Befehl|RECHTS ()-Funktion|RIGHTC ()-Funktion|  
|RLOCK ()-Funktion|ROLLBACK-Befehl|ROUND-Funktion|  
|RTOD ()-Funktion|RTRIM ()-Funktion||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|SCANNEN... ENDSCAN-Befehl|SCATTER-Befehl|S ()-Funktion|  
|Sekunden ()-Funktion|SEEK-Befehl|SEEK ()-Funktion|  
|Wählen Sie Befehl|SELECT ()-Funktion|SELECT-SQL-Befehl|  
|SET BLOCKSIZE-Befehl|SET-CARRY-Befehl|SET JAHRHUNDERT-Befehl|  
|SET COLLATE-Befehl|SET-DATABASE-Befehl|SET-Datum-Befehl|  
|SET-Standard-Befehl|SET DELETED-Befehl|GENAUE SET-Befehl|  
|EXKLUSIVE SET-Befehl|SET-FDOW-Befehl|SET-Felder-Befehl|  
|SET FILTER-Befehl|FESTE SET-Befehl|SET-FULLPATH-Befehl|  
|SET-FWEEK-Befehl|-Befehl festgelegte Stunden|Befehl "SET-INDEX"|  
|Befehl "SET LOCK"|SET MULTILOCKS der Wert-Befehl|Legen Sie in der Nähe von Befehl|  
|SET-NOCPTRANS-Befehl|SET benachrichtigen-Befehl|SET NULL-Befehl|  
|SET-OPTIMIZE-Befehl|SET-ORDER-Befehl|Befehl "SET"|  
|SET-PROCEDURE-Befehl|SET-RELATION-Befehl|SET-Beziehung deaktiviert Befehl|  
|SET-Verarbeitung wiederholen-Befehl|Befehl "Überspringen" festgelegt|SET-UDFPARMS-Befehl|  
|EINDEUTIGE SET-Befehl|SET-Befehl "Lautstärke"|SET ()-Funktion|  
|SETFLDSTATE ()-Funktion|SIGN ()-Funktion|SIN-Funktion|  
|Befehl "Überspringen"|SORT-Befehl|Leerzeichen ()-Funktion|  
|SQRT ()-Funktion|STORE-Befehl|STR ()-Funktion|  
|STRCONV ()-Funktion|STRTRAN ()-Funktion|STUFF-Funktion|  
|STUFFC ()-Funktion|SUBSTR-Funktion|SUBSTRC ()-Funktion|  
|SUM-Befehl|Sys(2011)-Funktion||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _TALLY|Arbeitsspeicher-Systemvariable _TRIGGERLEVEL|TAGCOUNT-Funktion|  
|TABLEUPDATE ()-Funktion|TAG ()-Funktion|Ziel ()-Funktion|  
|TAGNO ()-Funktion|TAN-Funktion|TRIM ()-Funktion|  
|Zeit ()-Funktion|Gesamt-Befehl|TXNLEVEL ()-Funktion|  
|TTOC ()-Funktion|TTOD ()-Funktion||  
|Typ ()-Funktion|TABLEREVERT ()-Funktion||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|EINDEUTIGE ()-Funktion|UNLOCK-Befehl|Befehl "USE"|  
|UPDATE-Befehl|(Oberen)-Funktion||  
|()-Funktion verwendet|UPDATE - SQL-Befehl||  
  
## <a name="v"></a>B  
  
||||  
|-|-|-|  
|VAL ()-Funktion|VERSION ()-Funktion||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Woche ()-Funktion|||  
  
## <a name="y"></a>J  
  
||||  
|-|-|-|  
|YEAR ()-Funktion|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP-Befehl|||

