---
title: Transact-SQL-Breakpoints | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f45a852838d3e54f994a55b29e3dcf64eaab8240
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="transact-sql-breakpoints"></a>Transact-SQL-Breakpoints
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Haltepunkte legen fest, dass der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Debugger die Ausführung bei einer bestimmten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung unterbricht. Sie können dann den Status der Codeelemente an diesem Punkt anzeigen.  
  
## <a name="breakpoints"></a>Breakpoints  
 Wenn Sie den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Debugger ausführen, können Sie einen Haltepunkt auf bestimmten Anweisungen umschalten. Wenn die Ausführung eine Anweisung mit einem Haltepunkt erreicht, hält der Debugger die Ausführung an, damit Sie Debuginformationen anzeigen können, z. B. die in Variablen und Parametern vorhandenen Werte.  
  
 Sie können Haltepunkte im Editorfenster einzeln verwalten, oder alle zusammen im Fenster **Haltepunkte** . Sie können Haltepunkte bearbeiten, um bestimmte Elemente festzulegen, wie z. B. die speziellen Bedingungen, unter denen der Haltepunkt die Ausführung anhalten soll, oder die Aktionen, die beim Ausführen des Haltepunkts durchgeführt werden sollen.  
  
## <a name="breakpoint-tasks"></a>Haltepunkttasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung angegeben wird, bei der der Debugger angehalten werden soll.|[Ein- und Ausschalten eines Breakpoints](../../relational-databases/scripting/toggle-a-breakpoint.md)|  
|Beschreibt, wie ein Haltepunkt vorübergehend deaktiviert und später erneut aktiviert wird. Beschreibt darüber hinaus, wie ein Haltepunkt gelöscht wird.|[Aktivieren, Deaktivieren und Löschen von Breakpoints](../../relational-databases/scripting/enable-disable-and-delete-breakpoints.md)|  
|Beschreibt, wie eine Bedingung angegeben wird, die definiert, ob Haltepunkte auf Grundlage der Auswertung eines angegebenen Transact-SQL-Ausdrucks unterbrochen werden.|[Angeben einer Breakpointbedingung](../../relational-databases/scripting/specify-a-breakpoint-condition.md)|  
|Beschreibt, wie eine Trefferanzahl festgelegt wird, die dazu führt, dass ein Haltepunkt nur dann unterbrochen wird, wenn die Anweisung, die den Haltepunkt enthält, mit einer festgelegten Häufigkeit ausgeführt wurde.|[Angeben einer Trefferanzahl](../../relational-databases/scripting/specify-a-hit-count.md)|  
|Beschreibt, wie ein Filter festgelegt wird, der bewirkt, dass ein Haltepunkt nur für angegebene Prozesse oder Threads unterbrochen wird.|[Angeben eines Breakpointfilters](../../relational-databases/scripting/specify-a-breakpoint-filter.md)|  
|Beschreibt, wie eine **Bei Treffer** -Aktion festgelegt wird, bei der es sich um einen Vorgang handelt, der beim Ausführen der Haltepunktanweisung durchgeführt wird. Ein Beispiel hierfür ist das Drucken einer Meldung.|[Angeben einer Breakpointaktion](../../relational-databases/scripting/specify-a-breakpoint-action.md)|  
|Beschreibt, wie die Position eines Haltepunkts bearbeitet wird.|[Bearbeiten einer Breakpointposition](../../relational-databases/scripting/edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Transact-SQL-Debuggerinformationen](../../relational-databases/scripting/transact-sql-debugger-information.md)  
  
  
