---
title: Räumliche Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bff0d376a1a3734385e2e914845ea6777451bf2b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spatial-data-sql-server"></a>Räumliche Daten (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Räumliche Daten stellen Informationen über die physische Position und die Form geometrischer Objekte dar. Bei diesen Objekten kann es sich um Punktpositionen oder komplexere Objekte handeln, z.&nbsp;B. Länder, Straßen oder Seen.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt zwei Typen von räumlichen Daten: den Datentyp **geometry** und den Datentyp **geography** .  
  
-   Der **geometry** -Datentyp stellt Daten in einem euklidischen (flachen) Koordinatensystem dar.  
  
-   Der **geography** -Datentyp stellt Daten in einem Erdkugel-Koordinatensystem dar.  
  
 Beide Datentypen werden als .NET CLR (Common Language Runtime)-Datentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]implementiert.  
  
> [!IMPORTANT]  
>  Laden Sie für eine ausführliche Beschreibung und Beispiele der in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]eingeführten räumlichen Funktionen das Whitepaper [Neue räumliche Funktionen in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407)herunter.  
  
##  <a name="reltasks"></a> Verwandte Aufgaben  
 [Erstellen, Aufbauen und Abfragen von geometry-Instanzen](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 Beschreibt die Methoden, die mit Instanzen des geometry-Datentyps verwendet werden können.  
  
 [Erstellen, Aufbauen und Abfragen von geography-Instanzen](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 Beschreibt die Methoden, die mit Instanzen des geography-Datentyps verwendet werden können.  
  
 [Abfragen von nächsten Nachbarn aus räumlichen Daten](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 Beschreibt das allgemeine Abfragemuster, das zum Suchen der räumlichen Objekte, die einem bestimmten räumlichen Objekt am nächsten liegen, verwendet wird.  
  
 [Erstellen, Ändern und Löschen von räumlichen Indizes](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 Stellt Informationen zum Erstellen, Ändern und Löschen eines räumlichen Indexes bereit.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)  
 Bietet eine Einführung in die räumlichen Datentypen.  
  
-   [Punkt](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [Übersicht über räumliche Indizes](../../relational-databases/spatial/spatial-indexes-overview.md)  
 Bietet eine Einführung in räumliche Indizes und beschreibt Mosaik und Mosaikschemas.  
  
  
