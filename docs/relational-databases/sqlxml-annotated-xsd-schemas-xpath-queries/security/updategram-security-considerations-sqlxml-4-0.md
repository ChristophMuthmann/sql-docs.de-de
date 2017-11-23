---
title: "Sicherheitsüberlegungen zu Updategrams (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3b6379e6407e8e2821ed34fc8f2137b9b1d170ee
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="updategram-security-considerations-sqlxml-40"></a>Sicherheitsüberlegungen zu Updategrams (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Im folgenden werden Sicherheitsrichtlinien zur Verwendung von Updategrams:  
  
-   Vermeiden Sie die Verwendung von Standardzuordnungen, wenn Sie Daten mithilfe von Updategrams aktualisieren. Bei Verwendung einer Standardzuordnung wird einem Elementnamen in einem Updategram ein Tabellenname und einem Attributnamen wird eine Spalte zugeordnet. Dadurch werden die Datentabelle und die Spaltendaten der Datenbank verfügbar gemacht, und dies kann potenziell ein Sicherheitsrisiko darstellen. Wenn Sie stattdessen ein eigenes Zuordnungsschema angeben, um die Elemente und Attribute eines Updategrams den Datenbanktabellen und –spalten zuzuordnen, dann können Sie für das Updategram beliebige Element- und Attributnamen wählen und dem Schema die Zuordnung dieser Namen zu Datenbanktabellen und –spalten überlassen. So werden die Datenbankinformationen nicht in einem Updategram verfügbar gemacht.  
  
-   Lassen Sie nicht zu, dass Benutzer eigene Updategrams erstellen und ausführen. Updategrams sollten sich in Form von Vorlagen auf dem Server befinden und nicht mithilfe von Anwendungen im ASP-Stil dynamisch erstellt werden, da sonst die Daten der Datenbank gefährdet werden könnten. Dieses Risiko lässt sich ausschließen, indem Benutzer lediglich erlaubt wird, über die als Vorlagen bereitgestellten Updategrams auf die Daten zuzugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Updategramms zum Ändern von Daten in SQLXML 4.0](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  
