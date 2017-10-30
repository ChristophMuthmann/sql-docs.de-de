---
title: Sichten (Integration Services-Katalog) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b7293a70046df19eef816d3e7830518959ecbc98
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="views-integration-services-catalog"></a>Sichten (Integration Services-Katalog)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt werden die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sichten beschrieben, die zum Verwalten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekten, die in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wurden, verfügbar sind.  
  
 Abfrage der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Ansichten, um zu überprüfen, Objekte, Einstellungen und operative Daten, die im rowsetcache der **SSISDB** Katalog.  
  
 Der Standardname des Katalogs ist SSISDB. Die Objekte, die im Katalog gespeichert werden, umfassen Projekte, Pakete, Parameter, Umgebungen und Verwendungsverläufe.  
  
 Sie können die Datenbanksichten und gespeicherten Prozeduren direkt verwenden oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]und die verwaltete API die Sichten Abfragen und rufen Sie die gespeicherten Prozeduren, die beschrieben werden, in diesem Abschnitt können Sie viele Aufgaben ausführen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Catalog. catalog_properties &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 Zeigt die Eigenschaften der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [Catalog. effective_object_permissions &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 Zeigt die gültigen Berechtigungen des aktuellen Prinzipals für alle Objekte im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.environment_variables &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 Zeigt die umgebungsvariablendetails für alle Umgebungen, in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.environments &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 Zeigt die Umgebungsdetails für alle Umgebungen, in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog. Umgebungen enthalten Variablen, auf die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekten verwiesen werden kann.  
  
 [catalog.execution_parameter_values &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 Zeigt die tatsächlichen Parameterwerte an, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen während einer Instanz der Ausführung verwendet werden.  
  
 [catalog.executions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 Zeigt die Instanzen der Paketausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an. Die Ausführung von Paketen mit dem Task "Paket ausführen" erfolgt in der gleichen Ausführungsinstanz wie die Ausführung des übergeordneten Pakets.  
  
 [Catalog. explicit_object_permissions &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 Zeigt nur die Berechtigungen an, die dem Benutzer explizit zugewiesen wurden.  
  
 [catalog.extended_operation_info &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 Zeigt erweiterte Informationen für alle Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [Catalog.Folders &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 Zeigt die Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.object_parameters &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 Zeigt die Parameter für alle Pakete und Projekte in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.object_versions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 Zeigt die Versionen von Objekten im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an. In dieser Version werden in dieser Sicht nur Versionen von Projekten unterstützt.  
  
 [catalog.operation_messages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 Zeigt Meldungen an, die während der Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog protokolliert werden.  
  
 [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 Zeigt die Details aller Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.packages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 Zeigt die Details für alle Pakete, die in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.environment_references &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 Zeigt die umgebungsverweise für alle Projekte in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [catalog.projects &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 Zeigt die Details für alle Projekte, die in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
 [Catalog.validations &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 Zeigt die Details aller Projekt- und paketüberprüfungen in der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Katalog.  
  
[Catalog.master_properties &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
Zeigt die Eigenschaften der [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale-Out-Master.

[Catalog.worker_agents &#40; SSISDB-Datenbank &#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
Zeigt die Informationen des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale-Out-Worker.  

