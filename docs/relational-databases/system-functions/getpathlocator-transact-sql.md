---
title: GetPathLocator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs: TSQL
helpviewer_keywords: GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30e1f626885e850d8aca6cc30360033c055855f2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt den path_locator-ID-Wert für die angegebene Datei bzw. das angegebene Verzeichnis in einer FileTable zurück.  
  
||  
|-|  
|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://msdn.microsoft.com/library/bb500435.aspx)).|  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>Argumente  
 *filenamespace_path*  
 Ein Namespacepfad in der FileTable. Der Namespacepfad hat den Typ **nvarchar(max)**.  
  
 Wenn die Datenbank zu einer Always On-verfügbarkeitsgruppe gehört die **GetPathLocator** -Funktion akzeptiert den Namen des virtuellen Netzwerks (VNN) oder den Computernamen.  
  
## <a name="return-type"></a>Rückgabetyp  
 **hierarchyid**  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Weitere Informationen finden Sie unter [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="examples"></a>Beispiele  
 Sie können die **GetPathLocator** -Funktion verwenden, wenn Sie Dateien von einem Dateiserver zu einer FileTable migrieren. In diesem Szenario sollen die Dateien in die FileTable verschoben und anschließend der ursprüngliche UNC-Pfad für jede Datei durch den FileTable-UNC-Pfad ersetzt werden. Ein vollständiges Beispiel finden Sie unter [Laden von Dateien in FileTables](../../relational-databases/blob/load-files-into-filetables.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
