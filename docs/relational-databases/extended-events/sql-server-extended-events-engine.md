---
title: Modul für erweiterte Ereignisse von SQL Server | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], engine
ms.assetid: d74642a5-42b9-4a15-aa3d-f98bfe695050
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 451e9fbbb9601d2a3238594ffd9bfd22c979846f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-extended-events-engine"></a>Modul für erweiterte Ereignisse von SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events-Modul ist eine Sammlung von Diensten und Objekten, die:  
  
-   die Definition von Ereignissen ermöglichen,  
  
-   die Verarbeitung von Ereignisdaten ermöglichen,  
  
-   Dienste und Objekte für erweiterte Ereignisse im System verwalten und  
  
-   eine Liste von Sitzungen für erweiterte Ereignisse führen und den Zugriff auf diese Liste verwalten.  
  
 Das Modul für erweiterte Ereignisse selbst stellt keine Ereignisse oder beim Auslösen eines Ereignisses erforderlichen Aktionen bereit. Die Prozesse, die das Modul für erweiterte Ereignisse verwenden, definieren die Interaktion mit dem Modul. Diese Prozesse fügen Ereignispunkte hinzu und stellen die bei Auslösung eines Ereignisses erforderlichen Aktionen bereit.  
  
 Die folgende Abbildung zeigt eine vereinfachte Ansicht einer Sitzung für erweiterte Ereignisse. Weitere Informationen finden Sie unter [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md).  
  
 ![Detaillierte Architektur von erweiterten Ereignissen](../../relational-databases/extended-events/media/xearchitecturedetailed.gif "Detailed extended events architecture")  
  
 Beachten Sie Folgendes:  
  
-   Jeder Windows-Prozess kann über ein oder mehrere Module (**Win32-Prozess**, **Win32-Modul**) verfügen. Diese werden auch als *Binärdateien* oder *ausführbare Module*bezeichnet.  
  
-   Jedes Windows-Prozessmodul kann mindestens ein Paket für erweiterte Ereignisse (**Paket**) enthalten, das wiederum mindestens ein Objekt für erweiterte Ereignisse (**Typ**, **Ziel**, **Aktion**, **Zuordnung**, **Prädikat**und **Ereignis**) enthalten kann.  
  
-   Ein Hostprozess kann nur eine Instanz des Moduls für erweiterte Ereignisse (**Modul für erweiterte Ereignisse**) aufweisen. Dieses führt die folgenden Aufgaben aus:  
  
    -   Es verwaltet einige Aspekte der Sitzung (z. B. das Aufzählen von Sitzungen).  
  
    -   Es übernimmt die Verteilung (**Verteiler**). Dies ist mit einem Threadpool vergleichbar.  
  
    -   Es verarbeitet Speicherpuffer (**Puffer**) für Ereignisse. Wenn Puffer aufgefüllt sind, werden sie an Ziele verteilt.  
  
-   Wenn eine Sitzung erstellt wurde und optional Ereignisse an die Sitzung (**Sitzungskontext**) gebunden wurden:  
  
    -   Es können auch Instanzen von Zielen (**Zielinstanz**) erstellt und der Sitzung hinzugefügt werden.  
  
    -   Wenn Puffer aufgefüllt sind, werden diese an Ziele verteilt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  
