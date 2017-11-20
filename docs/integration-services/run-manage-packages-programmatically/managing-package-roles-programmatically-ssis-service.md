---
title: Verwalten von Paketrollen (SSIS-Dienst) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7a7fb000389756caf0c2f2ea00cd0b80e75557d8
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="managing-package-roles-programmatically-ssis-service"></a>Programmgesteuertes Verwalten von Paketrollen (SSIS-Dienst)
  Wenn Sie programmgesteuert mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen arbeiten, möchten Sie möglicherweise bestimmen, welche Rollen für die Anwendung auf Pakete verfügbar sind, oder die Rollen, die auf ein einzelnes Paket angewendet werden, bestimmen oder festlegen. Die <xref:Microsoft.SqlServer.Dts.Runtime.Application> Klasse von der <xref:Microsoft.SqlServer.Dts.Runtime> Namespace bietet eine Vielzahl von Methoden, um diese Anforderungen zu erfüllen.  
  
 Rollen gelten nur für gespeicherte Pakete der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Msdb** Datenbank. Weitere Informationen über Paketrollen finden Sie unter [Integration Services Roles &#40; SSIS-Dienst &#41; ](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 Alle in diesem Thema erläuterten Methoden erfordern einen Verweis auf die **Microsoft.SqlServer.ManagedDTS** -Assembly. Nachdem Sie den Verweis in einem neuen Projekt hinzugefügt haben, importieren die <xref:Microsoft.SqlServer.Dts.Runtime> Namespace mithilfe einer **mit** oder **Importe** Anweisung.  
  
> [!IMPORTANT]  
>  Die Methoden der <xref:Microsoft.SqlServer.Dts.Runtime.Application> -Klasse zum Arbeiten mit dem SSIS-Paketspeicher unterstützen nur ".", "localhost" oder den Namen für den lokalen Server. Sie können "(local)" nicht verwenden.  
  
## <a name="determining-which-roles-are-available"></a>Bestimmen, welche Rollen verfügbar sind  
 Um zu bestimmen, welche Rollen für die auf einem bestimmten Server gespeicherten Pakete verfügbar sind, rufen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse auf.  
  
## <a name="determining-which-roles-are-assigned"></a>Bestimmen, welche Rollen zugewiesen sind  
 Um zu bestimmen, welche Rollen einem bestimmten Paket bereits zugewiesen wurden, rufen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A>-Methode auf. Rufen Sie die <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A>-Methode auf, um einem Paket Rollen zuzuweisen.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Rollen &#40; SSIS-Dienst &#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  

