---
title: 'Lektion 1: Konvertieren einer Tabelle in eine hierarchische Struktur | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 283b0012724a4bcdef1601dbccb30d441234441a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>Lektion 1: Konvertieren einer Tabelle in eine hierarchische Struktur
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
Kunden mit Tabellen, die hierarchische Beziehungen mithilfe von Selbstjoins darstellen, können diese Tabellen in eine hierarchische Struktur konvertieren, indem Sie diese Lektion als Richtlinie verwenden. Es ist relativ leicht, von dieser Darstellung zu einer mit **hierarchyid**zu migrieren. Nach der Migration verfügen die Benutzer über ein grundlegendes Verständnis hierarchischer Darstellungen, die für effizientere Abfragen auf verschiedene Weise indiziert werden können.  
  
In dieser Lektion wird eine vorhandene Tabelle untersucht und eine neue Tabelle mit einer **hierarchyid** -Spalte erstellt. Daraufhin wird diese Tabelle mit den Daten der Quelltabelle gefüllt, und schließlich werden drei Indizierungsstrategien dargestellt. Diese Lektion enthält die folgenden Themen:  
  
-   [Untersuchen der aktuellen Struktur der Mitarbeitertabelle](../../relational-databases/tables/lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
-   [Auffüllen einer Tabelle mit vorhandenen hierarchischen Daten](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
-   [Optimieren der NewOrg-Tabelle](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
-   [Zusammenfassung: Konvertieren einer Tabelle in eine hierarchische Struktur](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## <a name="prerequisites"></a>Voraussetzungen  
Für diese Lektion benötigen Sie die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
[Untersuchen der aktuellen Struktur der Mitarbeitertabelle](../../relational-databases/tables/lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 2: Erstellen und Verwalten von Daten in einer hierarchischen Tabelle](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  
