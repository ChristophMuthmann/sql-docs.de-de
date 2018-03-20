---
title: Verwenden von WQL und Skriptsprachen mit dem WMI-Anbieter | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 833aa7dcfad44a7717f3cbe85c1029542985413d
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>Verwenden von WQL und Skriptsprachen mit dem WMI-Anbieter
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Verwaltungsanwendungen greifen auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienste und -Netzwerkeinstellungen mithilfe des WMI-Anbieters (Windows Management Instrumentation) für Konfigurationsverwaltungsobjekte auf zwei verschiedene Arten zu:  
  
-   Mithilfe eines WQL-Editors oder eines Abfragetools, wie beispielsweise WBEMTest.exe, zum Abfragen des Objektsatzes mit der WMI-Sprache (WQL)  
  
-   Mithilfe einer Skriptsprache, z. B. VBScript  
  
 Alternativ können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienste und -Netzwerkeinstellungen programmgesteuert mithilfe von verwalteten WMI-Objekten in SMO verwaltet werden. Weitere Informationen über das Programmieren von WMI Objekte verwaltet werden, finden Sie unter [Verwalten von Diensten und Netzwerkeinstellungen durch die Verwendung der WMI-Anbieter](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 Der Zugriff auf den WMI-Anbieter für die Konfigurationsverwaltung erfolgt über den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager und über [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console. Weitere Informationen zum Zugreifen auf den WMI-Anbieter über eine Benutzeroberfläche finden Sie unter [Verwalten von Diensten: Themen &#40;SQL Server-Konfigurations-Manager&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6).  
  
## <a name="see-also"></a>Siehe auch  
 [Zugreifen auf WMI-Anbieter für Konfigurationsverwaltung mit WQL](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [Ändern der SQL Server-Dienst erweiterten Eigenschaften mit VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
