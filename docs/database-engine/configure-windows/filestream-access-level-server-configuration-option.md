---
title: Filestream-Zugriffsebene (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfd8a4fe115b8c768d50318a12551ad8c0721c82
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="filestream-access-level-server-configuration-option"></a>Filestream-Zugriffsebene (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie die Option FILESTREAM-Zugriffsebene, um die FILESTREAM-Zugriffsebene für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu ändern.  
  
> [!NOTE]  
>  Damit diese Option wirksam wird, müssen die Windows-Verwaltungseinstellungen für FILESTREAM aktiviert sein. Sie können diese Einstellungen bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder über den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager aktivieren.  
  
|Wert|Definition|  
|-----------|----------------|  
|0|Deaktiviert die FILESTREAM-Unterstützung für diese Instanz.|  
|1|Aktiviert FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff.|  
|2|Aktiviert FILESTREAM für [!INCLUDE[tsql](../../includes/tsql-md.md)] und für den Win32-Streamingzugriff.|  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration des Datenbankmoduls - Filestream](http://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [Aktivieren und Konfigurieren von FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
