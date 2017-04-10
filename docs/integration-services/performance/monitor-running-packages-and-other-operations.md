---
title: "&#220;berwachen der Ausf&#252;hrung von Paketen und anderen Vorg&#228;ngen | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# &#220;berwachen der Ausf&#252;hrung von Paketen und anderen Vorg&#228;ngen
  Sie können [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketausführungen, Projektüberprüfungen und andere Vorgänge mit einem oder mehreren der folgenden Tools überwachen. Bestimmte Tools, z. B. Datenabzweigungen, sind nur für Projekte verfügbar, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt werden.  
  
-   Protokolle  
  
     Weitere Informationen finden Sie unter [Integration Services-Protokollierung &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
-   Berichte  
  
     Weitere Informationen finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
-   Sichten  
  
     Weitere Informationen finden Sie unter [Sichten &#40;Integration Services-Katalog&#41;](../../integration-services/system-views/views-integration-services-catalog.md).  
  
-   Leistungsindikatoren  
  
     Weitere Informationen finden Sie unter [Performance Counters](../../integration-services/performance/performance-counters.md).  
  
-   Datenabzweigungen  
  
## Vorgangstypen  
 Mehrere verschiedene Typen von Vorgängen werden im **SSISDB**-Katalog auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server überwacht. Jeder Vorgang kann mehrere ihm zugeordnete Meldungen aufweisen. Jede Meldung kann einem von mehreren Typklassen zugeordnet werden. Eine Meldung kann z. B. vom Typ Information, Warnung oder Fehler sein. Die vollständige Liste von Meldungstypen finden Sie in der Dokumentation zur Transact-SQL-Sicht [catalog.operation_messages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md). Eine vollständige Liste der Vorgangstypen finden Sie unter [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).  
  
 Neun verschiedene Statustypen werden verwendet, um den Status eines Vorgangs anzugeben. Eine vollständige Liste der Statustypen finden Sie in der Sicht [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).  
  
## Verwandte Inhalte  
 Blogeintrag [SSIS T-SQL API Overview](http://go.microsoft.com/fwlink/?LinkId=249051) (Übersicht über die SSIS-T-SQL-API) auf blogs.msdn.com.  
  
  