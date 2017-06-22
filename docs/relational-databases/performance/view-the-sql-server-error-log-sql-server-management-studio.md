---
title: Anzeigen des SQL Server-Fehlerprotokolls (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/29/2016
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
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4acdc87a3317c38b5b19235dae681bce426244e3
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-the-sql-server-error-log-sql-server-management-studio"></a>Anzeigen des SQL Server-Fehlerprotokolls (SQL Server Management Studio)
  Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll enthält benutzerdefinierte Ereignisse und bestimmte Systemereignisse, die für die Problembehandlung nützlich sind. 
  

  ## <a name="how-to-view-the-logs"></a>Anzeigen der Protokolle
1.  Wählen Sie in SSMS **Objekt-Explorer**aus.

>**Öffnen** von Objekt-Explorer: Die Tastenkombination ist **F8**. Klicken Sie im oberen Menü auf Ansicht/Objekt-Explorer ![Object_explorer](../../relational-databases/performance/media/object-explorer.png) 


2.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer Instanz von SQL Server her, und erweitern Sie dann diese Instanz.
  
3.  Suchen und erweitern Sie den Abschnitt **Verwaltung** (unter der Voraussetzung, dass Sie über Berechtigungen zum Anzeigen verfügen).

4.  Klicken Sie mit der rechten Maustaste auf **SQL Server-Protokolle**, wählen Sie „Ansicht“ und dann **SQL Server-Protokoll anzeigen**aus.
 ![View_SQLServer_Log_SSMS](../../relational-databases/performance/media/view-sqlserver-log-ssms.png) 
 
5.  Der Protokolldatei-Viewer wird mit einer Liste der verfügbaren Protokolle angezeigt (das kann einen Moment dauern).
  
6. Eine Reihe von Personen hat den nützlichen Beitrag [Identify location of the SQL Server Error Log file (Bestimmen des Speicherorts der SQL Server-Fehlerprotokolldatei)](https://www.mssqltips.com/sqlservertip/2506/identify-location-of-the-sql-server-error-log-file/)[MSSQLTips.com](https://www.mssqltips.com/) empfohlen. Da finden Sie eine Menge wirklich guter Informationen – probieren Sie es unbedingt aus!
  
  

