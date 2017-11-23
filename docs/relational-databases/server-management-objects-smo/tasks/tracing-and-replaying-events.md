---
title: Verfolgen und Wiedergeben von Ereignissen | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- replaying events
- traces [SMO]
- events [SMO], replaying
- events [SMO], tracing
ms.assetid: f41b3f85-2f6c-4c3e-9776-8c73d2cc7a53
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3f21d2fb03590680afb0ceaf405448f6ad17761
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="tracing-and-replaying-events"></a>Verfolgen und Wiedergeben von Ereignissen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]In SMO werden die **Trace** und **Replay** Objekte in der <xref:Microsoft.SqlServer.Management.Trace> Namespace stellen einen programmgesteuerten Zugriff auf die [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] Funktionalität, die verwendet wird, für die Überwachung einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]oder [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Daten über die einzelnen Ereignisse können aufgezeichnet und in einer Datei oder Tabelle zur späteren Analyse gespeichert werden. Beispielsweise können Sie eine Produktionsumgebung überwachen und feststellen, welche Prozeduren langsam ablaufen und dadurch die Leistung beeinträchtigen.  
  
 Die **Ablaufverfolgung** und **Replay** Objekte stehen eine Reihe von Objekten, die zum Erstellen von ablaufverfolgungen in einer Instanz von verwendet werden kann [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Diese Objekte können in Ihren eigenen Anwendungen verwendet werden, um manuell Ablaufverfolgungen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] zu erstellen. Darüber hinaus SMO **Ablaufverfolgung** Objekte können verwendet werden, zum Lesen von SQL-Ablaufverfolgungsdateien und-Tabellen durch die Überwachung erstellte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], oder DTS-Protokollierung.  
  
 SMO **Trace** Objekten können Sie die folgenden Funktionen ausführen:  
  
-   Erstellen einer Ablaufverfolgung.  
  
-   Festlegen von Filtern für die Ablaufverfolgung.  
  
-   Festlegen der zu verfolgenden Ereignisse.  
  
-   Stoppen und Starten einer Ablaufverfolgung.  
  
-   Lesen von Ablaufverfolgungsdateien und Ablaufverfolgungstabellen.  
  
-   Abrufen von Informationen zu Ereignissen in einer Ablaufverfolgung.  
  
-   Abrufen von Informationen zu Filtern in einer Ablaufverfolgung.  
  
-   Programmgesteuertes Bearbeiten von Ablaufverfolgungsdaten.  
  
-   Schreiben von Ablaufverfolgungstabellen und Ablaufverfolgungsdateien.  
  
-   Wiedergeben von Ablaufverfolgungsdateien oder Ablaufverfolgungstabellen.  
  
 Die Ablaufverfolgungsdaten aus der **Ablaufverfolgung** und **Replay** Objekte können von der SMO-Anwendung verwendet werden oder manuell mithilfe von untersucht werden [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md). Die Ablaufverfolgungsdaten sind auch kompatibel mit der [SQL-Ablaufverfolgung](../../../relational-databases/sql-trace/sql-trace.md) gespeicherten Systemprozeduren, die auch eine Ablaufverfolgung ermöglichen.  
  
 Die SMO-Ablaufverfolgungsobjekte befinden sich im <xref:Microsoft.SqlServer.Management.Trace>-Namespace, für den ein Verweis auf die Datei Microsoft.SQLServer.ConnectionInfo.dll erforderlich ist.  
  
 Die **Ablaufverfolgung** und **Replay** Objekte erfordern eine [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> Objekt zum Herstellen einer Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Die [ServerConnection](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common.serverconnection.aspx) Objekt befindet sich in der [Microsoft.SqlServer.Management.Common](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.management.common) -Namespace, der ein Verweis auf die Datei Microsoft.SQLServer.ConnectionInfo.dll erforderlich ist.  
  
> [!NOTE]  
>  Die **Ablaufverfolgung** und **Replay** Objekte werden auf einer 64-Bit-Plattform nicht unterstützt.  
  
  
