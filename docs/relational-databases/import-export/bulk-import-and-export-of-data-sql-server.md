---
title: Massenimport und -export von Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
caps.latest.revision: "61"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 0a7a6c256b102c43decf8cc003ce2ceae808e621
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Massenimport und -export von Daten (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt den Massenexport von Daten (*Massendaten*) aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle und den Massenimport in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle oder eine nicht partitionierte Sicht. 
  
-   Der*Massenexport* bezieht sich auf das Kopieren von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle in eine Datendatei.

-   Beim*Massenimport* werden Daten aus einer Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle geladen. Sie können beispielsweise Daten von einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel-Anwendung in eine Datendatei exportieren und dann einen Massenimport der Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle ausführen.  
 
##  <a name="MethodsForBuliIE"></a> Methoden für den Massenimport und -export von Daten  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird der Massenexport von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle und der Massenimport in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle oder eine nicht partitionierte Sicht unterstützt. Dazu stehen die folgenden grundlegenden Methoden zur Verfügung.  
 
  
|Methode|Description|Importiert Daten|Exportiert Daten|  
|------------|-----------------|------------------|------------------|  
|[bcp (Hilfsprogramm)](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Ein Befehlszeilenprogramm (Bcp.exe), mit dem Massenexporte und -importe von Daten ausgeführt und Formatdateien generiert werden können.|ja|ja|  
|[BULK INSERT-Anweisung](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung, mit der Daten direkt aus einer Datendatei in eine Datenbanktabelle oder nicht partitionierte Sicht importiert werden.|ja|nein|  
|[INSERT ... SELECT * FROM OPENROWSET(BULK...)-Anweisung](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung, bei der mit dem OPENROWSET-Massenrowsetanbieter ein Massenimport von Daten in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle ausgeführt wird. Dabei wird die OPENROWSET(BULK…)-Funktion angegeben, um Daten in einer INSERT-Anweisung auszuwählen.|ja|nein| 
|[SQL Server-Import/Export-Assistent](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)|Der Assistent erstellt einfache Pakete, die Daten zwischen vielen häufigen Datenformaten, einschließlich Datenbanken, Kalkulationstabellen und Textdateien, importieren und exportieren.|ja|ja|  
  
> [!IMPORTANT]
> CSV (Comma-Separated Value)-Dateien werden von SQL Server-Massenimportvorgängen nicht unterstützt. In manchen Fällen kann jedoch eine CSV-Datei als Datendatei für einen Massenimport von Daten in SQL Server verwendet werden. Das Feldabschlusszeichen einer CSV-Datei muss kein Komma sein. Weitere Informationen finden Sie unter [Vorbereiten von Daten für den Massenexport oder -import (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).

> [!NOTE]
> Nur das Hilfsprogramm „bcp“ wird von Azure SQL-Datenbank und Azure SQL Data Warehouse zum Importieren und Exportieren von Dateien unterstützt, die durch Trennzeichen getrennt sind.
  
##  <a name="FFs"></a> Formatdateien  
 Das Hilfsprogramm [bcp](../../tools/bcp-utility.md) sowie die Anweisungen [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) und [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) unterstützen alle die Verwendung einer als *Formatdatei* bezeichneten speziellen Datei zum Speichern von Formatinformationen für jedes Feld in einer Datendatei. In einer Formatdatei können auch Informationen zu der korrespondierenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle enthalten sein. Über die Formatdatei können alle Formatinformationen bereitgestellt werden, die für den Massenexport von Daten aus einer Instanz und für den Massenimport von Daten in eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erforderlich sind.  
  
 Formatdateien bieten eine flexible Möglichkeit zum Interpretieren von Daten, wie diese in der Datendatei während des Imports vorhanden sind, und zum Formatieren von Daten in der Datendatei während des Exports. Durch diese Flexibilität besteht nicht mehr die Notwendigkeit, einen speziellen Code für das Interpretieren der Daten zu schreiben oder die Daten für die speziellen Anforderungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder der externen Anwendung umzuformatieren. Wenn Sie beispielsweise einen Massenexport von Daten ausführen, die in eine Anwendung geladen werden sollen, für die durch Trennzeichen getrennte Werte erforderlich sind, können Sie eine Formatdatei verwenden, um Kommas als Feldabschlusszeichen in den exportierten Daten einzufügen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt zwei Arten von Formatdateien: XML-Formatdateien und Nicht-XML-Formatdateien.  
  
 Formatdateien können nur mithilfe des Hilfsprogramms [bcp](../../tools/bcp-utility.md) generiert werden. Weitere Informationen finden Sie unter [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md). Weitere Informationen zu Formatdateien finden Sie unter [Formatdateien zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
> [!NOTE]
> Wenn keine Formatdatei während eines Massenexport- oder Massenimportvorgangs zur Verfügung steht, können Sie die Standardformatierung mithilfe der Befehlszeile überschreiben.

|Verwandte Themen|
|---|
|[Vorbereiten von Daten für den Massenexport oder -import (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)|
|[Datenformate für Massenimport oder Massenexport (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des nativen Formats zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden von nativen Unicode-Formaten zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)|
|[Angeben von Datenformaten für die Kompatibilität bei Verwendung von bcp (SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Angeben des Dateispeichertyps mithilfe von bcp (SQL Server)](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Angeben der Präfixlänge in Datendateien mittels bcp (SQL Server)](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Angeben der Feldlänge mithilfe von bcp (SQL Server)](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Angeben von Feld- und Zeilenabschlusszeichen (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)|
|[Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)|
|[Beibehalten von Identitätswerten beim Massenimport von Daten (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)|
|[Formatdateien zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Erstellen einer Formatdatei (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Massenimport von Daten mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Überspringen einer Tabellenspalte mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Auslassen eines Datenfelds mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)|
 
  
## <a name="more-information"></a>Weitere Informationen.  
 [Voraussetzungen für die minimale Protokollierung beim Massenimport](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Beispiele für den Massenimport und -export von XML-Dokumenten &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [Kopieren von Datenbanken auf andere Server](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [Ausführen von Massenladen von XML-Daten &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [Durchführen von Massenkopiervorgängen](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)   

  
  
