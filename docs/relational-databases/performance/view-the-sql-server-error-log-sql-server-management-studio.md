---
title: Anzeigen des SQL Server-Fehlerprotokolls (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying logs
- errors [SQL Server], logs
- logs [SQL Server], SQL Server error logs
- logs [SQL Server], viewing
ms.assetid: 55f468ba-146c-4ab3-95cd-d35d051afd12
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 20a301e257244b66e1c149c7cf8cf1f2489eb489
ms.openlocfilehash: a8c1290e33ad567520c813a1f365830644f545c7
ms.contentlocale: de-de
ms.lasthandoff: 09/29/2017

---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Anzeigen des SQL Server-Fehlerprotokolls (SQL Server Management Studio)

Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll enthält benutzerdefinierte Ereignisse und bestimmte Systemereignisse, die für die Problembehandlung nützlich sind. 

## <a name="how-to-view-the-logs"></a>Anzeigen der Protokolle

1.  Wählen Sie **Objekt-Explorer** in SSMS aus. **Öffnen** Sie den Objekt-Explorer entweder mit **F8**. oder klicken Sie im oberen Menü auf **Ansicht**, und wählen Sie **Objekt-Explorer** aus:
    
    ![Object_explorer](../../relational-databases/performance/media/object-explorer.png) 

2.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von SQL Server her, und erweitern Sie dann diese Instanz.
  
3.  Suchen und erweitern Sie den Abschnitt **Verwaltung** (unter der Voraussetzung, dass Sie über Berechtigungen zum Anzeigen verfügen).

4.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Protokolle**, wählen Sie erst **Ansicht** und anschließend **SQL Server-Protokoll anzeigen** aus.

    ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5.  Der Protokolldatei-Viewer öffnet sich, und es wird eine Liste der verfügbaren Protokolle angezeigt (dies kann einen Moment dauern).
  
6. Eine Reihe von Personen hat den nützlichen Beitrag [Identify location of the SQL Server Error Log file (Bestimmen des Speicherorts der SQL Server-Fehlerprotokolldatei)](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/)[MSSQLTips.com](https://www.mssqltips.com/) empfohlen. Da finden Sie eine Menge wirklich guter Informationen – probieren Sie es unbedingt aus!


