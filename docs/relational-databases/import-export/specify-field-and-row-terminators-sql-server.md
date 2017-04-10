---
title: "Angeben von Feld- und Zeilenabschlusszeichen (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "08/10/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "bcp-Hilfsprogramm [SQL Server], Abschlusszeichen"
  - "Feldabschlusszeichen [SQL Server]"
  - "Datenformate [SQL Server], Abschlusszeichen"
  - "Zeilenabschlusszeichen [SQL Server]"
  - "Abschlusszeichen [SQL Server]"
ms.assetid: f68b6782-f386-4947-93c4-e89110800704
caps.latest.revision: 39
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 39
---
# Angeben von Feld- und Zeilenabschlusszeichen (SQL Server)
  Für Zeichendatenfelder geben Ihnen optionale Abschlusszeichen die Möglichkeit, das Ende jedes Felds in einer Datendatei mit einem *Feldabschlusszeichen* und das Ende jeder Zeile mit einem *Zeilenabschlusszeichen*zu markieren. Abschlusszeichen stellen eine Möglichkeit dar, für Datendatei lesende Programmen anzugeben, wo ein Feld oder eine Zeile endet und ein anderes Feld oder eine andere Zeile beginnt.  
  
> [!IMPORTANT]  
>  Verwenden Sie beim systemeigenen Format oder systemeigenen Unicode-Format Längenpräfixe anstelle der Feldabschlusszeichen. Bei Daten im nativen Format kann es zu Konflikten mit Abschlusszeichen kommen, weil Datendateien im nativen Format im internen Binärdatenformat von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert werden.  
  
## Als Abschlusszeichen unterstützte Zeichen  
 Von dem Befehl **bcp** , der BULK INSERT-Anweisung und dem OPENROWSET BULK-Rowsetanbieter wird eine Reihe von Zeichen als Feld- oder Zeilenabschlusszeichen unterstützt und in jedem Fall nach der ersten Instanz jedes Abschlusszeichens gesucht. In der folgenden Tabelle sind die als Abschlusszeichen unterstützten Zeichen aufgeführt.  
  
|Abschlusszeichen|Kennzeichen|  
|---------------------------|------------------|  
|Registerkarte|\t<br /><br /> Dies ist das Standardfeldabschlusszeichen.|  
|Neue-Zeile-Zeichen|\n<br /><br /> Dies ist das Standardzeilenabschlusszeichen.|  
|Wagenrücklauf/Zeilenvorschub|\r|  
|Umgekehrter Schrägstrich*|\\\|  
|NULL-Abschlusszeichen (nicht sichtbares Abschlusszeichen)**|\0|  
|Jedes Zeichen, das gedruckt werden kann (Steuerzeichen können nicht gedruckt werden, ausgenommen Null, Tabstopp, Neue Zeile und Wagenrücklauf)|(*, A, t, l usw.)|  
|Eine Zeichenfolge von bis zu 10 Zeichen, die gedruckt werden können, einschließlich einiger oder aller oben aufgeführten Abschlusszeichen|(**\t\*\*, Ende, !!!!!!!!!!, \t - \n usw.)|  
  
 *Um ein Steuerzeichen zu erzeugen, können in Verbindung mit dem Escapezeichen des umgekehrten Schrägstrichs nur die Zeichen t, n, r, 0 und '\0' verwendet werden.  
  
 **Obwohl das NULL-Steuerzeichen (\0) beim Drucken nicht sichtbar ist, handelt es sich dabei um ein eigenständiges Zeichen in der Datendatei. Dies bedeutet, dass das Verwenden des Null-Steuerzeichens als Feld- oder Zeilenabschlusszeichen einen Unterschied dazu darstellt, überhaupt kein Feld- oder Zeilenabschlusszeichen zu verwenden.  
  
> [!IMPORTANT]  
>  Wenn ein Abschlusszeichen innerhalb der Daten auftritt, wird es als Abschlusszeichen, nicht als Daten interpretiert, und die Daten nach diesem Zeichen als zum nächsten Feld oder Datensatz zugehörig interpretiert. Wählen Sie deshalb die Abschlusszeichen mit Bedacht aus, um sicherzustellen, dass sie nicht anderweitig in Ihren Daten vorkommen. Beispielsweise ist ein niedriges Ersatzzeichen als Feldabschlusszeichen keine gute Wahl, wenn die Daten dieses niedrige Ersatzzeichen enthalten.  
  
## Verwenden von Zeilenabschlusszeichen  
 Beim Zeilenabschlusszeichen kann es sich um das gleiche Zeichen wie dem Abschlusszeichen für das letzte Feld handeln. Im Allgemeinen ist allerdings ein eigenständiges Zeilenabschlusszeichen nützlich. Bei tabellarischer Ausgabe beenden Sie beispielsweise das letzte Feld in jeder Zeile mit dem Neue-Zeile-Zeichen (\n) und alle anderen Felder mit dem Tabstoppzeichen (\t). Um jeden Datensatz auf eine eigene Zeile in der Datendatei zu platzieren, geben Sie die Kombination \r\n als Zeilenabschlusszeichen an.  
  
> [!NOTE]  
>  Wenn Sie **bcp** interaktiv verwenden und \n (Zeilenvorschub) als Zeilenabschlusszeichen angeben, wird dieses Zeichen von **bcp** automatisch mit dem Präfix \r (Wagenrücklauf) versehen, womit als Ergebnis das Zeilenabschlusszeichen \r\n steht.  
  
## Angeben von Abschlusszeichen für den Massenexport  
 Wenn Sie beim Massenexport von **char** oder **nchar**-Daten ein nicht-standardmäßiges Abschlusszeichen verwenden möchten, müssen Sie das Abschlusszeichen für den Befehl **bcp** angeben. Zum Angeben der Abschlusszeichen stehen die folgenden Möglichkeiten zur Verfügung:  
  
-   Mit einer Formatdatei, in der das Abschlusszeichen Feld für Feld angegeben wird.  
  
    > [!NOTE]  
    >  Informationen zur Verwendung von Formatdateien finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Ohne Formatdatei gibt es die folgenden Alternativen:  
  
    -   Verwenden des Schalters **-t** zum Angeben des Feldabschlusszeichens für alle Felder mit Ausnahme des letzten Felds in einer Zeile, und Verwenden des Schalters **-r** zum Angeben eines Zeilenabschlusszeichens.  
  
    -   Verwenden eines Zeichenformatschalters (**-c** oder **-w**) ohne den Schalter **-t**, womit als Feldabschlusszeichen das Tabulatorzeichen (\t) festgelegt wird. Dies entspricht der Angabe von **-t**\t.  
  
        > [!NOTE]  
        >  Wenn Sie den Schalter **-n** (native Daten) oder den Schalter **-N** (native Unicode-Daten) angeben, werden keine Abschlusszeichen eingefügt.  
  
    -   Wenn ein interaktiver Befehl **bcp** die Option **in** oder **out** ohne den Formatdateischalter (**-f**) oder einen Datenformatschalter (**-n**, **-c**, **-w** oder **-N**) enthält, und Sie keine Präfixlänge und Feldlänge angegeben haben, erfordert der Befehl die Eingabe des Feldabschlusszeichens für jedes Feld (standardmäßig kein Abschlusszeichen):  
  
         `Enter field terminator [none]:`  
  
         Im Allgemeinen ist der Standard angemessen. Beachten Sie jedoch bei **char** - und **nchar** -Datenfeldern den folgenden Unterabschnitt "Richtlinien für die Verwendung von Abschlusszeichen". Ein Beispiel, das die Verwendung der Aufforderung im Kontext veranschaulicht, finden Sie unter [ Angeben von Datenformaten für die Kompatibilität bei Verwendung von „bcp“ &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
        > [!NOTE]  
        >  Nachdem Sie interaktiv alle Felder in einem **bcp**-Befehl angegeben haben, werden Sie vom Befehl dazu aufgefordert, Ihre Antworten für die einzelnen Felder in einer Nicht-XML-Formatdatei zu speichern. Weitere Informationen zu Nicht-XML-Formatdateien finden Sie unter [Nicht-XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
### Richtlinien für die Verwendung von Abschlusszeichen  
 In einigen Fällen ist ein Abschlusszeichen für **char** - oder **nchar** -Datenfelder nützlich. Beispiel:  
  
-   Für eine Datenspalte, die einen NULL-Wert in einer Datendatei enthält, die in ein Programm importiert wird, das die Präfixlängeninformation nicht interpretieren kann.  
  
     Jede Datenspalte, die einen NULL-Wert enthält, gilt als Spalte variable Länge. Wenn keine Präfixlängen vorhanden sind, wird ein Abschlusszeichen benötigt, um das Ende eines NULL-Felds zu identifizieren und sicherzustellen, dass die Daten ordnungsgemäß interpretiert werden.  
  
-   Für eine lange Spalte mit fester Länge, deren Breite von vielen Zeilen nicht vollständig genutzt wird.  
  
     In dieser Situation kann das Angeben eines Abschlusszeichens den Speicherplatz minimieren, sodass das Feld als Feld variabler Länge behandelt werden kann.  
  
### Beispiele  
 In diesem Beispiel wird ein Massenexport von Daten aus der `AdventureWorks.HumanResources.Department`-Tabelle in die `Department-c-t.txt`-Datendatei mithilfe des Zeichenformats ausgeführt, wobei ein Komma als Feldabschlusszeichen und das Neue-Zeile-Zeichen (\n) als Zeilenabschlusszeichen dient.  
  
 Der Befehl **bcp** verfügt über folgende Schalter.  
  
|Schalter|Beschreibung|  
|------------|-----------------|  
|**-c**|Gibt an, dass die Datenfelder als Zeichendaten geladen werden.|  
|**-t** `,`|Gibt ein Komma (,) als Feldabschlusszeichen an.|  
|**-r** \n|Gibt das Zeilenabschlusszeichen als Neue-Zeile-Zeichen an. Dabei handelt es sich um das standardmäßige Zeilenabschlusszeichen, die Angabe ist also optional.|  
|**-T**|Gibt an, dass das Hilfsprogramm **bcp** die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe integrierter Sicherheit über eine vertrauenswürdige Verbindung herstellt. Wenn **-T** nicht angegeben wird, müssen Sie **-U** und **-P** angeben, um sich erfolgreich anzumelden.|  
  
 Weitere Informationen finden Sie unter [bcp Utility](../../tools/bcp-utility.md).  
  
 Geben Sie an der [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Eingabeaufforderung Folgendes ein:  
  
```  
bcp AdventureWorks.HumanResources.Department out C:\myDepartment-c-t.txt -c -t, -r \n -T  
```  
  
 Dadurch wird `Department-c-t.txt`mit 16 Datensätzen zu jeweils vier Feldern erstellt. Die Felder werden durch ein Komma getrennt.  
  
## Angeben von Abschlusszeichen für den Massenimport  
 Wenn Sie einen Massenimport von **char**- oder **nchar**-Daten ausführen, müssen vom Massenimportbefehl die in der Datendatei verwendeten Abschlusszeichen erkannt werden können. Wie Abschlusszeichen angegeben werden können, hängt vom Massenimportbefehl ab:  
  
-   **bcp**  
  
     Für die Angabe von Abschlusszeichen wird bei Massenimport- und -exportvorgängen dieselbe Syntax verwendet. Weitere Informationen finden Sie unter "Angeben von Abschlusszeichen für den Massenexport" weiter oben in diesem Thema.  
  
-   BULK INSERT  
  
     Abschlusszeichen können für einzelne Felder in einer Formatdatei oder für die gesamten Datendatei angegeben werden, indem die in der folgenden Tabelle aufgeführten Qualifizierer verwendet werden:  
  
    |Qualifizierer|Beschreibung|  
    |---------------|-----------------|  
    |FIELDTERMINATOR **='***Feldabschlusszeichen***'**|Gibt das Feldabschlusszeichen an, das für Zeichen- und Unicodezeichen-Datendateien verwendet werden soll.<br /><br /> Der Standardwert ist \t (Tabstoppzeichen).|  
    |ROWTERMINATOR **='***Zeilenabschlusszeichen***'**|Gibt das Zeilenabschlusszeichen an, das für Zeichen- und Unicodezeichen-Datendateien verwendet werden soll.<br /><br /> Der Standardwert ist \n (Neue-Zeile-Zeichen).|  
  
     Weitere Informationen finden Sie unter [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
     Für den OPENROWSET-Massenrowsetanbieter können Abschlusszeichen nur in der Formatdatei angegeben werden. Dies ist bis auf Datentypen für große Objekte vorgeschrieben. Wenn von einer Zeichendatendatei ein nicht-standardmäßiges Abschlusszeichen verwendet wird, muss dieses in der Formatdatei definiert werden. Weitere Informationen finden Sie unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md) und [Massenimport von Daten mithilfe einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
     Weitere Informationen zur OPENROWSET BULK-Klausel finden Sie unter [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
### Beispiele  
 In den Beispielen in diesem Abschnitt wird jeweils ein Massenimport von Zeichendaten aus der `Department-c-t.txt` -Datendatei, die im vorhergehenden Beispiel erstellt wurde, in die `myDepartment` -Tabelle in der [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] -Beispieldatenbank ausgeführt. Vor dem Ausführen dieser Beispiele müssen Sie diese Tabelle erstellen. Führen Sie zum Erstellen dieser Tabelle unter dem **dbo** -Schema im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Abfrage-Editor den folgenden Code aus:  
  
```tsql  
USE AdventureWorks;  
GO  
DROP TABLE myDepartment;  
CREATE TABLE myDepartment   
(DepartmentID smallint,  
Name nvarchar(50),  
GroupName nvarchar(50) NULL,  
ModifiedDate datetime not NULL CONSTRAINT DF_AddressType_ModifiedDate DEFAULT (GETDATE())  
);  
GO 
```  
  
#### A. Verwenden von bcp zum interaktiven Angeben von Abschlusszeichen  
 Im folgenden Beispiel wird ein Massenimport der `Department-c-t.txt` -Datendatei mithilfe eines `bcp` -Befehls ausgeführt. Die mit diesem Befehl verwendeten Schalter sind mit den für den Massenexport gültigen identisch. Weitere Informationen finden Sie unter "Angeben von Abschlusszeichen für den Massenexport" weiter oben in diesem Thema.  
  
 Geben Sie an der Windows-Eingabeaufforderung Folgendes ein:  
  
```  
bcp AdventureWorks..myDepartment in C:\myDepartment-c-t.txt -c -t , -r \n -T  
```  
  
#### B. Verwenden von BULK INSERT zum interaktiven Angeben von Abschlusszeichen  
 Im folgenden Beispiel wird ein Massenimport der `Department-c-t.txt` -Datendatei mithilfe einer `BULK INSERT` -Anweisung ausgeführt, die die in der folgenden Tabelle aufgeführten Qualifizierer verwendet.  
  
|Option|Attribut|  
|------------|---------------|  
|DATAFILETYPE **='**char**'**|Gibt an, dass die Datenfelder als Zeichendaten geladen werden.|  
|FIELDTERMINATOR **='**`,`**'**|Gibt ein Komma (`,`) als Feldabschlusszeichen an.|  
|ROWTERMINATOR **='**`\n`**'**|Gibt das Zeilenabschlusszeichen als Neue-Zeile-Zeichen an.|  
  
 Führen Sie im Abfrage-Editor von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] folgenden Code aus:  
  
```tsql  
USE AdventureWorks;  
GO  
BULK INSERT myDepartment FROM 'C:\myDepartment-c-t.txt'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      ROWTERMINATOR = '\n'  
);  
GO  
```  
  
## Siehe auch  
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Angeben der Feldlänge mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [Angeben der Präfixlänge in Datendateien mittels bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Angeben des Dateispeichertyps mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  