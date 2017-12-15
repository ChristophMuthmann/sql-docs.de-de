---
title: "Dateispeicherorte für Standard- und benannte Instanzen von SQL Server | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 4209e4270df9c7af22e79fb3b8700db4be992524
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>Dateispeicherorte für Standard- und benannte Instanzen von SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Eine Installation von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] besteht aus einer oder mehreren separaten Instanzen. Eine Instanz (Standard- als auch benannte Instanz) besitzt eine Reihe eigener Programm- und Datendateien sowie mehrere freigegebene Dateien, die für alle Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf dem Computer freigegeben werden.  
  
 Für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]umfasst, verfügt jede Komponente über einen vollständigen Satz an Daten- und ausführbaren Dateien sowie die für alle Komponenten freigegebenen Dateien.  
  
 Zum Isolieren der Installationsspeicherorte für jede Komponente werden eindeutige Instanz-IDs für jede Komponente innerhalb einer bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz generiert.  
  
> [!IMPORTANT]  
>  Programm- und Datendateien können weder auf einem Wechseldatenträger, auf einem Dateisystem mit Komprimierung, in einem Verzeichnis mit Systemdateien noch auf freigegebenen Laufwerken einer Failoverclusterinstanz installiert werden.  
>  
>  Möglicherweise müssen Sie Softwareanwendungen wie beispielsweise Viren- und Spywarescanner so konfigurieren, dass SQL Server-Ordner und -Dateitypen ausgeschlossen werden. Weitere Informationen finden Sie im folgenden Artikel: [Gewusst wie: Auswählen, wie Antivirussoftware auf Computern ausgeführt werden soll, auf denen SQL Server ausgeführt wird](https://support.microsoft.com/kb/309422).
> 
>  Systemdatenbanken (Master, Model, MSDB und TempDB) und [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Benutzerdatenbanken können mit dem SMB (Server Message Block)-Dateiserver als Speicheroption installiert werden. Dies gilt sowohl für eigenständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - als auch für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Failoverclusterinstallationen (FCI). Weitere Informationen finden Sie unter [Installieren von SQL Server mit SMB-Dateifreigabe als Speicheroption](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
>   
>  Löschen Sie keines der folgenden Verzeichnisse oder dessen Inhalt: Binn, Data, Ftdata, HTML oder 1033. Andere Verzeichnisse können ggf. gelöscht werden. Möglicherweise können Sie auf diese Weise verloren gegangene Funktionalität oder Daten dann aber nur abrufen, indem Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]deinstallieren und anschließend erneut installieren. Löschen oder ändern Sie keine HTM-Dateien im Verzeichnis HTML. Sie sind für die ordnungsgemäße Funktion der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tools erforderlich.  
  
## <a name="shared-files-for-all-instances-of-includessnoversionincludesssnoversion-mdmd"></a>Freigegebene Dateien für alle Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Dateien, die häufig von allen Instanzen auf einem Computer verwendet werden, werden im Ordner [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)] installiert. \<*Laufwerk*> ist der Laufwerkbuchstabe, auf dem die Komponenten installiert sind. Dies ist in der Regel Laufwerk „C:“. \<*nnn*> gibt die Version an. In der folgenden Tabelle werden die Versionen für die Pfade angezeigt. 

|\<*nnn*>|Version
|-----|-----
|140|[!INCLUDE[ssqlv14](../../includes/sssqlv14-md.md)]
|130|[!INCLUDE[ssqlv13](../../includes/sssql15-md.md)]
|120|SQL Server 2014
|110|[!INCLUDE[sssql11](../../includes/sssql11-md.md)] 
  
## <a name="file-locations-and-registry-mapping"></a>Dateispeicherorte und Registrierungszuordnung  
 Während des Setups von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird für jede Serverkomponente eine Instanz-ID generiert. Die Serverkomponenten in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]und [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Die Standardinstanz-ID wird mit dem folgenden Format erstellt:  
  
-   Auf MSSQL für [!INCLUDE[ssDE](../../includes/ssde-md.md)]folgt die Hauptversionsnummer, ggf. gefolgt von einem Unterstrich und der Nebenversionsnummer, und ein Punkt, woraufhin wiederum der Instanzname folgt.  
  
-   Auf MSSQL für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]folgt die Hauptversionsnummer, ggf. gefolgt von einem Unterstrich und der Nebenversionsnummer, und ein Punkt, woraufhin wiederum der Instanzname folgt.  
  
-   Auf MSRS für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]folgt die Hauptversionsnummer, ggf. gefolgt von einem Unterstrich und der Nebenversionsnummer, und ein Punkt, woraufhin wiederum der Instanzname folgt.  
  
 Beispiele für Standardinstanz-IDs in dieser Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lauten wie folgt:  
  
-   MSSQL14.MSSQLSERVER für eine Standardinstanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   MSAS14.MSSQLSERVER für eine Standardinstanz von [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]  
  
-   MSSQL14.MyInstance für eine benannte Instanz von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] namens „MyInstance“  
  
    >[!NOTE]
    >Die zweistellige Zahl in der Instanzpfad-ID kennzeichnet die Versionsnummer. In den vorherigen Beispielen stand die Versionsnummer 14 für [!INCLUDE[ssqlv14](../../includes/sssqlv14-md.md)]. 

 Die Verzeichnisstruktur für eine mit dem Namen "MyInstance" benannte [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Instanz, die [!INCLUDE[ssDE](../../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]umfasst und in den Standardverzeichnissen installiert ist, lautet wie folgt:  
  
-   C:\Programme\Microsoft SQL Server\MSSQL14.MyInstance\  
  
-   C:\Programme\Microsoft SQL Server\MSAS14.MyInstance\  
  
 Sie können jeden Wert für die Instanz-ID angeben, sollten aber Sonderzeichen und reservierte Schlüsselwörter vermeiden.  
  
 Sie können während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups eine nicht standardmäßige Instanz-ID angeben. Anstelle von \<Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird ein \<benutzerdefinierter Pfad\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, wenn der Benutzer eine Änderung des Standardinstallationsverzeichnisses auswählt. Beachten Sie, dass die Instanz-IDs, die mit einem Unterstrich (_) beginnen oder das Nummernzeichen (#) oder Dollarzeichen ($) enthalten, nicht unterstützt werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Clientkomponenten sind nicht instanzabhängig und bekommen daher keine Instanz-ID zugewiesen. Standardmäßig werden nicht instanzabhängige Komponenten in einem einzelnen Verzeichnis installiert: [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]. Wenn der Installationspfad einer freigegebenen Komponente geändert wird, wirkt sich diese Änderung auch auf die anderen freigegebenen Komponenten aus. Bei allen zukünftigen Installationen werden die nicht instanzbezogenen Komponenten wieder im gleichen Verzeichnis installiert wie bei der ursprünglichen Installation.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ist die einzige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponente, die nach der Installation Instanzumbenennung unterstützt. Wenn eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] umbenannt wird, ändert sich die Instanz-ID nicht. Nach abgeschlossener Instanzumbenennung wird die während der Installation erstellte Instanz-ID von Verzeichnissen und Registrierungsschlüsseln weiterhin verwendet.  
  
 Die Registrierungsstruktur wird für instanzabhängige Komponenten unter HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*Instanz_ID* erstellt. Beispiel:  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS14.MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS14.MyInstance  
  
 Die Registrierung verwaltet auch eine Zuordnung der Instanz-ID zum Instanznamen. Die Zuordnung der Instanz-ID zum Instanznamen wird folgendermaßen verwaltet:  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\SQL] "InstanceName"="MSSQL14"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\OLAP] "InstanceName"="MSAS14"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\RS] "InstanceName"="MSRS14"  
  
## <a name="specifying-file-paths"></a>Angeben von Dateipfaden  
 Beim Setup können Sie den Installationspfad für die folgenden Funktionen ändern:  
  
 Der Installationspfad wird im Setup nur für die Funktionen angezeigt, die einen vom Benutzer konfigurierbaren Zielordner besitzen.  
  
|Komponente|Standardpfad|Konfigurierbarer oder fester Pfad|  
|---------------|------------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Serverkomponenten|\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<Instanz-ID>\ |Konfigurierbar|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Datendateien|\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<Instanz-ID>\ |Konfigurierbar|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] server|\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS14.\<Instanz-ID>\ |Konfigurierbar|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Datendateien|\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS14.\<Instanz-ID>\ |Konfigurierbar|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Berichtsserver|\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS14.\<Instanz-ID>\Reporting Services\ReportServer\Bin\ |Konfigurierbar|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Berichts-Manager|\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS14.\<Instanz-ID\Reporting Services\ReportManager\ |Fester Pfad|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<Installationsverzeichnis>\140\DTS\\ <sup>1</sup> |Konfigurierbar |  
|Clientkomponenten (außer bcp.exe und sqlcmd.exe)|\<Installationsverzeichnis>\140\Tools\\ <sup>1</sup> |Konfigurierbar |  
|Clientkomponenten (bcp.exe und sqlcmd.exe)|\<Installationsverzeichnis>\Client SDK\ODBC\110\Tools\Binn|Fester Pfad|  
|Replikations- und serverbasierte COM-Objekte|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\\ <sup>2</sup> |Fester Pfad|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Von Integration Services bereitgestellte DLLs für das Data Transformation Runtime-Modul, das Data Transformation Pipeline-Modul und das **dtexec** -Eingabeaufforderungshilfsprogramm|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|Fester Pfad|  
|DLLs, die die Verbindungsunterstützung für Integration Services verwalten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Verbindungen|Fester Pfad|  
|DLLs für alle Arten von Enumeratoren, die von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt werden|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEach-Enumeratoren|Fester Pfad|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser-Dienst, WMI-Anbieter|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Shared\ |Fester Pfad|  
|Komponenten, die von allen Instanzen von gemeinsam genutzt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Shared\ |Fester Pfad|  
  
>[!WARNING]
>Stellen Sie sicher, dass der Ordner „\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\“ durch entsprechend eingeschränkte Berechtigungen geschützt wird.  
  
Beachten Sie, dass das Standardlaufwerk für Dateispeicherorte *systemdrive*lautet, normalerweise Laufwerk C. Installationspfade für untergeordnete Funktionen werden durch die Installationspfade der übergeordneten Funktion bestimmt.  
  
<sup>1</sup> Ein einzelner Installationspfad wird von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] und Clientkomponenten gemeinsam genutzt. Wenn der Installationspfad einer Komponente geändert wird, wirkt sich diese Änderung auch auf die anderen Komponenten aus. Bei allen zukünftigen Installationen werden die Komponenten wieder am gleichen Speicherort installiert wie bei der ursprünglichen Installation.  
  
<sup>2</sup> Dieses Verzeichnis wird von allen auf dem Computer installierten Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet. Wenn Sie ein Update auf eine der Instanzen auf dem Computer anwenden, wirken sich alle Änderungen an den Dateien dieses Ordners auch auf die übrigen auf dem Computer installierten Instanzen aus. Wenn Sie Funktionen zu einer vorhandenen Installation hinzufügen, können Sie den Speicherort einer vorher installierten Funktion nicht ändern und auch keinen Speicherort für eine neue Funktion angeben. Sie müssen zusätzliche Funktionen entweder in die durch das Setup bereits vorgegebenen Verzeichnisse installieren, oder Sie deinstallieren das Produkt und installieren es anschließend neu.  
  
> [!NOTE]  
>  Bei gruppierten Konfigurationen müssen Sie ein lokales Laufwerk auswählen, das für jeden Knoten des Clusters verfügbar ist.  
  
 Wenn Sie beim Setup einen Installationspfad für die Serverkomponenten oder Datendateien angeben, verwendet das Setup-Programm die Instanzkennung zusätzlich zum angegebenen Speicherort für Programm- und Datendateien. Die Instanz-ID wird vom Setup nicht für Tools und andere freigegebene Dateien verwendet. Darüber hinaus verwendet das Setup keine Instanz-ID für das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Programm und Datendateien. Für das [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Repository wird jedoch eine Instanz-ID verwendet.  
  
 Wenn Sie einen Installationspfad für die Funktion [!INCLUDE[ssDE](../../includes/ssde-md.md)] festlegen, wird dieser Pfad vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup als Stammverzeichnis für alle instanzspezifischen Ordner der Installation, einschließlich der SQL-Datendateien, verwendet. Wenn Sie in diesem Fall „C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL14.\<Instanzname>\MSSQL\\“ als Stammverzeichnis festlegen, werden die instanzspezifischen Verzeichnisse am Ende dieses Pfads hinzugefügt.  
  
 Wenn die im Installations-Assistenten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellte Upgradefunktionalität USESYSDB verwendet wird, kann der Fall eintreten, dass das Produkt in einer rekursiven Ordnerstruktur installiert wird. Ein Beispiel ist \<*SQL-Programmdateien*>\MSSQL14\MSSQL\MSSQL10_50\MSSQL\Data\\. Legen Sie stattdessen bei Verwendung der USESYSDB-Funktion nur einen Installationspfad für die Funktion "SQL-Datendateien" und nicht für die Funktion [!INCLUDE[ssDE](../../includes/ssde-md.md)] fest.  
  
> [!NOTE]  
>  Datendateien werden erwartungsgemäß immer in einem untergeordneten Verzeichnis mit dem Namen Data gesucht. Geben Sie beispielsweise beim Upgrade „C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MSSQL14.\<Instanzname>\“ als Stammpfad zum Datenverzeichnis der Systemdatenbanken an, wenn sich die Datendateien unter „C:\Programme\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MSSQL14.\<Instanzname>\MSSQL\Data“ befinden.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration des Datenbankmodells - Datenverzeichnisse](http://msdn.microsoft.com/library/9b1fa0fc-623b-479a-afc3-4f13bd850487)   
 [Konfigurationseigenschaften von Analysis Services – Datenverzeichnisse](http://msdn.microsoft.com/library/ef732855-b7af-4f40-a619-5573c1c354bb)  
  
  
