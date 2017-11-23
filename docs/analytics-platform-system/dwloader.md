---
title: "Dwloader Command-Line-Ladeprogramm für Parallel Data Warehouse"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "** Dwloader ** ist ein Befehlszeilentool Parallel Data Warehouse (PDW), die Zeilen der Tabelle in einem Massenvorgang in eine vorhandene Tabelle lädt."
ms.date: 11/04/2016
ms.topic: article
ms.assetid: f79b8354-fca5-41f7-81da-031fc2570a7c
caps.latest.revision: "90"
ms.openlocfilehash: 0335005e2e0590efe28a0cbf7dff6aaacfea331f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dwloader-command-line-loader"></a>Dwloader Command-Line-Ladeprogramm
**Dwloader** ist ein Befehlszeilentool Parallel Data Warehouse (PDW), die Zeilen der Tabelle in einem Massenvorgang in eine vorhandene Tabelle lädt. Beim Laden von Zeilen können Sie alle Zeilen bis zum Ende der Tabelle hinzufügen (*append-Modus* oder *Fastappend-Modus*), neue Zeilen angefügt, und aktualisieren Sie vorhandene Zeilen (*Upsert-Modus*), oder löschen Sie alle vorhandene Zeilen vor dem Laden, und klicken Sie dann alle Zeilen in eine leere Tabelle einfügen (*Modus laden*).  
  
**Prozess zum Laden von Daten**  
  
1.  Vorbereiten der Quelldaten an.  
  
    Verwenden Sie eigene ETL-Prozess, um die Quelldaten zu erstellen, die Sie laden möchten. Die Quelldaten müssen formatiert werden, um das Schema der Zieltabelle überein. Speichern Sie die Quelldaten in eine oder mehrere Textdateien, und kopieren Sie die Textdateien im selben Verzeichnis auf dem Server geladen. Informationen über den Server laden können, finden Sie unter [erwerben und Konfigurieren eines Servers geladen](acquire-and-configure-loading-server.md)  
  
2.  Bereiten Sie die Optionen für das Laden.  
  
    Entscheiden Sie, welche Optionen für das Laden Sie verwenden möchten. Optionen für das Laden in einer Konfigurationsdatei zu speichern. Kopieren Sie die Konfigurationsdatei in einen lokalen Speicherort auf dem Server geladen. Die **Dwloader** Konfigurationsoptionen werden in diesem Thema beschrieben.  
  
3.  Bereiten Sie die Last-Optionen vor.  
  
    Festlegen, wie **Dwloader** Zeilen behandelt, die nicht geladen werden. Um den Ladevorgang **Dwloader** zuerst die Daten in eine Stagingtabelle geladen und dann werden die Daten in die Zieltabelle übertragen. Wie das Ladeprogramm für Daten in die Stagingtabelle geladen wird, überwacht es die Anzahl der Zeilen, die nicht geladen werden. Zeilen, die nicht ordnungsgemäß formatiert werden beispielsweise nicht geladen. Fehlerhafte Zeilen werden in einer Datei für die Ablehnung kopiert. Standardmäßig bricht die Last nach der ersten Ablehnung ab, es sei denn, Sie geben Sie einen anderen Ablehnung Schwellenwert.  
  
4.  Installieren Sie **Dwloader**.  
  
    Installieren Sie Dwloader auf den Server laden, wenn es nicht bereits installiert ist. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Führen Sie **Dwloader**.  
  
    Melden Sie sich an den Server laden, und führen Sie die ausführbare Datei **dwloader.exe** mit den entsprechenden Befehlszeilenoptionen.  
  
6.  Überprüfen Sie die Ergebnisse aus.  
  
    Sehen Sie sich die fehlerhaften Zeilen (angegeben mit -R) Datei, um festzustellen, ob alle Zeilen konnte nicht geladen. Wenn diese Datei leer ist, werden alle Zeilen erfolgreich geladen. **Dwloader** transaktional ist, wird damit Wenn alle fehlschlägt (außer abgelehnte Zeilen) und befinden alle Schritte auf ihren ursprünglichen Zustand Rollback ausgeführt werden.  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>Syntax  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]   
}  
```  
  
## <a name="arguments"></a>Argumente  
**-h**  
Zeigt die einfache Hilfeinformationen zu mit dem Loader. Hilfe wird nur angezeigt, wenn keine anderen Befehlszeilenparametern angegeben werden.  
  
**U -** *Login_name*  
Eine gültige Anmeldung für SQL Server-Authentifizierung mit entsprechenden Berechtigungen zum Ausführen der Last.  
  
**-P** *Kennwort*  
Das Kennwort für eine SQL Server-Authentifizierung *Login_name*.  
  
**-W**  
Windows-Authentifizierung verwenden. (Nein *Login_name* oder *Kennwort* erforderlich.) 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *Parameter_file_name*  
Verwenden Sie eine Parameterdatei *Parameter_file_name*, anstelle von Befehlszeilenparametern. *Parameter_file_name* darf Befehlszeilenparameter außer *User_name* und *Kennwort*. Wenn ein Parameter in der Befehlszeile angegeben und in der Parameterdatei angegeben wird, überschreibt der Befehlszeile den File-Parameter.  
  
Die Parameterdatei enthält einen Parameter, ohne die  **-**  Präfix pro Zeile.  
  
Beispiele:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S***Target_appliance*  
Gibt an, die SQL Server PDW Appliance, die die geladenen Daten zu erhalten.  
  
*Infiniband-Verbindungen*, *Target_appliance* angegeben ist, als < Gerätename >-SQLCTL01. Diese benannte Verbindung konfigurieren, erfahren Sie unter [InfiniBand-Netzwerkadapter konfigurieren](configure-infiniband-network-adapters.md).  
  
Für Ethernet-Verbindungen *Target_appliance* ist die IP-Adresse für den Steuerelement-Knoten-Cluster.  
  
Wenn nicht angegeben, Standardwert Dwloader ist der Wert, der bei der Installation Dwloader angegeben wurde. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**T -** *Target_database_name.* [*Schema*]. *Table_name*  
Der dreiteilige Name für die Zieltabelle.  
  
**-I:***Source_data_location*  
Der Speicherort der ein oder mehrere Quelldateien zu laden. Jeder Quelldatei muss eine Textdatei oder einer Textdatei, die mit Gzip komprimiert wird. Nur eine Quelldatei kann in jeder Gzip-Datei komprimiert werden.  
  
So formatieren Sie eine Quelldatei:  
  
-   Die Quelldatei muss in Übereinstimmung mit den Optionen für das Laden formatiert werden.  
  
-   Jede Zeile in einer Quelldatei enthält die Daten für eine Tabellenzeile. Die Quelldaten müssen das Schema der Zieltabelle überein. Zusätzlich müssen die Spalte Reihenfolge und Datentypen übereinstimmen. Jedes Feld in der Zeile stellt eine Spalte in der Zieltabelle.  
  
-   Standardmäßig werden die Felder variabler Länge sind und durch ein Trennzeichen getrennt. Verwenden Sie zum Angeben der Trennzeichentyp < Variable_length_column_options > Befehlszeilenoptionen stehen zur Verfügung. Um Felder mit fester Länge anzugeben, verwenden Sie die Befehlszeilenoptionen < Fixed_width_column_options >.  
  
Um den Speicherort der Quelle anzugeben:  
  
-   Speicherort für die Daten kann ein Netzwerkpfad oder einen lokalen Pfad zu einem Verzeichnis auf dem Server geladen werden.  
  
-   Um alle Dateien in einem Verzeichnis anzugeben, geben Sie den Verzeichnispfad an, gefolgt von der * Platzhalterzeichen.  Das Ladeprogramm lädt keine Dateien aus Unterverzeichnisse, die den Quellspeicherort für die Daten werden... Die Loader-Fehler, wenn ein Verzeichnis in einer Gzip-Datei vorhanden ist.  
  
-   Um einige der Dateien in einem Verzeichnis anzugeben, verwenden Sie eine Kombination von Zeichen und die * Platzhalter.  
  
So laden Sie mehrere Dateien mit einem Befehl:  
  
-   Alle Dateien müssen im gleichen Verzeichnis vorhanden sein.  
  
-   Die Dateien müssen alle Textdateien, alle Gzip-Dateien oder eine Kombination von Text und Gzip-Dateien befinden.  
  
-   Darf keine der Dateien Headerinformationen ein.  
  
-   Alle Dateien müssen den gleichen Zeichencodierungstyp verwenden. Die Option – e angezeigt.  
  
-   Alle Dateien müssen in derselben Tabelle geladen werden.  
  
-   Alle Dateien werden verkettet und als wären sie eine Datei sind, und die abgelehnten Zeilen ist in einer einzelnen Reject-Datei geladen.  
  
Beispiele:  
  
-   -i \\\loadserver\loads\daily\\*.gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday.*  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *Load_failure_file_name*  
Treten Fehler beim Laden, **Dwloader** speichert die Zeile, die geladen und die Beschreibung des Fehlers die Fehlerinformationen in einer Datei namens konnte *Load_failure_file_name*. Wenn diese Datei bereits vorhanden ist, werden Dwloader die vorhandene Datei überschrieben. *Load_failure_file_name* wird erstellt, wenn der erste Fehler auftritt. Wenn alle Zeilen erfolgreich laden *Load_failure_file_name* wird nicht erstellt.  
  
**--fh** *Number_header_rows*  
Die Anzahl der Zeilen (Zeilen), um am Anfang des ignorieren *Source_data_file_name*. Die Standardeinstellung ist 0.  
  
< Variable_length_column_options >  
Die Optionen für eine *Source_data_file_name* , die Spalten mit variabler Länge Zeichen getrennt wurde. Standardmäßig *Source_data_file_name* ASCII-Zeichen in Spalten variabler Länge enthält.  
  
Bei ASCII-Dateien sind NULL-Werte dargestellt, indem Trennzeichen fortlaufend. Z. B. in eine Pipe getrennte Datei ("|"), ein NULL-Wert wird angegeben als "||". In einer durch Trennzeichen getrennte Datei, sind durch ein NULL-Wert ",,". Darüber hinaus die **-E** (--EmptyStringAsNull) Option muss angegeben werden. Weitere Informationen zum -E finden Sie weiter unten.  
  
**e -** *Character_encoding*  
Gibt einen Typ als zeichencodierung für die Daten aus der Datendatei geladen werden. Optionen sind ASCII (Standard), UTF8, UTF16-Format oder UTF16BE, wobei UTF16-Format little-endian und UTF16BE ist big-Endian. Diese Optionen sind Groß-/Kleinschreibung beachtet.  
  
**t -** *Field_delimiter*  
Das Trennzeichen für jedes Feld (Spalte) in der Zeile. Das Feldtrennzeichen kann einen oder mehrere dieser ASCII-Escape-Zeichen oder ASCII-Hexadezimalwerten...  
  
|Name|Escape-Zeichen|Hexadezimalzeichen|  
|--------|--------------------|-----------------|  
|Registerkarte|\t|0 x 09|  
|Wagenrücklauf (CR)|\r|0x0D|  
|Zeilenvorschub (LF)|\n|0x0A|  
|CRLF|\r\n|0x0d0x0a|  
|Komma|','|0x2c|  
|Doppeltes Anführungszeichen|\\"|0 x 22|  
|Einfaches Anführungszeichen|\\'|0 x 27|  
  
Um einen senkrechten Strich in der Befehlszeile angeben, müssen Sie ihn in doppelte Anführungszeichen "|". Dies wird vom Befehlszeilenparser Fehlinterpretation vermeiden. Andere Zeichen sind in einfache Anführungszeichen eingeschlossen.  
  
Beispiele:  
  
-t "|"  
  
-t ""  
  
-t 0x0a  
  
\t -t  
  
-t "~ | ~"  
  
**R -** *Row_delimiter*  
Das Trennzeichen für jede Zeile der Quelldatendatei. Das Zeilentrennzeichen ist mindestens ein ASCII-Werte.  
  
Um ein Wagenrücklauf (CR), Zeilenvorschubzeichen (LF) oder Tabstoppzeichen als Trennzeichen angeben, können Sie die Escape-Zeichen ("\r", "\n", "\t") oder ihre hexadezimale Werte (0 X, 0d 09) verwenden. Verwenden Sie zum Angeben eines anderen Sonderzeichen als Trennzeichen ihren Hexadezimalwert.  
  
Beispiele für CR-LF:  
  
R - \r\n  
  
-R 0x0d0x0a  
  
Beispiele für CR:  
  
R - \r  
  
-R 0x0d  
  
Beispiele für LF:  
  
R - \n  
  
-R 0x0a  
  
Ein LF ist erforderlich für Unix. Ein CR ist erforderlich für Windows.  
  
**-s** *String_delimiter*  
Das Trennzeichen für Zeichenfolgendaten Typfeld einer Eingabedatei mit Texttrennzeichen an. Die Zeichenfolgentrennzeichen ist mindestens ein ASCII-Werte.  Er kann als Zeichen angegeben werden (z. B. -s *) oder als einen hexadezimalen Wert (z. B. -s 0 x 22 für ein doppeltes Anführungszeichen).  
  
Beispiele:  
  
-s *  
  
-s 0 x 22  
  
< Fixed_width_column_options >  
Die Optionen für eine Quelldatei für die Daten, die Spalten fester Länge aufweist. Standardmäßig *Source_data_file_name* ASCII-Zeichen in Spalten variabler Länge enthält.  
  
Spalten mit fester Breite werden nicht unterstützt, wenn – e UTF8 ist.  
  
**-w** *Fixed_width_config_file*  
Pfad und Name der Konfigurationsdatei, die die Anzahl der Zeichen in jeder Spalte angibt. Jedes Feld muss angegeben werden.  
  
Diese Datei muss auf dem Server laden befinden. Der Pfad kann es sich um einen UNC-, relativer oder absoluter Pfad sein. Jede Zeile in *Fixed_width_config_file* enthält den Namen einer Spalte und die Anzahl der Zeichen für diese Spalte. Es wie folgt wird nur eine Zeile pro Spalte, und die Reihenfolge in der Datei muss die Reihenfolge, in der Zieltabelle entsprechen:  
  
*Column_name*=*Anzahl_Zeichen*  
  
*Column_name*=*Anzahl_Zeichen*  
  
Beispiel fester Breite der Datei "App.config":  
  
SalesCode = 3  
  
SalesID = 10  
  
Beispiel werden Zeilen in *Source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
Im vorherigen Beispiel wird die erste Zeile geladene haben, SalesCode = "230" und SalesID = "Shirts0056". Die zweite geladene Zeile müssen SalesCode = "320" und SaleID = "Towels1356".  
  
Informationen zum Behandeln von führende und nachfolgende Leerzeichen oder Daten typkonvertierung im Modus mit fester Breite finden Sie unter [Datentyp Konvertierungsregeln für Dwloader](dwloader-data-type-conversion-rules.md).  
  
**e -** *Character_encoding*  
Gibt einen Typ als zeichencodierung für die Daten aus der Datendatei geladen werden. Optionen sind ASCII (Standard), UTF8, UTF16-Format oder UTF16BE, wobei UTF16-Format little-endian und UTF16BE ist big-Endian. Diese Optionen sind Groß-/Kleinschreibung beachtet.  
  
Spalten mit fester Breite werden nicht unterstützt, wenn – e UTF8 ist.  
  
**R -** *Row_delimiter*  
Das Trennzeichen für jede Zeile der Quelldatendatei. Das Zeilentrennzeichen ist mindestens ein ASCII-Werte.  
  
Um ein Wagenrücklauf (CR), Zeilenvorschubzeichen (LF) oder Tabstoppzeichen als Trennzeichen angeben, können Sie die Escape-Zeichen ("\r", "\n", "\t") oder ihre hexadezimale Werte (0 X, 0d 09) verwenden. Verwenden Sie zum Angeben eines anderen Sonderzeichen als Trennzeichen ihren Hexadezimalwert.  
  
Beispiele für CR-LF:  
  
R - \r\n  
  
-R 0x0d0x0a  
  
Beispiele für CR:  
  
R - \r  
  
-R 0x0d  
  
Beispiele für LF:  
  
R - \n  
  
-R 0x0a  
  
Ein LF ist erforderlich für Unix. Ein CR ist erforderlich für Windows.  
  
**-D** { **Ymd** | Ydm | Mdy | Myd |  DMY | Dym | *Custom_date_format* }  
Gibt die Reihenfolge der Monat (m), (d) Tag und Jahr (y) für alle Datetime-Felder in der Eingabedatei an. Die Standardreihenfolge ist Ymd. Um mehrere Formate der gleichen Quelldatei Reihenfolge anzugeben, verwenden Sie die – dt-Option.  
  
YMD | DMY  
Das Ydm und Dmy können die gleichen Eingabeformaten. Beide ermöglichen das Jahr am Anfang oder Ende des Datums sein. Z. B. für beide **Ydm** und **Dmy** Datumsformate, 2013-02-03 oder 2013-02-03-konnte in der Eingabedatei haben.  
  
Das ydm  
Sie können nur als Ydm in Spalten vom Datentyp Datetime und Smalldatetime formatierte Eingabe laden. Das Ydm-Werte können nicht in eine Spalte des datetime2, Datum oder "DateTimeOffset"-Datentyp nicht geladen werden.  
  
dmy  
ermöglicht das Mdy <month> <space> <day> <comma> <year>.  
  
Beispiele für Mdy Eingabedaten für das am 1. Januar 1975:  
  
-   1. Januar 1975  
  
-   01 Jan 75  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
Geben Sie Beispiele für die Datei unter dem Monat März 04,2010: 03-2010-04, 2010/3/4  
  
dym  
Beispiele für die Datei als Eingabe für die 04 März 2010: 04-2010-03, 4/2010/3.  
  
*custom_date_format*  
*Custom_date_format* ist ein benutzerdefinierten Datumsformat (z. B. MM/TT/JJJJ) und nur für Abwärtskompatibilität enthalten. Dwloader wird nicht Enfoce das benutzerdefinierte Datumsformat. Wenn Sie stattdessen ein benutzerdefiniertes Datumsformat angeben **Dwloader** in die entsprechende Einstellung Ymd, Ydm, Mdy, MYD-, Dym oder Dmy konvertiert wird.  
  
Wenn Sie den – D MM/TT/JJJJ angeben, erwartet Dwloader z. B. alle Datum Eingabe mit Monat sortiert werden, zunächst dann Tag und anschließend im Jahr (Mdy). 2 Zeichen Monate, 2 Tage für Ziffern und 4 Ziffern entsprechend den Angaben von der benutzerdefinierten Datumsformat erzwungen nicht. Hier sind einige Beispiele für Methoden, die Datumsangaben in der Eingabedatei formatiert werden, können Wenn das Datumsformat – D MM/TT/JJJJ ist: 01/02/2013 Jan.02.2013, 1/2/2013  
  
Umfassendere Formatierungsinformationen, finden Sie unter [Datentyp Konvertierungsregeln für Dwloader](dwloader-data-type-conversion-rules.md).  
  
**dt -** *Datetime_format_file*  
Jedes Format "DateTime" wird angegeben, in einer Datei namens *Datetime_format_file*. Im Gegensatz zu den Befehlszeilenparametern müssen nicht den Parametern, die Leerzeichen enthalten, in doppelte Anführungszeichen eingeschlossen werden. Das Format "DateTime" kann nicht geändert werden, wie Sie Daten laden. Die Quelldatei und der entsprechenden Spalte in der Zieltabelle müssen das gleiche Format aufweisen.  
  
Jede Zeile enthält den Namen einer Spalte in die Zieltabelle und das Format "DateTime".  
  
Beispiele:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d:** *Staging_database_name*  
Der Name der Datenbank, die die Stagingtabelle enthalten soll. Der Standardwert ist die Datenbank mit der Option "-T", also die Datenbank für die Zieltabelle angegeben. Weitere Informationen zur Verwendung einer Stagingdatenbank finden Sie unter [die Staging-Datenbank erstellen](staging-database.md).  
  
**M -** *Load_mode_option*  
Gibt an, ob für anfügen, Upsert, oder die Daten neu laden. Der Standardmodus ist angefügt werden soll.  
  
Anfügen  
Das Ladeprogramm Zeilen am Ende der vorhandenen Zeilen in der Zieltabelle eingefügt.  
  
fastappend  
Das Ladeprogramm Zeilen direkt, ohne eine temporäre Tabelle, bis zum Ende der vorhandenen Zeilen in die Zieltabelle eingefügt. Fastappend erfordert die Multi-Transaktion (– m) Option. Eine staging-Datenbank kann nicht angegeben werden, wenn Fastappend verwenden. Es ist kein Rollback mit Fastappend, was bedeutet, dass die Wiederherstellung aus einer fehlerhaften oder abgebrochenen Last vom Auslastungstest-Prozess verarbeitet werden muss.  
  
Upsert **-K***Merge_column* [,... *n* ]    
Das Ladeprogramm verwendet die SQL Server-Merge-Anweisung, um vorhandene Zeilen aktualisiert, und fügen Sie neue Zeilen.  
  
Die Option-K gibt die Spalte(n) auf die Zusammenführung basieren. Diese Spalten bilden einen Merge-Schlüssel, der eine eindeutige Zeile darstellen soll. Wenn der Merge-Schlüssel in der Zieltabelle vorhanden ist, wird die Zeile aktualisiert. Wenn der Merge-Schlüssel in der Zieltabelle nicht vorhanden ist, wird die Zeile angefügt.  
  
Für Tabellen mit Hash verteilt muss der Merge-Schlüssel werden oder die verteilungsspalte enthalten.  
  
Bei replizierten Tabellen ist der Merge-Schlüssel der Kombination aus einer oder mehreren Spalten. Diese Spalten werden entsprechend den Anforderungen der Anwendung angegeben.  
  
Mehrere Spalten müssen ohne Leerzeichen, Kommas oder Leerzeichen durch Kommas getrennt und in einfache Anführungszeichen eingeschlossen sein.  
  
Zwei Zeilen in der Quelltabelle übereinstimmenden Merge Schlüsselwerte aufweisen, müssen ihre jeweiligen Zeilen identisch sein.  
  
zum erneuten Laden  
Das Ladeprogramm schneidet die Zieltabelle ab, bevor die Daten eingefügt.  
  
**-b** *Batchsize*  
Nur für die Verwendung von Microsoft-Support empfohlen *Batchsize* beträgt die Batchgröße von SQL Server für das Massenkopieren, die in SQL Server-Instanzen auf den Serverknoten DMS ausführt.  Wenn *Batchsize* angegeben ist, wird SQL Server PDW überschreibt die Batchgröße für das Laden, die bei jedem Laden dynamisch berechnet wird.  
  
Ab SQL Server 2012 PDW, berechnet der Steuerelementknoten dynamisch eine Batchgröße bei jedem Laden standardmäßig. Diese automatische Berechnung basiert auf mehreren Parametern wie Arbeitsspeichergröße, Zieltyp für die Tabelle, Tabelle Zielschema, Typ der arbeitsauslastung, Dateigröße und Ressourcenklasse des Benutzers.  
  
Z. B. wenn der Auslastungstest-Modus FASTAPPEND ist und die Tabelle einen gruppierten columnstore-Index, SQL Server PDW wird vom Standard wurde versucht, eine Batchgröße von 1.048.576 verwenden, sodass Zeilengruppen geschlossen werden, und Laden direkt im columnstore-Index ohne durchlaufen die deltastore. Wenn die Batchgröße von 1.048.576 von Arbeitsspeicher nicht möglich ist, werden Dwloader, wählen Sie eine kleinere Batchgröße.  
  
Wenn der Typ der arbeitsauslastung FASTAPPEND, ist die *Batchsize* gilt für das Laden von Daten in die Tabelle, andernfalls *Batchsize* gilt für das Laden von Daten in die Stagingtabelle.  
  
< Reject_options >  
Gibt die Optionen zum Bestimmen der Anzahl der Fehler beim Laden, die das Ladeprogramm ermöglichen. Wenn der Fehler beim Laden der Schwellenwert überschritten wird, wird das Ladeprogramm anzuhalten und keinen Commit für alle Zeilen.  
  
**-rt** { **Wert** | Prozentsatz}  
Gibt an, ob die -*Reject_value* in der **-rv** *Reject_value* Option ist ein literal Anzahl von Zeilen (Wert) oder einer Rate von Fehler (in Prozent). Der Standardwert ist Wert.  
  
Der Prozentsatz-Option ist eine Echtzeit-Berechnung, die in Abständen entsprechend der Rs - Option erfolgt.  
  
Beispielsweise ist, wenn das Ladeprogramm 100 Zeilen und 25 laden Versuch ein Fehler auf, und 75 erfolgreich ausgeführt werden, klicken Sie dann die Fehlerrate 25 %.  
  
**-rv** *Reject_value*  
Gibt die Anzahl oder den Prozentsatz der Zeile ablehnungen, um zuzulassen, bevor Sie die Last anhalten. Die **-rt** Option bestimmt, ob *Reject_value* bezieht sich auf die Anzahl der Zeilen oder den Prozentsatz der Zeilen.  
  
Die Standardeinstellung *Reject_value* ist 0.  
  
Bei Verwendung mit -rt Wert beendet das Ladeprogramm die Last aus, wenn die abgelehnte Zeilenanzahl Reject_value überschreitet.  
  
Wenn mit -rt Prozentsatz verwenden, das Ladeprogramm berechnet den Prozentsatz in Intervallen (-Rs-Option). Aus diesem Grund kann der Prozentsatz von fehlerhaften Zeilen überschreiten *Reject_value*.  
  
**Rs -** *Reject_sample_size*  
Verwendet die `-rt percentage` Option, um die Überprüfungen inkrementelle Prozentsatz anzugeben. Z. B. wenn Reject_sample_size 1000 ist, wird das Ladeprogramm berechnen Sie den Prozentsatz von fehlerhaften Zeilen nach 1000 Zeilen zu laden versucht hat. Sie berechnet den Prozentsatz von fehlerhaften Zeilen neu, nachdem er versucht, jede zusätzliche 1000 Zeilen zu laden.  
  
**-c**  
Entfernt Leerstellen vom linken und rechten Seite des Char, Nchar, Varchar und Nvarchar-Felder. Konvertiert jedes Feld, das nur Leerzeichen auf die leere Zeichenfolge enthält.  
  
Beispiele:  
  
"" wird abgeschnitten, um "  
  
'Abc' wird zu 'Abc' abgeschnitten.  
  
Bei der – c mit -E, Eintritt der – E Vorgang zuerst. Felder, die nur Leerstellen enthalten, werden auf die leere Zeichenfolge, und nicht auf NULL konvertiert.  
  
**-E**  
Konvertieren Sie leere Zeichenfolgen in NULL. Standardmäßig werden diese Konvertierungen nicht ausführen.  
  
**-m**  
Verwenden Sie mit mehreren Transaktionsmodus für die zweite Phase des Ladevorgangs. Beim Laden von Daten aus der Stagingtabelle in eine verteilte Tabelle.  
  
Mit **– m**, SQL Server PDW ausführt und führt einen Commit für lädt parallel. Dies viel schneller als die Standardzeit Lademodus führt jedoch nicht Transaktion-sicher ist.  
  
Ohne **– m**, SQL Server PDW ausführt und führt einen Commit für lädt Seriell über die Verteilungen in jedem Knoten der COMPUTE- und gleichzeitig über den Serverknoten. Diese Methode ist langsamer als mit mehreren Transaktionsmodus, aber Transaktion-sicher ist.  
  
**m -** ist optional für *Anfügen*, *laden*, und *Upsert*.  
  
**m -** für Fastappend ist erforderlich.  
  
**-m** bei replizierten Tabellen nicht verwendet werden.  
  
**-m** gilt nur für die zweite Phase der laden. Es gilt nicht für die erste Phase der laden; Laden von Daten in die Stagingtabelle ein.  
  
Es ist kein Rollback mit Multi-Transaktionsmodus, was bedeutet, dass die Wiederherstellung aus einer fehlerhaften oder abgebrochenen Last vom Auslastungstest-Prozess verarbeitet werden muss.  
  
Es wird empfohlen, **– m** nur, wenn in eine leere Tabelle laden, damit Sie ohne Datenverlust wiederherstellen können. Die Wiederherstellung eines Ladefehlers: Löschen Sie die Zieltabelle, beheben Sie das Problem laden, Neuerstellen die Zieltabelle und führen Sie die Last dann erneut aus.  
  
**-N**  
Stellen Sie sicher, dass das Zielgerät ein gültiges SQL Server PDW-Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle verfügt. Hiermit können Sie gewährleisten, Ihre Daten wird nicht von einem Angreifer übernommen und in einem nicht autorisierten Speicherort gesendet. Das Zertifikat muss bereits auf dem Gerät installiert werden. Die einzige Möglichkeit zum Installieren des Zertifikats ist für den Administrator der Appliance, es mit dem Configuration Manager-Tool zu installieren. Bitten Sie Ihren Appliance-Administrator, wenn Sie nicht sicher sind, ob das Gerät ein vertrauenswürdiges Zertifikat installiert wurde.  
  
**Se-**  
Überspringen Sie das Laden von leere Dateien. Dies lässt auch Dekomprimieren leere Gzip-Dateien.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
0 (Erfolg) oder andere ganzzahlige Wert (Fehler)  
  
Verwenden Sie eine Befehlsdatei Fenster oder einen Batch `errorlevel` den Rückgabecode angezeigt. Beispiel:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
Verwenden Sie bei Verwendung von PowerShell `$LastExitCode`.  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert LOAD-Berechtigung und die entsprechenden Berechtigungen (INSERT, UPDATE, DELETE) für die Zieltabelle an. Erfordert die Berechtigung "erstellen" (für das Erstellen einer temporären Tabelle) für die staging-Datenbank. Wenn eine Stagingdatenbank nicht verwendet wird, ist die Berechtigung "erstellen" in der Zieldatenbank erforderlich. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
Informationen zu datentypkonvertierungen mit Dwloader laden, finden Sie unter [Datentyp Konvertierungsregeln für Dwloader](dwloader-data-type-conversion-rules.md).  
  
Wenn ein Parameter ein oder mehrere Leerzeichen enthält, setzen Sie den Parameter in doppelte Anführungszeichen.  
  
Sie sollten das Ladeprogramm aus dem Installationsverzeichnis ausführen. Die ausführbare Dwloader ist bereits mit dem Gerät installiert und befindet sich im Verzeichnis C:\Program Files\Microsoft SQL Server Data Warehouse\DWLoader.  
  
Sie können einen Parameter, die in der Parameterdatei angegeben wird außer Kraft setzen (-f-Option) wird, indem dieser als Befehlszeilenparameter.  
  
Sie können mehrere Instanzen des Ladeprogramms gleichzeitig ausführen. Die maximale Anzahl von Instanzen Ladeprogramm ist vorkonfiguriert und kann nicht geändert werden. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
Geladene Daten möglicherweise mehr oder weniger Speicherplatz auf dem Gerät als in den Quellspeicherort. Sie können Test-Importe mit Teilmengen der Daten zu schätzen Sie Verbrauch Datenträger ausführen.  
  
Obwohl **Dwloader** ist ein Prozess Transaction und Rollback ordnungsgemäß bei einem Fehler, sie kann nicht zurückgesetzt werden, zurückgesendet, sobald das Massenladen erfolgreich abgeschlossen wurde. Abbrechen von einer aktiven **Dwloader** verarbeiten, geben Sie STRG + C.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
Die Gesamtgröße aller Lasten, die gleichzeitig ausgeführt werden, muss kleiner als LOG_SIZE für die Datenbank, und es empfiehlt sich die Gesamtgröße der alle gleichzeitigen lädt ist weniger als 50 % der der LOG_SIZE. Um diese maximale Größe zu erreichen, können Sie große Lasten in mehrere Batches aufteilen. Weitere Informationen zu LOG_SIZE, finden Sie unter [CREATE DATABASE](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
Beim Laden mehrerer Dateien mit einer Last-Befehl werden alle abgelehnte Zeilen in der gleichen Reject-Datei geschrieben. Die Reject-Datei werden nicht angezeigt, welche Eingabedatei jede abgelehnte Zeile enthält.  
  
Die leere Zeichenfolge sollte nicht als Trennzeichen verwendet werden. Wenn eine leere Zeichenfolge als ein Zeilentrennzeichen verwendet wird, schlägt das Laden fehl. Bei Verwendung als Trennzeichen für Spalten wird die Last ignoriert das Trennzeichen und setzt die den Standardwert "|" als Spaltentrennzeichen. Die leere Zeichenfolge wird ignoriert, wenn als Zeichenfolgentrennzeichen verwendet wird, und das Standardverhalten angewendet wird.  
  
## <a name="locking-behavior"></a>Sperrverhalten  
**Dwloader** Sperrverhalten variiert je nach den *Load_mode_option*.  
  
-   **append** – Append ist die empfohlene und die am häufigsten verwendete Option. Fügen Sie lädt Daten in eine Stagingtabelle ein. Das Sperren wird nachfolgend detailliert beschrieben.  
  
-   **Schnelle Anfügen** – lädt direkt in der endgültigen Tabelle eine Tabellensperre ExclusiveUpdate dauert Fast anfügen, und ist der einzige Modus, der keine Stagingtabelle verwendet.  
  
-   **Laden** – laden Lädt Daten in eine Stagingtabelle und eine exklusive Sperre für die Stagingtabelle und die endgültige Tabelle erfordert. Zum erneuten Laden wird für gleichzeitige Vorgänge nicht empfohlen.  
  
-   **Upsert** – Upsert lädt Daten in eine Stagingtabelle, und führt dann einen Merge-Vorgang aus der Stagingtabelle an der endgültigen Tabelle. Upsert erfordert keine exklusive Sperren für die neue Tabelle. Leistung bei Verwendung von Upsert weicht möglicherweise ab. Testen Sie das Verhalten in Ihrer Umgebung.  
  
### <a name="locking-behavior"></a>Sperrverhalten  
**Eine Append-Modus sperren**  
  
Anfügen kann in mehreren im Transaktionsmodus ausgeführt wird (mit dem – m-Argument) ausgeführt werden jedoch nicht sichere Transaktion. Fügen Sie aus diesem Grund sollte als ein Transaktionsvorgang (ohne den – m-Argument) verwendet werden. Leider ist während des letzten INSERT SELECT Vorgangs im Transaktionsmodus aktuell ungefähr sechs Mal langsamer als die mit mehreren Transaktionsmodus ausgeführt wird.  
  
Append-Modus lädt Daten in zwei Phasen. Stufe eins lädt Daten aus der Quelldatei, in eine Stagingtabelle gleichzeitig (Fragmentierung erfolgen kann). Phase zwei werden Daten aus der Stagingtabelle in der endgültigen Tabelle geladen. Die zweite Phase führt eine **INSERT INTO... Wählen Sie WITH (TABLOCK)** Vorgang. Die folgende Tabelle zeigt das Sperrverhalten für die endgültige Tabelle und Protokollierungsverhalten Verwendung append-Modus:  
  
|Tabellentyp|Multi-Transaktion<br />Modus (-m)|Tabelle ist leer.|Parallelität unterstützt|Protokollierung|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Heap|ja|ja|ja|minimale|  
|Heap|ja|Nein|ja|minimale|  
|Heap|Nein|Ja|Nein|minimale|  
|Heap|Nein|Nein|Nein|minimale|  
|CL|ja|ja|Nein|minimale|  
|CL|ja|Nein|ja|Full|  
|CL|Nein|Ja|Nein|minimale|  
|CL|Nein|Nein|ja|Full|  
  
Die oben aufgeführten Tabelle zeigt **Dwloader** mit der Append-Modus in einem Heap oder gruppierten Index (CI) Tabelle, mit oder ohne das Multi-Transaktions-Flag beim Laden und in eine leere Tabelle oder eine nicht leere Tabelle zu laden. Der Sperr- und Protokollierungsverhaltens Verhalten jeder solche Kombination laden wird in der Tabelle angezeigt. Z. B. Laden (2.) Phase mit der Append-Modus in einen gruppierten Index ohne Multi-Transaktionsmodus ausgeführt wird und in eine leere Tabelle haben PDW eine exklusive Sperre für die Tabelle zu erstellen und Protokollierung ist minimal. Dies bedeutet, dass ein Kunde kann nicht gleichzeitig (2.) Phase und Abfrage in eine leere Tabelle geladen werden. Allerdings mit der gleichen Konfiguration in eine nicht leere Tabelle zu laden, PDW keine exklusive Sperre für die Tabelle und zur Parallelität ist möglich. Leider wird vollständige Protokollierung verlangsamen des Prozesses.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-dwloader-example"></a>A. Einfache Dwloader-Beispiel  
Das folgende Beispiel zeigt die Initiierung der **Ladeprogramm** nur die erforderlichen Optionen aktiviert. Andere Optionen stammen aus der Konfigurationsdatei des globalen *loadparamfile.txt*.  
  
Beispiel für die Verwendung von SQL Server-Authentifizierung.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
Das gleiche Beispiel mit Windows-Authentifizierung.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
Beispiel für die Verwendung der Argumente für eine Quelldatei und die Fehlerdatei.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Laden Sie Daten in eine Tabelle der AdventureWorks  
Das folgende Beispiel ist Teil eines Batchskripts, die Daten in lädt **AdventureWorksPDW2012**.  Um das vollständige Skript anzuzeigen, öffnen Sie die aw_create.bat-Datei, die im Lieferumfang der **AdventureWorksPDW2012** Installationspaket. 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

Der folgende Codeausschnitt verwendet Dwloader zum Laden von Daten in die Tabellen DimAccount und DimCurrency. Dieses Skript wird eine Ethernetadresse verwendet. Wenn es InfiniBand verwendet wurde, wäre Server *< Appliance_name >*`-SQLCTL01`.  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
Im folgenden wird der DDL-Code für die DimAccount-Tabelle.  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
Im folgenden ist ein Beispiel für die Datendatei DimAccount.txt, die Daten geladen wurden in die Tabelle DimAccount enthält.  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. Laden von Daten über die Befehlszeile  
Das Skript in Beispiel B kann hierzu alle Parameter in der Befehlszeile ersetzt werden, wie im folgenden Beispiel gezeigt.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe –S <Control node IP> -E –M reload –e UTF16 -i .\DimAccount.txt –T AdventureWorksPDW2012.dbo.DimAccount –R DimAccount.bad –t "|" –r \r\n –U <login> -P <password>  
```  
  
Beschreibung der Befehlszeilenparameter:  
  
-   *C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe* Installationsort der dwloader.exe ist.  
  
-   *-S* gefolgt von der IP-Adresse des steuerungsknotens.  
  
-   *E -* gibt an, dass Sie leere Zeichenfolgen als NULL laden.  
  
-   *Laden Sie -M* gibt an, dass die Zieltabelle abgeschnitten werden, bevor die Daten eingefügt.  
  
-   *– e UTF16* die Quelldatei verwendeten Zeichencodierungstyp mit little-endian angibt.  
  
-   *-i.\DimAccount.txt* gibt an, die Daten in einer Datei namens DimAccount.txt, die im aktuellen Verzeichnis vorhanden ist.  
  
-   *T - AdventureWorksPDW2012.dbo.DimAccount* gibt den Namen der 3-Teil der Tabelle, die die Daten empfängt.  
  
-   *-R DimAccount.bad* gibt an, die Zeilen, die nicht geladen werden in eine Datei namens DimAccount.bad geschrieben.  
  
-   *– t "|"*  gibt an, die Felder in der Eingabedatei DimAccount.txt, durch einen senkrechten Strich getrennt werden.  
  
-   *R - \r\n* gibt jede Zeile in DimAccount.txt endet mit einem Wagenrücklauf und einem Zeilenvorschubzeichen.  
  
-   *-U < Login_name > – P <password>*  gibt den Anmeldenamen und das Kennwort für die Anmeldung, die Berechtigungen zum Ausführen der Last verfügt.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
