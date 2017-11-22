---
title: Proaktives Zwischenspeichern (Dimensionen) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], proactive caching
- proactive caching [Analysis Services]
ms.assetid: 7d57fe93-6e5f-4a50-844f-dd2bbdbb94a5
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4771869da2e8603cf09a5e579f358a408207e777
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="proactive-caching-dimensions"></a>Proaktives Zwischenspeichern (Dimensionen)
  Proaktives Zwischenspeichern ermöglicht automatische MOLAP-Cacheerstellung und die Verwaltung von OLAP-Objekten. Cubes integrieren auf der Grundlage der von der Datenbank empfangenen Benachrichtigungen unverzüglich die Änderungen, die an den Daten in der Datenbank vorgenommen wurden. Das Ziel der proaktiven Zwischenspeicherung ist die Bereitstellung der Leistung von herkömmlichem MOLAP, während die Unmittelbarkeit und die einfache Handhabung von ROLAP erhalten bleibt.  
  
 Ein einfaches <xref:Microsoft.AnalysisServices.ProactiveCaching>-Objekt besteht aus: Zeitsteuerungsspezifikation und Tabellenbenachrichtigung. Die Zeitsteuerungsspezifikation definiert den zeitlichen Rahmen zum Aktualisieren des Caches, nachdem eine Änderungsbenachrichtigung empfangen wurde. Die Tabellenbenachrichtigung definiert das Benachrichtigungsschema zwischen der Datentabelle und dem <xref:Microsoft.AnalysisServices.ProactiveCaching>-Objekt.  
  
  
