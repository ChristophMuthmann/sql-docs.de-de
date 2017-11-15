---
title: MSSQLSERVER_905 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 905 (Database Engine error)
ms.assetid: c828bb2e-e554-4f81-b76c-2b3740d2b944
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 32453b9fec43391f5e701304876659aeb4a4cd56
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver905"></a>MSSQLSERVER_905
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|905|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBSTARTUP_EE_PARTITIONING|  
|Meldungstext|Die '%.*ls'-Datenbank kann in dieser Edition von SQL Server nicht gestartet werden, weil sie eine '%.\*ls'-Partitionsfunktion enthält. Das Partitionieren wird nur von SQL Server Enterprise Edition unterstützt.|  
  
## <a name="explanation"></a>Erklärung  
Die Datenbank enthält mindestens eine partitionierte Tabelle bzw. mindestens einen partitionierten Index. In dieser Edition von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann keine Partitionierung verwendet werden. Deshalb kann die Datenbank nicht ordnungsgemäß gestartet werden. Partitionierte Tabellen und Indizes sind nicht in jeder Edition von [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügbar. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="user-action"></a>Benutzeraktion  
Trennen Sie die Datenbank mithilfe der gespeicherten Prozedur sp_detach_db. Verschieben Sie die Dateien bei Bedarf, und fügen Sie dann die Datenbank an eine Instanz der unterstützen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Edition an. Verwenden Sie dazu CREATE DATABASE mit der FOR ATTACH-Option oder der FOR ATTACH_REBUILD_LOG-Option. Deaktivieren Sie die Partitionierung für alle Tabellen, und entfernen Sie die Partitionierungsfunktionen. Trennen Sie die Datenbank wieder, und fügen Sie sie an den aktuellen Server an.  
  
