---
title: SMO-Objektmodell | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e3bc9ec53d5550f8671b7ac9bb786ae9d631f6df
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="smo-object-model"></a>SMO-Objektmodell
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Das SMO-Objektmodell besteht aus einer Hierarchie von Objekten. Das <xref:Microsoft.SqlServer.Management.Smo.Server>-Objekt ist das Objekt oberster Ebene, und alle Instanzklassenobjekte befinden sich unter dem <xref:Microsoft.SqlServer.Management.Smo.Server>-Objekt.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>-Klasse ist eine Klasse oberster Ebene mit einer separaten Objekthierarchie. Die <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> -Objekt stellt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Diensten und Netzwerkeinstellungen, die über den WMI-Anbieter verfügbar.  
  
 Neben den <xref:Microsoft.SqlServer.Management.Smo.Server>- und <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>-Objekten gibt es mehrere Hilfsklassen, die Tasks oder Vorgänge darstellen, beispielsweise <xref:Microsoft.SqlServer.Management.Smo.Transfer>, <xref:Microsoft.SqlServer.Management.Smo.Backup> und <xref:Microsoft.SqlServer.Management.Smo.Restore>.  
  
 Das SMO-Objektmodell besteht aus mehreren Namespaces. Weitere Informationen finden Sie unter [SMO-Namespaces](../../relational-databases/server-management-objects-smo/smo-object-model-namespaces.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Diagramm des SMO-Objektmodells](../../relational-databases/server-management-objects-smo/smo-object-model-diagram.md)   
 [SMO-Namespaces](../../relational-databases/server-management-objects-smo/smo-object-model-namespaces.md)   
 [Konzepte des WMI-Anbieters für die Konfigurationsverwaltung](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
