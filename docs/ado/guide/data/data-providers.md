---
title: Datenanbieter | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
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
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e6d00455aecf64a1de3f8304c8be5ec18b7de7c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="data-providers"></a>Datenanbieter
Datenanbieter stellen unterschiedliche Datenquellen wie SQL-Datenbanken, indizierten sequenziellen Dateien, Kalkulationstabellen, Dokumentspeicher und e-Mail-Dateien dar. Anbieter machen Daten gleichmäßig über eine allgemeine Abstraktion wird aufgerufen, das Rowset verfügbar.  
  
 ADO ist leistungsstark und flexibel, da es mehrere unterschiedliche Daten-Anbieter herstellen und weiterhin verfügbar das gleiche Programmiermodell, unabhängig vom angegebenen Anbieter die bestimmten Funktionen machen kann. Allerdings da jeden Datenanbieter eindeutig ist, variieren wie Ihre Anwendung mit ADO kommuniziert vom Datenanbieter.  
  
 Beispielsweise sind die Features und Funktionen von OLE DB-Anbieter für SQL Server, die verwendet wird, um Microsoft SQL Server-Datenbanken zugreifen, wesentlich von denen unterscheiden, von der Microsoft OLE DB-Anbieter für Internet Publishing, die verwendet wird, um den Zugriff auf Datei Speicher auf einem Webserver.
