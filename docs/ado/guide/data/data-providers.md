---
title: Datenanbieter | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b49d223faaf5a90a8dcdb6654a9b5107245a9564
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="data-providers"></a>Datenanbieter
Datenanbieter stellen unterschiedliche Datenquellen wie SQL-Datenbanken, indizierten sequenziellen Dateien, Kalkulationstabellen, Dokumentspeicher und e-Mail-Dateien dar. Anbieter machen Daten gleichmäßig über eine allgemeine Abstraktion wird aufgerufen, das Rowset verfügbar.  
  
 ADO ist leistungsstark und flexibel, da es mehrere unterschiedliche Daten-Anbieter herstellen und weiterhin verfügbar das gleiche Programmiermodell, unabhängig vom angegebenen Anbieter die bestimmten Funktionen machen kann. Allerdings da jeden Datenanbieter eindeutig ist, variieren wie Ihre Anwendung mit ADO kommuniziert vom Datenanbieter.  
  
 Beispielsweise sind die Features und Funktionen von OLE DB-Anbieter für SQL Server, die verwendet wird, um Microsoft SQL Server-Datenbanken zugreifen, wesentlich von denen unterscheiden, von der Microsoft OLE DB-Anbieter für Internet Publishing, die verwendet wird, um den Zugriff auf Datei Speicher auf einem Webserver.
