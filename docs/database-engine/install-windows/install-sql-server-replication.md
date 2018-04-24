---
title: Installieren der SQL Server-Replikation | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a7bbef0fe861660b5db2f25ca41b2cb525911a7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-replication"></a>Installieren der SQL Server-Replikation

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Die Replikationskomponenten können mithilfe des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder über die Eingabeaufforderung installiert werden. Installieren Sie die Replikation, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren oder wenn Sie eine vorhandene Instanz ändern.  
  
Nachdem die Replikationskomponenten installiert wurden, müssen Sie den Server konfigurieren, um die Replikation verwenden zu können. Weitere Informationen finden Sie unter [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
>[!IMPORTANT]  
>Wenn Sie Replikationskomponenten während der Änderung einer vorhandenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent nach Abschluss der Installation beenden und neu starten. Dadurch wird sichergestellt, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent die Subsysteme des Replikations-Agents erkennt und Replikations-Agents in Auftragsschritten aufrufen kann.  
  
## <a name="installing-replication-by-using-setup"></a>Installieren der Replikation mithilfe des Setups  
**So installieren Sie die Replikation, wenn Sie eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- Wählen Sie zum Installieren der Replikationskomponenten, einschließlich der Replikationsverwaltungsobjekte (Replication Management Objects, RMO), auf der Seite **Funktionsauswahl** des Installations-Assistenten die Option **SQL Server-Replikation** aus.  
  
## <a name="installing-replication-from-the-command-prompt"></a>Installieren der Replikation an der Eingabeaufforderung  
 **So installieren Sie die Replikation, wenn Sie eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- Siehe [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von SQL Server](../../database-engine/install-windows/install-sql-server.md)   
 [Installieren von SQL Server von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Features Supported by the Editions of SQL Server (Von den Editionen von SQL Server unterstützte Features)](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
  
