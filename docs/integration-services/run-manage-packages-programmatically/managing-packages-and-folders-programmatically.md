---
title: Programmgesteuerte Verwaltung von Paketen und Ordnern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f53a752a5c6035bef8450a0eeabcbbf27829226d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="managing-packages-and-folders-programmatically"></a>Programmgesteuerte Verwaltung von Paketen und Ordnern
<a name="top"></a> Beim programmgesteuerten Arbeiten mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen möchten Sie vielleicht feststellen, ob ein einzelnes Paket oder ein einzelner Ordner vorhanden ist, oder Sie möchten die Ordner mit gespeicherten Paketen verwalten. Die <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse des <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace stellt eine Reihe von Methoden bereit, die diese Anforderungen erfüllen.    
    
##  <a name="exists"></a> Bestimmen, ob ein Paket oder ein Ordner vorhanden ist    
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
    
 [Zurück zum Anfang](#top)    
    
##  <a name="managing"></a> Verwalten von Paketen und Ordnern    
 Die <xref:Microsoft.SqlServer.Dts.Runtime.Application>-Klasse des <xref:Microsoft.SqlServer.Dts.Runtime>-Namespace stellt zusätzliche Methoden zum Verwalten von Paketen und den Ordnern, in denen diese gespeichert sind, bereit.    
    
###  <a name="managing_rempkg"></a> Entfernen eines Pakets    
 Rufen Sie zum programmgesteuerten Entfernen eines gespeicherten Pakets eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Zurück zum Anfang](#top)    
    
###  <a name="managing_create"></a> Erstellen eines Ordners    
 Rufen Sie zum programmgesteuerten Erstellen eines Speicherordners eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Zurück zum Anfang](#top)    
    
###  <a name="managing_remfldr"></a> Entfernen eines Ordners    
 Rufen Sie zum programmgesteuerten Entfernen eines Speicherordners eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Zurück zum Anfang](#top)    
    
###  <a name="managing_rename"></a> Umbenennen eines Ordners    
 Rufen Sie zum programmgesteuerten Umbenennen eines Speicherordners eine der folgenden Methoden auf:    
    
|Speicherort|Aufzurufende Methode|    
|----------------------|--------------------|    
|SSIS-Paketspeicher|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Zurück zum Anfang](#top)    
    
## <a name="see-also"></a>Siehe auch    
 [Paketverwaltung &#40;SSIS-Dienst&#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Programmgesteuertes Auflisten verfügbarer Pakete](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
