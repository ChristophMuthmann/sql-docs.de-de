---
title: "Verwenden von CDC Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: db5c718a-6e7f-48ec-82a3-9d5b131716e5
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Verwenden von CDC Services
  In diesem Verfahren wird beschrieben, wie Sie mithilfe der CDC Service Configuration Console eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz für die Verwendung von Oracle CDC Services vorbereiten und einen neuen CDC-Dienst erstellen.  
  
### So verwenden Sie CDC-Dienste  
  
1.  Wählen Sie im Menü **Start** die Option **CDC Service Configuration for Oracle**.  
  
2.  Wählen Sie im linken Bereich die Option **Local CDC Services** (Stammebene).  
  
3.  Führen Sie eine oder beide der folgenden Tasks aus:  
  
    -   **Prepare SQL Server**  
  
         Aktivieren Sie diese Option im **Aktionsbereich** rechts in der CDC Service Configuration Console.  
  
         Sie können auch mit der rechten Maustaste auf **Local CDC Services** klicken und **Prepare SQL Server** wählen.  
  
         Das Dialogfeld Preparing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instance for Oracle CDC wird geöffnet.  
  
         Zum Vorbereiten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz auf Oracle CDC-Dienste muss die Anmeldung über eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung mit der festen Serverrolle `dbcreator` verfügen. Diese Anmeldung wird verwendet, um die MSXDBCDC-Datenbank zu erstellen, die zum Hinzufügen von Oracle CDC Services und im weiteren Verlauf von Oracle CDC-Instanzen erforderlich ist.  
  
         Informationen zur Verwendung dieses Dialogfelds finden Sie unter [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md). Informationen zum Aktivieren einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz für CDC finden Sie unter [Vorbereiten von SQL Server für CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md).  
  
    -   **Erstellen eines neuen CDC-Diensts**  
  
         Klicken Sie auf der rechten Seite der CDC Service Configuration Console im **Aktionsbereich** auf **Neuer Dienst** .  
  
         Sie können auch mit der rechten Maustaste auf **Local CDC Services** klicken und **Neuer Dienst** auswählen.  
  
         Das Dialogfeld New Oracle CDC Service wird geöffnet.  
  
         Informationen zur Verwendung dieses Dialogfelds finden Sie unter [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md). Informationen zum Erstellen oder Bearbeiten eines CDC-Diensts finden Sie unter [How to Create and Edit a CDC Service](../../integration-services/change-data-capture/how-to-create-and-edit-a-cdc-service.md).  
  
         Die vom Oracle CDC Service verwendete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung muss lediglich Mitglied der festen Serverrolle `public` sein. Es sind keine anderen Berechtigungen erforderlich. Um den Oracle CDC Service zu erstellen, muss die Anmeldung jedoch die Schreibberechtigung für die MSXDBCDC-Datenbank besitzen, z. B. muss der Anmeldung die Datenbankrolle **db_owner** zugewiesen werden. Wenn mit einer Anmeldung ohne Schreibberechtigung für die MSXDBDCDC-Datenbank versucht wird, eine neue Oracle CDC-Instanz zu erstellen, wird eine Fehlermeldung angezeigt. Klicken Sie in diesem Dialogfeld auf **OK** , um das Dialogfeld Verbindung mit SQL Server herstellen anzuzeigen.  
  
         Informationen zum Eingeben der Anmeldeinformationen für eine Anmeldung, die über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügt, z. B. die Datenbankrolle **db_owner**, finden Sie unter [Erstellen und Bearbeiten eines CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) und [Verbindung mit SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
## Siehe auch  
 [Verwenden von CDC Services](../../integration-services/change-data-capture/work-with-cdc-services.md)  
  
  