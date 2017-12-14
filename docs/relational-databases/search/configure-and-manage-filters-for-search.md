---
title: "Konfigurieren und Verwalten von Filtern für die Suche | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: "68"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cca26f3d6479fb798806d5e6ed0cbcbf8b991272
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-and-manage-filters-for-search"></a>Konfigurieren und Verwalten von Filtern für die Suche
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Die Indizierung von Dokumenten in einer Spalte mit dem Datentyp **varbinary**, **varbinary(max)**, **image** oder **xml** erfordert zusätzliche Verarbeitungsschritte. Diese Verarbeitung muss von einem Filter durchgeführt werden. Der Filter extrahiert die Textinformationen aus dem Dokument (hierbei wird die Formatierung entfernt). Der Filter überträgt den Text anschließend an die Komponente für die Wörtertrennung für die Sprache, die der Tabellenspalte zugeordnet ist.  
  
 Ein bestimmter Filter ist immer spezifisch für einen bestimmten Dokumenttyp (DOC, PDF, XLS, XML usw.). Diese Filter implementieren die IFilter-Schnittstelle. Weitere Informationen zu diesen Dokumenttypen erhalten Sie, indem Sie die [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) -Katalogsicht abfragen.  
  
 Binäre Dokumente können in einer einzelnen **varbinary(max)** - oder **image** -Spalte gespeichert werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wählt für jedes Dokument anhand der Dateierweiterung den entsprechenden Filter aus. Da die Dateierweiterung nicht sichtbar ist, wenn die Datei in einer **varbinary(max)** - oder **image** -Spalte gespeichert wird, muss die Dateierweiterung (DOC, XLS, PDF usw.) in einer separaten Spalte der Tabelle gespeichert werden. Diese wird als Typspalte bezeichnet. Die Typspalte kann einen beliebigen zeichenbasierten Datentyp aufweisen. Sie enthält die Dokumentdateierweiterung, beispielsweise DOC für ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word-Dokument. In der **Document** -Tabelle in [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]hat die **Document** -Spalte den Typ **varbinary(max)**, und die Typspalte **FileExtension**hat den Typ **nvarchar(8)**.  
  
> [!NOTE]  
>  Ein Filter kann ggf. eingebettete Objekte im übergeordneten Objekt behandeln. Dies ist abhängig von der Implementierung des Filters. Filter werden in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jedoch nicht für das Verfolgen von Links zu anderen Objekten konfiguriert.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert seine eigenen XML- und HTML-Filter. Zusätzlich lädt [!INCLUDE[msCoName](../../includes/msconame-md.md)] auch alle Filter für proprietäre Formate von  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](.doc, .xdoc, .ppt usw.), die bereits auf dem Betriebssystem installiert sind. Um die Filter zu identifizieren, die gerade auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geladen werden, verwenden Sie die gespeicherte Prozedur [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) wie folgt:  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 Bevor Sie Filter für nicht von [!INCLUDE[msCoName](../../includes/msconame-md.md)] stammende Formate verwenden können, müssen Sie sie jedoch manuell in die Serverinstanz laden. Weitere Informationen zum Installieren zusätzlicher Filter finden Sie unter [Anzeigen oder Ändern von registrierten Filtern und Wörtertrennungen](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
 **So zeigen Sie die Typspalte in einem vorhandenen Volltextindex an**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
## <a name="see-also"></a>Siehe auch  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [FILESTREAM-Kompatibilität mit anderen SQL Server-Funktionen](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
