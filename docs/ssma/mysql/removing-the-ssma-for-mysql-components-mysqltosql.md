---
title: Entfernen von SSMA für die MySQL-Komponenten (MySQLToSql) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: adf008b1a6bbcd584c0d3c0ee90dcb4345cf1819
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Entfernen von SSMA für die MySQL-Komponenten (MySQLToSql)
Nach Abschluss des Migrieren von Datenbanken von MySQL zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], möglicherweise möchten Sie SSMA-Komponenten zu deinstallieren. Sie können die Clientkomponenten jederzeit deinstallieren. Allerdings bei der Deinstallation der Erweiterung Pack vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , dann SSMA wird Migration von Daten aus MySQL in die Zieldatenbank (SQL Server-oder SQL Azure) verwenden das serverseitige-Datenmodul Migration nicht mehr unterstützt.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>SSMA deinstalliert für MySQL-Client.  
SSMA deinstallieren Sie mithilfe **Software**.  
  
**So deinstallieren Sie SSMA**  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie **Microsoft SQL Server Migration Assistant für MySQL**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie SSMA deinstallieren möchten, klicken Sie auf **Ja**.  
  
## <a name="uninstalling-the-extension-pack"></a>Die Erweiterung-Pack-Deinstallation  
Sie können über die Erweiterung Pack entfernen **Software**.  
  
**So deinstallieren Sie die Erweiterung pack**  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie **Microsoft SQL Server Migration Assistant für MySQL-Erweiterung Pack**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie das Pack Erweiterung deinstallieren möchten, klicken Sie auf **Ja**.  
  
4.  Klicken Sie auf die Instanzen mit Hilfsprogrammen Datenbankskripts-Seite, wählen Sie eine Instanz, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf der Seite "Verbindungsparameter" Wählen Sie die Authentifizierungsmethode aus, und klicken Sie dann auf **Weiter**.  
  
    Windows-Authentifizierung wird Windows-Anmeldeinformationen verwenden, um zu versuchen, melden Sie sich mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Bei Auswahl des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldename und Kennwort.  
  
6.  Klicken Sie auf der Seite Vorgang abgeschlossen auf **OK**.  
  
7.  Klicken Sie auf der Seite zum Fertigstellen auf **beenden**.  
  
Nach Abschluss der Deinstallation können Sie überprüfen, die Objekte der **sysdb.ssma_MySQL** Schema und möglicherweise die gesamte **Sysdb** Datenbank, die mit mehr [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Jedoch, wenn Sie andere SSMA-Produkte verwenden, sie auch verwenden, die **Sysdb** Datenbank. Wenn die Datenbank vorhanden ist, und Sie sicher sind, dass die Objekte in dieser Datenbank keine anderen Datenbanken verweisen, können Sie die Datenbank trennen.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für MySQL-Client &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Installing SSMA Components on SQL Server (Installieren von SSMA-Komponenten auf SQL Server)](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
