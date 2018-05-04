---
title: Entfernen von SSMA für die DB2-Komponenten (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 4ee0d698-6246-48eb-b963-d62be81cab6a
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fb208c93150274a42b9325a9760abb645c352a43
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="removing-ssma-for-db2-components-db2tosql"></a>Entfernen von SSMA für die DB2-Komponenten (DB2ToSQL)
Nach Abschluss des Migrieren von Datenbanken von DB2 nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], möglicherweise möchten Sie SSMA-Komponenten zu deinstallieren. Sie können die Clientkomponenten jederzeit deinstallieren. Allerdings sollten Sie nicht die Erweiterung Pack vom Deinstallieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wenn die migrierten Datenbanken nicht mehr Funktionen verwenden die **ssma_DB2** Schema der **Sysdb** Datenbank.  
  
## <a name="uninstalling-the-ssma-for-db2-client"></a>SSMA deinstalliert für DB2-Client.  
SSMA deinstallieren Sie mithilfe **Software**.  
  
**So deinstallieren Sie SSMA**  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für DB2**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie SSMA deinstallieren möchten, klicken Sie auf **Ja**.  
  
## <a name="uninstalling-the-extension-pack"></a>Die Erweiterung-Pack-Deinstallation  
Wenn Sie sicher sind, verwenden die migrierten Datenbanken nicht Objekte in der **sysdb.ssma_DB2** Schema, Sie können die Erweiterung Pack entfernen, indem Sie aus dem Schema löschen – es gibt keine Windows-Deinstallation ist  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für DB2-Client &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-client-db2tosql.md)  
[Installieren SSMA-Komponenten in SQLServer &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
  
