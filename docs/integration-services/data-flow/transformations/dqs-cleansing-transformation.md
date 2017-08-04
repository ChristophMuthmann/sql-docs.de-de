---
title: DQS-Bereinigung Transformation | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2851f1310e241dd921e0777408e000eb37836a81
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="dqs-cleansing-transformation"></a>DQS-Bereinigungstransformation
  Die DQS-Bereinigungstransformation korrigiert Daten aus einer verbundenen Datenquelle mithilfe von Data Quality Services (DQS), indem sie genehmigte Regeln anwendet, die für die verbundene Datenquelle oder eine ähnliche Datenquelle erstellt wurden. Weitere Informationen zu Datenkorrekturregeln finden Sie unter [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Weitere Informationen zu DQS finden Sie unter [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Die DQS-Bereinigungstransformation bestimmt, ob die Daten korrigiert werden müssen, indem sie die Daten in einer Eingabespalte verarbeitet. Dabei gelten folgende Bedingungen:  
  
-   Die Spalte ist für die Datenkorrektur ausgewählt.  
  
-   Der Datentyp der Spalte wird in der Datenkorrektur unterstützt.  
  
-   Der Spalte ist eine Domäne mit einem kompatiblen Datentyp zugeordnet.  
  
 Die Transformation umfasst auch eine Fehlerausgabe, die Sie zur Behandlung von Fehlern auf Zeilenebene konfigurieren können. Die Fehlerausgabe wird mit dem **Transformations-Editor für die DQS-Bereinigung**konfiguriert.  
  
 Sie können die [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) in den Datenfluss einschließen, um Zeilen mit Daten zu ermitteln, bei denen es sich wahrscheinlich um Duplikate handelt.  
  
## <a name="data-quality-projects-and-values"></a>Data Quality-Projekte und -Werte  
 Wenn Sie Daten mit der DQS-Bereinigungstransformation verarbeiten, wird ein Bereinigungsprojekt auf dem Data Quality-Server erstellt. Das Projekt wird mit dem Data Quality Client verwaltet. Mit dem Data Quality Client können Sie außerdem die Projektwerte in eine DQS-Wissensdatenbankdomäne importieren. Sie können die Werte nur in eine Domäne (oder verknüpfte Domäne) importieren, für deren Verwendung die DQS-Bereinigungstransformation konfiguriert wurde.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
-   [Öffnen von Integration Services-Projekten im Data Quality-Client](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importieren von Bereinigungsprojektwerten in eine Domäne](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Anwenden von Datenqualitätsregeln auf eine Datenquelle](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Öffnen, Entsperren, Umbenennen und Löschen eines Data Quality-Projekts](https://msdn.microsoft.com/library/hh510417.aspx)  
  
-   Artikel [Bereinigung komplexer Daten unter Verwendung von Verbunddomänen](http://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)auf social.technet.microsoft.com.  
  
  
