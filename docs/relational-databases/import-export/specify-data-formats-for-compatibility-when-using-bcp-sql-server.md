---
title: "Angeben von Datenformaten f&#252;r die Kompatibilit&#228;t bei Verwendung von bcp (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Massenexport [SQL Server], Kompatibilität"
  - "Massenimport [SQL Server], Kompatibilität"
  - "Kompatibilität [SQL Server], Datenformate"
  - "Datenformate [SQL Server], Kompatibilität"
  - "bcp-Hilfsprogramm [SQL Server], Kompatibilität"
ms.assetid: cd5fc8c8-eab1-4165-9468-384f31e53f0a
caps.latest.revision: 38
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# Angeben von Datenformaten f&#252;r die Kompatibilit&#228;t bei Verwendung von bcp (SQL Server)
  In diesem Thema werden die Datenformatattribute, feldspezifischen Eingabeaufforderungen und das Speichern von Feld-nach-Feld-Daten in einer Formatdatei des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**bcp**-Befehls, die keine XML-Datei ist, beschrieben. Das Verständnis dieser Konzepte kann für Sie nützlich sein, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten für den Massenimport in ein anderes Programm, z. B. ein anderes Datenbankprogramm, mit einem Massenexportvorgang exportieren. Die Standarddatenformate in (systemeigen, Zeichen oder Unicode) der Quelltabelle können mit dem vom anderen Programm erwarteten Datenlayout inkompatibel sein. Falls eine Inkompatibilität vorliegt, müssen Sie beim Exportieren von Daten das Datenlayout beschreiben.  
  
> [!NOTE]  
>  Wenn Sie keine Erfahrung mit Datenformaten zum Importieren oder Exportieren von Daten haben, finden Sie Informationen unter [Datenformate für Massenimport oder Massenexport &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md).  
  
 **In diesem Thema:**  
  
-   [bcp-Datenformatattribute](#bcpDataFormatAttr)  
  
-   [Übersicht über die feldspezifischen Eingabeaufforderungen](#FieldSpecificPrompts)  
  
-   [Speichern von feldspezifischen Daten in einer Nicht-XML-Formatdatei](#FieldByFieldNonXmlFF)  
  
##  <a name="bcpDataFormatAttr"></a> bcp-Datenformatattribute  
 Mit dem **bcp**-Befehl können Sie die Struktur jedes Felds in einer Datendatei im Hinblick auf die folgenden Datenformatattribute angeben:  
  
-   Dateispeichertyp  
  
     Der *Dateispeichertyp* beschreibt, wie Daten in der Datendatei gespeichert werden. Daten können in eine Datendatei als Typ der Datenbanktabelle (systemeigenes Format), als Zeichendarstellung (Zeichenformat) oder als beliebiger Datentyp, bei dem die implizite Konvertierung unterstützt wird, exportiert werden. Beispielsweise kann ein **smallint** als ein **int** kopiert werden. Benutzerdefinierte Datentypen werden als Basistypen exportiert. Weitere Informationen finden Sie unter [Angeben des Dateispeichertyps mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
-   Präfixlänge  
  
     Als kompakteste Form der Dateispeicherung beim Massenexportieren von Daten im systemeigenen Format in eine Datendatei setzt der Befehl **bcp** mindestens ein Zeichen, das auf die Länge des Felds hinweist, vor jedes Feld. Diese Zeichen werden als *Längenpräfixzeichen*bezeichnet. Weitere Informationen finden Sie unter [Angeben der Präfixlänge in Datendateien mittels bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md).  
  
-   Feldlänge  
  
     Die Feldlänge weist auf die maximale Anzahl von Zeichen hin, die zum Darstellen der Daten im Zeichenformat benötigt werden. Die Feldlänge ist bereits bekannt, wenn die Daten im systemeigenen Format gespeichert werden. Weitere Informationen finden Sie unter [Angeben der Feldlänge mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md).  
  
-   Feldabschlusszeichen  
  
     Für Zeichendatenfelder kann mit optionalen abschließenden Zeichen das Ende jedes Felds in einer Datendatei (mithilfe eines *Feldabschlusszeichens*) und das Ende jeder Zeile (mithilfe eines *Zeilenabschlusszeichens*) markiert werden. Abschließende Zeichen sind eine Möglichkeit, um Programme, die die Datendatei lesen, darauf hinzuweisen, an welcher Stelle ein Feld oder eine Zeile endet und ein anderes Feld bzw. eine andere Zeile beginnt. Weitere Informationen finden Sie unter [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
 [&#91;Nach oben&#93;](#Top)  
  
##  <a name="FieldSpecificPrompts"></a> Übersicht über die feldspezifischen Eingabeaufforderungen  
 Wenn ein interaktiver **bcp**-Befehl die Option **in** oder **out**, jedoch keinen Formatdateischalter (**-f**) bzw. keinen Datenformatschalter (**-n**, **-c**, **-w** oder **-N**) für die Spalten der Quell- oder Zieltabelle enthält, fordert der Befehl zur Eingabe der vorherigen Attribute auf. Für jede Eingabeaufforderung stellt der Befehl **bcp** einen Standardwert basierend auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentyp der Tabellenspalte bereit. Wenn Sie den Standardwert für alle Eingabeaufforderungen übernehmen, erhalten Sie dieselben Ergebnisse wie beim Angeben des systemeigenen Formats (**-n**) in der Befehlszeile. Für jede Eingabeaufforderung wird ein Standardwert in eckigen Klammern angezeigt: [*Standard*]. Durch Drücken der EINGABETASTE wird der angezeigte Standardwert übernommen. Wenn Sie einen Wert angeben möchten, der vom Standardwert abweicht, geben Sie den neuen Wert an der Eingabeaufforderung ein.  
  
### Beispiel  
 Im folgenden Beispiel werden mit dem Befehl **bcp** Daten aus der `HumanResources.myTeam` -Tabelle interaktiv in die Datei `myTeam.txt` massenexportiert. Bevor Sie das Beispiel ausführen können, müssen Sie diese Tabelle erstellen. Informationen zu dieser Tabelle und zum Erstellen der Tabelle finden Sie unter [HumanResources.myTeam-Beispieltabelle &#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md).  
  
 Der Befehl gibt weder eine Formatdatei noch einen Datentyp an, weshalb **bcp** zur Eingabe von Datenformatinformationen auffordert. Geben Sie an der Eingabeaufforderung von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Folgendes ein:  
  
```  
bcp AdventureWorks.HumanResources.myTeam out myTeam.txt -T  
```  
  
 bcp fordert für jede Spalte zur Eingabe feldspezifischer Werte auf. Das folgende Beispiel zeigt die feldspezifischen Eingabeaufforderungen für die Spalten `EmployeeID` und `Name` der Tabelle und schlägt den Standard-Dateispeichertyp (systemeigenes Format) für jede Spalte vor. Die Präfixlängen der Spalten `EmployeeID` und `Name` betragen 0 bzw. 2. Der Benutzer gibt ein Komma (`,`) als Feldabschlusszeichen für jedes Feld an.  
  
 `Enter the file storage type of field EmployeeID [smallint]:`  
  
 `Enter prefix-length of field EmployeeID [0]:`  
  
 `Enter field terminator [none]:,`  
  
 `Enter the file storage type of field Name [nvarchar]:`  
  
 `Enter prefix length of field Name [2]:`  
  
 `Enter field terminator [none]:,`  
  
 `.`  
  
 `.`  
  
 `.`  
  
 Gleichwertige Eingabeaufforderungen (soweit erforderlich) werden für jede Tabellenspalte angezeigt.  
  
 [&#91;Nach oben&#93;](#Top)  
  
##  <a name="FieldByFieldNonXmlFF"></a> Speichern von feldspezifischen Daten in einer Nicht-XML-Formatdatei  
 Nachdem alle Tabellenspalten angegeben wurden, werden Sie vom **bcp**-Befehl gefragt, ob optional eine Nicht-XML-Formatdatei generiert werden soll, in der die gerade eingegebenen feldspezifischen Informationen gespeichert werden (siehe vorheriges Beispiel). Wenn Sie eine Formatdatei generieren, können Sie diese beim Exportieren von Daten aus dieser Tabelle oder Importieren identisch strukturierter Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden.  
  
> [!NOTE]  
>  Mithilfe der Formatdatei können Sie Daten aus der Datendatei in eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] massenimportieren oder Daten aus der Tabelle massenexportieren, ohne das Format erneut angeben zu müssen. Weitere Informationen finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
 Das folgende Beispiel erstellt die Nicht-XML-Formatdatei `myFormatFile.fmt`:  
  
 `Do you want to save this format information in a file? [Y/n] y`  
  
 `Host filename: [bcp.fmt]myFormatFile.fmt`  
  
 Der Standardname der Formatdatei ist bcp.fmt, Sie können aber einen anderen Dateinamen angeben.  
  
> [!NOTE]  
>  Für eine Datendatei, die ein einziges Datenformat für den Dateispeichertyp verwendet, wie z.B. das Zeichenformat oder das native Format, können Sie mit der Option **format** schnell eine Formatdatei erstellen, ohne Daten zu exportieren oder zu importieren. Diese Vorgehensweise hat den Vorteil, dass sie einfach ist und die Möglichkeit bietet, eine XML-Formatdatei oder eine Nicht-XML-Formatdatei zu erstellen. Weitere Informationen finden Sie unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
 [&#91;Nach oben&#93;](#Top)  
  
## Verwandte Aufgaben  
  
-   [Angeben des Dateispeichertyps mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
-   [Angeben der Präfixlänge in Datendateien mittels bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Angeben der Feldlänge mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)  
  
-   [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
## Verwandte Inhalte  
 Keine.  
  
## Siehe auch  
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [Datenformate für Massenimport oder Massenexport &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  