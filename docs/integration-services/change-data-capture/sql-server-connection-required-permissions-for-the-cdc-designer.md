---
title: Für SQL Server-Verbindung erforderliche Berechtigungen für den CDC Designer | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e5fd6b021c6baa82e47e83eac92b52e05c934fe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>SQL Server-Verbindung erfordert Berechtigungen für den CDC Designer
  Die CDC Designer Console erfordert für die Ausführung ihrer Tasks Verbindungsinformationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In diesem Thema werden die Informationen beschrieben, die im Dialogfeld **Verbindung mit SQL Server herstellen** zum Einrichten der Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angegeben werden können.  
  
 Das Dialogfeld **Verbindung mit SQL Server herstellen** wird jeweils bei Bedarf geöffnet, z. B. wenn keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindungsinformationen verfügbar sind oder wenn die Informationen zwar vorhanden sind, aber die Verbindung nicht die erforderlichen Berechtigungen aufweist.  
  
 In der folgenden Tabelle werden die verschiedenen Aufgaben beschrieben, für die eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erforderlich ist, sowie die erforderlichen Berechtigungen für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Benutzer (Anmeldung).  
  
|Task|Mindestberechtigungen|  
|----------|-------------------------|  
|Anzeigen der Liste mit den CDC-Diensten und -Instanzen, die die zugeordnete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz verwenden|`db_datareader` -Rolle für MSXDBCDC|  
|Starten/Beenden von CDC-Instanzen|`db_datareader` und `db_datawriter` für MSXDBCDC|  
|Anzeigen des CDC-Instanzstatus|`db_owner` -Rolle für die CDC-Instanzdatenbank|  
|Erstellen einer neuen Oracle CDC-Instanzdatenbank|`dbcreator` – feste Serverrolle|  
|Erstellen einer neuen Oracle CDC-Instanz|`db_datareader` -Rolle für MSXDBCDC<br /><br /> `db_owner` -Rolle für die erstellte CDC-Datenbank|  
|Abrufen von Bereitstellungsskripts|`db_datareader` und `db_datawriter` für MSXDBCDC<br /><br /> `db_owner` -Rolle für die zugehörige CDC-Datenbank|  
|Ändern der Konfiguration und Hinzufügen/Entfernen von Aufzeichnungsinstanzen|`db_datareader` und `db_datawriter` für MSXDBCDC<br /><br /> `db_owner` -Rolle für die zugehörige CDC-Datenbank|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Zugreifen auf die CDC Designer Console](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [SQL Server-Verbindung für die Instanzerstellung](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
