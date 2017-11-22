---
title: Importieren und Exportieren von Massendaten mithilfe des Hilfsprogramms bcp (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/28/2016
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
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d54b06efb1383586c7df2f65ba12d35939d83f48
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importieren und Exportieren von Massendaten mithilfe des Hilfsprogramms bcp (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Thema erhalten Sie einen Überblick zum Verwenden des Hilfsprogramms [bcp](../../tools/bcp-utility.md) zum Exportieren von Daten von jeder Stelle innerhalb einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, an der eine SELECT-Anweisung verwendet werden kann, einschließlich partitionierter Sichten.  
  
 Das Hilfsprogramm bcp (Bcp.exe) ist ein Befehlszeilentool, das die BCP-API (Bulk Copy Program) verwendet. Mit dem Hilfsprogramm bcp werden die folgenden Tasks ausgeführt:  
  
-   Massenexport von Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle in eine Datendatei.  
  
-   Massenexport von Daten aus einer Abfrage.  
  
-   Massenimport von Daten aus einer Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle.  
  
-   Generieren von Formatdateien.  
  
 Auf das Hilfsprogramm „bcp“ wird über den Befehl **bcp** zugegriffen. Für den Massenimport von Daten mithilfe des Befehls **bcp** ist es erforderlich, das Schema der Tabelle und die Datentypen der Spalten zu verstehen, es sei denn, Sie verwenden eine bereits vorhandene Formatdatei.  
  
 Mit dem Hilfsprogramm "bcp" können Daten aus einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle in eine Datendatei exportiert und dann in anderen Programmen verwendet werden. Das Hilfsprogramm kann auch dazu verwendet werden, Daten aus einem anderen Programm, meist einem anderen Datenbank-Managementsystem (DBMS, Database Management System), in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle zu importieren. Die Daten werden zuerst aus dem Quellprogramm in eine Datendatei exportiert und dann, in einem getrennten Vorgang, aus der Datendatei in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle kopiert.  
  
 Der Befehl **bcp** stellt Schalter bereit, mit denen Sie den Datentyp der Datendatei und andere Informationen angeben. Wenn diese Schalter nicht angegeben werden, werden vom Befehl Formatierungsinformationen (z. B. der Typ der Datenfelder in einer Datendatei) abgefragt. Anschließend müssen Sie festlegen, ob Sie eine Formatdatei mit Ihren interaktiven Antworten erstellen möchten. Eine Formatdatei ist oft hilfreich, wenn Sie für zukünftige Massenimport- oder Massenexportvorgänge flexibel sein müssen. Sie können die Formatdatei bei späteren **bcp**-Befehlen für äquivalente Datendateien angeben. Weitere Informationen finden Sie unter [Angeben von Datenformaten für die Kompatibilität bei Verwendung von „bcp“ &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
>**Hinweis:** Das bcp-Hilfsprogramm wird mithilfe der ODBC-Massenkopierung geschrieben.
  
 Eine Beschreibung der **bcp** -Befehlssyntax finden Sie unter [bcp (Hilfsprogramm)](../../tools/bcp-utility.md).  
  
## <a name="examples"></a>Beispiele  
|Die folgenden Themen enthalten Beispiele zur Verwendung von „bcp“: |
|---|
|[bcp Utility](../../tools/bcp-utility.md)<br /><br />Datenformate für Massenimport oder Massenexport (SQL Server)<br />&emsp;&#9679;&emsp;[Verwenden das native Format zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden von nativen Unicode-Formaten zum Importieren oder Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[Angeben von Feld- und Zeilenabschlusszeichen (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[Beibehalten von Identitätswerten beim Massenimport von Daten (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />Formatdateien zum Importieren oder Exportieren von Daten (SQL Server)<br />&emsp;&#9679&emsp;[Erstellen einer Formatdatei (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Massenimport von Daten mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Überspringen einer Tabellenspalte mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Auslassen eines Datenfelds mithilfe einer Formatdatei (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Verwenden einer Formatdatei zum Zuordnen von Tabellenspalten zu Datendateifeldern (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[Beispiele für den Massenimport und -export von XML-Dokumenten (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

  
## <a name="more-examples-and-information"></a>Weitere Beispiele und Informationen  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT-Klausel &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [Vorbereiten des Massenimports von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Massenimport und -export von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Erstellen einer Formatdatei &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
  
