---
title: Programmgesteuertes Verwalten von Paketrollen (SSIS-Dienst) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 677001394feba9d7125eeea8d20efceb7e162d5a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Programmgesteuertes Verwalten von Paketrollen (SSIS-Dienst)
  Wenn Sie programmgesteuert mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen arbeiten, möchten Sie möglicherweise bestimmen, welche Rollen für die Anwendung auf Pakete verfügbar sind, oder die Rollen, die auf ein einzelnes Paket angewendet werden, bestimmen oder festlegen. Die <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse des <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace stellt eine Reihe von Methoden bereit, die diese Anforderungen erfüllen.  
  
 Rollen gelten nur für Pakete, die in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb**-Datenbank gespeichert sind. Weitere Informationen zu Paketrollen finden Sie unter [Integration Services-Rollen &#40;SSIS-Dienst&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Alle in diesem Thema erläuterten Methoden erfordern einen Verweis auf die **Microsoft.SqlServer.ManagedDTS** -Assembly. Nachdem Sie den Verweis in einem neuen Projekt hinzugefügt haben, importieren Sie den <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace mit einer **using**- oder **Imports**-Anweisung.  
  
> [!IMPORTANT]  
>  Die Methoden der <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse zum Arbeiten mit dem SSIS-Paketspeicher unterstützen nur „.“, localhost oder den Namen des lokalen Servers. Sie können "(local)" nicht verwenden.  
  
## <a name="determining-which-roles-are-available"></a>Bestimmen, welche Rollen verfügbar sind  
 Um zu bestimmen, welche Rollen für die auf einem bestimmten Server gespeicherten Pakete verfügbar sind, rufen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse auf.  
  
## <a name="determining-which-roles-are-assigned"></a>Bestimmen, welche Rollen zugewiesen sind  
 Um zu bestimmen, welche Rollen einem bestimmten Paket bereits zugewiesen wurden, rufen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>-Methode auf. Rufen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>-Methode auf, um einem Paket Rollen zuzuweisen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Integration Services-Rollen &#40;SSIS-Dienst&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
