---
title: "Entfernen von SSMA für Sybase-Komponenten (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dadcc8384871ceaebd0151859f4017c88ed6a219
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Entfernen von SSMA für Sybase-Komponenten (SybaseToSQL)
Nach Abschluss des Migrieren von Datenbanken von Sybase Adaptive Server Enterprise (ASE) auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], möglicherweise möchten Sie SSMA-Komponenten zu deinstallieren. Können Sie die Clientkomponenten jederzeit deinstallieren, aber Sie sollten keine Deinstallieren der Erweiterung Pack vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , wenn Sie sicher sind, dass die migrierten Datenbanken nicht mehr Funktionen verwenden die **Ssma_syb** Schema der **Sysdb** Datenbank.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>SSMA deinstallieren für Sybase-Clients  
SSMA deinstallieren Sie mithilfe **Software**.  
  
**So deinstallieren Sie SSMA**  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie **Microsoft SQL Server Migration Assistant für Sybase**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie SSMA deinstallieren möchten, klicken Sie auf **Ja**.  
  
## <a name="uninstalling-the-extension-pack"></a>Die Erweiterung-Pack-Deinstallation  
Wenn Sie sicher sind, verwenden die migrierten Datenbanken nicht Objekte in der **sysdb.ssma_syb** Schema können, entfernen Sie das Pack Erweiterung mit **Software**.  
  
So deinstallieren Sie die Erweiterung pack  
  
1.  Öffnen Sie in der Systemsteuerung **Software**.  
  
2.  Wählen Sie **Microsoft SQL Server Migration Assistant für Sybase Erweiterung Pack**, und klicken Sie dann auf **entfernen**.  
  
3.  Um zu bestätigen, dass Sie das Pack Erweiterung deinstallieren möchten, klicken Sie auf **Ja**.  
  
4.  Klicken Sie auf die Instanzen mit Hilfsprogrammen Datenbankskripts-Seite, auf **Weiter**.  
  
5.  Klicken Sie auf der Seite "Verbindungsparameter" Wählen Sie die Authentifizierungsmethode aus, und klicken Sie dann auf **Weiter**.  
  
    Windows-Authentifizierung wird Ihre Windows-Anmeldeinformationen verwenden, um zu versuchen, mit der Instanz von SQL Server anmelden. Wenn Sie SQL Server-Authentifizierung auswählen, müssen Sie einen SQL Server-Anmeldename und ein Kennwort eingeben.  
  
6.  Klicken Sie auf der Seite Vorgang abgeschlossen auf **OK**.  
  
7.  Klicken Sie auf der Seite zum Fertigstellen auf **beenden**.  
  
Nach der Deinstallation, bestätigen Sie, dass die **sysdb.ssma_syb** Schema und möglicherweise die gesamte **Sysdb** Datenbank, die mit mehr [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Jedoch, wenn Sie andere SSMA-Produkte verwenden, sie auch verwenden, die **Sysdb** Datenbank. Wenn die Datenbank vorhanden ist, und Sie sicher sind, dass keine anderen Datenbanken Objekte in dieser Datenbank verweisen, können Sie die Datenbank trennen.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für Sybase Client &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Installieren SSMA-Komponenten auf SQLServer &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
