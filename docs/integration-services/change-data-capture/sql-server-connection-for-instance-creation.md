---
title: SQL Server-Verbindung für die Instanzerstellung | Microsoft-Dokumentation
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
ms.assetid: 81d0e7e2-d8f0-4bd9-9565-218ce996f28e
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72521e3cbe7057b80c89c24b82440b7b2cacd7ad
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-connection-for-instance-creation"></a>SQL Server-Verbindung für die Instanzerstellung
  Einer der ersten Schritte beim Erstellen einer Oracle CDC-Instanz ist die Erstellung einer CDC-Datenbank auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz. Diese CDC-Datenbank wird für SQL Server CDC aktiviert, und für diese Aktivierung ist eine Anmeldung durch einen Benutzer erforderlich, der Mitglied der festen Serverrolle `sysadmin` ist.  
  
 Wenn ein Benutzer, der den Assistenten zum **Erstellen einer Oracle-CDC-Instanz** startet, kein Mitglied der festen Serverrolle `sysadmin` ist, wird das Dialogfeld **Verbindung mit SQL Server herstellen** geöffnet. Darin werden die Anmeldeinformationen für ein Mitglied der Rolle `sysadmin` angefordert, damit der Task zum Aktivieren der Datenbank für SQL Server CDC ausgeführt werden kann. Wenn die CDC-Datenbank erstellt wird, wird die `sysadmin` -Anmeldung verworfen, und der Vorgang wird mit der ursprünglichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung fortgesetzt, die beim Zugreifen auf die Oracle Designer Console verwendet wurde.  
  
## <a name="task-list"></a>Aufgabenliste  
 Geben Sie im Dialogfeld **Verbindung mit SQL Server herstellen** die folgenden Informationen ein.  
  
 **Servername**  
 Geben Sie den Namen des Servers ein, auf dem sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet.  
  
 **Authentifizierung**  
 Wählen Sie eine der folgenden Optionen aus:  
  
-   **Windows-Authentifizierung**  
  
-   **SQL Server-Authentifizierung:** Wenn Sie diese Option aktivieren, müssen Sie **Benutzername** und **Kennwort** für den Benutzer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingeben, mit dem Sie eine Verbindung herstellen.  
  
 Der angemeldete Benutzer muss über eine Datenbankrolle verfügen, die den Zugriff auf die MSXCDCDB-Datenbank ermöglicht. Es wird empfohlen, dass der angemeldete Benutzer außerdem Zugriff auf weitere Datenbanken hat, die verwendet werden, da der Benutzer die Daten in diesen Datenbanken sonst nicht anzeigen kann.  
  
 **Optionen**  
 Klicken Sie auf den Pfeil, um die verfügbaren Optionen anzuzeigen, die konfiguriert werden sollen. Sie können für diese Optionen auch die Standardwerte unverändert lassen. Verfügbare Optionen:  
  
-   **Verbindungstimeout**: Geben Sie den Zeitraum (in Sekunden) ein, wie lange der CDC Service für Oracle auf eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] warten soll, bevor ein Timeout eintritt. Der Standardwert lautet **15**.  
  
-   **Ausführungstimeout**: Geben Sie den Zeitraum (in Sekunden) ein, wie lange der Oracle CDC-Windows-Dienst auf die Ausführung eines Befehls warten soll, bevor ein Timeout eintritt. Der Standardwert ist **30**.  
  
-   **Verbindung verschlüsseln**: Wählen Sie **Verbindung verschlüsseln** für die Kommunikation zwischen dem Oracle CDC Service und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz aus, bei der eine verschlüsselte Verbindung verwendet werden soll.  
  
-   **Erweitert**: Klicken Sie auf **Erweitert** , und geben Sie ggf. zusätzliche Verbindungseigenschaften in das Dialogfeld „Erweiterte Verbindungseigenschaften“ ein.  
  
     Weitere Informationen zum Dialogfeld „Erweiterte Verbindungseigenschaften“ finden Sie unter [Erweiterte Verbindungseigenschaften](../../integration-services/change-data-capture/advanced-connection-properties.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen der SQL Server-Änderungsdatenbank](../../integration-services/change-data-capture/create-the-sql-server-change-database.md)   
 [SQL Server-Verbindung erfordert Berechtigungen für den CDC Designer](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
