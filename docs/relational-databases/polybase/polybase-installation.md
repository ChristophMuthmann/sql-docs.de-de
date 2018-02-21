---
title: PolyBase-Installation | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase, installation
ms.assetid: 3a1e64be-9bfc-4408-accd-35990e1a6b52
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6a207474995eb36fbda4b446949bdf188f959edd
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="polybase-installation"></a>PolyBase-Installation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Besuchen Sie [SQL Server Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016), um eine Testversion von SQL Server zu installieren. 
  
## <a name="prerequisites"></a>Voraussetzungen  
  
-   Eine 64-Bit-Evaluierungs-Edition von SQL Server  
  
-   Microsoft .NET Framework 4.5.  
  
-   Oracle Java SE RunTime Environment (JRE), Version 7.51 oder höher (64-Bit) (Sowohl [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) als auch [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) funktionieren). Wechseln Sie zu [Java SE-Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Das Installationsprogramm schlägt fehl, wenn JRE nicht vorhanden ist.  
  
-   Mindestens erforderlicher Arbeitsspeicher: 4 GB  
  
-   Mindestfestplattenspeicher: 2 GB  
  
-   TCP/IP muss für Polybase aktiviert sein, damit es ordnungsgemäß funktioniert. TCP/IP ist standardmäßig in allen Editionen von SQL Server aktiviert. Davon ausgenommen sind nur die Editionen Developer und Express SQL Server. Damit Polybase auch in den Developer- und Express-Edition ordnungsgemäß funktionieren kann, müssen Sie die TCP/IP-Konnektivität aktivieren (Informationen dazu finden Sie unter [Enable or Disable a Server Network Protocol (Aktivieren und -Deaktivieren eines Server-Netzwerkprotokolls](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)).
  
 **Hinweise**  
  
 PolyBase kann nur auf einer SQL Server-Instanz pro Computer installiert werden.  
  
## <a name="single-node-or-polybase-scaleout-group"></a>Einzelknoten oder PolyBase-Gruppe mit horizontaler Skalierung
Planen Sie vor der Installation von PolyBase auf den SQL Server-Instanzen, ob Sie eine Einzelknoteninstallation oder eine PolyBase-Erweiterungsgruppe möchten. Vergewissern Sie sich für eine PolyBase-Gruppe mit horizontaler Skalierung, dass folgende Anforderungen erfüllt sind: 
- Alle Computer befinden sich in derselben Domäne.
- Sie verwenden während der Installation dasselbe Dienstkonto und Kennwort.
- Ihre SQL Server-Instanzen können über das Netzwerk miteinander kommunizieren.
- Alle SQL Server-Instanzen weisen die gleiche Version von SQL Server auf.

Sobald PolyBase entweder eigenständig oder in einer Gruppe mit horizontaler Skalierung installiert wurde, können Sie dies nicht mehr ändern. Sie müssen die Funktion deinstallieren und wieder neu installieren, um diese Einstellung zu ändern.

## <a name="install-using-the-installation-wizard"></a>Installieren mithilfe des Installations-Assistenten  
  
1.  Führen Sie das **SQL Server-Installationscenter**aus. Legen Sie die SQL Server-Installationsmedien ein, und doppelklicken Sie auf **Setup.exe**.  
  
2.  Klicken Sie auf **Installation**, dann auf **New Standalone SQL Server installation or add features**(Neue eigenständige SQL Server-Installation oder Hinzufügen von Funktionen).  
  
3.  Wählen Sie auf der Seite „Funktionsauswahl“ **PolyBase Query Service for External Data**(PolyBase-Abfragedienst für externe Daten).  
  
4.  Konfigurieren Sie auf der Seite „Serverkonfiguration“ die Dienste **SQL Server PolyBase-Modul** und SQL Server PolyBase-Datenverschiebungsdienst so, dass sie unter demselben Konto ausgeführt werden.  
  
    > **WICHTIG!** In einer PolyBase-Erweiterungsgruppe müssen die Dienste PolyBase-Modul und PolyBase-Datenverschiebung auf allen Knoten unter dem gleichen Domänenkonto ausgeführt werden.  
    > Weitere Informationen finden Sie unter „horizontales Hochskalieren von PolyBase“.  
  
5.  Wählen Sie auf der **PolyBase-Konfigurationsseite**eine der beiden Optionen aus. Weitere Informationen finden Sie unter [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md) (PolyBase-Erweiterungsgruppen).  
  
    -   Verwenden Sie die SQL Server-Instanz als eigenständige, für PolyBase aktivierte Instanz.  
  
         Wählen Sie diese Option aus, um die SQL Server-Instanz als eigenständigen Hauptknoten zu verwenden.  
  
    -   Verwenden Sie die SQL Server-Instanz als Teil der PolyBase-Erweiterungsgruppe.  Durch die Auswahl dieser Option wird die Firewall für eingehende Verbindungen mit den Diensten SQL Server-Datenbankmodul, SQL Server PolyBase-Modul und SQL Server PolyBase-Datenverschiebung sowie dem SQL-Browser geöffnet. Die Firewall wird für eingehende Verbindungen von anderen Knoten in einer PolyBase-Erweiterungsgruppe geöffnet.  
  
         Durch Auswahl dieser Option werden auch Firewallverbindungen des Microsoft Distributed Transaction Coordinator (MSDTC)-Diensts zugelassen und die MSDTC-Registrierungseinstellungen geändert.  
  
6.  Geben Sie auf der Seite **PolyBase-Konfiguration**den Portbereich mit mindestens sechs Ports an. SQL Server-Setup wird die ersten sechs verfügbaren Ports aus diesem Bereich zuweisen.  
  
##  <a name="installing"></a> Installieren mithilfe einer Eingabeaufforderung  
 Verwenden Sie die Werte in dieser Tabelle, um Installationsskripte zu erstellen. Die beiden Dienste **SQL Server PolyBase-Modul** und **SQL Server PolyBase-Datenverschiebung** müssen unter demselben Konto ausgeführt werden. In einer PolyBase-Gruppe mit horizontaler Skalierung müssen PolyBase-Dienste auf allen Knoten unter demselben Domänenkonto ausgeführt werden.  
  
|SQL Server-Komponente|Parameter und Werte|Description|  
|--------------------------|--------------------------|-----------------|  
|SQL Server-Setupsteuerung|**Erforderlich**<br /><br /> /FEATURES=PolyBase|Wählt die PolyBase-Funktion aus.|  
|SQL Server PolyBase-Modul|**Optional**<br /><br /> /PBENGSVCACCOUNT|Gibt das Konto für den Moduldienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|SQL Server PolyBase-Modul|**Optional**<br /><br /> /PBENGSVCPASSWORD|Gibt das Kennwort für das Moduldienstkonto an.|  
|SQL Server PolyBase-Modul|**Optional**<br /><br /> /PBENGSVCSTARTUPTYPE|Gibt den Startmodus für den PolyBase-Moduldienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|SQL Server PolyBase-Datenverschiebungsdienst|**Optional**<br /><br /> /PBDMSSVCACCOUNT|Gibt das Konto für den Datenverschiebungsdienst an. Der Standardwert ist **NT Authority\NETWORK SERVICE**.|  
|SQL Server PolyBase-Datenverschiebungsdienst|**Optional**<br /><br /> /PBDMSSVCPASSWORD|Gibt das Kennwort für das Datenverschiebungskonto an.|  
|SQL Server PolyBase-Datenverschiebungsdienst|**Optional**<br /><br /> /PBDMSSVCSTARTUPTYPE|Gibt den Startmodus für den Datenverschiebungsdienst an: Automatisch (Standard), Deaktiviert und Manuell.|  
|PolyBase|**Optional**<br /><br /> /PBSCALEOUT|Gibt an, ob die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe aus Computeknoten verwendet wird. <br />Unterstützte Werte: **True**, **False**|  
|PolyBase|**Optional**<br /><br /> /PBPORTRANGE|Gibt einen Portbereich für PolyBase-Dienste mit mindestens sechs Ports an. Beispiel:<br /><br /> `/PBPORTRANGE=16450-16460`|  
  
 **Beispiel**  
  
 Hier wird ein Beispiel-Setupskript gezeigt.  
  
```  
  
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,Polybase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
  
```  
  
## <a name="post-installation-notes"></a>Hinweise zur Installationsnachbereitung  
 PolyBase installiert drei Benutzerdatenbanken, und zwar DWConfiguration, DWDiagnostics und DWQueue.   Diese sind für die Verwendung von PolyBase gedacht und dürfen nicht verändert oder gelöscht werden.  
  
### <a name="how-to-confirm-installation"></a>So bestätigen Sie die Installation  
 Führen Sie den folgenden Befehl aus. Wenn PolyBase installiert ist, wird 1 zurückgegeben, andernfalls 0.  
  
```sql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
### <a name="firewall-rules"></a>Firewallregeln  
 SQL Server PolyBase-Setup erstellt die folgenden Firewallregeln auf dem Computer.  
  
-   SQL Server PolyBase – Datenbankmodul – \<SQL Server-Instanzname> (eingehendes TCP)  
  
-   SQL Server PolyBase – PolyBase-Dienste – \<SQL Server-Instanzname> (eingehendes TCP)  
  
-   SQL Server-PolyBase – SQL-Browser – (eingehendes UDP)  
  
 Wenn Sie auswählen, dass die SQL Server-Instanz als Teil einer PolyBase-Erweiterungsgruppe verwendet werden soll, werden diese Regeln bei der Installation aktiviert und die Firewall wird für eingehende Verbindungen mit den Diensten SQL Server-Datenbankmodul, SQL Server PolyBase-Modul und SQL Server PolyBase-Datenverschiebung sowie dem SQL-Browser geöffnet. Wenn der Firewalldienst des Computers während der Installation jedoch nicht ausgeführt wird, kann SQL Server-Setup diese Regeln nicht aktivieren. In diesem Fall müssen Sie den Firewalldienst des Computers starten und diese Regeln nach der Installation aktivieren.  
  
#### <a name="to-enable-the-firewall-rules"></a>So aktivieren Sie die Firewallregeln  
  
-   Öffnen Sie die **Systemsteuerung**.  
  
-   Klicken Sie auf **System und Sicherheit**, und klicken Sie auf **Windows-Firewall**.  
  
-   Klicken Sie auf **Erweiterte Einstellungen**und dann auf **Eingehende Regeln**.  
  
-   Klicken Sie mit der rechten Maustaste auf die deaktivierte Regel, und klicken Sie dann **Regel aktivieren**.  
  
### <a name="polybase-service-accounts"></a>PolyBase-Dienstkonten
Deinstallieren Sie die PolyBase-Funktion, und installieren Sie sie erneut, um die Dienstkonten für das PolyBase-Modul und die PolyBase-Datenverschiebungsdienste zu ändern.
   
## <a name="next-steps"></a>Nächste Schritte  
 Siehe [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md).  
  
  
