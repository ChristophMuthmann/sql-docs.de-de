---
title: Erstellen von SMO-Programmen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8813cbaa9426993f1e1d584d536bf2fa6ccf123a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="creating-smo-programs"></a>Erstellen von SMO-Programmen
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Die allgemeinen Programmierungsaufgaben für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO)-Objekte umfassen Bereiche, die allen Objekten gemein sind, wie z. B. das Ausführen von Methoden, das Einstellen von Eigenschaften oder die Bearbeitung von Auflistungen.  
  
|Thema|Description|  
|-----------|-----------------|  
|[Herstellen einer Verbindung mit einer Instanz von SQLServer](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|Das grundlegendste SMO-Programm, das eine Verbindung zu einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herstellt. Veranschaulicht die Windows-Authentifizierung und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Authentifizierung. Enthält zudem Beispiele, die das Herstellen einer Verbindung mit einer lokalen und einer Remoteinstanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zeigen.|  
|[Trennen von einer Instanz von SQLServer](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|Ein Programm, das veranschaulicht, wie die Verbindung zur Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] getrennt wird.|  
|[Aufrufen von Methoden](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|In diesem Abschnitt wird die allgemeine Vorgehensweise zum Aufrufen von Methoden beschrieben. Zeigt die Verwendung von Parametern und die Handhabung von Tabellen mit Daten, die in einem <xref:System.Data.DataTable>-Objekt zurückgegeben wurden. Enthält zudem ein Beispiel, wie einen Objektkonstruktor aufgerufen und zum Aufrufen der **Klon** Methode.|  
|[Einstellen von Eigenschaften – SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|In diesem Abschnitt wird beschrieben, wie verschiedene Eigenschaftentypen festgelegt werden. Es wird gezeigt, wie Objekteigenschaften festgelegt und abgerufen werden. Zudem werden Beispiele für das Festlegen von Objekteigenschaften bei Erstellung des Objekts gegeben, und es wird erläutert, wie alle Eigenschaften eines Objekts durchlaufen werden.|  
|[Verwenden von Auflistungen](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|Verschiedene Programme, mit denen die für Objektauflistungen verwendeten Techniken erläutert werden. Zeigt, wie mit Auflistungen auf ein Objekt verwiesen wird. Beinhaltet auch ein Beispiel, das verdeutlicht, wie die Elemente einer Auflistung durchlaufen werden.|  
|[Behandeln von SMO-Ereignissen](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|In diesem Abschnitt wird beschrieben, wie Ereignisse in SMO eingerichtet und behandelt werden. Anhand eines Beispiels wird gezeigt, wie ein Ereignishandler und das Ereignisabonnement eingerichtet werden.|  
|[Behandeln von SMO-Ausnahmen](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|In diesem Abschnitt wird beschrieben, wie Ausnahmen in SMO aufgefangen werden. Er enthält zudem Beispiele, wie eine Ausnahme erfasst und eine innere Ausnahme angezeigt wird.|  
|[Arbeiten mit Datentypen](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|In diesem Abschnitt wird beschrieben, wie mit den verschiedenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentypen gearbeitet wird. Es wird darauf eingegangen, wie ein Datentyp mit der Spezifikation im Objektkonstruktor erstellt wird. Anhand eines Beispiels wird außerdem erläutert, wie ein Datentyp mit dem Standardkonstruktor erstellt wird.|  
|[Verwenden von Transaktionen](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|In diesem Abschnitt wird beschrieben, wie die Transaktionsverarbeitung in einem SMO-Programm implementiert wird. Ein Beispiel veranschaulicht, wie Transaktionen in einem SMO-Programm verwendet werden.|  
|[Verwenden des Aufzeichnungsmodus](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|In diesem Abschnitt wird beschrieben, wie die Ausgabe des SMO-Programms aufgezeichnet wird. Im Beispiel wird das SMO-Programm als [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisung zur späteren Ausführung an die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz gesendet.|  
  
  
