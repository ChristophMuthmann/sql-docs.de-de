---
title: Programmgesteuertes Speichern von Paketen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: building-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- programmatically saving a package
- saving a package programmatically
ms.assetid: 4204f817-d5df-475a-9338-d7f01305d566
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b27925b4e1234c2c32b6070a733dae598727a5f2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="saving-a-package-programmatically"></a>Programmgesteuertes Speichern von Paketen
  Nachdem Sie ein neues Paket programmgesteuert erstellt oder ein vorhandenes geändert haben, sollten Sie Ihre Änderungen speichern.  
  
 Alle in diesem Thema erläuterten Methoden zum Speichern von Paketen erfordern einen Verweis auf die **Microsoft.SqlServer.ManagedDTS** -Assembly. Nachdem Sie den Verweis in einem neuen Projekt hinzugefügt haben, importieren Sie den <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace mit einer **using**- oder **Imports**-Anweisung.  
  
## <a name="saving-a-package-programmatically"></a>Programmgesteuertes Speichern von Paketen  
 Rufen Sie eine der folgenden Methoden der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse auf, um ein Paket programmgesteuert zu speichern:  
  
|Speicherort|Aufzurufende Methode|  
|----------------------|--------------------|  
|File|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToXml%2A>|  
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServer%2A><br /><br /> oder<br /><br /> <xref:Microsoft.SqlServer.Dts.Runtime.Application.SaveToSqlServerAs%2A>|  
  
> [!IMPORTANT]  
>  Die Methoden der <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse zum Arbeiten mit dem SSIS-Paketspeicher unterstützen nur "." oder den Namen des lokalen Servers. "(local)" oder "localhost" können nicht verwendet werden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Speichern von Paketen](../../integration-services/save-packages.md)  
  
  
