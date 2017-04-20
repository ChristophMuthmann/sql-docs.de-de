---
title: Dialogfeld Verbindungseigenschaften | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connectionproperties.f1
helpviewer_keywords:
- Connection Properties dialog box
ms.assetid: 6df812ad-4d80-4503-8a23-47719ce85624
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8e258a6b81a9061c08ba4df098afa4e67c74df3a
ms.lasthandoff: 04/11/2017

---
# <a name="connection-properties-dialog-box"></a>Verbindungseigenschaften (Dialogfeld)
Zeigen Sie mithilfe dieses Dialogfelds die aktuellen Verbindungseigenschaften an. Das Dialogfeld wird angezeigt, wenn Sie in verschiedenen Dialogfeldern des Objekt-Explorers auf **Verbindungseigenschaften anzeigen** klicken. Die auf dieser Seite angezeigten Eigenschaften sind schreibgeschützt.  
  
Wenn Sie Eigenschaften, z. B. den Wert für **Datenbank**, ändern möchten, stellen Sie, bevor Sie das Dialogfeld **Verbindungseigenschaften** öffnen, mit dem Objekt-Explorer eine Verbindung zu der gewünschten Datenbank her.  
  
Hinweis: Das Abfragetimeout für SQL Azure liegt bei 30 Minuten.  
  
## <a name="authentication"></a>Authentifizierung  
Zeigt die Authentifizierungseigenschaften für die aktuelle Verbindung an. Zu den Authentifizierungseigenschaften zählen der Anmeldename und die Authentifizierungsmethode, die beim Herstellen der Verbindung verwendet wurden. Zum Ändern der Authentifizierungseigenschaften trennen Sie die Verbindung zu [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und stellen Sie dann erneut eine Verbindung zwischen dem Objekt-Explorer und dem Server her, wobei Sie die gewünschten Verbindungsoptionen verwenden.  
  
**Authentifizierungsmethode**  
Für die aktuelle Verbindung verwendete Authentifizierungsmethode.  
  
**Benutzername**  
Bei der Verbindungsauthentifizierung für die Anmeldung verwendeter Benutzername.  
  
## <a name="connection-category"></a>Verbindungskategorie  
Zeigt die Verbindungseigenschaften für die aktuelle Verbindung an. Die meisten Verbindungseigenschaften wurden beim Herstellen der Verbindung auf der Registerkarte **Verbindungseigenschaften** des Dialogfelds **Verbindung mit Server herstellen** ausgewählt.  
  
**Datenbank**  
Name der Datenbank, mit der zurzeit eine Verbindung besteht. Diese Einstellung können Sie über die Symbolleiste des SQL-Editors ändern.  
  
**SPID**  
Der Verbindung durch den Server zugewiesene Systemprozess-ID. Diese kann für die Verbindung nicht geändert werden.  
  
**Netzwerkprotokoll**  
Das für die [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] -Verbindung verwendete Netzwerkprotokoll. Zum Ändern dieser Größe stellen Sie mithilfe der gewünschten Verbindungseigenschaften die Verbindung erneut her.  
  
**Netzwerkpaketgröße**  
Bei der Kommunikation mit dem Server verwendete Netzwerkpaketgröße. Zum Ändern dieser Größe stellen Sie mithilfe der gewünschten Verbindungseigenschaften die Verbindung erneut her.  
  
**Verbindungstimeout**  
Die beim Herstellen einer Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] abzuwartende Zeitdauer (in Sekunden), bevor ein Timeout eintritt und eine Fehlermeldung an den Benutzer ausgegeben wird. Zum Ändern dieser Größe stellen Sie mithilfe der gewünschten Verbindungseigenschaften die Verbindung erneut her.  
  
**Ausführungstimeout**  
Zeitdauer (in Sekunden), die auf den Abschluss eines Tasks auf dem Server gewartet werden soll. Zum Ändern dieser Größe stellen Sie mithilfe der gewünschten Verbindungseigenschaften die Verbindung erneut her.  
  
**Verschlüsselt**  
Gibt an, ob die aktuelle Verbindung verschlüsselt ist. Zum Ändern dieser Größe stellen Sie mithilfe der gewünschten Verbindungseigenschaften die Verbindung erneut her.  
  
## <a name="product-category"></a>Product Category  
Zeigt die Produkteigenschaften für die aktuelle Verbindung an. Diese Eigenschaften beschreiben das Produkt, die Version, den Instanznamen und die Sortierung des Servers. Die Eigenschaften werden während der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] festgelegt.  
  
**Produktname**  
Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Produktname.  
  
**Produktversion**  
Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Produktversion.  
  
**Servername**  
Der Name des Computers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ausgeführt wird.  
  
**Der Instanzname.**  
Der Instanzname des Servers. Die Standardinstanz ist leer.  
  
**Sprache**  
Die Sprachversion des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Produkts.  
  
**Sortierung**  
Die Sortierung des Servers.  
  
## <a name="server-environment-category"></a>Serverumgebungskategorie  
Zeigt die Serverumgebungseigenschaften für die aktuelle Verbindung in Bezug auf die Serverhardware und das Betriebssystem an. Diese Eigenschaften können mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]nicht konfiguriert werden.  
  
**Computername**  
Der Name des Servercomputers, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ausgeführt wird.  
  
**Platform**  
Der Name und Hersteller des Betriebssystems sowie die CPU-Familie des Servers.  
  
**Betriebssystem**  
Die auf dem Server installierte Version von [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows.  
  
**Prozessoren**  
Anzahl der Prozessoren auf dem Server.  
  
**Arbeitsspeicher für das Betriebssystem**  
Der gesamte auf dem Server vorhandene physische Arbeitsspeicher in Megabytes.  
  
## <a name="see-also"></a>Siehe auch  
[Eigenschaftenseiten in SQL Server Management Studio](../../ssms/property-pages-in-sql-server-management-studio.md)  
[Verbindung mit Server herstellen &amp;#40;Seite Anmeldung im Datenbankmodul&amp;#41;](../../ssms/f1-help/connect-to-server-login-page-database-engine.md)  
  

