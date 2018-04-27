---
title: Erstellen der SQL Server-Änderungsdatenbank | Microsoft-Dokumentation
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
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d6a055e32af1186651e182c223b9018ba7bd5ad
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-the-sql-server-change-database"></a>Erstellen der SQL Server-Änderungsdatenbank
  Wenn Sie den Assistenten für neue Instanzen starten, wird die Seite Create CDC Database geöffnet. Verwenden Sie die Seite Create CDC Database, um Informationen zur neuen CDC-Instanz bereitzustellen und eine neue Änderungsdatenbank zu erstellen.  
  
 Wenn Sie eine neue CDC-Datenbank erstellen, wird diese für SQL Server CDC aktiviert. Für diese Aktivierung ist eine Anmeldung durch einen Benutzer erforderlich, der Mitglied der festen Serverrolle `sysadmin` ist.  
  
 Wenn ein Benutzer, der den Assistenten zum Erstellen einer Oracle CDC-Instanz startet, kein Mitglied der festen Serverrolle `sysadmin` ist, wird das Dialogfeld Verbindung mit SQL Server herstellen geöffnet. Darin werden die Anmeldeinformationen für ein Mitglied der Rolle sysadmin angefordert, damit der Task Enable the database for SQL Server CDC ausgeführt werden kann. Wenn die CDC-Datenbank erstellt wird, wird die `sysadmin` -Anmeldung verworfen, und der Vorgang wird mit der ursprünglichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung fortgesetzt, die beim Zugreifen auf die Oracle Designer Console verwendet wurde.  
  
> [!IMPORTANT]  
>  Für andere Tasks als „Datenbank für SQL Server CDC aktivieren“ muss die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung, die zum Ausführen des Assistenten für neue Instanzen verwendet wird, über die feste Serverrolle `dbcreator` und die UPDATE-Berechtigungen für die MSXDBCDC-Datenbank verfügen.  
  
 Informationen zum Eingeben der Daten im Dialogfeld Verbindung mit SQL Server herstellen finden Sie unter [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md).  
  
## <a name="options"></a>Tastatur  
 **Oracle CDC-Instanz**  
 Geben Sie die folgenden Informationen zur CDC-Instanz an, die Sie erstellen.  
  
-   **Name**: Geben Sie einen Namen für den neuen Dienst ein. Dieser Name wird auch als Name der neuen Änderungsdatenbank verwendet.  
  
-   **Beschreibung**: Geben Sie eine Beschreibung für die neue Instanz ein, um sie besser identifizieren zu können. Diese Eingabe ist optional.  
  
 **SQL Server Change Database**  
 Dieser Abschnitt wird verwendet, um die Datenbank zu erstellen.  
  
1.  **Change Database**: Der Name der neuen Änderungsdatenbank. Der Name der Datenbank entspricht dem Namen, den Sie der Instanz gegeben haben. In diesem schreibgeschützten Feld wird der vollständige Pfad zur Datenbank angezeigt.  
  
2.  **Datenbank erstellen**: Klicken Sie auf **Datenbank erstellen** , um die Datenbank zu erstellen.  
  
     Zum Erstellen der Datenbank muss die Anmeldung über die Serverrolle `sysasmin` verfügen. Weitere Informationen finden Sie oben unter dem Sicherheitshinweis.  
  
     Nachdem Sie die Datenbank erstellt haben, können Sie auf **Weiter** klicken, um den Schritt [Connect to an Oracle Source Database](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md)auszuführen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen der Instanz für die SQL Server-Änderungsdatenbank](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle CDC Service](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
  
