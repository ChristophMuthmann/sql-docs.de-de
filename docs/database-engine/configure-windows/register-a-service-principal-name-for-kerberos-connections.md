---
title: "Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 11/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
caps.latest.revision: "59"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4eba9f74d9eb5a46cfda7d5d28c1584c20fb22e7
ms.sourcegitcommit: ef1fa818beea435f58986af3379853dc28f5efd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Registrieren eines Dienstprinzipalnamens für Kerberos-Verbindungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Die Kerberos-Authentifizierung kann mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, wenn die beiden folgenden Bedingungen erfüllt sind:  
  
-   Der Client- und der Servercomputer müssen Teil der gleichen Windows-Domäne sein oder sich in vertrauenswürdigen Domänen befinden.  
  
-   Ein Dienstprinzipalname (Service Principal Name, SPN) muss in Active Directory registriert sein. Dieser Dienst nimmt die Rolle des Schlüsselverteilungscenters (KDC) in einer Windows-Domäne an. Der Dienstprinzipalname wird, wenn er registriert wurde, dem Windows-Konto zugeordnet, mit dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzendienst gestartet wurde. Wenn die Registrierung des Dienstprinzipalnamens nicht erfolgt oder dabei ein Fehler aufgetreten ist, kann die Windows-Sicherheitsschicht nicht das Konto bestimmen, das dem Dienstprinzipalname zugewiesen ist. Das bedeutet, die Kerberos-Authentifizierung wird nicht verwendet.  
  
    > [!NOTE]  
    >  Wenn der Server den Dienstprinzipalnamen nicht automatisch registrieren kann, muss der Dienstprinzipalname manuell registriert werden. Siehe [Manuelle SPN-Registrierung](#Manual).  
  
Durch Abfragen der dynamischen Verwaltungssicht sys.dm_exec_connections können Sie überprüfen, ob eine Verbindung Kerberos verwendet. Führen Sie die folgende Abfrage aus, und überprüfen Sie den Wert der Spalte auth_scheme, der "KERBEROS" lautet, wenn Kerberos aktiviert ist.  
  
```t-sql  
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;  
```  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos-Konfigurations-Manager für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ist ein Diagnosetool zur Behebung Kerberos-bezogener Verbindungsprobleme bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Microsoft Kerberos-Konfigurations-Manager für SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
##  <a name="Role"></a> Die Rolle des Dienstprinzipalnamens bei der Authentifizierung  
 Wenn eine Anwendung eine Verbindung öffnet und die Windows-Authentifizierung verwendet, übergibt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computernamen, -Instanznamen und optional einen SPN. Wenn die Verbindung einen Dienstprinzipalnamen übergibt, wird dieser ohne Änderungen verwendet.  
  
 Wenn die Verbindung keinen Dienstprinzipalnamen übergibt, wird ein Standard-Dienstprinzipalname basierend auf verwendetem Protokoll, Servernamen und Instanzennamen erstellt.  
  
 In beiden Szenarien wird der Dienstprinzipalname an das Schlüsselverteilungscenter gesendet, um ein Sicherheitstoken zum Authentifizieren der Verbindung abzurufen. Wenn kein Sicherheitstoken abgerufen werden kann, verwendet die Authentifizierung NTLM.  
  
 Ein Dienstprinzipalname (SPN, Service Principal Name) ist der Name, über den ein Client eine Instanz eines Diensts eindeutig identifiziert. Der Kerberos-Authentifizierungsdienst kann einen SPN zum Authentifizieren eines Diensts verwenden. Wenn ein Client eine Verbindung zu einem Dienst herstellen möchte, sucht er eine Instanz des Diensts, verfasst einen SPN für diese Instanz, stellt eine Verbindung zum Dienst her und übergibt den SPN zur Authentifizierung an den Dienst.  
  
> [!NOTE]  
>  Die Informationen in diesem Thema gelten auch für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurationen, die Clustering verwenden.  
  
 Die bevorzugte Methode für die Authentifizierung von Benutzern bei SQL Server ist Windows-Authentifizierung. Clients, die Windows-Authentifizierung verwenden, werden mit NTLM oder Kerberos authentifiziert. In einer Active Directory-Umgebung wird immer zuerst Kerberos-Authentifizierung ausgeführt. Die Kerberos-Authentifizierung ist für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Clients, die Named Pipes verwenden, nicht verfügbar.  
  
##  <a name="Permissions"></a> Berechtigungen  
 Beim Starten des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Diensts versucht dieser, den Dienstprinzipalnamen (Service Principal Name, SPN) zu registrieren. Wenn das Konto, das SQL Server startet, nicht über die Berechtigung zum Registrieren eines SPN in den Active Directory-Domänendiensten verfügt, schlägt dieser Aufruf fehl, und im Anwendungsereignisprotokoll sowie im SQL Server-Fehlerprotokoll wird eine Warnmeldung protokolliert. Um den SPN zu registrieren, muss [!INCLUDE[ssDE](../../includes/ssde-md.md)] unter einem integrierten Konto, z. B. einem lokalen System (nicht empfohlen) oder NETWORK SERVICE, oder unter einem Konto mit Berechtigung zum Registrieren eines SPN, z. B. einem Domänenadministratorkonto, ausgeführt werden. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter dem Betriebssystem  [!INCLUDE[win7](../../includes/win7-md.md)] oder  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] ausgeführt wird, können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit einem virtuellen Konto oder einem verwalteten Dienstkonto (MSA) ausführen. Sowohl virtuelle Konten als auch MSAs können einen SPN registrieren. Wird unter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kein solches Konto ausgeführt, wird der SPN beim Starten nicht registriert, sodass der Domänenadministrator den SPN manuell registrieren muss.  
  
> [!NOTE]  
>  Wenn die Windows-Domäne zum Ausführen auf einer geringeren Ebene als der [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Windows Server 2008 R2-Funktionsebene konfiguriert ist, verfügt das verwaltete Dienstkonto nicht über die notwendigen Berechtigungen zum Registrieren der SPNs für den [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Dienst. Ist die Kerberos-Authentifizierung erforderlich, muss der Domänenadministrator die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -SPNs über das verwaltete Dienstkonto manuell registrieren.  
  
 Der KB-Artikel [Verwenden der Kerberos-Authentifizierung in SQL Server](http://support.microsoft.com/kb/319723)enthält Informationen zum Gewähren von Lese- und Schreibberechtigungen für einen SPN für ein Nicht-Domänenadministratorkonto.  
  
 Weitere Informationen sind unter [Implementieren von eingeschränkter Kerberos-Delegierung mit SQL Server 2008](http://technet.microsoft.com/library/ee191523.aspx)verfügbar  
  
##  <a name="Formats"></a> SPN-Formate  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]wurde das SPN-Format geändert, um die Kerberos-Authentifizierung unter TCP/IP, Named Pipes und Shared Memory zu unterstützen. Die folgenden SPN-Formate für benannte und Standardinstanzen werden unterstützt.  
  
**Benannte Instanz**  
  
-   **MSSQLSvc/\<FQDN>:[\<Port> | \<Instanzname>]**, wobei:  
  
    -   **MSSQLSvc** der Dienst ist, der registriert wird.  
  
    -   **\<FQDN>** der vollqualifizierte Domänenname des Servers ist.  
  
    -   **\<Port>** die TCP-Portnummer ist.  
  
    -   **\<Instanzname>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Name der** -Instanz ist.  
  
**Standardinstanz**  
  
-   **MSSQLSvc/\<FQDN>:\<Port>** | **MSSQLSvc/\<FQDN>**, wobei:  
  
    -   **MSSQLSvc** der Dienst ist, der registriert wird.  
  
    -   **\<FQDN>** der vollqualifizierte Domänenname des Servers ist.  
  
    -   **\<Port>** die TCP-Portnummer ist.  
  
    > [!NOTE]
    > Beim neuen SPN-Format ist keine Portnummer erforderlich. Somit können Server mit mehreren Ports oder Protokolle ohne Portnummern Kerberos-Authentifizierung verwenden.  
   
|||  
|-|-|  
|MSSQLSvc/\<FQDN>:<port>|Der vom Anbieter erstellte Standard-SPN, wenn TCP verwendet wird. \<Port> ist eine TCP-Portnummer.|  
|MSSQLSvc/\<FQDN>|Der vom Anbieter erstellte Standard-SPN für eine Standardinstanz, wenn ein anderes Protokoll als TCP verwendet wird. \<FQDN> ist ein vollqualifizierter Domänenname.|  
|MSSQLSvc/\<FQDN>:\<Instanzname>|Der vom Anbieter erstellte Standard-SPN für eine benannte Instanz, wenn ein anderes Protokoll als TCP verwendet wird. \<Instanzname> ist der Name einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz.|  

> [!NOTE]  
> Bei TCP/IP-Verbindungen, bei denen der TCP-Port im SPN enthalten ist, muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] das TCP-Protokoll für einen Benutzer aktivieren, um mithilfe der Kerberos-Authentifizierung eine Verbindung herzustellen. 

##  <a name="Auto"></a> Automatische SPN-Registrierung  
 Beim Starten einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] versucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , den SPN für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst zu registrieren. Wird die Instanz beendet, versucht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die Registrierung des SPN wieder aufzuheben. Bei TCP/IP-Verbindungen wird der SPN im folgenden Format registriert: *MSSQLSvc/\<FQDN>*:*\<tcpport>*. Sowohl benannte Instanzen als auch die Standardinstanz werden als *MSSQLSvc* registriert, wobei der *\<tcpport>*-Wert zur Unterscheidung der Instanzen dient.  
  
 Bei anderen Verbindungen, die Kerberos unterstützen, wird der SPN im Format *MSSQLSvc/\<FQDN>*/*\<Instanzname>* für eine benannte Instanz registriert. Die Standardinstanz wird im folgenden Format registriert: *MSSQLSvc/\<FQDN>*.  
  
 Die Registrierung bzw. die Aufhebung der Registrierung eines SPN muss möglicherweise manuell durchgeführt werden, wenn der Dienst nicht über die Berechtigungen für diese Aktionen verfügt.  
  
##  <a name="Manual"></a> Manuelle SPN-Registrierung  
Um den SPN manuell zu registrieren, muss der Administrator das Setspn.exe-Tool verwenden, das mit den Microsoft [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] -Supporttools geliefert wird. Weitere Informationen finden Sie im KB-Artikel [Supporttools in Windows Server 2003 Service Pack 1](http://support.microsoft.com/kb/892777) .  
  
Setspn.exe ist ein Befehlszeilentool, mit dem Sie die SPN-Verzeichniseigenschaft lesen, ändern und löschen können. Mit diesem Tool können Sie auch die aktuellen SPN anzeigen, die Standard-SPN des Kontos zurücksetzen und zusätzliche SPN hinzufügen oder löschen.  
  
Das folgende Beispiel veranschaulicht die Syntax, die zur manuellen Registrierung eines SPN für eine TCP/IP-Verbindung unter Verwendung eines Domänenbenutzerkontos zu verwenden ist:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```  
  
> [!NOTE]
> Wenn bereits ein SPN vorhanden ist, muss er gelöscht werden, um ihn erneut registrieren zu können. Verwenden Sie dafür den `setspn` -Befehl und den `-D` -Schalter. In den folgenden Beispielen wird veranschaulicht, wie Sie einen neuen instanzbasierten SPN manuell registrieren können. Verwenden Sie für eine Standardinstanz mit einem Domänenbenutzerkonto Folgendes:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
Verwenden Sie für eine benannte Instanz Folgendes:  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com/instancename redmond\accountname  
```  
  
##  <a name="Client"></a> Clientverbindungen  
 Clienttreiber unterstützen vom Benutzer angegebene SPN. Wenn jedoch kein SPN angegeben wurde, wird er auf der Grundlage des Clientverbindungstyps automatisch erstellt. Bei einer TCP-Verbindung wird ein SPN im Format *MSSQLSvc*/*FQDN*:[*port*] sowohl für benannte als auch für Standardinstanzen verwendet.  
  
Für Verbindungen mit Named Pipes und gemeinsam genutzten Speicherbereichen wird für eine benannte Instanz ein SPN im Format *MSSQLSvc/\<FQDN>:\<Instanzname>* und für die Standardinstanz *MSSQLSvc/\<FQDN>* verwendet.  
  
 **Verwenden eines Dienstkontos als SPN**  
  
Dienstkonten können als SPN verwendet werden. Sie werden durch das Verbindungsattribut für die Kerberos-Authentifizierung angegeben und liegen in den folgenden Formaten vor:  
  
-   **username@domain** oder **Domäne\Benutzername** für ein Domänenbenutzerkonto  
  
-   **Computer$@domain** oder **Host\FQDN** für ein Computerdomänenkonto, z.B. Lokales System oder NETWORK SERVICES.  
  
Um die Authentifizierungsmethode einer Verbindung zu bestimmen, führen Sie die folgende Abfrage aus.  
  
```t-sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
##  <a name="Defaults"></a> Authentifizierungsstandardwerte  
 In der folgenden Tabelle werden die Authentifizierungsstandardwerte beschrieben, die auf Grundlage von SPN-Registrierungsszenarios verwendet werden.  
  
|Szenario|Authentifizierungsmethode|  
|--------------|---------------------------|  
|Der SPN ist dem richtigen Domänenkonto, virtuellen Konto, MSA oder integrierten Konto zugeordnet. Beispiel: Lokales System oder NETWORK SERVICE.|Lokale Verbindungen verwenden NTLM, Remoteverbindungen verwenden Kerberos.|  
|Der SPN entspricht dem richtigen Domänenkonto, virtuellen Konto, MSA oder integrierten Konto.|Lokale Verbindungen verwenden NTLM, Remoteverbindungen verwenden Kerberos.|  
|Der SPN ist einem falschen Domänenkonto, virtuellen Konto, MSA oder integrierten Konto zugeordnet.|Die Authentifizierung schlägt fehl.|  
|Die SPN-Suche schlägt fehl, oder der SPN ist nicht dem richtigen Domänenkonto, virtuellen Konto, MSA oder integrierten Konto zugeordnet bzw. entspricht nicht dem richtigen Domänenkonto, virtuellen Konto, MSA oder integrierten Konto.|Lokale Verbindungen und Remoteverbindungen verwenden NTLM.|  
  
> [!NOTE]  
> "Richtig" bedeutet in diesem Fall, dass es sich bei dem Konto, das dem registrierten SPN zugeordnet ist, um das Konto handelt, unter dem der SQL Server-Dienst ausgeführt wird.  
  
##  <a name="Comments"></a> Kommentare  
 Die dedizierte Administratorverbindung (Dedicated Administrator Connection, DAC) verwendet einen auf Instanznamen basierenden SPN. Die Kerberos-Authentifizierung kann mit einer DAC verwendet werden, wenn dieser SPN erfolgreich registriert wurde. Alternativ kann ein Benutzer den Kontonamen als SPN festlegen.  
  
 Wenn die SPN-Registrierung beim Starten fehlschlägt, wird dieser Fehler im Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgezeichnet, und der Startvorgang wird fortgesetzt.  
  
 Wenn die Aufhebung der SPN-Registrierung beim Herunterfahren fehlschlägt, wird dieser Fehler im Fehlerprotokoll von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgezeichnet, und das Herunterfahren wird fortgesetzt.  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützung von Dienstprinzipalnamen &#40;SPN&#41; in Clientverbindungen](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)   
 [Dienstprinzipalnamen (SPN) in Clientverbindungen (OLE DB)](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)   
 [Dienstprinzipalnamen (SPN) in Clientverbindungen (ODBC)](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)   
 [SQL Server Native Client-Funktionen](../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Behandeln von Problemen mit der Kerberos-Authentifizierung in einer Reporting Services-Umgebung](http://technet.microsoft.com/library/ff679930.aspx)  
  
  
