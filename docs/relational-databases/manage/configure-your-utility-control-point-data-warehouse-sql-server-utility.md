---
title: "Konfigurieren des Data Warehouses für den Steuerungspunkt für das Hilfsprogramm (SQL Server-Hilfsprogramm) | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f1bcf9ce22256ee273ae7cb10756f6fb181f764
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Konfigurieren des Data Warehouses für den Steuerungspunkt für das Hilfsprogramm (SQL Server-Hilfsprogramm)
  Die von verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen gesammelten Daten werden im UMDW (Utility Management Data Warehouse) gespeichert. Der UMDW-Dateiname lautet sysutility_mdw.  
  
 Sie können die Beibehaltungsdauer der UMDW-Daten konfigurieren. Weitere Informationen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Die folgenden Konfigurationseinstellungen sind in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht konfigurierbar:  
  
-   UMDW-Name: Sysutility_mdw.  
  
-   Uploadfrequenz für den Sammlungssatz: Alle 15 Minuten  
  
 Das UMDW-Verzeichnis ist konfigurierbar: \<Systemlaufwerk>:\Programme\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, wobei \<Systemlaufwerk> normalerweise Laufwerk C:\ entspricht. Die Protokolldatei „Sysutility_mdw_\<GUID>_LOG“ befindet sich im selben Verzeichnis.  
  
> [!NOTE]  
>  Der Speicherort der UMDW-Datei (sysutility_mdw) kann mithilfe von Detach/Attach oder ALTER DATABASE geändert werden. Es wird empfohlen, ALTER DATABASE zu verwenden. Weitere Informationen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
