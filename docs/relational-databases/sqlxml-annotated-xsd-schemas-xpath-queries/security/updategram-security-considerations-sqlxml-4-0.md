---
title: Sicherheitsüberlegungen zu Updategrams (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6f9a1227be077396e9e7575780be16c7b0a9fa04
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="updategram-security-considerations-sqlxml-40"></a>Sicherheitsüberlegungen zu Updategrams (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Im Folgenden finden Sie Sicherheitsrichtlinien zur Verwendung von Updategrams:  
  
-   Vermeiden Sie die Verwendung von Standardzuordnungen, wenn Sie Daten mithilfe von Updategrams aktualisieren. Bei Verwendung einer Standardzuordnung wird einem Elementnamen in einem Updategram ein Tabellenname und einem Attributnamen wird eine Spalte zugeordnet. Dadurch werden die Datentabelle und die Spaltendaten der Datenbank verfügbar gemacht, und dies kann potenziell ein Sicherheitsrisiko darstellen. Wenn Sie stattdessen ein eigenes Zuordnungsschema angeben, um die Elemente und Attribute eines Updategrams den Datenbanktabellen und –spalten zuzuordnen, dann können Sie für das Updategram beliebige Element- und Attributnamen wählen und dem Schema die Zuordnung dieser Namen zu Datenbanktabellen und –spalten überlassen. So werden die Datenbankinformationen nicht in einem Updategram verfügbar gemacht.  
  
-   Lassen Sie nicht zu, dass Benutzer eigene Updategrams erstellen und ausführen. Updategrams sollten sich in Form von Vorlagen auf dem Server befinden und nicht mithilfe von Anwendungen im ASP-Stil dynamisch erstellt werden, da sonst die Daten der Datenbank gefährdet werden könnten. Dieses Risiko lässt sich ausschließen, indem Benutzer lediglich erlaubt wird, über die als Vorlagen bereitgestellten Updategrams auf die Daten zuzugreifen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Updategrams zum Ändern von Daten in SQLXML 4.0](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  
