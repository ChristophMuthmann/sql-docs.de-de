---
title: Programmgesteuertes Verwalten von Paketen und Ordnern | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a40acf3a586c74119d948291fd179f78833cb37a
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="managing-packages-and-folders-programmatically"></a>Programmgesteuerte Verwaltung von Paketen und Ordnern
<a name="top"></a>Beim programmgesteuerten arbeiten mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete, Sie möchten u. u. zu bestimmen, ob ein einzelnes Paket oder ein Ordner vorhanden ist, oder zum Verwalten der Ordner, in denen Pakete gespeichert sind. Die <xref:Microsoft.SqlServer.Dts.Runtime.Application> Klasse von der <xref:Microsoft.SqlServer.Dts.Runtime> Namespace bietet eine Vielzahl von Methoden, um diese Anforderungen zu erfüllen.    
    
##  <a name="exists"></a>Bestimmen, ob ein Paket oder ein Ordner vorhanden ist    
 Um programmgesteuert zu ermitteln, ob ein gespeichertes Paket vorhanden ist, rufen Sie eine der folgenden Methoden auf, bevor Sie versuchen, das Paket zu laden und auszuführen:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Um programmgesteuert zu ermitteln, ob ein Ordner vorhanden ist, rufen Sie eine der folgenden Methoden auf, bevor Sie versuchen, die in dem Ordner gespeicherten Pakete aufzulisten:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Zurück nach oben](#top)    
    
##  <a name="managing"></a>Verwalten von Paketen und Ordnern    
 Die <xref:Microsoft.SqlServer.Dts.Runtime.Application> Klasse von der <xref:Microsoft.SqlServer.Dts.Runtime> Namespace stellt zusätzliche Methoden zum Verwalten von Paketen und die Ordner, in denen diese gespeichert sind.    
    
###  <a name="managing_rempkg"></a>Entfernen eines Pakets    
 Rufen Sie zum programmgesteuerten Entfernen eines gespeicherten Pakets eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Zurück nach oben](#top)    
    
###  <a name="managing_create"></a>Erstellen eines Ordners    
 Rufen Sie zum programmgesteuerten Erstellen eines Speicherordners eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Zurück nach oben](#top)    
    
###  <a name="managing_remfldr"></a>Entfernen eines Ordners    
 Rufen Sie zum programmgesteuerten Entfernen eines Speicherordners eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Zurück nach oben](#top)    
    
###  <a name="managing_rename"></a>Umbenennen eines Ordners    
 Rufen Sie zum programmgesteuerten Umbenennen eines Speicherordners eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Zurück nach oben](#top)    
    
## <a name="see-also"></a>Siehe auch    
 [Paketverwaltung &#40; SSIS-Dienst &#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Programmgesteuertes Auflisten verfügbarer Pakete](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
