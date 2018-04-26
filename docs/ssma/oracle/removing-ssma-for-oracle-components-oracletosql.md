---
title: Entfernen von SSMA für die Oracle-Clientkomponenten (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: f55d809746dc5782a8d591cd6e85322394035cb2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Entfernen von SSMA für die Oracle-Clientkomponenten (OracleToSQL)
Nach Abschluss des Migrieren von Datenbanken aus Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], möglicherweise möchten Sie SSMA-Komponenten zu deinstallieren. Sie können die Clientkomponenten jederzeit deinstallieren. Allerdings sollten Sie nicht die Erweiterung Pack vom Deinstallieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wenn die migrierten Datenbanken nicht mehr Funktionen verwenden die **Ssma_oracle** Schema der **Sysdb** Datenbank.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>SSMA deinstalliert für Oracle-Client.  
SSMA deinstallieren Sie mithilfe **Software**.  
  
**So deinstallieren Sie SSMA**  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant für Oracle**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie SSMA deinstallieren möchten, klicken Sie auf **Ja**.  
  
## <a name="uninstalling-the-extension-pack"></a>Die Erweiterung-Pack-Deinstallation  
Wenn Sie sicher sind, verwenden die migrierten Datenbanken nicht Objekte in der **sysdb.ssma_oracle** Schema können, entfernen Sie das Pack Erweiterung mit **Software**.  
  
**So deinstallieren Sie die Erweiterung pack**  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie **Microsoft SQL Server Migration Assistant für Oracle-Erweiterung Pack**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie das Pack Erweiterung deinstallieren möchten, klicken Sie auf **Ja**.  
  
4.  Klicken Sie auf die Instanzen mit Hilfsprogrammen Datenbankskripts-Seite, wählen Sie eine Instanz, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite "Verbindungsparameter" Wählen Sie die Authentifizierungsmethode aus, und klicken Sie dann auf **Weiter**.  
  
    Windows-Authentifizierung wird Windows-Anmeldeinformationen verwenden, um zu versuchen, melden Sie sich mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Bei Auswahl des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldename und Kennwort.  
  
6.  Klicken Sie auf der Seite Vorgang abgeschlossen auf **OK**.  
  
7.  Klicken Sie auf der Seite zum Fertigstellen auf **beenden**.  
  
Nach der Deinstallation können Sie bestätigen, die Objekte der **sysdb.ssma_oracle** Schema und möglicherweise die gesamte **Sysdb** Datenbank, die mit mehr [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Jedoch, wenn Sie andere SSMA-Produkte verwenden, sie auch verwenden, die **Sysdb** Datenbank. Wenn die Datenbank vorhanden ist, und Sie sicher sind, dass keine anderen Datenbanken Objekte in dieser Datenbank verweisen, können Sie die Datenbank trennen.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Installieren SSMA-Komponenten in SQLServer &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
