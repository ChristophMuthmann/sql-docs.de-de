---
title: "Installieren von SSMA für SAP ASE (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 09/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 759a7084024e1c608431683de6dae5a6fb40304e
ms.openlocfilehash: 7b2c96006c5495c89486c8a86e1b60b64f2dd22c
ms.contentlocale: de-de
ms.lasthandoff: 10/03/2017

---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Installieren von SSMA für SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) for SAP ASE besteht aus einer Clientanwendung, die Sie verwenden zum Durchführen einer Migration von SAP Adaptive Server Enterprise (ASE) auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Es enthält auch einen Erweiterung Pack, der die Datenmigration sowie die Verwendung von Systemfunktionen ASE in die migrierten Datenbanken unterstützt.  
  
Installieren Sie die Clientanwendung auf dem Computer, von dem aus Sie die Migrationsschritte ausführen werden. Müssen Sie die Erweiterung-Pack-Dateien auf dem Computer, auf denen ausgeführt wird, installieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , in denen migrierte Datenbanken gehostet werden.  
  
## <a name="upgrading-ssma-for-sybase"></a>Aktualisieren von SSMA für Sybase  
Wenn Sie auf eine höhere Version von SSMA für SAP ASE aktualisieren möchten, müssen Sie deinstalliert werden, den Client und Server Erweiterung Pack und dann die neuere Version installieren.  
  
Wenn Sie ein Projekt von einer früheren Version von SSMA für SAP ASE öffnen, werden Sie SSMA gefragt, ob Sie das Projekt auf die neuere Version konvertieren möchten. Klicken Sie auf **Ja** bei dem Projekt in der neueren Version von SSMA ordnungsgemäß funktionieren.  
  
## <a name="contents"></a>Inhalt  
  
|Thema|Description|  
|---------|---------------|  
|[Installieren SSMA für SAP ASE Client &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Enthält Informationen und Anweisungen zur Installation des SSMA-Clients.|  
|[Installieren SSMA-Komponenten auf SQLServer &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Enthält Informationen und Anweisungen für die Installation der Erweiterung Pack auf Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Entfernen von SSMA für SAP ASE Komponenten &#40; SybaseToSQL &#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Stellt Anweisungen zum Deinstallieren des Clients Programm und die Erweiterung Pack bereit.|  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von SAP ASE Datenbanken zu SQL Server - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
