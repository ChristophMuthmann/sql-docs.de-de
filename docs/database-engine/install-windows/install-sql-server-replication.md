---
title: Installieren der SQL Server-Replikation | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0afd7ea022cb4901e1f536a1066036f246802173
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-replication"></a>Installieren der SQL Server-Replikation
  Die Replikationskomponenten können mithilfe des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder über die Eingabeaufforderung installiert werden. Installieren Sie die Replikation, wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren oder wenn Sie eine vorhandene Instanz ändern.  
  
 Nachdem die Replikationskomponenten installiert wurden, müssen Sie den Server konfigurieren, um die Replikation verwenden zu können. Weitere Informationen finden Sie unter [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md) in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
> [!IMPORTANT]  
>  Wenn Sie Replikationskomponenten während der Änderung einer vorhandenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installieren, müssen Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent nach Abschluss der Installation beenden und neu starten. Dadurch wird sichergestellt, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent die Subsysteme des Replikations-Agents erkennt und Replikations-Agents in Auftragsschritten aufrufen kann.  
  
## <a name="installing-replication-by-using-setup"></a>Installieren der Replikation mithilfe des Setups  
 **So installieren Sie die Replikation, wenn Sie eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Wählen Sie zum Installieren der Replikationskomponenten, einschließlich der Replikationsverwaltungsobjekte (Replication Management Objects, RMO), auf der Seite **Funktionsauswahl** des Installations-Assistenten die Option **SQL Server-Replikation** aus.  
  
## <a name="installing-replication-from-the-command-prompt"></a>Installieren der Replikation an der Eingabeaufforderung  
 **So installieren Sie die Replikation, wenn Sie eine neue Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   Siehe [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)   
 [Installieren von SQL Server 2016 von der Eingabeaufforderung](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
  
  

