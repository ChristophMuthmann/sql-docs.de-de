---
title: "Konfigurieren des Data Warehouses für den Steuerungspunkt für das Hilfsprogramm (SQL Server-Hilfsprogramm) | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5da84662b3ca25c57d7dc09f04fe292c3e24aeef
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Konfigurieren des Data Warehouses für den Steuerungspunkt für das Hilfsprogramm (SQL Server-Hilfsprogramm)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die von verwalteten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen gesammelten Daten werden im UMDW (Utility Management Data Warehouse) gespeichert. Der UMDW-Dateiname lautet „sysutility_mdw“.  
  
 Sie können die Beibehaltungsdauer der UMDW-Daten konfigurieren. Weitere Informationen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d).  
  
 Die folgenden Konfigurationseinstellungen sind in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht konfigurierbar:  
  
-   UMDW-Name: Sysutility_mdw.  
  
-   Uploadfrequenz für den Sammlungssatz: Alle 15 Minuten  
  
 Das UMDW-Verzeichnis ist konfigurierbar: \<Systemlaufwerk>:\Programme\Microsoft SQL Server\MSSQL10_50.<UCP_Name>\MSSQL\Data\\, wobei \<Systemlaufwerk> normalerweise Laufwerk C:\ entspricht. Die Protokolldatei „Sysutility_mdw_\<GUID>_LOG“ befindet sich im selben Verzeichnis.  
  
> [!NOTE]  
>  Der Speicherort der UMDW-Datei (sysutility_mdw) kann mithilfe von Detach/Attach oder ALTER DATABASE geändert werden. Es wird empfohlen, ALTER DATABASE zu verwenden. Weitere Informationen finden Sie unter [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
