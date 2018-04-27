---
title: Sichten (Integration Services-Katalog) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- views [Integration Services]
ms.assetid: d0294d43-4852-46dc-9afa-d0c19ea9aa03
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3734681114d3dcdfc8e787ff752fc14329cfa330
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="views-integration-services-catalog"></a>Sichten (Integration Services-Katalog)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt werden die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Sichten beschrieben, die zum Verwalten von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekten, die in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wurden, verfügbar sind.  
  
 Fragen Sie die [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Sichten ab, um Objekte, Einstellungen und operative Daten zu überprüfen, die im **SSISDB**-Katalog gespeichert werden.  
  
 Der Standardname des Katalogs ist „SSISDB“. Die Objekte, die im Katalog gespeichert werden, umfassen Projekte, Pakete, Parameter, Umgebungen und Verwendungsverläufe.  
  
 Sie können die Datenbanksichten und gespeicherten Prozeduren direkt verwenden oder benutzerdefinierten Code schreiben, mit dem die verwaltete API aufgerufen wird. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] und die verwaltete API führen zur Ausführung vieler Tasks eine Abfrage der Sichten durch und rufen gespeicherte Prozeduren auf, die in diesem Abschnitt beschrieben werden.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [catalog.catalog_properties &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
 Zeigt die Eigenschaften des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalogs an.  
  
 [catalog.effective_object_permissions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md)  
 Zeigt die gültigen Berechtigungen des aktuellen Prinzipals für alle Objekte im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.environment_variables &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
 Zeigt die Umgebungsvariablendetails für alle Umgebungen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.environments &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
 Zeigt die Umgebungsdetails für alle Umgebungen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an. Umgebungen enthalten Variablen, auf die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Projekten verwiesen werden kann.  
  
 [catalog.execution_parameter_values &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
 Zeigt die tatsächlichen Parameterwerte an, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen während einer Instanz der Ausführung verwendet werden.  
  
 [catalog.executions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
 Zeigt die Instanzen der Paketausführung im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an. Die Ausführung von Paketen mit dem Task "Paket ausführen" erfolgt in der gleichen Ausführungsinstanz wie die Ausführung des übergeordneten Pakets.  
  
 [catalog.explicit_object_permissions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md)  
 Zeigt nur die Berechtigungen an, die dem Benutzer explizit zugewiesen wurden.  
  
 [catalog.extended_operation_info &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
 Zeigt erweiterte Informationen für alle Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.folders &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md)  
 Zeigt die Ordner im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.object_parameters &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
 Zeigt die Parameter für alle Pakete und Projekte im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.object_versions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
 Zeigt die Versionen von Objekten im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an. In dieser Version werden in dieser Sicht nur Versionen von Projekten unterstützt.  
  
 [catalog.operation_messages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
 Zeigt Meldungen an, die während der Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog protokolliert werden.  
  
 [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
 Zeigt die Details aller Vorgänge im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.packages &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
 Zeigt die Details für alle Pakete an, die im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog angezeigt werden.  
  
 [catalog.environment_references &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
 Zeigt die Umgebungsverweise für alle Projekte im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
 [catalog.projects &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
 Zeigt die Details für alle Projekte an, die im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog angezeigt werden.  
  
 [catalog.validations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md)  
 Zeigt die Details aller Projekt- und Paketüberprüfungen im [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Katalog an.  
  
[catalog.master_properties &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)  
Zeigt die Eigenschaften des ausgewählten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Masters an.

[catalog.worker_agents &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)  
Zeigt die Informationen des [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out-Workers an.  
