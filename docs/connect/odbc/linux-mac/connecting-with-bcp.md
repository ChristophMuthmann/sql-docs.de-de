---
title: Herstellen einer Verbindung mit "bcp" | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
caps.latest.revision: "33"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7e9db6a1ea636975a3f5719d9a1b3e9d5721eb6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-with-bcp"></a>Herstellen einer Verbindung mit bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Die [Bcp](http://go.microsoft.com/fwlink/?LinkID=190626) Dienstprogramm finden Sie in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS. Auf dieser Seite werden die Unterschiede gegenüber der Windows-Version des `bcp`.
  
- Das Feldabschlusszeichen ist ein Tabulator („\t“).  
  
- Das Zeilenabschlusszeichen ist ein Zeilenvorschub („\n“).  
  
- Zeichenmodus ist das bevorzugte Format für `bcp` formatieren, Dateien und Datendateien, die keine Sonderzeichen enthalten.  
  
> [!NOTE]  
> Ein umgekehrter Schrägstrich "\\" auf ein Befehlszeilenargument muss entweder in Anführungszeichen oder mit Escapezeichen versehen. Beispielsweise müssen ein Zeilenumbruch als benutzerdefiniertes Zeilenabschlusszeichen angeben, Sie einen der folgenden Mechanismen verwenden:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
Im folgenden finden Sie eine Beispiel-Befehlsaufruf von `bcp` zum Kopieren von Tabellenzeilen in eine Textdatei:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Verfügbare Optionen
In der aktuellen Version sind die folgende Syntax und Optionen verfügbar:  

[*database***.**]*schema***.***table* **in** *data_file* | **out** *data_file*

- -a *packet_size*  
Gibt an, wie viele Bytes pro Netzwerkpaket an den Server bzw. vom Server gesendet werden.  
  
- -b *batch_size*  
Gibt die Anzahl von Zeilen pro importierten Datenbatch an.  
  
- -c  
Verwendet einen Zeichendatentyp.  
  
- -d *database_name*  
Gibt die Datenbank an, mit der eine Verbindung hergestellt werden soll.  
  
- -d  
Bewirkt, dass der Wert, der zum Übergeben der `bcp` Option "-S" als einen Datenquellennamen (DSN) interpretiert werden. Weitere Informationen finden Sie unter "DSN-Unterstützung in Sqlcmd und Bcp" in [Herstellen einer Verbindung mit Sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md).  
  
- e - *Error_file* gibt der vollständige Pfad einer Fehlerdatei an, die zum Speichern von einem Zeilen werden, die `bcp` -Hilfsprogramm nicht aus der Datei in die Datenbank übertragen.  
  
- -e  
Verwendet für die Identitätsspalte in der importierten Datendatei einen Identitätswert oder -werte.  
  
- -f *format_file*  
Gibt den vollständigen Pfad einer Formatdatei an.  
  
- -F *first_row*  
Gibt die Nummer der ersten Zeile an, die aus einer Tabelle exportiert oder von einer Datendatei importiert werden soll.  
  
- -k  
Gibt an, dass während des Vorgangs keine Standardwerte in leere Spalten eingefügt werden, sondern ein NULL-Wert für diese Spalten beibehalten werden soll.  
  
- -l  
Gibt einen Anmeldungstimeout an. Die Option "– i" gibt die Anzahl der Sekunden, bevor Sie eine Anmeldung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ein Timeout eintritt, wenn Sie versuchen, eine Verbindung mit einem Server herstellen. Das Standardtimeout für die Anmeldung ist 15 Sekunden. Das Anmeldungstimeout muss eine Zahl zwischen 0 und 65534 sein. Wenn der angegebene Wert kein numerischer Wert ist oder außerhalb dieses Bereichs liegt, generiert `bcp` eine Fehlermeldung. Der Wert 0 gibt ein unbegrenztes Timeout.
  
- -L *last_row*  
Gibt die Nummer der letzten Zeile an, die aus einer Tabelle exportiert oder von einer Datendatei importiert werden soll.  
  
- -m *max_errors*  
Gibt die maximale Anzahl von Syntaxfehlern, die vor dem auftreten können die `bcp` Operation abgebrochen wird.  
  
- -n  
Verwendet die systemeigenen (Datenbank-) Datentypen, um den Massenkopiervorgang auszuführen.  
  
- -P *password*  
Gibt das Kennwort für die Anmelde-ID an.  
  
- -Q  
Führt die SET QUOTED_IDENTIFIERS ON-Anweisung in der Verbindung zwischen dem Hilfsprogramm `bcp` und einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-Instanz aus.  
  
- -r *row_terminator*  
Gibt das Zeilenabschlusszeichen an.  
  
- -r  
Gibt an, dass beim Massenkopieren von Währungs-, Datums- und Zeitdaten in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] das Länderformat verwendet wird, das durch die Gebietsschemaeinstellung des Clientcomputers definiert wird.  
  
- -S *server*  
Gibt den Namen des der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Instanz für die Verbindung, oder -D wird verwendet, einen DSN.  
  
- -t *field_terminator*  
Gibt das Feldabschlusszeichen an.  
  
- -T  
Gibt an, dass die `bcp` Hilfsprogramm Verbinden mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] über eine vertrauenswürdige Verbindung (integrierte Sicherheit).  
  
- -U *login_id*  
Gibt die Anmelde-ID an, die zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] verwendet wird.  
  
- -v  
Meldet die Versionsnummer und das Copyright für das Hilfsprogramm `bcp`.  
  
- -w  
Verwendet Unicode-Zeichen, um den Massenkopiervorgang auszuführen.  
  
In dieser Version werden Latin-1- und UTF-16-Zeichen unterstützt.  
  
## <a name="unavailable-options"></a>Nicht verfügbare Optionen
In der aktuellen Version sind die folgende Syntax und Optionen nicht verfügbar:  

- -c  
Gibt die Codepage für die in der Datendatei enthaltenen Daten an.  
  
- -h *hint*  
Gibt den oder die Hinweise an, die beim Massenimportieren von Daten in eine Tabelle oder Sicht verwendet werden.  
  
- -i *input_file*  
Gibt den Namen einer Antwortdatei an.  
  
- -n  
Verwendet die systemeigenen (Datenbank-) Datentypen für Daten, die keinen Zeichendatentyp haben, sowie Unicode-Zeichen für Zeichendaten.  
  
- -o *output_file*  
Gibt den Namen einer Datei an, in die die Ausgabe geschrieben wird, die von der Eingabeaufforderung umgeleitet wurde.  
  
- -V (80 | 90 | 100)  
Verwendet Datentypen aus einer früheren Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
- -x  
Bei Verwendung mit den Optionen Format und -f format_file wird anstelle der standardmäßigen Nicht-XML-Formatdatei eine XML-basierte Formatdatei generiert.  
  
## <a name="see-also"></a>Siehe auch

[Herstellen einer Verbindung mit **Sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
