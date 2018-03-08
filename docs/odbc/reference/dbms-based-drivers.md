---
title: DBMS-basierten Treibern | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c841b4404132e4fe385c9c3aa6fd12bdd2eb8a0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="dbms-based-drivers"></a>DBMS-basierten Treibern
DBMS-basierten Treibern sind mit Datenquellen wie z. B. Oracle- oder SQL Server verwendet, die ein eigenständiges Datenbankmodul für den Treiber bereitstellen. Diese Treiber Zugriff auf die physischen Daten über die eigenständigen Datenbankmodul; d. h. SQL-Anweisungen zum Senden und Abrufen von Ergebnissen aus dem Modul.  
  
 Da die DBMS-basierten Treibern Motor vorhandene Datenbank verwenden, sind sie in der Regel leichter als dateibasierten Treibern zu schreiben. Obwohl ein DBMS-basierten Treiber einfach durch Übersetzen ODBC-Aufrufe von systemeigenen API-Aufrufe implementiert werden kann, führt dies ein langsamer Treiber. Eine bessere Möglichkeit zum Implementieren eines DBMS-basierten Treibers ist die zugrunde liegenden Daten Stream-Protokoll verwendet wird, das in der Regel ist die Funktionsweise der systemeigenen API. Beispielsweise sollten ein SQL Server-Treiber TDS (die Daten streamen Protokoll für SQL Server) verwenden, anstatt DB-Library (systemeigene API für SQL Server). Eine Ausnahme von dieser Regel wird bei ODBC die systemeigenen API ist. Watcom SQL ist z. B. ein eigenständiger Modul, befindet sich auf dem gleichen Computer wie die Anwendung und wird direkt als der Treiber geladen.  
  
 DBMS-basierten Treibern fungieren als Clients in einer Client-/Server-Konfiguration, fungiert, in dem die Datenquelle als Server. In den meisten Fällen befinden sich der Client (Treiber) und Server (Datenquelle) auf verschiedenen Computern zwar sowohl auf dem gleichen Computer unter einem Multitasking-Betriebssystem befinden können. Eine dritte Möglichkeit ist eine *Gateway* die befindet sich zwischen den Treiber und die Datenquelle. Ein Gateway ist eine Softwarekomponente, die bewirkt, dass ein DBMS an, wie eine andere aussehen. Beispielsweise können Anwendungen, in SQL Server verwenden, auch DB2-Daten über das Gateway des Micro Decisionware DB2 zugreifen; Dieses Produkt wird DB2 Aussehen von SQL Server.  
  
 Die folgende Abbildung zeigt drei verschiedene Konfigurationen von DBMS-basierten Treibern. Befinden sich in der ersten Konfiguration der Treiber und die Datenquelle auf demselben Computer. Im zweiten Fall befinden sich auf verschiedenen Computern die Treiber und die Datenquellensicht. Im dritten die Treiber und die Datenquellensicht auf unterschiedlichen Computern befinden und ein Gateway zwischen ihnen, die auf noch einem anderen Computer befindet.  
  
 ![Drei Konfigurationen von DBMS &#45; basierend Treiber](../../odbc/reference/media/pr07.gif "pr07")
