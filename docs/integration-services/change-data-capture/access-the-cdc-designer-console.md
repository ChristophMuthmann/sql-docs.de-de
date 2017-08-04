---
title: Zugriff auf die CDC Designer Console | Microsoft Docs
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
- accMsDes
ms.assetid: b168c64e-c1b5-42d4-a92a-84de1dd0324e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e1266809582119e6316b821c54f93f4217c21316
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="access-the-cdc-designer-console"></a>Zugreifen auf die CDC Designer Console
  Sie können auf die CDC Designer Console über den Computer zugreifen, auf dem Sie die Konsole installiert haben. Weitere Informationen zur Installation finden Sie unter Installation.  
  
 Wenn Sie die CDC Designer Console öffnen, wird das Dialogfeld Verbindung mit SQL Server herstellen geöffnet.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung, mit der auf den CDC Designer zugegriffen wird, muss über UPDATE-Berechtigungen für die MSXDBCDC-Datenbank verfügen. Außerdem muss die Anmeldung auch über die feste Serverrolle `dbcreator` verfügen, um neue Oracle CDC-Instanzen erstellen zu können. Es wird empfohlen, dass die Anmeldung auch über den SELECT-Zugriff auf die verwendeten CDC-Datenbanken verfügt. Andernfalls kann der Benutzer den Status dieser Datenbanken nicht anzeigen.  
  
 Geben Sie im Dialogfeld Verbindung mit SQL Server herstellen die folgenden Informationen ein.  
  
### <a name="server-name"></a>Servername  
 Geben Sie den Namen des Servers ein, auf dem sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet.  
  
### <a name="authentication"></a>Authentifizierung  
 Wählen Sie eine der folgenden Optionen aus:  
  
-   **Windows-Authentifizierung**  
  
-   **SQL Server-Authentifizierung:**Wenn Sie diese Option aktivieren, müssen Sie **Benutzername** und **Kennwort** für den Benutzer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingeben, mit dem Sie eine Verbindung herstellen.  
  
 Der angemeldete Benutzer muss über eine Datenbankrolle verfügen, die den Zugriff auf die MSXCDCDB-Datenbank ermöglicht. Es wird empfohlen, dass der angemeldete Benutzer außerdem Zugriff auf weitere Datenbanken hat, die verwendet werden, da der Benutzer die Daten in diesen Datenbanken sonst nicht anzeigen kann.  
  
### <a name="options"></a>enthalten  
 Klicken Sie auf den Pfeil, um die verfügbaren Optionen anzuzeigen, die konfiguriert werden sollen. Sie können für diese Optionen auch die Standardwerte unverändert lassen. Verfügbare Optionen:  
  
 **Verbindungstimeout**  
 Geben Sie den Zeitraum (in Sekunden) ein, wie lange der CDC Service for Oracle auf eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] warten soll, bevor ein Timeout eintritt. Der Standardwert lautet **15**.  
  
 **Ausführungstimeout**  
 Geben Sie den Zeitraum (in Sekunden) ein, wie lange der Oracle CDC-Windows-Dienst auf die Ausführung eines Befehls wartet, bis ein Timeout eintritt. Der Standardwert ist **30**.  
  
 **Verbindung verschlüsseln**  
 Wählen Sie **Verbindung verschlüsseln** für die Kommunikation zwischen dem Oracle CDC Service und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz aus, die eine verschlüsselte Verbindung verwendet.**Erweitert:**Klicken Sie auf **Erweitert** , und geben Sie ggf. zusätzliche Verbindungseigenschaften in das Dialogfeld „Erweiterte Verbindungseigenschaften“ ein.  
  
 **Erweitert:**  
 Klicken Sie auf **Erweitert** , und geben Sie ggf. zusätzliche Verbindungseigenschaften in das Dialogfeld „Erweiterte Verbindungseigenschaften“ ein.  
  
 Weitere Informationen zum Dialogfeld „Erweiterte Verbindungseigenschaften“ finden Sie unter [Erweiterte Verbindungseigenschaften](../../integration-services/change-data-capture/advanced-connection-properties.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Verbindung erforderliche Berechtigungen für den CDC Designer](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-designer.md)  
  
  
