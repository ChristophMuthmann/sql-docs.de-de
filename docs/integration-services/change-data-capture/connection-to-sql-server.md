---
title: "Verbindung zu SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Verbindung zu SQL Server
  Wenn eine Anmeldung ohne Datenbankrolle, die über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügt (z.B. die Rolle **db_owner**), versucht, eine Oracle CDC-Instanz zu erstellen, wird das Dialogfeld „Verbindung mit SQL Server herstellen“ angezeigt.  
  
 In diesem Dialogfeld müssen Sie die Anmeldeinformationen für eine Anmeldung eingeben, die über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügt, z.B. die Datenbankrolle **db_owner** zum Erstellen der neuen Oracle CDC-Instanz.  
  
 Geben Sie im Dialogfeld Verbindung mit SQL Server herstellen die folgenden Informationen ein.  
  
### Servername  
 Geben Sie den Namen des Servers ein, auf dem sich [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet.  
  
### Authentifizierung  
 Wählen Sie eine der folgenden Optionen aus:  
  
-   Windows-Authentifizierung  
  
-   **SQL Server-Authentifizierung:** Wenn Sie diese Option aktivieren, müssen Sie **Benutzername** und **Kennwort** für den Benutzer von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingeben, mit dem Sie eine Verbindung herstellen.  
  
### enthalten  
 Klicken Sie auf den Pfeil, um die verfügbaren Optionen anzuzeigen, die konfiguriert werden sollen. Sie können für diese Optionen auch die Standardwerte unverändert lassen. Verfügbare Optionen:  
  
-   **Verbindungstimeout:** Geben Sie den Zeitraum (in Sekunden) ein, wie lange das Programm auf die Herstellung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindung warten soll, bevor ein Timeoutfehler eintritt. Der Standardwert lautet **15**.  
  
-   **Ausführungstimeout:** Geben Sie den Zeitraum (in Sekunden) ein, wie lange das Programm auf die Beendigung der SQL-Befehlsausführung warten soll, bevor ein Timeoutfehler eintritt. Der Standardwert ist **30**.  
  
-   **Verbindung verschlüsseln:** Aktivieren Sie **Verbindung verschlüsseln**, um sicherzustellen, dass die hergestellte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindung verschlüsselt wird, um für Datenschutz zu sorgen.  
  
-   **Erweitert:** Klicken Sie auf **Erweitert**, und geben Sie ggf. zusätzliche Verbindungseigenschaften in das Dialogfeld „Erweiterte Verbindungseigenschaften“ ein.  
  
## Siehe auch  
 [Für SQL Server-Verbindung erforderliche Berechtigungen für den CDC Service](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  