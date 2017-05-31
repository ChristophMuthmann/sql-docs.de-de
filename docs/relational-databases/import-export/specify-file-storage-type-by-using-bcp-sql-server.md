---
title: Angeben des Dateispeichertyps mithilfe von bcp (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], file storage types
- importing data, file storage types
- native data format [SQL Server]
- file storage types [SQL Server]
- data formats [SQL Server], file storage types
ms.assetid: 85e12df8-1be7-4bdc-aea9-05aade085c06
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fc454960a271c4fdfeb5e04337b2fb8ab1790127
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="specify-file-storage-type-by-using-bcp-sql-server"></a>Angeben des Dateispeichertyps mithilfe von bcp (SQL Server)
  Der *Dateispeichertyp* beschreibt, wie Daten in der Datendatei gespeichert werden. Daten können in eine Datendatei als Typ der Datenbanktabelle (systemeigenes Format), als Zeichendarstellung (Zeichenformat) oder als beliebiger Datentyp, bei dem die implizite Konvertierung unterstützt wird, exportiert werden. Beispielsweise kann ein **smallint** als ein **int**kopiert werden. Benutzerdefinierte Datentypen werden als Basistypen exportiert.  
  
## <a name="the-bcp-prompt-for-file-storage-type"></a>Die bcp-Eingabeaufforderung für den Dateispeichertyp  
 Wenn ein interaktiver **bcp** -Befehl die Option **in** oder **out** , jedoch keinen Formatdateischalter (**-f**) bzw. keinen Datenformatschalter (**-n**, **-c**, **-w**oder **-N**) enthält, fordert der Befehl wie folgt zur Eingabe des Dateispeichertyps für jedes Datenfeld auf:  
  
 `Enter the file storage type of field <field_name> [<default>]:`  
  
 Ihre Eingabe hängt dann von der Aufgabe ab, die Sie ausführen möchten (siehe folgende Liste).  
  
-   Wenn Sie Daten von einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine Datendatei der kompaktesten Speicherform, die möglich ist (systemeigenes Datenformat), massenexportieren möchten, nehmen Sie die Standard-Dateispeichertypen an, die von **bcp**bereitgestellt werden. Eine Liste der systemeigenen Dateispeichertypen finden Sie unter "Systemeigene Dateispeichertypen" weiter unten in diesem Thema.  
  
-   Für das Massenexportieren von Daten aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine Datendatei im Zeichenformat geben Sie **char** als Dateispeichertyp für alle Spalten in der Tabelle an.  
  
-   Für den Massenimport von Daten in eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus einer Datendatei geben Sie den Dateispeichertyp als **char** für Typen an, die im Zeichenformat gespeichert sind. Geben Sie für im systemeigenen Datentypformat gespeicherte Daten einen entsprechenden Dateispeichertyp wie folgt an:  
  
    |Dateispeichertyp|Eingabe an der Eingabeaufforderung|  
    |-----------------------|-----------------------------|  
    |**char***|**c**[**har**]|  
    |**varchar**|**c[har]**|  
    |**nchar**|**w**|  
    |**nvarchar**|**w**|  
    |**text***\*|**T**[**ext**]|  
    |**ntext2**|**W**|  
    |**binary**|**x**|  
    |**varbinary**|**x**|  
    |**image***\*|**I**[**mage**]|  
    |**datetime**|**d[ate]**|  
    |**smalldatetime**|**D**|  
    |**Uhrzeit**|**te**|  
    |**Datum**|**de**|  
    |**datetime2**|**d2**|  
    |**datetimeoffset**|**do**|  
    |**decimal**|**n**|  
    |**numeric**|**n**|  
    |**float**|**f[loat]**|  
    |**real**|**r**|  
    |**Int**|**i[nt]**|  
    |**bigint**|**B[igint]**|  
    |**smallint**|**s[mallint]**|  
    |**tinyint**|**t[inyint]**|  
    |**money**|**m[oney]**|  
    |**smallmoney**|**M**|  
    |**bit**|**b[it]**|  
    |**uniqueidentifier**|**u**|  
    |**sql_variant**|**V[ariant]**|  
    |**timestamp**|**x**|  
    |**UDT** (ein benutzerdefinierter Datentyp)|**U**|  
    |**XML**|**X**|  
  
     \*Die Interaktion für Feldlänge, Präfixlänge und Abschlusszeichen bestimmt die Speicherplatzgröße, die in einer Datendatei für nicht auf Zeichen basierende Daten zugeordnet wird, die als **char** -Dateispeichertyp exportiert werden.  
  
     \*\* Die Datentypen **ntext**, **text**und **image** werden in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entfernt. Vermeiden Sie den Gebrauch dieser Datentypen bei neuen Entwicklungen, und richten Sie sich auf die Änderung von Anwendungen ein, in denen sie zurzeit verwendet werden. Verwenden Sie stattdessen **nvarchar(max)**, **varchar(max)**und **varbinary(max)** .  
  
## <a name="native-file-storage-types"></a>Systemeigene Dateispeichertypen  
 Jeder systemeigene Speichertyp wird in der Formatdatei als entsprechender Datentyp der Hostdatei aufgezeichnet.  
  
|Dateispeichertyp|Datentyp in der Hostdatei|  
|-----------------------|-------------------------|  
|**char***|SQLCHAR|  
|**varchar**|SQLCHAR|  
|**nchar**|SQLNCHAR|  
|**nvarchar**|SQLNCHAR|  
|**text***\*|SQLCHAR|  
|**ntext***\*|SQLNCHAR|  
|**binary**|SQLBINARY|  
|**varbinary**|SQLBINARY|  
|**image***\*|SQLBINARY|  
|**datetime**|SQLDATETIME|  
|**smalldatetime**|SQLDATETIM4|  
|**decimal**|SQLDECIMAL|  
|**numeric**|SQLNUMERIC|  
|**float**|SQLFLT8|  
|**real**|SQLFLT4|  
|**int**|SQLINT|  
|**bigint**|SQLBIGINT|  
|**smallint**|SQLSMALLINT|  
|**tinyint**|SQLTINYINT|  
|**money**|SQLMONEY|  
|**smallmoney**|SQLMONEY4|  
|**bit**|SQLBIT|  
|**uniqueidentifier**|SQLUNIQUEID|  
|**sql_variant**|SQLVARIANT|  
|**timestamp**|SQLBINARY|  
|UDT (ein benutzerdefinierter Datentyp)|SQLUDT|  
  
 \*Für Datendateien, die im Zeichenformat gespeichert sind, wird **char** als Dateispeichertyp verwendet. SQLCHAR ist deshalb für Zeichendatendateien der einzige Datentyp, der in einer Formatdatei aufgeführt ist.  
  
 \*\*Sie können keinen Massenimport von Daten in **text**-, **ntext**- und **image** -Spalten durchführen, die DEFAULT-Werte aufweisen.  
  
## <a name="additional-considerations-for-file-storage-types"></a>Zusätzliche Aspekte von Dateispeichertypen  
 Beachten Sie beim Massenexport von Daten aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine Datendatei Folgendes:  
  
-   Sie können immer **char** als Dateispeichertyp angeben.  
  
-   Wenn Sie einen Dateispeichertyp eingeben, der eine ungültige implizite Konvertierung darstellt, erzeugt **bcp** einen Fehler. Obwohl Sie beispielsweise **int** für **smallint** -Daten angeben können, kommt es zu Überlauffehlern, wenn Sie **smallint** für **int** -Daten angeben.  
  
-   Wenn Nicht-Zeichen-Datentypen wie **float**, **money**, **datetime**oder **int** als entsprechende Datenbanktypen gespeichert werden, werden die Daten im systemeigenen Format von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in die Datendatei geschrieben.  
  
    > [!NOTE]  
    >  Nachdem Sie interaktiv alle Felder in einem **bcp**-Befehl angegeben haben, werden Sie vom Befehl dazu aufgefordert, Ihre Antworten für die einzelnen Felder in einer Nicht-XML-Formatdatei zu speichern. Weitere Informationen zu Nicht-XML-Formatdateien finden Sie unter [Nicht-XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Angeben der Feldlänge mithilfe von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [Angeben von Feld- und Zeilenabschlusszeichen &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)   
 [Angeben der Präfixlänge in Datendateien mittels bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
  
