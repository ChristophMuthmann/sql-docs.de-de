---
title: Externe Skripts aktiviert (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: SQL2016_New_Updated
ms.date: 08/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external scripts enabled
- external_scripts_enabled_TSQL
helpviewer_keywords: external scripts enabled option
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 05c5af488241c28a5b83c01ac089fa5e1e1715c0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="external-scripts-enabled-server-configuration-option"></a>Externe Skripts aktiviert – Serverkonfigurationsoption
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Aktivieren Sie mit der Option **external scripts enabled** die Ausführung von Skripts mit bestimmten Remotespracherweiterungen. Diese Eigenschaft ist standardmäßig deaktiviert. Beim Setup kann diese Eigenschaft optional auf TRUE festgelegt werden, wenn **Advanced Analytics Services** installiert wird.  
  

 Bevor Sie mit der gespeicherten Prozedur **sp_execute_external_script** ein externes Skript ausführen können, müssen Sie die Option „external script enabled“ aktivieren. Führen Sie mit **sp_execute_external_script** Skripts aus, die in einer unterstützten Sprache wie beispielsweise R geschrieben wurden. In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]besteht [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] aus einer Serverkomponente, die mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]installiert wird, sowie Arbeitsstationstools und Verbindungsbibliotheken, der Datenanalysten mit der Hochleistungsumgebung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verbinden.  Installieren Sie das Feature **Advanced Analytics-Erweiterungen** während des Setups von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um die Ausführung von R-Skripts zu ermöglichen. Weitere Informationen finden Sie unter [Installing Previous Versions of SQL Server R Services](http://msdn.microsoft.com/library/48380645-9e72-4744-bebb-1c1fd8a18c43).  
  
 Führen Sie das folgende Skript aus, um externe Skripts zu aktivieren:  
  
```  
sp_configure 'external scripts enabled', 1;  
RECONFIGURE WITH OVERRIDE;  
```  
  
 Starten Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu, damit diese Änderung wirksam wird.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
