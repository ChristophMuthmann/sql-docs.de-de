---
title: "Nicht unterstützte Visual FoxPro-Befehle und Funktionen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df2f3bfdb37ab506de3fe99d8c7d1e5e9764ef43
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Nicht unterstützte Visual FoxPro-Befehle und Funktionen (Visual FoxPro-ODBC-Treiber)
Die folgende Tabelle enthält FoxPro Befehle und Funktionen, die von Microsoft® Visual FoxPro unterstützt werden, werden von der Visual FoxPro-ODBC-Treiber nicht unterstützt.  
  
 Wenn Ihre Anwendung mit Daten, deren Regeln, Trigger, Standardwerte kommuniziert oder gespeicherte Prozeduren dieser Funktionen oder Visual FoxPro-Befehle aufrufen, generiert der Treiber einen Fehler.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Nicht unterstützte Visual FoxPro-Befehle und Funktionen  
  
||||  
|-|-|-|  
|#DEFINE... #UNDEF|#IF... Präprozessor #ENDIF-Direktive|#IFDEF &#124; #IFNDEF|  
|#INCLUDE Präprozessor-Direktive|:: Bereichsauflösungsoperator|! Befehl (Siehe &#124; ausführen! Befehl "")|  
|? &#124; ?? Befehl|??? Befehl|\ &#124; \\\ Befehl|  
|@ ... BOX-Befehl|@ ... CLASS-Befehl|@ ... CLEAR-Befehl|  
|@ ... Bearbeiten - Befehl Felder bearbeiten|@ ... FILL-Befehl|@ ... GET|  
|@ ... Menübefehl|@ ... PROMPT-Befehl|@ ... Angenommen, Befehl|  
|@ ... Bildlauf-Befehl|@ ... -Befehl||  
  
## <a name="a"></a>Ein  
  
||||  
|-|-|-|  
|AKZEPTIEREN-Befehl|ACLASS ()-Funktion|Aktivieren des Menübefehls|  
|POPUP-Befehl aktivieren|Bildschirm-Befehl aktivieren|Aktivieren Sie im Fenster-Befehl|  
|ActivateCell-Methode|Fügen Sie den Befehl Klasse hinzu|ADIR ()-Funktion|  
|AFONT ()-Funktion|AINSTANCE ()-Funktion|Arbeitsspeicher-Systemvariable _ALIGNMENT|  
|AMEMBERS ()-Funktion|ANSITOOEM ()-Funktion|APRINTERS ()-Funktion|  
|ASELOBJ ()-Funktion|Befehl unterstützen||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Strich ()-Funktion|BARCOUNT ()-Funktion|BARPROMPT ()-Funktion|  
|Arbeitsspeicher-Systemvariable _BEAUTIFY|Arbeitsspeicher-Systemvariable _BOX|Befehl durchsuchen|  
|Arbeitsspeicher-Systemvariable _BROWSER|Erstellen von APP-Befehl|Erstellen von EXE-Befehl|  
|Befehl "Projekt" erstellen|Arbeitsspeicher-Systemvariable _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _CALCVALUE|Arbeitsspeicher-Systemvariable _CLIPTEXT|Arbeitsspeicher-Systemvariable _CONVERTER|  
|Arbeitsspeicher-Systemvariable _CUROBJ|CALL-Befehl|CANCEL-Befehl|  
|CAPSLOCK-Funktion|Befehl "CD"|Befehl zum Ändern|  
|Befehl "chdir"|CHRSAW ()-Funktion|Schließen MEMO-Befehl|  
|CNTBAR ()-Funktion|CNTPAD ()-Funktion|Spalten-Nr ()-Funktion|  
|COMPILE-Befehl|Kompilieren Sie die DATABASE-Befehl|Kompilieren von FORM-Befehl|  
|COMPOBJ ()-Funktion|Container-Objekt|Control-Objekt|  
|Befehl "Datei kopieren"|Kopieren Sie MEMO-Befehl|Erstellen von Klasse-Befehl|  
|Erstellen Sie CLASSLIB-Befehl|Erstellen Sie die Farbe SET-Befehl|CREATE-Befehl|  
|Erstellen der CONNECTION-Befehl|Erstellen des DATABASE-Befehl|Erstellen von FORM-Befehl|  
|Erstellen von Befehl|Erstellen der LABEL-Befehl|Erstellen Sie im Menübefehl|  
|Befehl "Projekt" erstellen|Abfragebefehl erstellen|Erstellen von Berichts-Befehl|  
|Erstellen (Befehl)|Erstellen von SQL-Ansicht-Befehl|Erstellen Sie TRIGGER-Befehl|  
|Erstellen von VIEW (Befehl)|CREATEOBJECT ()-Funktion|CURDIR ()-Funktion|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _DBLCLICK|Arbeitsspeicher-Systemvariable _DIARYDATE|DBSETPROP ()-Funktion|  
|DDE-Funktionen|Deaktivieren des Menübefehls|Deaktivieren Sie POPUP-Befehl|  
|Deaktivieren Sie im Fenster-Befehl|DECLARE - DLL-Befehl|Deklarieren Sie Befehl|  
|LEISTE Befehl definieren|Definieren Sie im Feld Befehl|Definieren von Klasse-Befehl|  
|Definieren des Menübefehls|Definieren von PAD-Befehl|Definieren Sie POPUP-Befehl|  
|Definieren Sie die Fenster-Befehl|Löschen der CONNECTION-Befehl|Löschen Sie die DATABASE-Befehl|  
|Löschen Sie die Datei (Befehl)|DELETE-TRIGGER-Befehl|Löschen von VIEW (Befehl)|  
|Befehl "DIR"|DIRECTORY-Befehl|Anzeigebefehl|  
|Anzeige VERBINDUNGEN-Befehl|Anzeige-DATABASE-Befehl|Anzeige-DLLS-Befehl|  
|Anzeige-Dateien-Befehl|Arbeitsspeicher-Anzeigebefehl|Anzeige Objekte-Befehl|  
|Anzeige PROZEDUREN-Befehl|Anzeige-STATUS-Befehl|Anzeige-Struktur-Befehl|  
|Anzeige-Tabellen-Befehl|Anzeige Ansichten-Befehl|Befehl bilden|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Bearbeiten (Befehl)|Fehler-Befehl||  
|ERASE-Befehl|Externer Befehl|EXPORT-Befehl|  
|WERFEN Sie Befehl|WERFEN Sie Seite-Befehl||  
  
## <a name="f"></a>V  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _FOXDOC|Arbeitsspeicher-Systemvariable _FOXGRAPH|FEOF-Funktion|  
|FCLOSE-Funktion|FCREATE ()-Funktion|FGETS-Funktion|  
|FERROR ()-Funktion|FFLUSH-Funktion|FKLABEL ()-Funktion|  
|Filter-Befehl|Befehl "Suchen"|FOPEN-Funktion|  
|FKMAX ()-Funktion|FONTMETRIC ()-Funktion|FSEEK-Funktion|  
|FPUTS-Funktion|FREAD-Funktion||  
|FWRITE-Funktion|FCHSIZE ()-Funktion||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _GENGRAPH|Arbeitsspeicher-Systemvariable _GENMENU|Arbeitsspeicher-Systemvariable _GENPD|  
|Arbeitsspeicher-Systemvariable _GENSCRN|Arbeitsspeicher-Systemvariable _GENXTAB|GETBAR ()-Funktion|  
|GETCOLOR-Funktion|GETDIR ()-Funktion|GETEXPR-Befehl|  
|GETFILE ()-Funktion|GETFONT-Funktion|GETOBJECT-Funktion|  
|GETPAD ()-Funktion|GETPICT ()-Funktion|GETPRINTER ()-Funktion|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Befehl "Hilfe"|Ausblenden des Menübefehls|Ausblenden von POPUP-Befehl|  
|Ausblenden der Fenster-Befehl|HOME ()-Funktion||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS ()-Funktion|IMPORT-Befehl|INPUT-Befehl|  
|INDEX-Befehl|INKEY ()-Funktion|ISCOLOR ()-Funktion|  
|INSERT-Befehl|INSMODE ()-Funktion||  
|ISMOUSE ()-Funktion|Arbeitsspeicher-Systemvariable _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|JOIN-Befehl|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Tastenkombination|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _LMARGIN|LABEL-Befehl|LASTKEY ()-Funktion|  
|"LineNo" ()-Funktion|LIST-Befehle|VERBINDUNGEN auflisten (Befehl)|  
|LOAD-Befehl|LocFile ABGELEGT ()-Funktion||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL ()-Funktion|MD-Befehl|Menü, um den Befehl|  
|Arbeitsspeicher ()-Funktion|Menübefehl|MKDIR-Befehl|  
|Menü ()-Funktion|MESSAGEBOX ()-Funktion|Ändern der CONNECTION-Befehl|  
|Ändern Sie den Befehl Klasse|Befehl ändern|Ändern der Formular-Befehl|  
|Ändern Sie die DATABASE-Befehl|Ändern Sie die Datei (Befehl)|MEMO-Befehl ändern|  
|Allgemeine Befehl ändern|Ändern der LABEL-Befehl|Ändern der Befehl "Projekt"|  
|Ändern des Menübefehls|Ändern der PROCEDURE-Befehl|Ändern der Bildschirm-Befehl|  
|Ändern der Abfragebefehl|Ändern Sie die BERICHTSSERVER-Befehl|Ändern Sie die Fenster-Befehl|  
|Ändern der Struktur-Befehl|Ändern von VIEW (Befehl)|Befehl zum Verschieben der Fenster|  
|Der Befehl für Maus|MOVE-POPUP-Befehl|MROW ()-Funktion|  
|MRKBAR ()-Funktion|MRKPAD ()-Funktion||  
|MWINDOW ()-Funktion|MDOWN ()-Funktion||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUM-Taste ()-Funktion|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM ()-Funktion|OBJTOCLIENT ()-Funktion|ON Strich Befehl|  
|OEMTOANSI ()-Funktion|ZUM Befehl "APLABOUT"|ON EXIT Menübefehl|  
|ESCAPE-Befehl|ZUM Beenden der Befehl "BALKEN"|Schlüssel =-Befehl|  
|ON EXIT PAD-Befehl|ON EXIT POPUP-Befehl|ON PAD-Befehl|  
|ZUM Befehl "Beschriftung"|ZUM Befehl "MACHELP"|ZUM Befehl "Auswahl LEISTE"|  
|AUF der Seite "-Befehl|ZUM Befehl "READERROR"|AUF Auswahl POPUP-Befehl|  
|AUF Auswahl Menübefehl|ZUM Befehl "Auswahl PAD"||  
|AUF den Befehl "Herunterfahren"|OBJVAR ()-Funktion||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _PADVANCE|Arbeitsspeicher-Systemvariable _PAGENO|Arbeitsspeicher-Systemvariable _PBPAGE|  
|Arbeitsspeicher-Systemvariable _PCOLNO|Arbeitsspeicher-Systemvariable _PCOPIES|Arbeitsspeicher-Systemvariable _PDRIVER|  
|Arbeitsspeicher-Systemvariable _PDSETUP|Arbeitsspeicher-Systemvariable _PECODE|Arbeitsspeicher-Systemvariable _PEJECT|  
|Arbeitsspeicher-Systemvariable _PEPAGE|Arbeitsspeicher-Systemvariable _PLENGTH|Arbeitsspeicher-Systemvariable _PLINENO|  
|Arbeitsspeicher-Systemvariable _PLOFFSET|Arbeitsspeicher-Systemvariable _PPITCH|Arbeitsspeicher-Systemvariable _PQUALITY|  
|Arbeitsspeicher-Systemvariable _PRETEXT|Arbeitsspeicher-Systemvariable _PSCODE|Arbeitsspeicher-Systemvariable _PSPACING|  
|Arbeitsspeicher-Systemvariable _PWAIT|PACK-DATABASE-Befehl|AUFFÜLLZEICHEN ()-Funktion|  
|PCOL ()-Funktion|PEMSTATUS ()-Funktion|MAKRO-Befehl "WIEDERGEBEN"|  
|POP Tastaturbefehl|POP Menübefehl|POP-POPUP-Befehl|  
|POPUP-Funktion|PRINTJOB... ENDPRINTJOB-Befehl|PRINTSTATUS ()-Funktion|  
|PRMBAR ()-Funktion|PRMPAD ()-Funktion|PROMPT-Funktion|  
|PROW ()-Funktion|PRTINFO ()-Funktion|PUSH-Tastaturbefehl|  
|PUSH-Menübefehl|PUSH-POPUP-Befehl|PUTFILE ()-Funktion|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Beenden (Befehl)|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _RMARGIN|RD-Befehl|READKEY ()-Funktion|  
|Lesen Sie Befehl|Lesen des Menübefehls|RELEASE-LEISTE-Befehl|  
|Refresh()-Funktion|NEUINDIZIEREN-Befehl|RELEASE-Bibliothek-Befehl|  
|RELEASE-CLASSLIB-Befehl|RELEASE-Befehl|RELEASE-PAD-Befehl|  
|RELEASE-MENÜS-Befehl|RELEASE-Modul-Befehl|Version von WINDOWS-Befehl|  
|RELEASE-POPUPS-Befehl|RELEASE-PROCEDURE-Befehl|Umbenennen eines Menübefehls|  
|Entfernen Sie den Befehl Klasse|Benennen Sie den Befehl Klasse|Umbenennen von VIEW (Befehl)|  
|Umbenennen der CONNECTION-Befehl|Befehl "TABLE" Umbenennen|Stellen Sie vom Befehl wieder her|  
|Bericht-Befehl|REQUERY-Funktion|Der SYNCHRONISIERUNGSBEFEHL der Fenster|  
|Der SYNCHRONISIERUNGSBEFEHL der MAKROS|Der SYNCHRONISIERUNGSBEFEHL der Bildschirm|RGBSCHEME ()-Funktion|  
|Befehl "fortsetzen"|RGB-Funktion|AUSFÜHRUNG &#124;! Befehl|  
|RMDIR-Befehl|Zeile ()-Funktion||  
|RUNSCRIPT-Befehl|RDLEVEL ()-Funktion||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Speichern Sie die MAKROS-Befehl|Speichern der Bildschirm-Befehl|Befehl Speichern|  
|Speichern Sie die WINDOWS-Befehl|Schema ()-Funktion|SCOLS ()-Funktion|  
|Bildlauf-Befehl|Arbeitsspeicher-Systemvariable _screen|SET-Befehl|  
|Alternative SET-Befehl|SET ANSI-Befehl|SET-APLABOUT-Befehl|  
|SET AUTOSPEICHERN-Befehl|SET BELL-Befehl|SET BLINK-Befehl|  
|SET-BORDER-Befehl|SET einfacher BRSTATUS-Befehl|SET-CLASSLIB-Befehl|  
|SET-löschen-Befehl|SET-Uhr-Befehl|Festlegen des Befehls|  
|SET-Farbe des Schema-Befehl|SET Farbe SET-Befehl|SET-Farbe Befehl|  
|KOMPATIBLE SET-Befehl|SET-CONFIRM-Befehl|SET-Konsole-Befehl|  
|SET-CPCOMPILE|SET-CPDIALOG|SET CURRENCY-Befehl|  
|SET CURSOR-Befehl|SET-DATASESSION-Befehl|SET-DEBUG-Befehl|  
|SET-DEZIMALZAHLEN-Befehl|SET-TRENNZEICHEN-Befehl|SET-DEVELOPMENT-Befehl|  
|SET-Gerät-Befehl|SET-Anzeige-Befehl|SET-DOHISTORY-Befehl|  
|Gruppe "ECHO"-Befehl|SET-ESCAPE-Befehl|SET-FORMAT-Befehl|  
|SET-Funktion (Befehl)|SET-Überschriften-Befehl|SET-Befehl "Hilfe"|  
|SET-HELPFILTER-Befehl|SET-INTENSITÄT-Befehl|SET-KEY-Befehl|  
|SET-KEYCOMP-Befehl|SET-LOGERRORS-Befehl|SET-MACDESKTOP-Befehl|  
|SET-MACHELP-Befehl|SET-MACKEY-Befehl|SET MARGIN-Befehl|  
|Festlegen des Befehls markieren|Legen Sie die Markierung Befehl|SET-MEMOWIDTH-Befehl|  
|SET-Nachricht-Befehl|SET-Maus-Befehl|SET KILOMETERSTAND-Befehl|  
|SET OLEOBJECT-Befehl|SET-PALETTE-Befehl|SET-PDSETUP-Befehl|  
|Zeigen Sie SET-Befehl|SET-PRINTER-Befehl|SET-READBORDER-Befehl|  
|SET-REFRESH-Befehl|SET-Ressource-Befehl|SET-Sicherheit-Befehl|  
|SET SCOREBOARD-Befehl|SET-Sekunden-Befehl|SET-TRENNZEICHEN-Befehl|  
|SET-SCHATTEN-Befehl|Überspringen von SET-Befehls|SET-Speicherplatz (Befehl)|  
|SET-STATUS-Befehl|Festlegen der Statusleiste (Befehl)|SET-Schritt-Befehl|  
|PERSISTENTE SET-Befehl|SET-SYSFORMATS-Befehl|SET-SYSMENU-Befehl|  
|SET TALK-Befehl|SET-TEXTMERGE-Befehl|SET TEXTMERGE TRENNZEICHEN-Befehl|  
|SET-Thema-Befehl|SET Thema ID-Befehl|SET-TRBETWEEN-Befehl|  
|SET TYPEAHEAD-Befehl|SET-Ansicht-Befehl|SET-Fenster des MEMO-Befehl|  
|SET-XCMDFILE-Befehl|Arbeitsspeicher-Systemvariable _SHELL|GET-Befehls "anzeigen"|  
|ANZEIGEN (Befehl) Ruft|Anzeigen des Menübefehls|ANZEIGEN (Objektbefehl|  
|POPUP-Befehls "anzeigen"|ANZEIGEN (Befehl) Fenster|Größe POPUP-Befehl|  
|Größe Fenster-Befehl|SKPBAR ()-Funktion|SKPPAD ()-Funktion|  
|SOUNDEX-Funktion|Arbeitsspeicher-Systemvariable _SPELLCHK|SQL-Funktionen|  
|SROWS ()-Funktion|Arbeitsspeicher-Systemvariable _STARTUP|Befehl "Anhalten"|  
|Sys() Funktionen mit Ausnahme von SYS(2011)|SYSMETRIC ()-Funktion||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Arbeitsspeicher-Systemvariable _TABS|TEXT... ENDTEXT-Befehl|TXTWIDTH ()-Funktion|  
|TRANSFORMIEREN ()-Funktion|Arbeitsspeicher-Systemvariable _TRANSPORT||  
|Eingabe des Befehls|Arbeitsspeicher-Systemvariable _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|AKTUALISIERTE ()-Funktion|Befehl "USE"||  
  
## <a name="v"></a>B  
  
||||  
|-|-|-|  
|Überprüfen Sie die DATABASE-Befehl|VARREAD ()-Funktion|VERSION ()-Funktion|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Ko_mmunikation Arbeitsspeicher Systemvariable|Arbeitsspeicher-Systemvariable _WIZARD|WCHILD ()-Funktion|  
|Warten Sie, Befehl|WBORDER ()-Funktion|WFONT ()-Funktion|  
|WCOLS ()-Funktion|WEXIST ()-Funktion|WLROW ()-Funktion|  
|MIT... ENDWITH-Befehl|WLAST ()-Funktion|WONTOP ()-Funktion|  
|WMAXIMUM ()-Funktion|WLCOL ()-Funktion|WREAD ()-Funktion|  
|WOUTPUT ()-Funktion|WMINIMUM ()-Funktion|WVISIBLE ()-Funktion|  
|WPARENT ()-Funktion|WTITLE ()-Funktion||  
|WROWS ()-Funktion|Arbeitsspeicher-Systemvariable _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZOOM-Fenster-Befehl|||
