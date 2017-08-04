---
title: SQL-Volltextfilterdaemon-Startprogramm (SQL Server-Konfigurations-Manager) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b4768f274310400e99a355676b2c0cd7a27666e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Startprogramm für SQL-Volltextfilterdaemon (SQL Server-Konfigurations-Manager)
  Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wird der FDHOST (SQL-Volltextfilterdaemon)-Startprogrammdienst von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextsuche zum Starten des Filterdaemon-Hostprozesses verwendet, der für das Filtern bei der Volltextsuche und die Wörtertrennung verantwortlich ist. Dieser Dienst muss ausgeführt werden, damit die Volltextsuche verwendet werden kann. Der FDHOST-Startprogrammdienst ist ein instanzabhängiger Dienst, dem eine bestimmte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zugeordnet ist. Der FDHOST-Startprogrammdienst gibt die Dienstkontoinformationen an jeden gestarteten Filterdaemon-Hostprozess weiter. Informationen zu den Prozessen des Filterdaemonhosts finden Sie unter „Architektur der Volltextsuche“ in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
  
