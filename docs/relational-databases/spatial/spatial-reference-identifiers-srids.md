---
title: SRIDs (Spatial Reference Identifiers) | Microsoft Dokumentation
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
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cfc36294df1962a8ee2334435fb2d49a72baea2c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spatial-reference-identifiers-srids"></a>SRIDs (Spatial Reference Identifiers)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Jede räumliche Instanz hat einen SRID (Spatial Reference Identifier), einen räumlichen Referenzbezeichner. Der SRID bezieht sich auf ein räumliches Referenzsystem, das auf der jeweiligen Ellipsenform basiert, die für eine flache Erdabbildung oder runde Erdabbildung verwendet wird.  
  
> [!IMPORTANT]  
>  Laden Sie für eine ausführliche Beschreibung und Beispiele der in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]eingeführten räumlichen Funktionen (einschließlich einer neuen SRID) das Whitepaper [New Spatial Features in SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407)(in englischer Sprache) herunter.  
  
 Eine räumliche Spalte kann Objekte mit unterschiedlichen SRIDs enthalten. Allerdings können nur räumliche Instanzen mit dem gleichen SRID verwendet werden, wenn Daten mit räumlichen Datenmethoden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bearbeitet werden. Das von zwei räumlichen Dateninstanzen abgeleitete Ergebnis einer beliebigen räumlichen Methode ist nur dann gültig, wenn diese Instanzen den gleichen SRID haben und die gleiche Maßeinheit, Bezugsebene und Projektion zur Bestimmung der Koordinaten der Instanzen verwendet wurde. Die gängigsten Maßeinheiten für einen SRID sind Meter oder Quadratmeter.  
  
 Wenn zwei räumliche Instanzen nicht über den gleichen SRID verfügen, dann geben mit diesen Instanzen verwendete Methoden des **geometry** - oder **geography** -Datentyps NULL zurück. Damit beispielsweise das folgende Prädikat ein Ergebnis ungleich NULL zurückgibt, müssen die beiden **geometry** -Instanzen `geometry1` und `geometry2`den gleichen SRID besitzen:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  Das Spatial Reference Identification-System wird durch den [European Petroleum Survey Group-Standard (EPSG)](http://go.microsoft.com/fwlink/?LinkId=99349) definiert. Hierbei handelt es sich um einen für die Kartografie, Landvermessung und Speicherung geodätischer Daten entwickelten Satz von Standards. Dieser Standard ist Eigentum des Oil and Gas Producers (OGP) Surveying and Positioning Committee.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über räumliche Datentypen](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
