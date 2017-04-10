---
title: "Lektion 1: Konvertieren einer Tabelle in eine hierarchische Struktur | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "HierarchyID"
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Lektion 1: Konvertieren einer Tabelle in eine hierarchische Struktur
Kunden mit Tabellen, die hierarchische Beziehungen mithilfe von Selbstjoins darstellen, können diese Tabellen in eine hierarchische Struktur konvertieren, indem Sie diese Lektion als Richtlinie verwenden. Es ist relativ leicht, von dieser Darstellung zu einer mit **hierarchyid**zu migrieren. Nach der Migration verfügen die Benutzer über ein grundlegendes Verständnis hierarchischer Darstellungen, die für effizientere Abfragen auf verschiedene Weise indiziert werden können.  
  
In dieser Lektion wird eine vorhandene Tabelle untersucht und eine neue Tabelle mit einer **hierarchyid** -Spalte erstellt. Daraufhin wird diese Tabelle mit den Daten der Quelltabelle gefüllt, und schließlich werden drei Indizierungsstrategien dargestellt. Diese Lektion enthält die folgenden Themen:  
  
-   [Untersuchen der aktuellen Struktur der Mitarbeitertabelle](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
-   [Auffüllen einer Tabelle mit vorhandenen hierarchischen Daten](../../relational-databases/tables/populating-a-table-with-existing-hierarchical-data.md)  
  
-   [Optimieren der NewOrg-Tabelle](../../relational-databases/tables/optimizing-the-neworg-table.md)  
  
-   [Zusammenfassung: Konvertieren einer Tabelle in eine hierarchische Struktur](../../relational-databases/tables/summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## Erforderliche Komponenten  
Für diese Lektion benötigen Sie die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank.  
  
## Nächste Aufgabe in der Lektion  
[Untersuchen der aktuellen Struktur der Mitarbeitertabelle](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
## Nächste Lektion  
[Lektion 2: Erstellen und Verwalten von Daten in einer hierarchischen Tabelle](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  
