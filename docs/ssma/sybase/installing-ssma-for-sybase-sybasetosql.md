---
title: Installieren von SSMA für SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d4548d2e831fd2f4f2610d60a3268f4790144bd1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Installieren von SSMA für SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) für SAP Adaptive Server Enterprise (ASE) besteht aus einer Clientanwendung, die Sie verwenden zum Durchführen einer Migration von SAP ASE zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Es enthält auch einen Erweiterung Pack, der die Datenmigration sowie die Verwendung von Systemfunktionen ASE in die migrierten Datenbanken unterstützt.  
  
Installieren Sie die Clientanwendung auf dem Computer, von dem Sie die Migrationsschritte ausführen möchten. Installieren Sie die Erweiterung-Pack-Dateien auf dem Computer, auf denen ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] auf dem migrierten Datenbanken gehostet werden.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Upgraden von SSMA für SAP ASE  
Wenn Sie auf eine höhere Version von SSMA für SAP ASE aktualisieren möchten, müssen Sie zuerst den Client und Server Erweiterung Pack deinstallieren. Klicken Sie dann installieren Sie die neue Version.  
  
Wenn Sie ein Projekt von einer früheren Version von SSMA für SAP ASE öffnen, werden Sie SSMA gefragt, ob Sie das Projekt auf die neuere Version konvertieren möchten. Klicken Sie auf **Ja** bei dem Projekt in der neueren Version von SSMA ordnungsgemäß funktionieren.  
  
## <a name="contents"></a>Inhalt  
  
|Artikel|Description|  
|---------|---------------|  
|[Installieren von SSMA für SAP ASE Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Enthält Informationen und Anweisungen für die Installation von SSMA für SAP ASE-Client.|  
|[Installieren SSMA-Komponenten in SQLServer &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Enthält Informationen und Anweisungen für die Installation der Erweiterung Pack auf Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Entfernen von SSMA für SAP ASE Komponenten &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Stellt Anweisungen zum Deinstallieren des Clients Programm und die Erweiterung Pack bereit.|  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von SAP ASE-Datenbanken zu SQL Server - Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
