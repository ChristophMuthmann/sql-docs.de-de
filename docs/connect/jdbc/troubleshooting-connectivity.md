---
title: Behandlung von Verbindungsproblemen | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4adcdafe8b82a8b35dbb9b27c15749673a56bce2
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="troubleshooting-connectivity"></a>Behandlung von Verbindungsproblemen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] erfordert, dass TCP/IP installiert ist und ausgeführt, für die Kommunikation mit Ihrem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Sie können die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Konfigurations-Manager überprüfen, welche netzwerkbibliotheksprotokolle installiert sind.  
  
 Für Datenbankverbindungsfehler gibt es eine Vielzahl von Gründen, Sie können u. a. folgende Änderungen vornehmen:  
  
-   TCP/IP ist nicht aktiviert für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], oder die angegebene Server oder Port-Nummer ist falsch. Überprüfen Sie, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] auf dem angegebenen Server und Port mit TCP/IP lauscht. In diesem Fall wird eine ähnliche Ausnahme wie die folgende gemeldet: "Fehler bei der Anmeldung. Es konnte keine TCP/IP-Verbindung zum Host hergestellt werden." die auf einen der folgenden Fehler hinweist:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ist installiert, aber TCP/IP wurde nicht als Netzwerkprotokoll für installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mithilfe der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Netzwerkkonfiguration für [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], oder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Konfigurations-Manager für [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] und höher.  
  
    -   TCP/IP als installiert ist ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Protokoll, aber es nicht auf den in der JDBC-Verbindungs-URL angegebenen Port überwacht. Der Standardport ist 1433, aber [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] kann bei der Produktinstallation an einen beliebigen Port Lauschen konfiguriert werden. Stellen Sie sicher, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Port 1433 lauscht. Sollte der Port geändert worden sein, vergewissern Sie sich, dass der in der JDBC-Verbindungs-URL angegebene Port dem geänderten Port entspricht. Weitere Informationen zur JDBC-Verbindungs-URL finden Sie unter [Erstellen der Verbindungs-URL](../../connect/jdbc/building-the-connection-url.md).  
  
    -   Die Adresse des Computers, der in der JDBC-Verbindung angegeben wird URL verweist nicht auf einem Server, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] installiert und gestartet wird.  
  
    -   TCP/IP der Netzwerkverbindung zwischen dem Client und Server mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] funktioniert nicht. Sie können die TCP/IP-Konnektivität zu überprüfen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mit Telnet. Geben Sie an der Befehlszeile aus, z. B. `telnet 192.168.0.0 1433` 192.168.0.0 ist, in dem die Adresse des Computers, der ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und bei 1433 um den Port lauscht an. Wenn Sie eine Meldung erhalten, aus der hervorgeht, "Telnet kann keine Verbindung herstellen", TCP/IP hört nicht an diesem Port für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verbindungen. Verwenden Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Netzwerkkonfiguration für [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], oder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Konfigurations-Manager für [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] und höher können Sie sicherstellen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] für die Verwendung von TCP/IP-Port 1433 konfiguriert.  
  
    -   Der vom Server verwendete Port wurde in der Firewall nicht geöffnet. Dazu gehört der Port, der vom Server verwendet wird, oder optional der Port, der einer benannten Instanz des Servers zugeordnet ist.  
  
-   Der angegebene Datenbankname ist falsch. Stellen Sie sicher, dass Sie auf eine vorhandene Anmeldung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
-   Der Benutzername oder das Kennwort ist falsch. Vergewissern Sie sich, dass die richtigen Werte verwendet werden.  
  
-   Bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung der JDBC-Treiber erfordert, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] wird mit installiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung, die nicht der Standardeinstellung entspricht. Stellen Sie sicher, dass diese Option enthalten ist, beim Installieren oder der Instanz von konfigurieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Diagnostizieren von Problemen mit dem JDBC-Treiber](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [Herstellen einer Verbindung mit SQLServer mit der JDBC-Treiber](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  

