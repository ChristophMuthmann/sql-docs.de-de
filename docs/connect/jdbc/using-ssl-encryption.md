---
title: "SSL-Verschlüsselung mit | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7923995b392dff8c80f1ee6ae3946e421dc46331
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-ssl-encryption"></a>Verwenden der SSL-Verschlüsselung
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Secure Sockets Layer (SSL)-Verschlüsselung kann verschlüsselte Datenübertragung über das Netzwerk zwischen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und einer Clientanwendung.  
  
 Secure Sockets Layer (SSL) ist ein Protokoll zum Einrichten eines sicheren Kommunikationskanals, um das Abfangen von kritischen oder vertraulichen Informationen im Netzwerk und bei anderen Internetkommunikationen zu verhindern. Durch SSL können der Client und der Server die Identität des anderen authentifizieren. Nach dem Authentifizieren der Teilnehmer stellt SSL verschlüsselte Verbindungen zwischen ihnen bereit, damit die Nachrichten sicher übertragen werden können.  
  
 Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] stellt eine Infrastruktur zum Aktivieren und deaktivieren die Verschlüsselung für eine bestimmte Verbindung basierend auf der benutzerdefinierten Verbindungseigenschaften und der Server und Client. Der Benutzer kann den Speicherort des Zertifikatspeichers und das Kennwort sowie einen Hostnamen zum Überprüfen des Zertifikats angeben und festlegen, wann der Verbindungskanal verschlüsselt werden soll.  
  
 Das Aktivieren der SSL-Verschlüsselung erhöht die Sicherheit von Daten, die netzwerkübergreifend zwischen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und Anwendungen übertragen werden. Durch das Aktivieren der Verschlüsselung kommt es jedoch zu Leistungseinbußen.  
  
 Die Themen in diesem Abschnitt wird beschrieben, wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] -Version unterstützt SSL-Verschlüsselung, einschließlich neue Verbindungseigenschaften und Konfigurieren des vertrauensspeichers auf Clientseite.  
  
> [!NOTE]  
>  Die **HostNameInCertificate** Connection-Eigenschaft wird empfohlen, um ein SSL-Zertifikat zu überprüfen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
|Thema|Description|  
|-----------|-----------------|  
|[Grundlegendes zur SSL-Unterstützung](../../connect/jdbc/understanding-ssl-support.md)|Beschreibt, wie die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] SSL-Verschlüsselung unterstützt.|  
|[Herstellen einer Verbindung mit SSL-Verschlüsselung](../../connect/jdbc/connecting-with-ssl-encryption.md)|Beschreibt die Vorgehensweise beim Herstellen einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mithilfe der neuen SSL-spezifischen Verbindungseigenschaften.|  
|[Konfigurieren des Clients für SSL-Verschlüsselung](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)|Beschreibt das Konfigurieren des Standardvertrauensspeichers auf Clientseite und das Importieren eines privaten Zertifikats im Vertrauensspeicher des Clientcomputers.|  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern von JDBC-Treiberanwendungen](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  

