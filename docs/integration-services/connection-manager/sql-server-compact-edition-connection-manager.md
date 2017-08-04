---
title: SQL Server Compact Edition-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dad3c3c379b62863de834386783b595c984c49ed
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition-Verbindungs-Manager
  Mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Verbindungs-Manager kann ein Paket eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenbank herstellen. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Ziel, das [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] enthält, lädt mithilfe dieses Verbindungs-Managers Daten in eine Tabelle einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenbank.  
  
> [!NOTE]  
>  Auf einem 64-Bit-Computer müssen Sie Pakete, die mit den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenquellen verbunden sind, im 32-Bit-Modus ausführen. Der Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, der von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenquellen verwendet wird, ist lediglich in einer 32-Bit-Version verfügbar.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>Konfiguration des SQL Server Compact Edition-Verbindungs-Managers  
 Wenn Sie einem Paket einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Verbindungs-Manager hinzufügen, wird von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ein Verbindungs-Manager erstellt, der zur Laufzeit zu einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Verbindung aufgelöst wird, die Eigenschaften des Verbindungs-Managers werden festgelegt, und der Verbindungs-Manager wird der **Connections** -Auflistung im Paket hinzugefügt.  
  
 Die **ConnectionManagerType** -Eigenschaft des Verbindungs-Managers ist auf **SQLMOBILE**festgelegt.  
  
 Es gibt folgende Möglichkeiten, um den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Verbindungs-Manager zu konfigurieren:  
  
-   Stellen Sie eine Verbindungszeichenfolge für den Speicherort der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Datenbank bereit.  
  
-   Stellen Sie ein Kennwort für eine kennwortgeschützte Datenbank bereit.  
  
-   Geben Sie den Server an, auf dem die Datenbank gespeichert ist.  
  
-   Geben Sie an, ob die im Verbindungs-Manager erstellte Verbindung zur Laufzeit beibehalten wird.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Verbindung“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [Verbindungs-Manager-Editor für SQL Server Compact Edition &#40;Seite „Alle“&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)festgelegt.  
  
  
