---
title: Datenanbieter | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 98eb787fc3dbaab7b55795a0a1b3a99d9a43e2a4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="data-providers"></a>Datenanbieter
Datenanbieter stellen unterschiedliche Datenquellen wie SQL-Datenbanken, indizierten sequenziellen Dateien, Kalkulationstabellen, Dokumentspeicher und e-Mail-Dateien dar. Anbieter machen Daten gleichmäßig über eine allgemeine Abstraktion wird aufgerufen, das Rowset verfügbar.  
  
 ADO ist leistungsstark und flexibel, da es mehrere unterschiedliche Daten-Anbieter herstellen und weiterhin verfügbar das gleiche Programmiermodell, unabhängig vom angegebenen Anbieter die bestimmten Funktionen machen kann. Allerdings da jeden Datenanbieter eindeutig ist, variieren wie Ihre Anwendung mit ADO kommuniziert vom Datenanbieter.  
  
 Beispielsweise sind die Features und Funktionen von OLE DB-Anbieter für SQL Server, die verwendet wird, um Microsoft SQL Server-Datenbanken zugreifen, wesentlich von denen unterscheiden, von der Microsoft OLE DB-Anbieter für Internet Publishing, die verwendet wird, um den Zugriff auf Datei Speicher auf einem Webserver.
