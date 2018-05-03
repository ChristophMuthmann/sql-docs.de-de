---
title: Dateiformat "Text" (Text-Datei-Treiber) | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 582860c2972f205244fd3d4e9f9cae45673df66f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="text-file-format-text-file-driver"></a>Dateiformat "Text" (Text-Datei-Treiber)
Der Text der ODBC-Treiber unterstützt beide Textdateien mit Trennzeichen und fester Breite an. Eine Textdatei besteht aus einer optionalen Kopfzeile und NULL oder mehr Textzeilen.  
  
 Obwohl die Headerzeile das gleiche Format wie die anderen Zeilen in der Textdatei verwendet wird, interpretiert der Text der ODBC-Treiber die Header Zeile Einträge als Spaltennamen, keine Daten.  
  
 Eine durch Trennzeichen getrennten Textzeile enthält eine oder mehrere Datenwerte, die durch Trennzeichen getrennte: Kommas, Tabstopps oder ein benutzerdefiniertes Trennzeichen. In der gesamten Datei muss die gleiche Trennzeichen verwendet werden. NULL-Werte werden durch zwei Trennzeichen in einer Zeile ohne Daten dazwischen gekennzeichnet. Zeichenfolgen in einer durch Trennzeichen getrennten Textzeile in doppelte Anführungszeichen eingeschlossen werden können (""). Keine Leerzeichen können vor oder nach einer durch Trennzeichen getrennten Werten auftreten.  
  
 Die Breite der einzelnen Einträge Daten in eine Textdatei mit fester Breite Linie wird in einem Schema angegeben. NULL-Werte werden durch Leerzeichen gekennzeichnet.  
  
 Tabellen sind beschränkt auf ein Maximum von 255 Felder. Feldnamen werden maximal 64 Zeichen umfassen und Feldbreiten 32.766 Zeichen beschränkt sind. Datensätze sind auf 65.000 Bytes beschränkt.  
  
 Nur für einen einzelnen Benutzer kann eine Textdatei geöffnet werden. Mehrere Benutzer werden nicht unterstützt.  
  
 Die folgenden Grammatik geschrieben für Programmierer, definiert das Format einer Textdatei, die von der ODBC-Texttreiber gelesen werden kann:  
  
|Format|Darstellung|  
|------------|--------------------|  
|Nicht kursiv|Zeichen, die wie gezeigt eingegeben werden müssen|  
|*Kursiv*|Argumente, die an anderer Stelle in der Grammatik definiert sind|  
|Klammern ([])|Optionale Elemente|  
|geschweifte Klammern ({})|Eine Liste von sich gegenseitig ausschließende Optionen|  
|Die senkrechten Striche (&#124;)|Separate sich gegenseitig ausschließende Optionen|  
|Auslassungspunkte (...)|Elemente, die einmal oder mehrmals wiederholt werden kann|  
  
 Das Format einer Textdatei ist:  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  Die Breite jeder Spalte in einer Textdatei mit fester Breite ist in der Datei Schema.ini angegeben.  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  Das Trennzeichen in einer benutzerdefinierten getrennte Textdatei wird in der Datei Schema.ini angegeben.  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  Für Dateien mit Trennzeichen wird ein NULL-Wert durch keine Daten zwischen zwei Trennzeichen dargestellt.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  Für Dateien mit fester Breite wird ein NULL-Wert, durch Leerzeichen dargestellt.
