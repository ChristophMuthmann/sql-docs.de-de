---
title: "Datenformate für Massenimport oder Massenexport (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data formats [SQL Server], choosing
- bulk importing [SQL Server], data formats
ms.assetid: 73fe6741-9437-4b26-b030-28b863e74399
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b345ce1668b5333ab08441f97093e19d3afb33d2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="data-formats-for-bulk-import-or-bulk-export-sql-server"></a>Datenformate für Massenimport oder Massenexport (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann Daten in Zeichendatenformat oder systemeigenem binärem Datenformat akzeptieren. Verwenden Sie das Zeichenformat, wenn Sie Daten zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und einer anderen Anwendung (z. B. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) bzw. einem anderen Datenbankserver (wie Oracle oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) verschieben. Das systemeigene Format kann nur verwendet werden, wenn Sie Daten zwischen verschiedenen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verschieben.  
  
 **In diesem Thema:**  
  
-   [Datenformate für Massenimport oder -export](#ComponentsAndConcepts)  
  
-   [Verwandte Aufgaben](#RelatedTasks)  
  
##  <a name="ComponentsAndConcepts"></a> Datenformate für Massenimport oder -export  
 In der folgenden Tabelle ist angegeben, welches Datenformat im Allgemeinen für die Verwendung geeignet ist. Die Wahl hängt von der Darstellung der Daten und von der Quelle bzw. dem Ziel des Vorgangs ab.  
  
|Vorgang|Systemeigenes Format|Systemeigenes Unicode-Format|Zeichen|Unicode-Zeichen|  
|---------------|------------|--------------------|---------------|-----------------------|  
|Massenübertragung von Daten zwischen mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe einer Datendatei, die keine Sonderzeichen oder Zeichen aus Doppelbyte-Zeichensätzen (Double-Byte Character Set, DBCS) enthält. Sofern keine Formatdatei verwendet wird, müssen diese Tabellen identisch definiert sein.|Ja*|—|—|—|  
|Für **sql_variant** -Spalten eignet sich das systemeigene Datenformat am besten, da es im Gegensatz zu Zeichen- und Unicode-Formaten die Metadaten für die einzelnen **sql_variant** -Werte beibehält.|ja|—|—|—|  
|Massenübertragung von Daten zwischen mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe einer Datendatei, die Sonderzeichen oder DBCS-Zeichen enthält.|—|ja|—|—|  
|Massenimport von Daten aus einer Textdatei, die von einem anderen Programm generiert wurde.|—|—|ja|—|  
|Massenexport von Daten in eine Textdatei, die in einem anderen Programm verwendet werden soll.|—|—|ja|—|  
|Massenübertragung von Daten zwischen mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe einer Datendatei, die Unicode-Daten, aber keine Sonderzeichen oder DBCS-Zeichen enthält.|—|—|—|ja|  
  
 \* Die schnellste Methode für den Massenexport von Daten aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei Verwendung von **bcp**.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Importieren von Daten aus früheren SQL Server-Versionen im systemeigenen Format oder im Zeichenformat](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Angeben von Datenformaten für die Kompatibilität bei Verwendung von bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)  
  
  
