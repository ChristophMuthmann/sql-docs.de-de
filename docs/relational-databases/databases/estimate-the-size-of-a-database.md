---
title: "Schätzen der Größe einer Datenbank | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d2d986d7e899e630429f431f040addb9076f081a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="estimate-the-size-of-a-database"></a>Schätzen der Größe einer Datenbank
  Wenn Sie eine Datenbank entwerfen, müssen Sie möglicherweise die Größe der Datenbank schätzen, wenn diese mit Daten aufgefüllt ist. Das Schätzen der Datenbankgröße kann Ihnen helfen, die Hardwarekonfiguration zu bestimmen, die für Folgendes benötigt wird:  
  
-   Erzielen der Leistung, die von den Anwendungen benötigt wird.  
  
-   Bereitstellen von physischem Speicherplatz in angemessenem Umfang, um Daten und Indizes zu speichern.  
  
 Durch das Schätzen der Datenbankgröße können Sie auch bestimmen, ob der Datenbankentwurf verfeinert werden muss. Sie könnten z. B. feststellen, dass die geschätzte Größe der Datenbank viel zu groß ist, um in Ihrer Organisation implementiert zu werden, und dass eine weitere Normalisierung erforderlich ist. Umgekehrt kann es auch vorkommen, dass der geschätzte Umfang kleiner ist als erwartet. Dann könnten Sie die Normalisierung teilweise oder ganz aufheben, um auf diese Weise die Abfrageleistung zu verbessern.  
  
 Um die Größe einer Datenbank zu schätzen, sollten Sie die Größe jeder einzelnen Tabelle schätzen und dann die ermittelten Werte addieren. Die Größe einer Tabelle hängt davon ab, ob die Tabelle über Indizes verfügt und, wenn dies der Fall ist, welcher Typ von Indizes verwendet wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[Schätzen der Größe einer Tabelle](../../relational-databases/databases/estimate-the-size-of-a-table.md)|Beschreibt die Schritte und Berechnungen, die zum Schätzen des Umfangs des Speicherplatzes erforderlich sind, der zum Speichern der Daten in einer Tabelle und für die zugehörigen Indizes benötigt wird.|  
|[Schätzen der Größe eines Heaps](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|Beschreibt die Schritte und Berechnungen, die zum Schätzen des Umfangs des Speicherplatzes erforderlich sind, der zum Speichern der Daten in einem Heap benötigt wird. Ein Heap ist eine Tabelle, die nicht über einen gruppierten Index verfügt.|  
|[Schätzen der Größe eines gruppierten Indexes](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|Beschreibt die Schritte und Berechnungen, die zum Schätzen des Umfangs des Speicherplatzes erforderlich sind, der zum Speichern der Daten in einem gruppierten Index benötigt wird.|  
|[Schätzen der Größe eines nicht gruppierten Index](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|Beschreibt die Schritte und Berechnungen, die zum Schätzen des Umfangs des Speicherplatzes erforderlich sind, der zum Speichern der Daten in einem nicht gruppierten Index benötigt wird.|  
  
  
