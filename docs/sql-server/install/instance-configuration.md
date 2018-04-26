---
title: Hilfe zum Installations-Assistenten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 2017-04-21
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: install
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
caps.latest.revision: 62
ms.author: mikeray
manager: craigg
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 4ef290dacb4863511444c1267ce98a28a9e80926
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="installation-wizard-help"></a>Hilfe zum Installations-Assistenten
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In diesem Artikel werden einige der Konfigurationsseiten im Installations-Assistenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beschrieben. 

## <a name="instance-configuration"></a>Instanzkonfiguration
Verwenden Sie die Seite **Instanzkonfiguration** des Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , um anzugeben, ob eine Standardinstanz oder eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]erstellt werden soll. Wenn noch keine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Server installiert wurde, wird eine Standardinstanz erstellt, es sei denn Sie geben eine benannte Instanz an.  
  
Jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz besteht aus einem Satz von Diensten mit bestimmten Einstellungen für Sortierungen und andere Optionen. Verzeichnisstruktur, Registrierungsstruktur und Dienstnamen spiegeln den Instanznamen und die von Ihnen bei der Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angegebene Instanz-ID wider.  
  
 Bei der Instanz kann es sich um eine Standardinstanz oder um eine benannte Instanz handeln. Der Name der Standardinstanz lautet MSSQLSERVER. Es ist kein Client erforderlich, um den Instanznamen zur Herstellung einer Verbindung anzugeben. Eine benannte Instanz wird vom Benutzer während des Setups festgelegt. Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als benannte Instanz installieren, ohne zuvor die Standardinstanz zu installieren. Es kann jeweils nur eine Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], unabhängig von der Version, als Standardinstanz fungieren.  
  
> [!NOTE]  
> Bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep können Sie den Instanznamen angeben, wenn Sie auf der Seite **Instanzkonfiguration** eine vorbereitete Instanz abschließen. Sie können die vorbereitete Instanz, die Sie abschließen, als Standardinstanz konfigurieren, wenn sich auf dem Computer keine vorhandene Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] befindet.  
  
### <a name="multiple-instances"></a>Mehrere Instanzen  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem einzelnen Server oder Prozessor, es kann jedoch nur eine einzige Instanz als Standardinstanz fungieren. Alle anderen müssen benannte Instanzen sein. Auf einem Computer können mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gleichzeitig ausgeführt werden, und jede Instanz wird unabhängig von den anderen Instanzen ausgeführt.  
  
 Weitere Informationen finden Sie unter [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
### <a name="options"></a>Tastatur  
 Nur Failoverclusterinstanzen: Geben Sie den Netzwerknamen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusters an. Anhand dieses Namens wird die Failoverclusterinstanz im Netzwerk identifiziert.  
  
 Standardinstanz oder benannte Instanz: Bei der Entscheidung der Frage, ob eine Standardinstanz oder eine benannte Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert werden soll, müssen folgende Informationen beachtet werden:  
  
-   Wenn Sie eine einzelne Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Datenbankserver installieren möchten, sollte dies eine Standardinstanz sein.  
  
-   Verwenden Sie eine benannte Instanz , wenn Sie mehrere Instanzen auf dem gleichen Computer verwenden möchten. Ein Server kann nur als Host für eine einzelne Standardinstanz dienen.  
  
-   Jede Anwendung, die [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] installiert, sollte die Installation als benannte Instanz vornehmen. Dadurch werden die Konflikte für den Fall minimiert, dass mehrere Anwendungen auf demselben Computer installiert werden.  
  
 **Standardinstanz**  
 Wählen Sie diese Option aus, um eine Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu installieren. Ein Computer kann nur als Host für eine Standardinstanz dienen, alle anderen Instanzen müssen benannt sein. Wenn eine Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist, ist es jedoch möglich, demselben Computer eine Standardinstanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] hinzufügen.  
  
 **Benannte Instanz**  
 Wählen Sie diese Option aus, um eine neue benannte Instanz zu erstellen. Beachten Sie beim Benennen einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Folgendes:  
  
-   Bei Instanznamen wird die Groß-/Kleinschreibung nicht berücksichtigt.  
  
-   Instanznamen dürfen nicht mit einem Unterstrich (_) beginnen oder enden.  
  
-   Instanznamen dürfen keine Begriffe wie "Standard" oder andere reservierte Schlüsselwörter enthalten. Wenn in einem Instanznamen ein reserviertes Schlüsselwort verwendet wird, tritt ein Setupfehler auf. Weitere Informationen finden Sie unter [Reservierte Schlüsselwörter &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
-   Wenn Sie MSSQLServer als Instanznamen angeben, wird eine Standardinstanz erstellt.  
  
-   Eine Installation von [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] wird immer als benannte Instanz von '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]' installiert. Sie können keinen anderen Instanznamen für diese Funktionsrolle angeben.  
  
-   Instanznamen können maximal 16 Zeichen enthalten.  
  
-   Das erste Zeichen eines Instanznamens muss ein Buchstabe sein. Akzeptable Buchstaben sind diejenigen, die durch Unicode Standard 2.0 definiert werden. Dazu gehören die lateinischen Zeichen a-z, A-Z sowie Buchstaben aus anderen Sprachen.  
  
-   Bei den anderen Zeichen kann es sich um Buchstaben des Unicode-Standards 2.0, Dezimalzeichen aus dem lateinischen Grundalphabet oder anderen nationalen Schriften, das Dollarzeichen ($) oder einen Unterstrich (_) handeln.  
  
-   Eingebettete Leerzeichen und sonstige Sonderzeichen sind in Instanznamen nicht zugelassen. Umgekehrte Schrägstriche (\\), Kommas (,), Doppelpunkte (:), Strichpunkte (;), einfache Anführungszeichen ('), kaufmännische Und-Zeichen (&), Bindestriche (-) und das At-Zeichen (@) sind ebenfalls nicht zulässig.  
  
     In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanznamen können nur gültige Zeichen der aktuellen Windows-Codepage verwendet werden. Wenn ein nicht unterstütztes Unicode-Zeichen verwendet wird, tritt ein Setupfehler auf.  
  
 **Erkannte Instanzen und Funktionen**  
 Zeigt eine Liste der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen und Komponenten an, die auf dem Computer installiert sind, auf dem das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup ausgeführt wird.  
  
 **Instanz-ID** – Standardmäßig wird der Instanzname als Instanz-ID verwendet. Das Ziel ist dabei, Installationsverzeichnisse und Registrierungsschlüssel für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu identifizieren. Dies ist der Fall für Standardinstanzen und benannte Instanzen. Bei einer Standardinstanz lauten Instanzname und Instanz-ID MSSQLSERVER. Um eine nicht standardmäßige Instanz-ID zu verwenden, geben Sie sie im Feld **Instanz-ID** an.  
  
> [!IMPORTANT]  
>  Bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep handelt es sich bei der auf dieser Seite angezeigten Instanz-ID um die Instanz-ID, die Sie während des Schritts Image vorbereiten des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep-Prozesses angegeben haben. Sie sind nicht in der Lage, während des Schritts Image abschließen eine andere Instanz-ID anzugeben.  
  
> [!NOTE]  
>  Instanz-IDs, die mit einem Unterstrich (_) beginnen oder das Nummernzeichen (#) oder Dollarzeichen ($) enthalten, werden nicht unterstützt.  
  
 Weitere Informationen zu Verzeichnissen, Dateispeicherorten und Namen für Instanz-IDs finden Sie unter [Dateispeicherorte für Standard- und benannte Instanzen von SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Alle Komponenten einer gegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden als Einheit verwaltet. Alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Service Packs und Updates werden für jede Komponente einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]übernommen.  
  
 Alle Komponenten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die denselben Instanznamen verwenden, müssen die folgenden Kriterien erfüllen:  
  
-   **Gleiche Version**  
  
-   **Gleiche Edition**  
  
-   **Gleiche Spracheinstellungen**  
  
-   **Gleicher gruppierter Status**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ist nicht clusterabhängig.  
  
-   **Gleiches Betriebssystem**  
  
## <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services-Konfiguration - Kontobereitstellung
  Verwenden Sie diese Seite zum Einrichten des Servermodus und zum Zuweisen von administrativen Berechtigungen an Benutzer oder Dienste, die uneingeschränkten Zugriff auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] benötigen. Während des Setups wird die lokale Windows-Gruppe „BUILTIN\Administrators“ der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Serveradministratorrolle der Instanz, die Sie installieren, nicht automatisch hinzugefügt. Wenn Sie der Serveradministratorrolle die lokale Gruppe "Administratoren" hinzufügen möchten, müssen Sie diese Gruppe explizit angeben.  
  
 Bei der Installation von [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] sollten Sie Administratoren von SharePoint-Farmen oder -Diensten, die für eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Serverbereitstellung in einer [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]-Farm zuständig sind, Administratorrechte gewähren.  
  
### <a name="options"></a>Tastatur  
 **Servermodus** - Der Servermodus gibt den Typ von Analysis Services-Datenbanken an, die auf dem Server bereitgestellt werden können. Servermodi werden während des Setups bestimmt und können später nicht mehr geändert werden. Die einzelnen Modi schließen einander aus. Das bedeutet, dass Sie zwei Instanzen von Analysis Services benötigen, die jeweils für einen anderen Modus konfiguriert sind, um beide klassische Lösungen - das OLAP- und das tabellarische Modell - zu unterstützen.  
  
 **Administratoren angeben** – Sie müssen mindestens einen Serveradministrator für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz angeben. Die Benutzer oder die Gruppen, die Sie angeben, werden Mitglieder der Serveradministratorrolle der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanz, die Sie installieren. Diese müssen Windows-Domänenbenutzerkonten in der gleichen Domäne wie der Computer sein, auf dem Sie die Software installieren.  
  
> [!NOTE]  
>  Die Benutzerkontensteuerung (User Account Control, UAC) ist eine Windows-Sicherheitsfunktion, bei der ein Administrator administrative Aktionen oder Anwendungen einzeln genehmigen muss, bevor diese ausgeführt werden können. Da die Benutzerkontensteuerung in den Standardeinstellungen aktiviert ist, werden Sie aufgefordert, einzelne Vorgänge, für die erhöhte Berechtigungen erforderlich sind, zu genehmigen. Sie können die Benutzerkontensteuerung konfigurieren, um das Standardverhalten zu ändern, oder sie für bestimmte Programme anpassen. Weitere Informationen über die Benutzerkontensteuerung und deren Konfiguration finden Sie unter [Schritt-für-Schritt-Anleitung zur Benutzerkontensteuerung](http://go.microsoft.com/fwlink/?linkid=196350) und [Benutzerkontensteuerung (Wikipedia)](http://go.microsoft.com/fwlink/?linkid=196351).  
  
### <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Configure Service Accounts &#40;Analysis Services&#41; (Konfigurieren von Dienstkonten und Analysis Services)](../../analysis-services/instances/configure-service-accounts-analysis-services.md) [Configure Windows Service Accounts and Permissions (Konfigurieren von Windows-Dienstkonten und -Berechtigungen)](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Konfigurationseigenschaften von Analysis Services – Datenverzeichnisse
  Die in der folgenden Tabelle angegebenen Standardverzeichnisse können beim Setup von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vom Benutzer konfiguriert werden: Die Berechtigung zum Zugriff auf diese Dateien wird den lokalen Administratoren und Mitgliedern der Sicherheitsgruppe SQLServerMSASUser $\<instance> gewährt, die während des Setups erstellt und bereitgestellt wird.  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
  
|Description|Standardverzeichnis|Empfehlungen|  
|-----------------|-----------------------|---------------------|  
|Datenstammverzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data\ |Stellen Sie sicher, dass der Ordner \Programme\Microsoft SQL Server\ durch entsprechend eingeschränkte Berechtigungen geschützt wird. Die Leistung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist in vielen Konfigurationen von der Leistung des Speichers abhängig, in dem sich das Datenverzeichnis befindet. Platzieren Sie dieses Verzeichnis im Speicher mit der höchsten Leistung, der mit dem System verknüpft ist. Stellen Sie für Failoverclusterinstallationen sicher, dass Datenverzeichnisse auf dem freigegebenen Datenträger platziert werden.|  
|Protokolldateiverzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log\ |Dies ist das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Protokolldateien, das auch das FlightRecorder-Protokoll enthält. Wenn Sie die Dauer von Flight Recorder erhöhen, stellen Sie sicher, dass für das Protokollverzeichnis genügend Speicherplatz zur Verfügung steht.|  
|Temporäres Verzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp\ |Platzieren Sie das temporäre Verzeichnis in einem leistungsstarken Speichersubsystem.|  
|Sicherungsverzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup\ |Dies ist das Verzeichnis für Standardsicherungsdateien von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Bei einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation werden in diesem Verzeichnis zudem die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datendateien des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts zwischengespeichert.<br /><br /> Stellen Sie sicher, dass zur Vermeidung von Datenverlusten entsprechende Berechtigungen festgelegt wurden und die Benutzergruppe für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst über die erforderlichen Berechtigungen zum Schreiben im Sicherungsverzeichnis verfügt. Die Verwendung eines zugeordneten Laufwerks für Sicherungsverzeichnisse wird nicht unterstützt.|  
  
### <a name="notes"></a>Hinweise  
  
-   Auf einer SharePoint-Farm bereitgestellte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanzen speichern Anwendungsdateien, Datendateien und Eigenschaften in Inhaltsdatenbanken und Dienstanwendungsdatenbanken.  
  
-   Wenn Sie Funktionen zu einer vorhandenen Installation hinzufügen, können Sie den Speicherort einer vorher installierten Funktion nicht ändern und auch keinen Speicherort für eine neue Funktion angeben.  

-   Möglicherweise müssen Sie Softwareanwendungen wie beispielsweise Viren- und Spywarescanner so konfigurieren, dass SQL Server-Ordner und -Dateitypen ausgeschlossen werden. Weitere Informationen finden Sie im folgenden Artikel: [Gewusst wie: Auswählen, wie Antivirussoftware auf Computern ausgeführt werden soll, auf denen SQL Server ausgeführt wird](https://support.microsoft.com/kb/309422).
  
-   Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genutzt werden. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] - und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Komponenten in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollten ebenfalls in separaten Verzeichnissen installiert werden.  
  
-   Programmdateien und Datendateien können in den folgenden Situationen nicht installiert werden:  
  
    -   Auf einem Wechseldatenträger  
  
    -   In einem Dateisystem, in dem die Komprimierung verwendet wird  
  
    -   In einem Verzeichnis, in dem sich Systemdateien befinden  
  
### <a name="see-also"></a>Weitere Informationen finden Sie unter  
 Weitere Informationen zu Verzeichnissen, Dateispeicherorten und Namen für Instanz-IDs finden Sie unter [Dateispeicherorte für Standard- und benannte Instanzen von SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
## <a name="database-engine-configuration---data-directories"></a>Konfiguration des Datenbankmodells - Datenverzeichnisse
  Verwenden Sie diese Seite, um den Installationspfad für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]-Programm und die Datendateien anzugeben. Auf Grundlage des Typs der Installation schließt der unterstützte Speicher möglicherweise einen lokalen Datenträger, freigegebenen Speicher oder SMB-Dateiserver ein.  
  
 Um eine SMB-Dateifreigabe als Verzeichnis anzugeben, müssen Sie den unterstützten UNC-Pfad manuell eingeben. Das Navigieren zu einer SMB-Dateifreigabe wird nicht unterstützt. Das folgende Format ist ein unterstütztes UNC-Pfadformat einer SMB-Dateifreigabe: \\\\Servername\ShareName\\\...  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Eigenständige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 In der folgenden Tabelle sind die unterstützten Speichertypen und die Standardverzeichnisse für eine eigenständige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgeführt, die während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setups vom Benutzer konfigurierbar sind.  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
  
|Description|Unterstützter Speichertyp|Standardverzeichnis|Empfehlungen|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Datenstammverzeichnis|Lokaler Datenträger, SMB-Dateiserver, freigegebener Speicher* |C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup konfiguriert Zugriffssteuerungslisten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verzeichnisse und unterbricht während der Konfiguration die Vererbung.|  
|Benutzerdatenbankverzeichnis|Lokaler Datenträger, SMB-Dateiserver, freigegebener Speicher*|C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data |Welche Vorgehensweise für Benutzerdatenverzeichnisse empfohlen wird, hängt von der Arbeitsauslastung und den Leistungsanforderungen ab.|  
|Benutzerdatenbank-Protokollverzeichnis|Lokaler Datenträger, SMB-Dateiserver, freigegebener Speicher*|C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Stellen Sie sicher, dass ausreichend Speicherplatz für das Protokollverzeichnis verfügbar ist.|  
|Sicherungsverzeichnis|Lokaler Datenträger, SMB-Dateiserver, freigegebener Speicher*|C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup|Legen Sie zur Vermeidung von Datenverlusten entsprechende Berechtigungen fest, und stellen Sie sicher, dass das Benutzerkonto für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst über die erforderlichen Berechtigungen zum Schreiben im Sicherungsverzeichnis verfügt. Die Verwendung eines zugeordneten Laufwerks für Sicherungsverzeichnisse wird nicht unterstützt.|  
  
 *Obwohl freigegebene Datenträger unterstützt werden, wird diese Vorgehensweise für eine eigenständige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht empfohlen.  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Failoverclusterinstanz  
 In der folgenden Tabelle sind die unterstützten Speichertypen und die Standardverzeichnisse für eine Failoverclusterinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgeführt, die während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setups vom Benutzer konfigurierbar sind.  
  
|Description|Unterstützter Speichertyp|Standardverzeichnis|Empfehlungen|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Datenstammverzeichnis|Freigegebener Speicher, SMB-Dateiserver|\<Laufwerk:>\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Tipp: Wenn "Freigegebener Datenträger" auf der Seite **Datenträgerauswahl für Cluster** ausgewählt wurde, ist der Standard der erste freigegebene Datenträger. Dieses Feld ist standardmäßig leer, wenn keine Auswahl auf der Seite **Datenträgerauswahl für Cluster** getroffen wurde.|Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup konfiguriert Zugriffssteuerungslisten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verzeichnisse und unterbricht während der Konfiguration die Vererbung.|  
|Benutzerdatenbankverzeichnis|Freigegebener Speicher, SMB-Dateiserver|\<Laufwerk:>Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Tipp: Wenn "Freigegebener Datenträger" auf der Seite **Datenträgerauswahl für Cluster** ausgewählt wurde, ist der Standard der erste freigegebene Datenträger. Dieses Feld ist standardmäßig leer, wenn keine Auswahl auf der Seite **Datenträgerauswahl für Cluster** getroffen wurde.|Welche Vorgehensweise für Benutzerdatenverzeichnisse empfohlen wird, hängt von der Arbeitsauslastung und den Leistungsanforderungen ab.|  
|Benutzerdatenbank-Protokollverzeichnis|Freigegebener Speicher, SMB-Dateiserver|\<Laufwerk:>\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Tipp: Wenn "Freigegebener Datenträger" auf der Seite **Datenträgerauswahl für Cluster** ausgewählt wurde, ist der Standard der erste freigegebene Datenträger. Dieses Feld ist standardmäßig leer, wenn keine Auswahl auf der Seite **Datenträgerauswahl für Cluster** getroffen wurde.|Stellen Sie sicher, dass ausreichend Speicherplatz für das Protokollverzeichnis verfügbar ist.|  
|Sicherungsverzeichnis|Lokaler Datenträger, freigegebener Speicher, SMB-Dateiserver|\<Laufwerk: >\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup<br /><br /> Tipp: Wenn "Freigegebener Datenträger" auf der Seite **Datenträgerauswahl für Cluster** ausgewählt wurde, ist der Standard der erste freigegebene Datenträger. Dieses Feld ist standardmäßig leer, wenn keine Auswahl auf der Seite **Datenträgerauswahl für Cluster** getroffen wurde.|Legen Sie zur Vermeidung von Datenverlusten entsprechende Berechtigungen fest, und stellen Sie sicher, dass das Benutzerkonto für den SQL Server-Dienst über die erforderlichen Berechtigungen zum Schreiben im Sicherungsverzeichnis verfügt. Die Verwendung eines zugeordneten Laufwerks für Sicherungsverzeichnisse wird nicht unterstützt.|  
  
### <a name="security-considerations"></a>Überlegungen zur Sicherheit  
 Das Setup konfiguriert Zugriffssteuerungslisten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verzeichnisse und unterbricht während der Konfiguration die Vererbung.  
  
 Die folgenden Empfehlungen gelten für den SMB-Dateiserver:  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto muss ein Domänenkonto sein, wenn ein SMB-Dateiserver verwendet wird.  
  
-   Das Konto, das verwendet wurde, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu installieren, muss über FULL CONTROL NTFS-Berechtigungen für den als Datenverzeichnis verwendeten SMB-Dateifreigabeordner verfügen.  
  
-   Dem Konto, das für die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, müssen SeSecurityPrivilege-Berechtigungen auf dem SMB-Dateiserver zugewiesen werden. Diese Berechtigung weisen Sie zu, indem Sie die Konsole "Lokale Sicherheitsrichtlinie" auf dem Dateiserver verwenden, um der Richtlinie zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verwalten von Überwachungs- und Sicherheitsprotokollen **das** -Setupkonto hinzuzufügen. Diese Einstellung ist im Abschnitt **Zuweisen von Benutzerrechten** unter **Lokale Richtlinien** in der Konsole **Lokale Sicherheitsrichtlinie** verfügbar.  
  
### <a name="notes"></a>Hinweise  
  
-   Wenn Sie Funktionen zu einer vorhandenen Installation hinzufügen, können Sie den Speicherort einer vorher installierten Funktion nicht ändern und auch keinen Speicherort für eine neue Funktion angeben.  
  
-   Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genutzt werden. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] - und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Komponenten in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollten ebenfalls in separaten Verzeichnissen installiert werden.  
  
-   Programmdateien und Datendateien können in den folgenden Situationen nicht installiert werden:  
  
    -   Auf einem Wechseldatenträger  
  
    -   In einem Dateisystem, in dem die Komprimierung verwendet wird  
  
    -   In einem Verzeichnis, in dem sich Systemdateien befinden  
  
    -   Auf einem zugeordneten Netzlaufwerk auf einer Failoverclusterinstanz  
  
### <a name="see-also"></a>Weitere Informationen finden Sie unter  
### <a name="analysis-services-configuration---data-directories"></a>Konfigurationseigenschaften von Analysis Services – Datenverzeichnisse
  Die in der folgenden Tabelle angegebenen Standardverzeichnisse können beim Setup von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vom Benutzer konfiguriert werden: Die Berechtigung zum Zugriff auf diese Dateien wird den lokalen Administratoren und Mitgliedern der Sicherheitsgruppe SQLServerMSASUser $\<instance> gewährt, die während des Setups erstellt und bereitgestellt wird.  
  
#### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
  
|Description|Standardverzeichnis|Empfehlungen|  
|-----------------|-----------------------|---------------------|  
|Datenstammverzeichnis |C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data |Stellen Sie sicher, dass der Ordner \Programme\Microsoft SQL Server\ durch entsprechend eingeschränkte Berechtigungen geschützt wird. Die Leistung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist in vielen Konfigurationen von der Leistung des Speichers abhängig, in dem sich das Datenverzeichnis befindet. Platzieren Sie dieses Verzeichnis im Speicher mit der höchsten Leistung, der mit dem System verknüpft ist. Stellen Sie für Failoverclusterinstallationen sicher, dass Datenverzeichnisse auf dem freigegebenen Datenträger platziert werden.|  
|Protokolldateiverzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log |Dies ist das Verzeichnis für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Protokolldateien, das auch das FlightRecorder-Protokoll enthält. Wenn Sie die Dauer von Flight Recorder erhöhen, stellen Sie sicher, dass für das Protokollverzeichnis genügend Speicherplatz zur Verfügung steht.|  
|Temporäres Verzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp |Platzieren Sie das temporäre Verzeichnis in einem leistungsstarken Speichersubsystem.|  
|Sicherungsverzeichnis|C:\Programme\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup |Dies ist das Verzeichnis für Standardsicherungsdateien von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Bei einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Installation werden in diesem Verzeichnis zudem die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Datendateien des [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Systemdiensts zwischengespeichert.<br /><br /> Stellen Sie sicher, dass zur Vermeidung von Datenverlusten entsprechende Berechtigungen festgelegt wurden und die Benutzergruppe für den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Dienst über die erforderlichen Berechtigungen zum Schreiben im Sicherungsverzeichnis verfügt. Die Verwendung eines zugeordneten Laufwerks für Sicherungsverzeichnisse wird nicht unterstützt.|  
  
#### <a name="notes"></a>Hinweise  
  
-   Auf einer SharePoint-Farm bereitgestellte [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Instanzen speichern Anwendungsdateien, Datendateien und Eigenschaften in Inhaltsdatenbanken und Dienstanwendungsdatenbanken.  
  
-   Wenn Sie Funktionen zu einer vorhandenen Installation hinzufügen, können Sie den Speicherort einer vorher installierten Funktion nicht ändern und auch keinen Speicherort für eine neue Funktion angeben.  

-   Möglicherweise müssen Sie Softwareanwendungen wie beispielsweise Viren- und Spywarescanner so konfigurieren, dass SQL Server-Ordner und -Dateitypen ausgeschlossen werden. Weitere Informationen finden Sie im folgenden Artikel: [Gewusst wie: Auswählen, wie Antivirussoftware auf Computern ausgeführt werden soll, auf denen SQL Server ausgeführt wird](https://support.microsoft.com/kb/309422).
  
-   Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genutzt werden. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] - und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Komponenten in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollten ebenfalls in separaten Verzeichnissen installiert werden.  
  
-   Programmdateien und Datendateien können in den folgenden Situationen nicht installiert werden:  
  
    -   Auf einem Wechseldatenträger  
  
    -   In einem Dateisystem, in dem die Komprimierung verwendet wird  
  
    -   In einem Verzeichnis, in dem sich Systemdateien befinden  
  
#### <a name="see-also"></a>Weitere Informationen finden Sie unter  
 Weitere Informationen zu Verzeichnissen, Dateispeicherorten und Namen für Instanz-IDs finden Sie unter [Dateispeicherorte für Standard- und benannte Instanzen von SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
    
 [Share and NTFS Permissions on a File Server (Share- und NTFS-Berechtigung für einen Dateiserver)](http://go.microsoft.com/fwlink/?LinkID=206571) 

## <a name="database-engine-configuration---filestream"></a>Konfiguration des Datenbankmoduls - Filestream
  Verwenden Sie diese Seite, um FILESTREAM für diese Installation von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zu aktivieren. FILESTREAM integriert [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in ein NTFS-Dateisystem, indem Blobdaten (Binary Large Object) vom Typ **varbinary(max)** als Dateien im Dateisystem gespeichert werden. [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen können FILESTREAM-Daten eingefügt, aktualisiert, abgefragt, gesucht und gesichert werden. Die Win32-Dateisystemschnittstellen stellen Streamingzugriff auf die Daten bereit.  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **FILESTREAM für Transact-SQL-Zugriff aktivieren**  
 Wählen Sie diese Option aus, um FILESTREAM für den [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff zu aktivieren. Dieses Steuerelement muss aktiviert werden, bevor die anderen Steuerelementoptionen verfügbar sind.  
  
 **FILESTREAM für E/A-Streamingzugriff auf Datei aktivieren**  
 Wählen Sie diese Option aus, um den Win32-Streamingzugriff für FILESTREAM zu aktivieren.  
  
 **Windows-Freigabename**  
 Verwenden Sie dieses Steuerelement, um den Namen der Windows-Freigabe einzugeben, in der die FILESTREAM-Daten gespeichert werden sollen.  
  
 **Streamingzugriff von Remoteclients auf FILESTREAM-Daten zulassen**  
 Aktivieren Sie dieses Steuerelement, damit Remoteclients auf diese FILESTREAM-Daten auf diesem Server zugreifen können.  
  
### <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aktivieren und Konfigurieren von FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

  
## <a name="database-engine-configuration---server-configuration"></a>Konfiguration des Datenbankmoduls – Serverkonfiguration
  Auf dieser Seite können Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sicherheitsmodus festlegen und Windows-Benutzer oder -Gruppen als Administratoren von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]hinzufügen.  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Überlegungen für das Ausführen von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wurde die Gruppe **BUILTIN\Administrators** für die Anmeldung bei [!INCLUDE[ssDE](../../includes/ssde-md.md)] bereitgestellt, und Mitglieder der lokalen Administratorgruppe konnten sich mit ihren Administratoranmeldeinformationen anmelden. Die Verwendung von erhöhten Berechtigungen ist keine bewährte Vorgehensweise. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] wird die Gruppe **BUILTIN\Administrators** nicht für die Anmeldung bereitgestellt. Daher sollten Sie für jeden Administratorbenutzer eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldung erstellen und diese während der Installation einer neuen Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]der festen Serverrolle sysadmin hinzufügen. Gehen Sie genauso für Windows-Konten vor, die zum Ausführen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Aufträgen verwendet werden. Dies schließt auch Replikations-Agent-Aufträge ein.  
  
### <a name="options"></a>Tastatur  
 **Sicherheitsmodus** – Wählen Sie Windows-Authentifizierung oder die Authentifizierung im gemischten Modus für die Installation aus.  
  
 **Windows-Prinzipal-Bereitstellung** – In früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]befand sich die lokale Windows-Gruppe Vordefiniert\Administrator in der sysadmin-Serverrolle von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , wodurch die Windows-Administratoren effektiv Zugriff auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erhielten. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]wird die Gruppe Vordefiniert\Administrator nicht in der Sysadmin-Serverrolle bereitgestellt. Stattdessen sollten Sie während des Setups explizit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratoren für Neuinstallationen festlegen.  
  
> [!IMPORTANT]  
>  Sie müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratoren für Neuinstallationen während des Setups explizit festlegen. Sie können den Setup-Vorgang erst nach Ausführung dieses Schrittes fortsetzen.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Administratoren angeben** – Sie müssen wenigstens einen Windows-Prinzipal für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angeben. Um das Konto hinzuzufügen, unter dem das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup ausgeführt werden soll, klicken Sie auf die Schaltfläche **Aktueller Benutzer** . Um der Liste der Systemadministratoren Konten hinzuzufügen bzw. daraus zu entfernen, klicken Sie auf **Hinzufügen** bzw. **Entfernen**und bearbeiten anschließend die Liste der Benutzer, Gruppen bzw. Computer, die für die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Administratorberechtigungen erhalten sollen.  
  
 Wenn Sie die Bearbeitung der Liste abgeschlossen haben, klicken Sie auf **OK**, und überprüfen Sie anschließend die Liste der Administratoren im Konfigurationsdialogfeld. Sobald die Liste vollständig ist, klicken Sie auf **Weiter**.  
  
 Bei Auswahl des gemischten Authentifizierungsmodus müssen Sie Anmeldeinformationen für das vordefinierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministrator-(SA-)Konto angeben.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows-Authentifizierungsmodus**  
 Wenn ein Benutzer eine Verbindung über ein Windows-Benutzerkonto herstellt, überprüft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Kontonamen und Kennwort mithilfe des Tokens für den Windows-Prinzipal im Betriebssystem. Dieser als Standardauthentifizierungsmodus verwendete Modus bietet eine höhere Sicherheit als der gemischte Modus. Die Windows-Authentifizierung verwendet das Kerberos-Sicherheitsprotokoll, stellt Maßnahmen zur Durchsetzung von Kennwortrichtlinien, z. B. zur Überprüfung der Komplexität sicherer Kennwörter, bereit und bietet Unterstützung für Kontosperrungen und Ablauf von Kennwörtern.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Legen Sie auf keinen Fall ein leeres oder unsicheres sa-Kennwort fest.  
  
 **Gemischter Modus (Windows-Authentifizierung oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung)**  
 Ermöglicht Benutzern das Herstellen einer Verbindung mithilfe der Windows-Authentifizierung bzw. der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung. Benutzer, die mithilfe eines Windows-Benutzerkontos Verbindungen herstellen, können vertrauenswürdige Verbindungen verwenden, die von Windows überprüft werden.  
  
 Wenn Sie den gemischten Authentifizierungsmodus auswählen und beim Ausführen älterer Anwendungen ausschließlich SQL-Anmeldungen verwenden, müssen Sie für alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konten sichere Kennwörter festlegen.  
  
> [!NOTE]  
>  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung wird nur aus Gründen der Abwärtskompatibilität bereitgestellt. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Kennwort eingeben**  
 Geben Sie die Systemadministratoranmeldung (sa) ein, uns bestätigen Sie sie. Kennwörter dienen als erste Schutzmaßnahme gegen Eindringlinge, daher ist die Festlegung sicherer Kennwörter von entscheidender Bedeutung für die Systemsicherheit. Legen Sie auf keinen Fall ein leeres oder unsicheres sa-Kennwort fest.  
  
> [!NOTE]  
>  Kennwörter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können zwischen 1 und 128 Zeichen (Kombinationen aus Buchstaben, Sonderzeichen und Ziffern) enthalten. Wenn Sie den gemischten Authentifizierungsmodus auswählen, müssen Sie ein sicheres sa-Kennwort eingeben, bevor Sie den Vorgang auf der nächsten Seite des Installations-Assistenten fortsetzen können.  
  
 **Richtlinien für sichere Kennwörter**  
 Sichere Kennwörter können von anderen nur schwer erraten und selbst von Computerprogrammen nicht ohne größeren Aufwand ausgespäht werden. Beim Festlegen von sicheren Kennwörtern dürfen keine verbotenen Richtlinien oder Bestimmungen verwendet werden, z. B.:  
  
-   Leeres Kennwort oder NULL  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 Beim Festlegen von sicheren Kennwörtern dürfen keine Angaben verwendet werden, die auf den Computer mit der Installation verweisen:  
  
-   Der Name des Benutzers, der zurzeit auf dem Computer angemeldet ist.  
  
-   Der Computername.  
  
 Ein sicheres Kennwort muss mehr als 8 Zeichen enthalten und wenigstens drei der folgenden vier Kriterien erfüllen:  
  
-   Es muss Großbuchstaben enthalten.  
  
-   Es muss Kleinbuchstaben enthalten.  
  
-   Es muss Zahlen enthalten.  
  
-   Es muss nicht alphanumerische Zeichen, z. B. #, % oder ^, enthalten.  
  
 Auf dieser Seite eingegebene Kennwörter müssen die Anforderungen der Richtlinien für sichere Kennwörter erfüllen. Bei Automatisierungen, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden, sollten Sie sicherstellen, dass das Kennwort die Anforderungen der Richtlinien für sichere Kennwörter erfüllt.  
  
### <a name="related-content"></a>Verwandte Inhalte  
 Weitere Informationen zum Auswählen von Windows-Authentifizierung im Vergleich zu der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung finden Sie unter [Choose an Authentication Mode (Wählen einer Authentifizierungsmethode)](../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Weitere Informationen zur Auswahl eines Kontos für die Ausführung von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]finden Sie unter [Configure Windows Service Accounts and Permissions (Konfigurieren von Windows-Dienstkonten und -Berechtigungen)](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).
  
## <a name="database-engine-configuration---tempdb"></a>Datenbankmodulkonfiguration – tempDB
  Verwenden Sie diese Seite, um den Speicherort, die Größe und die Vergrößerungseinstellungen für **tempdb** -Daten und -Protokolle anzugeben, ebenso wie die Anzahl an Dateien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. Auf Grundlage des Typs der Installation schließt der unterstützte Speicher möglicherweise einen lokalen Datenträger, freigegebenen Speicher oder SMB-Dateiserver ein.  
  
 Um eine SMB-Dateifreigabe als Verzeichnis anzugeben, müssen Sie den unterstützten UNC-Pfad manuell eingeben. Das Navigieren zu einer SMB-Dateifreigabe wird nicht unterstützt. Das folgende Format ist ein unterstütztes UNC-Pfadformat einer SMB-Dateifreigabe: \\\\Servername\ShareName\\\...  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>Daten- und Protokollverzeichnisse für eine eigenständige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 In der folgenden Tabelle sind die unterstützten Speichertypen und Standardverzeichnisse für eigenständige Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgeführt, die Sie während des Setups konfigurieren können.  
  
|Description|Unterstützter Speichertyp|Standardverzeichnis|Empfehlungen|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Datenverzeichnisse**|Lokaler Datenträger, SMB-Dateiserver, freigegebener Speicher* |C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup konfiguriert Zugriffssteuerungslisten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verzeichnisse und unterbricht während der Konfiguration die Vererbung.<br /><br /> Welche Vorgehensweise für die **temdb** -Verzeichnisse empfohlen wird, hängt von der Arbeitsauslastung und den Leistungsanforderungen ab. Geben Sie verschiedenen Ordner/Laufwerke an, um die Datendateien über mehrere Volumes zu verteilen.|  
|**Protokollverzeichnis**|Lokaler Datenträger, SMB-Dateiserver, freigegebener Speicher*|C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Stellen Sie sicher, dass ausreichend Speicherplatz für das Protokollverzeichnis verfügbar ist.|  
  
 *Obwohl freigegebene Datenträger unterstützt werden, wird diese Vorgehensweise für eine eigenständige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht empfohlen.  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Daten- und Protokollverzeichnisse für eine Failoverclusterinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 In der folgenden Tabelle sind die unterstützten Speichertypen und die Standardverzeichnisse für eine Failoverclusterinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgeführt, die während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setups vom Benutzer konfigurierbar sind.  
  
|Description|Unterstützter Speichertyp|Standardverzeichnis|Empfehlungen|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**tempdb** -Datenverzeichnis|Lokaler Datenträger, freigegebener Speicher, SMB-Dateiserver|\<Laufwerk:>\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\Data<br /><br /> Tipp: Wenn "Freigegebener Datenträger" auf der Seite **Datenträgerauswahl für Cluster** ausgewählt wurde, ist der Standard der erste freigegebene Datenträger. Dieses Feld ist standardmäßig leer, wenn keine Auswahl auf der Seite **Datenträgerauswahl für Cluster** getroffen wurde.|Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup konfiguriert Zugriffssteuerungslisten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verzeichnisse und unterbricht während der Konfiguration die Vererbung.<br /><br /> Stellen Sie sicher, dass das angegebene Verzeichnis oder die angegebenen Verzeichnisse (falls mehrere Dateien angegeben sind) für alle Clusterknoten gültig sind. Falls die **tempdb** -Verzeichnisse auf dem Failoverzielknoten während des Failovers nicht verfügbar sind, wird die SQL Server-Ressource nicht online geschaltet.|  
|**tempdb** -Protokollverzeichnis|Lokaler Datenträger, freigegebener Speicher, SMB-Dateiserver|\<Laufwerk:>\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Tipp: Wenn "Freigegebener Datenträger" auf der Seite **Datenträgerauswahl für Cluster** ausgewählt wurde, ist der Standard der erste freigegebene Datenträger. Dieses Feld ist standardmäßig leer, wenn keine Auswahl auf der Seite **Datenträgerauswahl für Cluster** getroffen wurde.|Welche Vorgehensweise für Benutzerdatenverzeichnisse empfohlen wird, hängt von der Arbeitsauslastung und den Leistungsanforderungen ab.<br /><br /> Stellen Sie sicher, dass das angegebene Verzeichnis für alle Clusterknoten gültig ist. Falls die **tempdb** -Verzeichnisse auf dem Failoverzielknoten während des Failovers nicht verfügbar sind, wird die SQL Server-Ressource nicht online geschaltet.<br /><br /> Stellen Sie sicher, dass ausreichend Speicherplatz für das Protokollverzeichnis verfügbar ist.|  
  
### <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 Konfigurieren Sie die Einstellungen für **tempdb** entsprechend Ihrer Arbeitsauslastung und den entsprechenden Anforderungen. Die folgenden Einstellungen gelten für **tempdb** -Datendateien:  
  
-   **Anzahl von Dateien** ist die Gesamtzahl der Datendateien für **tempdb**. Der Standardwert ist der niedrigere der folgenden beiden Werte: entweder acht, oder die Anzahl der logischen Kerne, die vom Setup erkannt wurden. Als allgemeine Regel gilt: Verwenden Sie die gleiche Anzahl an Datendateien wie logischen Prozessoren, falls die Anzahl von logischen Prozessoren acht oder weniger beträgt. Verwenden Sie acht Datendateien, falls die Anzahl von logischen Prozessoren größer als acht ist. Falls weiterhin ein Konflikt besteht, erhöhen Sie anschließend die Anzahl von Datendateien um ein Vielfaches von vier (bis hoch zur Anzahl von logischen Prozessoren) bis der Konflikt auf ein akzeptables Ausmaß reduziert ist, oder ändern Sie die Arbeitsauslastung oder den Code. 
  
-   **Anfangsgröße (MB)** ist die Anfangsgröße in MB für jede **tempdb** -Datendatei. Der Standardwert ist 8 MB (oder 4 MB für [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]führt eine maximale anfängliche Dateigröße von 262.144 MB (256 GB) ein. [!INCLUDE[sssql15](../../includes/sssql15-md.md)]hatte eine maximale anfängliche Dateigröße von 1024 MB. Alle **tempdb** -Datendateien haben die gleichen Anfangsgröße. Da **tempdb** bei jedem Start von SQL Server und bei jedem, von SQL Server durchgeführten Failover neu erstellt wird, sollten Sie eine Größe angeben, die der Größe nahekommt, die Ihre Arbeitsauslastung im Normalbetrieb erfordert. Aktivieren Sie die [Sofortige Datenbankdateiinitialisierung](../../relational-databases/databases/database-instant-file-initialization.md), um die Erstellung von **tempdb** weiter zu optimieren.  
  
-   **Gesamtanfangsgröße (MB)** ist die kumulierte Größe aller **tempdb** -Datendateien.  
  
-   **Automatische Vergrößerung (MB)** ist die Menge des Speicherplatzes in Megabyte, um die sich jede **tempdb** -Datendatei automatisch vergrößert, wenn es keinen Speicherplatz mehr gibt. In [!INCLUDE[sssql15](../../includes/sssql15-md.md)] und später vergrößern sich alle Datendateien gleichzeitig um die in dieser Einstellung angegebene Menge.  
  
-   **Gesamte automatische Vergrößerung (MB)** ist die kumulierte Größe der einzelnen Ereignisse der automatischen Vergrößerung.  
  
-   **Datenverzeichnisse** zeigen alle Verzeichnisse, die **tempdb** -Datendateien enthalten. Wenn mehrere Verzeichnisse vorhanden sind, werden die Datendateien reihum in den Verzeichnissen platziert. Falls Sie beispielsweise drei Verzeichnisse erstellen und acht Datendateien angeben, werden die Datendateien Nummer 1, 4 und 7 im ersten Verzeichnis erstellt. Die Datendateien 2, 5 und 8 werden im zweiten Verzeichnis erstellt. Die Datendateien 3 und 6 befinden sich im dritten Verzeichnis.  
  
-   Klicken Sie auf **Hinzufügen…**, um Verzeichnisse hinzufügen.  
  
-   Um ein Verzeichnis zu entfernen, wählen Sie das Verzeichnis aus, und klicken Sie auf **Entfernen**.  
  
 **TempDB-Protokolldatei** ist der Name der Protokolldatei. Er wird automatisch erstellt. Die folgenden Einstellungen gelten nur für **tempdb** -Protokolldateien:  
  
-   **Anfangsgröße (MB)** ist die Anfangsgröße der **tempdb** -Protokolldatei. Der Standardwert ist 8 MB (oder 4 MB für [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]führt eine maximale anfängliche Dateigröße von 262.144 MB (256 GB) ein. [!INCLUDE[sssql15](../../includes/sssql15-md.md)]hatte eine maximale anfängliche Dateigröße von 1024 MB. Da **tempdb** bei jedem Start von SQL Server und bei jedem, von SQL Server durchgeführten Failover neu erstellt wird, sollten Sie eine Größe angeben, die der Größe nahekommt, die Ihre Arbeitsauslastung im Normalbetrieb erfordert. Aktivieren Sie die [Sofortige Datenbankdateiinitialisierung](../../relational-databases/databases/database-instant-file-initialization.md), um die Erstellung von **tempdb** weiter zu optimieren.  
  
-   **Hinweis: tempdb** verwendet minimale Protokollierung. Das **tempdb** -Protokoll kann nicht gesichert werden. Es wird jedes Mal neu erstellt, wenn der SQL Server startet oder wenn eine Clusterinstanz einen Failover ausführt.  
  
-   **Automatische Vergrößerung (MB)** ist das Vergrößerungsinkrement des **tempdb** -Protokolls in Megabyte.  Der Standardwert von 64 MB erstellt die optimale Anzahl der virtuellen Protokolldateien während der Initialisierung.  
  
-   **Hinweis: tempdb** -Protokolldateien verwenden keine schnelle Dateiinitialisierung.  
  
-   **Protokollverzeichnis** ist das Verzeichnis, in dem **tempdb** -Protokolldateien erstellt werden. Es gib nur ein **tempdb** -Protokollverzeichnis.  
  
### <a name="security-considerations"></a>Überlegungen zur Sicherheit  
 Das Setup konfiguriert Zugriffssteuerungslisten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verzeichnisse und unterbricht während der Konfiguration die Vererbung.  

 Die folgenden Empfehlungen gelten für den SMB-Dateiserver:  
  
-   Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto muss ein Domänenkonto sein, wenn ein SMB-Dateiserver verwendet wird.  
  
-   Das Konto, das verwendet wurde, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu installieren, muss über FULL CONTROL NTFS-Berechtigungen für den als Datenverzeichnis verwendeten SMB-Dateifreigabeordner verfügen.  
  
-   Dem Konto, das für die Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird, müssen SeSecurityPrivilege-Berechtigungen auf dem SMB-Dateiserver zugewiesen werden. Diese Berechtigung weisen Sie zu, indem Sie die Konsole "Lokale Sicherheitsrichtlinie" auf dem Dateiserver verwenden, um der Richtlinie zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Verwalten von Überwachungs- und Sicherheitsprotokollen **das** -Setupkonto hinzuzufügen. Diese Einstellung ist im Abschnitt **Zuweisen von Benutzerrechten** unter **Lokale Richtlinien** in der Konsole **Lokale Sicherheitsrichtlinie** verfügbar.  
  
### <a name="notes"></a>Hinweise  
  
-   Wenn Sie keine Standardverzeichnisse angeben, sollten Sie sicherstellen, dass die Installationsordner nur für die Instanz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden. Keines der Verzeichnisse in diesem Dialogfeld sollte gemeinsam mit Verzeichnissen anderer Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genutzt werden. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)]- und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Komponenten in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sollten ebenfalls in separaten Verzeichnissen installiert werden.  
  
### <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Share and NTFS Permissions on a File Server (Share- und NTFS-Berechtigung für einen Dateiserver)](http://go.microsoft.com/fwlink/?LinkID=206571)  

## <a name="database-engine-configuration---user-instance"></a>Konfiguration des Datenbankmoduls - Benutzerinstanz
Mithilfe der Seite **Benutzerinstanz** können Sie eine separate Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für Benutzer ohne Administratorberechtigungen generieren. Zudem können Sie der Administratorrolle Benutzer hinzufügen.  
  
### <a name="option"></a>Option  
 Benutzerinstanzen aktivieren  
 Standardmäßig aktiviert. Um die Funktionalität zum Aktivieren von Benutzerinstanzen zu deaktivieren, deaktivieren Sie das Kontrollkästchen.  
  
 Die Benutzerinstanz, auch bekannt als untergeordnete Instanz oder Clientinstanz, ist eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die durch die übergeordnete Instanz (die primäre Instanz, die wie [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]als Dienst ausgeführt wird) für den Benutzer generiert wurde. Die Benutzerinstanz wird als Benutzerprozess in dem Sicherheitskontext des Benutzers ausgeführt. Die Benutzerinstanz ist von der übergeordneten Instanz und anderen Benutzerinstanzen, die auf dem Computer ausgeführt werden, isoliert. Im Zusammenhang mit der Benutzerinstanzfunktion wird auch der Ausdruck "Ausführen von Instanzen als normaler Benutzer" (RANU, Run As Normal User) verwendet.  
  
> [!NOTE]  
>  Während des Setups als Mitglieder der festen Serverrolle **sysadmin** bereitgestellte Anmeldungen werden in der Vorlagendatenbank als Administratoren bereitgestellt. Sie sind so lange Mitglieder der festen Serverrolle **sysadmin** auf der Benutzerinstanz, bis sie entfernt werden.  
  
 Benutzer zur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratorrolle hinzufügen  
 Standardmäßig deaktiviert. Aktivieren Sie dieses Kontrollkästchen, um den aktuellen Setupbenutzer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Administratorrolle hinzuzufügen.  
  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]-Benutzer, die Mitglieder von VORDEFINIERT\Administratoren sind, werden nicht automatisch der festen Serverrolle sysadmin hinzugefügt, wenn sie eine Verbindung mit [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] herstellen. Nur [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] -Benutzer, die explizit einer Administratorrolle auf Serverebene hinzugefügt wurden, können [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]verwalten. Mitglieder der Gruppe VORDEFINIERT\Administratoren können eine Verbindung mit der [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] -Instanz herstellen, verfügen jedoch nur über begrenzte Berechtigungen für Datenbankaufgaben. Daher müssen Benutzern, deren [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] -Berechtigungen in früheren Versionen von Windows von VORDEFINIERT\Administratoren und VORDEFINIERT\Benutzer vererbt wurden, unter [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] explizit Administratorberechtigungen in Instanzen von [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]erteilt werden.  
  
 Wenn Sie nach Beendigung dieses Installationsprogramms Änderungen an Benutzerrollen vornehmen möchten, verwenden Sie das Oberflächen-Konfigurationstool von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (SQLSAC.exe). Klicken Sie zum Aktualisieren der Liste der Benutzer in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministratorrolle auf den Link **Neuen Administrator hinzufügen** .  
  
 Stellen Sie sicher, dass im Feld **Bereitstellung für Benutzer** die Angaben zu Domänenname\Benutzername des Benutzers aufgeführt sind, dessen Berechtigungen aktualisiert werden sollen. Wählen Sie aus der Liste der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen im Bereich **Verfügbare Privilegien** die zu aktualisierende Rolle aus, und klicken Sie dann auf den Pfeil nach rechts. Wenn Sie den Benutzer allen verfügbaren Rollen für alle verfügbaren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen und allen verfügbaren Rollen hinzufügen möchten, klicken Sie auf den doppelten Pfeil nach rechts.  
  
 Klicken Sie zum Implementieren der Änderungen nach Abschluss der Auswahl auf [!INCLUDE[clickOK](../../includes/clickok-md.md)]. Klicken Sie auf **Abbrechen**, wenn Sie das Tool beenden möchten, ohne Änderungen vorzunehmen.  
  
  
