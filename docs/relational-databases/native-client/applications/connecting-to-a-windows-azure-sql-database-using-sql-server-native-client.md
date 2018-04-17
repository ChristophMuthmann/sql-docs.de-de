---
title: Herstellen einer Verbindung mit einer Windows Azure SQL-Datenbank mithilfe von SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: native-client|applications
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8145383913d7de07a1a6baf352eea1c3b9ede630
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-to-a-windows-azure-sql-database-using-sql-server-native-client"></a>Herstellen einer Verbindung mit einer Windows Azure SQL-Datenbank mithilfe von SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Ein Beispiel, in dem das Herstellen einer Verbindung mit einer [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] mithilfe von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client gezeigt wird, finden Sie unter [Entwicklung: Themen zur Vorgehensweise (Windows Azure SQL-Datenbank)](http://msdn.microsoft.com/library/ee621787.aspx).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Bekannte Probleme beim Herstellen einer Verbindung mit einer SQL-Datenbank  
 Die folgenden bekannten Probleme können auftreten, wenn mithilfe von [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hergestellt wird:  
  
-   Eine mithilfe von **SQLBrowseConnect** hergestellte Verbindung wird möglicherweise abgelehnt, wenn **SQLBrowseConnect** in mehreren Phasen verwendet wird.  Beispiel: Im ersten Aufruf wird der Treibername gesendet, im zweiten Aufruf werden Informationen zum Server und Anmeldeinformationen (Benutzer und Kennwort) gesendet, die Verbindung wird hergestellt, und im dritten Aufruf werden ein Datenbankname und eine Sprache gesendet.  Der dritte Aufruf bewirkt, dass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client eine USE-Anweisung zum Wechseln von Datenbanken ausgibt. Die USE-Anweisung wird jedoch in [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]nicht unterstützt und generiert den folgenden Fehler:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Anwendungen mit SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
