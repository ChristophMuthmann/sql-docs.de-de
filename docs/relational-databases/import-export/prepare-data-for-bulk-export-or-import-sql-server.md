---
title: "Vorbereiten von Daten für den Massenexport oder -import (SQL Server) | Microsoft-Dokumentation"
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
- bulk importing [SQL Server], planning
- bulk importing [SQL Server], from a CSV file
- data formats [SQL Server], planning operations
- CSV files [SQL Server]
- quoted fields in CSV files [SQL Server]
ms.assetid: 783fd581-2e5f-496b-b79c-d4de1e09ea30
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fbcca0ce4e711ba22215e9e6ff09389b02d6e80b
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="prepare-data-for-bulk-export-or-import-sql-server"></a>Vorbereiten von Daten für den Massenexport oder -import (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  In diesem Abschnitt werden Überlegungen, die beim Planen für Massenexportvorgänge relevant sind, sowie die Anforderungen für Massenimportvorgänge erläutert.  
  
> [!NOTE]  
>  Falls Sie sich in Bezug auf das Formatieren einer Datendatei für den Massenimport nicht sicher sind, verwenden Sie das Hilfsprogramm **bcp** , um Daten aus der Tabelle in eine Datendatei zu exportieren. Die Formatierung jedes Datenfelds in dieser Datei weist die Formatierung auf, die für den Massenimport von Daten in die entsprechende Tabellenspalte erforderlich ist. Verwenden Sie dieselbe Datenformatierung für die Felder Ihrer Datendatei.  
  
## <a name="data-file-format-considerations-for-bulk-export"></a>Überlegungen zum Datendateiformat für den Massenexport  
 Bevor Sie mithilfe des Befehls **bcp** einen Massenexportvorgang ausführen, sollten Sie Folgendes berücksichtigen:  
  
-   Wenn Daten in eine Datei exportiert werden, erstellt der Befehl **bcp** die Datendatei automatisch mithilfe des angegebenen Dateinamens. Wenn dieser Dateinamen bereits verwendet wird, überschreiben die Daten, die in die Datendatei massenkopiert werden, den vorhandenen Inhalt der Datei.  
  
-   Zum Massenexportieren aus einer Tabelle oder Sicht in eine Datendatei ist die SELECT-Berechtigung für die massenkopierte Tabelle oder Sicht erforderlich.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann parallele Scans verwenden, um Daten abzurufen. Daher ist normalerweise nicht sichergestellt, dass die Tabellenzeilen, die aus einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] massenexportiert werden, sich in der Datendatei in einer bestimmten Reihenfolge befinden. Verwenden Sie die Option **queryout** für den Massenexport aus einer Abfrage, damit massenexportierte Tabellenzeilen in der Datendatei in einer bestimmten Reihenfolge angezeigt werden, und geben Sie eine ORDER BY-Klausel an.  
  
## <a name="data-file-format-requirements-for-bulk-import"></a>Anforderungen an das Datendateiformat für den Massenexport  
 Zum Importieren von Daten in eine Datendatei muss die Datei die folgenden grundlegenden Anforderungen erfüllen:  
  
-   Die Datei muss ein Zeilen- und Spaltenformat aufweisen.  
  
> [!NOTE]  
>  Die Struktur der Datendatei muss nicht mit der Struktur der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle übereinstimmen, da Spalten während des Massenimportprozesses ausgelassen oder neu geordnet werden können.  
  
-   Die Daten in der Datendatei müssen ein unterstütztes Format aufweisen, z. B. ein Zeichen- oder systemeigenes Format.  
  
-   Die Daten können ein Zeichenformat oder ein systemeigenes binäres Format, einschließlich Unicode, aufweisen.  
  
-   Zum Importieren von Daten mithilfe des Befehls **bcp**, einer BULK INSERT-Anweisung oder einer INSERT ... SELECT * FROM OPENROWSET(BULK...)-Anweisung muss die Zieltabelle bereits vorhanden sein.  
  
-   Jedes Feld in der Datendatei muss mit der entsprechenden Spalte in der Zieltabelle kompatibel sein. Ein **int** -Feld kann z. B. nicht in eine **datetime** -Spalte geladen werden. Weitere Informationen finden Sie unter [Datenformate für Massenimport oder Massenexport &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md) und [Angeben von Datenformaten für die Kompatibilität bei Verwendung von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
    > [!NOTE]  
    >  Sie können den Befehl **bcp** mit dem Schalter **-F** *first_row* und/oder dem Schalter **-L** *last_row* verwenden, um anstelle der gesamten Datei eine Teilmenge von Zeilen anzugeben, die aus einer Datendatei importiert werden sollen. Weitere Informationen finden Sie unter [bcp Utility](../../tools/bcp-utility.md).  
  
-   Zum Importieren von Daten aus Datendateien mit Feldern fester Länge oder Breite verwenden Sie eine Formatdatei. Weitere Informationen finden Sie unter [XML-Formatdateien &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  
  
-   CSV (Comma-Separated Value)-Dateien werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Massenimportvorgängen nicht unterstützt. In manchen Fällen kann jedoch eine CSV-Datei als Datendatei für einen Massenimport von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Das Feldabschlusszeichen einer CSV-Datei muss kein Komma sein. Um als Datendatei für einen Massenimport verwendet werden zu können, muss eine CSV-Datei den folgenden Einschränkungen entsprechen:  
  
    -   Datenfelder enthalten nie das Feldabschlusszeichen.  
  
    -   Keiner oder alle der Werte in einem Datenfeld sind in Anführungszeichen ("") eingeschlossen.  
  
     Für den Massenimport von Daten aus einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] FoxPro- oder Visual FoxPro-Tabellendatei (.dbf) oder einer [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] -Arbeitsblattdatei (.xls), müssen die Daten in eine CSV-Datei umgewandelt werden, die den vorangehenden Einschränkungen entspricht. Die Dateierweiterung lautet normalerweise .csv. Anschließend kann die Datei mit der Dateinamenerweiterung .csv als Datendatei in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Massenimportvorgang verwendet werden.  
  
     In 32-Bit-Systemen ist es jedoch möglich, CSV-Daten mithilfe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET [mit dem OLE DB-Anbieter für Jet in eine](../../t-sql/functions/openrowset-transact-sql.md) -Tabelle ohne Massenimportoptimierungen zu importieren. Jet behandelt Textdateien als Tabellen mit dem durch eine schema.ini-Datei, die sich im gleichen Verzeichnis wie die Datenquelle befindet, festgelegten Schema.  Für CSV-Daten ist einer der Parameter in der Datei schema.ini "FORMAT=CSVDelimited". Für diese Lösung ist das Verständnis der Jet Test IISAMm-Vorgänge – die Verbindungszeichenfolgensyntax, Verwendung von schema.ini, Einstellungsoptionen für die Registrierung usw. – erforderlich.  Die besten Informationsquellen hierfür sind die Microsoft Access-Hilfe und Knowledge Base (KB)-Artikel. Weitere Informationen finden Sie unter [Initializing the Text Data Source Driver](https://msdn.microsoft.com/library/office/ff834391.aspx), [Verwendung eine verteilten Abfrage von SQLServer 7.0 mit einem verknüpften Server gesicherten Access-Datenbanken](http://go.microsoft.com/fwlink/?LinkId=128504)(maschinell übersetzter Artikel), [Verwendung von Jet OLE DB-Provider 4.0 an ISAM-Datenbanken](http://go.microsoft.com/fwlink/?LinkId=128505)(maschinell übersetzter Artikel) und [Gewusst wie: Öffnen Sie getrennte Textdateien mit der Jet-Provider Text IIsam (maschinell übersetzter Artikel)](http://go.microsoft.com/fwlink/?LinkId=128501).  
  
 Darüber hinaus ist Folgendes für den Massenimport von Daten aus einer Datendatei in eine Tabelle erforderlich:  
  
-   Benutzer müssen über INSERT- und SELECT-Berechtigungen für die Tabelle verfügen. Benutzer müssen auch über eine ALTER TABLE-Berechtigung verfügen, wenn sie Optionen wie das Deaktivieren von Einschränkungen verwenden, für die DLL-Vorgänge (Data Definition Language) erforderlich sind.  
  
-   Wenn Sie für das Massenimportieren von Daten BULK INSERT oder INSERT ... SELECT * FROM OPENROWSET(BULK...) verwenden, muss entweder das Sicherheitsprofil des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozesses (wenn sich der Benutzer mit dem bereitgestellten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen anmeldet) oder die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmeldung, die beim Delegieren der Sicherheit verwendet wird, über Zugriff für Lesevorgänge auf die Datendatei verfügen. Darüber hinaus muss der Benutzer zum Lesen der Datei über die ADMINISTER BULK OPERATIONS-Berechtigung verfügen.  
  
> [!NOTE]  
>  Das Massenimportieren in eine partitionierte Sicht wird nicht unterstützt, und Versuche, einen Massenimport von Daten in eine partitionierte Sicht auszuführen, schlagen fehl.  
  
## <a name="external-resources"></a>Externe Ressourcen  
 [Importieren von Daten aus Excel in SQL Server](http://support.microsoft.com/kb/321686)  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Informationen über die Verwendung des OLE DB-Anbieters für Jet zum Importieren der CSV-Daten wurden hinzugefügt.|  
  
## <a name="see-also"></a>Siehe auch  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)   
 [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
  
