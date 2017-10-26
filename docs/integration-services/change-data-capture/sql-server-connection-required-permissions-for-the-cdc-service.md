---
title: "SQL Server-Verbindung erforderliche Berechtigungen für den CDC-Dienst | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 406cb1233d871603a38dc2d904d7ecd894b5f0cd
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sql-server-connection-required-permissions-for-the-cdc-service"></a>Für SQL Server-Verbindung erforderliche Berechtigungen für den CDC Service
  Die CDC Service Configuration Console erfordert Verbindungsinformationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um die damit verbundenen Tasks auszuführen. In diesem Thema werden die Informationen beschrieben, die im Dialogfeld Verbindung mit SQL Server herstellen zum Einrichten der Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angegeben werden können.  
  
 Das Dialogfeld Verbindung mit SQL Server herstellen wird jeweils bei Bedarf geöffnet, z. B. wenn keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindungsinformationen verfügbar sind oder wenn die Informationen zwar vorhanden sind, aber die Verbindung nicht die erforderlichen Berechtigungen aufweist.  
  
 In der folgenden Tabelle werden die verschiedenen Tasks beschrieben, für die eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich ist, sowie die erforderlichen Berechtigungen für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer (Anmeldung).  
  
|Task|Mindestberechtigungen|  
|----------|-------------------------|  
|Vorbereiten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz|`dbcreator` Feste Serverrolle|  
|Erstellen einer Oracle CDC Service-SQL Server-Anmeldung zur Verwendung durch den Oracle CDC Service|`public` Feste Serverrolle|  
|Erstellen einer Oracle CDC Service-Anmeldung, die zum Registrieren des neuen Diensts in MSXDBCDC verwendet werden soll|`db_datareader` und `db_datawriter` für MSXDBCDC|  
|Bearbeiten einer Oracle CDC Service-Anmeldung, die zum Aktualisieren der Registrierung des Diensts in MSXDBCDC verwendet werden soll|`db_datareader` und `db_datawriter` für MSXDBCDC|  
|Löschen einer Oracle CDC Service-Anmeldung, die zum Aktualisieren der Registrierung des Diensts in MSXDBCDC verwendet werden soll|`db_datareader` und `db_datawriter` für MSXDBCDC|  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindung mit SQLServer](../../integration-services/change-data-capture/connection-to-sql-server.md)   
 [Verbindung zu SQLServer zum Löschen](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md)  
  
  

