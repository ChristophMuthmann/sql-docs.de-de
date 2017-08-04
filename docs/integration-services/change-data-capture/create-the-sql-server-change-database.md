---
title: "Erstellen der SQL Server-Änderungsdatenbank | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6934f245f0878e3491a7d1751e764dcf3db7bb46
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="create-the-sql-server-change-database"></a>Erstellen der SQL Server-Änderungsdatenbank
  Wenn Sie den Assistenten für neue Instanzen starten, wird die Seite Create CDC Database geöffnet. Verwenden Sie die Seite Create CDC Database, um Informationen zur neuen CDC-Instanz bereitzustellen und eine neue Änderungsdatenbank zu erstellen.  
  
 Wenn Sie eine neue CDC-Datenbank erstellen, wird diese für SQL Server CDC aktiviert. Für diese Aktivierung ist eine Anmeldung durch einen Benutzer erforderlich, der Mitglied der festen Serverrolle `sysadmin` ist.  
  
 Wenn ein Benutzer, der den Assistenten zum Erstellen einer Oracle CDC-Instanz startet, kein Mitglied der festen Serverrolle `sysadmin` ist, wird das Dialogfeld Verbindung mit SQL Server herstellen geöffnet. Darin werden die Anmeldeinformationen für ein Mitglied der Rolle sysadmin angefordert, damit der Task Enable the database for SQL Server CDC ausgeführt werden kann. Wenn die CDC-Datenbank erstellt wird, wird die `sysadmin` -Anmeldung verworfen, und der Vorgang wird mit der ursprünglichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung fortgesetzt, die beim Zugreifen auf die Oracle Designer Console verwendet wurde.  
  
> [!IMPORTANT]  
>  Für andere Tasks als „Datenbank für SQL Server CDC aktivieren“ muss die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung, die zum Ausführen des Assistenten für neue Instanzen verwendet wird, über die feste Serverrolle `dbcreator` und die UPDATE-Berechtigungen für die MSXDBCDC-Datenbank verfügen.  
  
 Informationen zum Eingeben der Daten im Dialogfeld Verbindung mit SQL Server herstellen finden Sie unter [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md).  
  
## <a name="options"></a>enthalten  
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
  
## <a name="see-also"></a>Siehe auch  
 [Vorgehensweise: Erstellen von SQL Server Change-Datenbankinstanz](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Der Oracle CDC Service](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
  
