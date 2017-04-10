---
title: "PowerShell-Skripts in Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# PowerShell-Skripts in Analysis Services
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] bietet PowerShell-Komponenten zum Navigieren, Verwalten und Abfragen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Serverobjekten sowie tabellarischen und mehrdimensionalen Objekten:  
  
-   **SQLAS**-Anbieter für die Navigation in der Objekthierarchie; verfügbar, wenn Sie eine lokale Instanz von Analysis Services verwenden (Servermodus ist nicht relevant)  
  
-   **SQLASCMDLETS**-Modul mit taskspezifischen Cmdlets für z.B. Sicherung, Wiederherstellung und Verarbeitung, aber auch dem allgemeinen [Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md), das beliebige ASSL/XMLA- oder TMSL-Abfragen (Tabular Model Scripting Language) sowie Skripteingabedateien akzeptiert.  
  
 Beide Komponenten implementieren eine Teilmenge der AMO-Verwaltungsschnittstelle (Analysis Services Management Objects) [Microsoft.AnalysisServices Namespace](http://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) und stellen Cmdlets zum Erstellen und Verwalten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Objekten bereit.  sind Erweiterungen des **SQLPS**-Stammmoduls für SQL Server. Um PowerShell-Komponenten von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwenden zu können, müssen Sie zunächst **SQLPS** importieren. Syntax und Beispiele für alle Cmdlets finden Sie in der [PowerShell-Referenz für Analysis Services](../../analysis-services/powershell/analysis-services-powershell-reference.md).  Ein Beispiel zur Verwendung von AMO-Typen in PowerShell zum Erstellen einer tabellarischen Datenbank finden Sie unter [Beispiel für AMO PowerShell](../../analysis-services/powershell/amo-powershell-example.md).  
  
##  <a name="bkmk_prereq"></a> Schritt 1: Installieren von PowerShell-Komponenten  
 Die empfohlene Vorgehensweise für das Abrufen von PowerShell-Komponenten ist die Installation von SQL Server Management Studio (SSMS). Über diesen Ansatz werden die PowerShell-Module für SQL Server und der Datenanbieter für Analysis Services Management (AMO) bereitgestellt. SSMS bietet Ihnen außerdem ein Tool zum einfachen Generieren von XMLA- und TMSL-Eingaben in Ihr PowerShell-Skript.  
  
 Erwägen Sie, eine lokale Instanz von Analysis Services zu installieren. Eine lokale Instanz ermöglicht die Navigation durch die Objekthierarchie über den **SQLAS**-Anbieter, selbst wenn Sie ihn nie zum Hosten einer Datenbank verwenden.  
  
1.  Unter [Herunterladen von SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/mt238290.aspx) erhalten Sie die neueste Version von Management Studio. Die neueste Version von Management Studio enthält ein aktualisiertes AMO, das Definitionen tabellarischer Metadatenobjekte für tabellarische Modell unterstützt, die mit dem Kompatibilitätsgrad 1200 erstellt wurden.  
  
2.  Öffnen Sie nach der Installation von Management Studio ein PowerShell-Fenster. Es muss sich nicht um ein Administratorfenster handeln.  
  
3.  Geben Sie `Get-Module -ListAvailable` ein, um zu bestätigen, dass die Module **SQLPS** und **SQLASCMDLETS** in der Liste angezeigt werden.  
  
     **SQLAS** wird erst angezeigt, wenn Sie auch eine lokale Instanz von Analysis Services (im tabellarischen oder mehrdimensionalen Modus) installieren.  
  
4.  Geben Sie `Get-Command -Module sqlascmdlets` ein, um eine Liste der Cmdlets zu erstellen, die zur Analysis Services-Verwaltung verwendet werden.  
  
     **SQLASCMDLETS** sind auch dann verfügbar, wenn der **SQLAS**-Anbieter nicht vorhanden ist.  
  
    -   [Add-RoleMember-Cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)  
  
    -   [Backup-ASDatabase-Cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)  
  
    -   [Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) **-inputfile**  
  
    -   [Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)  
  
    -   [Invoke-ProcessCube-Cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Invoke-ProcessDimension-Cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Invoke-ProcessPartition-Cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Invoke-ProcessTable-cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)  
  
    -   [Merge-Partition-Cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)  
  
    -   [New-RestoreFolder-Cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)  
  
    -   [New-RestoreLocations-Cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)  
  
    -   [Remove-RoleMember-Cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)  
  
    -   [Restore-ASDatabase-Cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)  
  
> [!NOTE]  
>  Windows PowerShell ist in neueren Versionen der Windows-Betriebssysteme standardmäßig installiert. Empfohlen wird mindestens Version 4.0.  
  
## Schritt 2: Laden von Komponenten, um eine interaktive Sitzung zu starten  
 Nachdem die Komponenten installiert wurden, wird durch ihr Laden eine interaktive Sitzung gestartet.  
  
1.  Geben Sie `Import-Module sqlps -DisableNameChecking` ein.  
  
     Die SQL Server PowerShell-Komponenten, einschließlich derjenigen für Analysis Services, werden geladen und die Warnung zu ungültigen Verbnamen unterdrückt.  
  
2.  EINGABETASTE `sqlserver:`  
  
     Die Aufforderung sollte sich in **PS SQLSERVER:\\>** ändern.  
  
3.  Wenn Analysis Services lokal installiert ist, können Sie in der Objekthierarchie navigieren. Geben Sie `cd sqlas` ein, um den **SQLAS**-Anbieter zu öffnen.  
  
4.  Geben Sie `dir` ein, um Analysis Services-Instanzen aufzulisten. Der Anbieter unterscheidet nicht zwischen tabellarischen und mehrdimensionalen Instanzen.  
  
## Berechtigungen  
 Eine interaktive PowerShell-Sitzung wird unter der Sicherheitsidentität der Person ausgeführt, die diese startet. Für die meisten Aufgaben ist es erforderlich, dass die Person, die die Sitzung startet, auch ein Analysis Services-Serveradministrator ist.  
  
 Für unbeaufsichtigte Vorgänge sollten geplante PowerShell-Tasks erwägt werden. Das Konto, unter dem das Zeitplanungsmodul ausgeführt wird, z. B. der SQL Server-Agent-Dienst, muss u. U. (abhängig von der Aufgabe) auch Analysis Services-Administratorrechte haben.  
  
 Lokale Datenordner, z. B. die standardmäßigen Sicherungs- und Datenverzeichnisse, sind bereits mit Dateisystemberechtigungen konfiguriert, die einer lokalen Instanz das Lesen dieser und das Schreiben in diese Speicherorte erlauben.  
  
 Für eine Remoteverwaltung, insbesondere auf Clientcomputern ohne installierte Analysis Services, benötigt die Analysis Services-Remoteserverinstanz, die die Aktion ausführt, Dateisystemberechtigungen zum Lesen von Dateien während der Wiederherstellung oder zum Schreiben von Dateien während der Sicherung.  
  
## Skripteingabedateien: ASSL/XMLA oder TMSL  
 Bei Verwendung von **invoke-ascmd** zum Ausführen von Skripts spielen Servermodus, Datenbanktyp und Kompatibilitätsgrad eine wesentliche Rolle beim Erstellen des Skripts.  
  
-   Mehrdimensionale und tabellarische Datenbanken mit Kompatibilitätsgraden von 1050 bis 1103 reagieren auf Skripts, die in XMLA (unter Verwendung der für Analysis Services-Objektdefinitionen spezifischen ASSL-Erweiterungen) geschrieben sind.  
  
-   Tabellarische Datenbanken mit dem SQL Server 2016- Kompatibilitätsgrad 1200 reagieren auf TMSL-Skripts.  
  
 Wenn Sie in derselben SQL Server 2016-Instanz mit gemischten Versionen tabellarischer Modelle arbeiten, denken Sie daran, das richtige Skript zu verwenden.  
  
> [!NOTE]  
>  Skripts können in SQL Server Management Studio generiert und nach Bedarf geändert werden. Skripts für tabellarische Datenbanken mit Kompatibilitätsgrad 1200 werden in TMSL erstellt. Alle anderen Skripts werden in XMLA/ASSL erstellt. Eine SQL Server 2016-Instanz im tabellarischen Modus unterstützt beide Skriptsprachen.  
  
## Lokale und Remoteverwaltung  
 Die lokale Verwaltung von Analysis Services über PowerShell-Skripts und -Befehle ist aus zwei Gründen einfacher:  
  
-   Sie können den **SQLAS**-Anbieter für die Navigation durch die Objekthierarchie verwenden.  
  
-   Dateiberechtigungen, die Analysis Services das Lesen der Standarddatenordner erlauben, z. B. für die Sicherungs- und Wiederherstellungsaufgaben, sind bereits vorhanden. Vorausgesetzt wird allerdings, dass diese Ordner als Speicherort für die Datenbank verwendet werden und die lokale Serverinstanz für den Vorgang genutzt wird.  
  
 Das Verwalten einer Remote-Instanz erfordert zusätzliche Konfiguration. Die folgenden Schritte setzen voraus, dass Sie die Installationsschritte für Management Studio abgeschlossen haben, sich die Instanz des Diensts jedoch auf einem Remotecomputer befindet. Sie müssen auf dem Analysis Services-Server über Administratorrechte verfügen.  
  
 Da Analysis Services remote vorhanden ist, gibt es keinen **SQLAS**-Anbieter für die lokale Navigation in der Objekthierarchie. Wenn Sie Dateien aus einem lokalen Ordner anstatt aus einer Analysis Services-Instanz wiederherstellen, müssen Sie Freigaben erstellen und dem Server Lesezugriff auf die Dateien erteilen.  
  
1.  Öffnen Sie ein PowerShell-Fenster für Administratoren.  
  
2.  EINGABETASTE `Set-ExecutionPolicy RemoteUnsigned`  
  
3.  Stellen Sie im Datei-Explorer sicher, dass alle Ordner mit gespeicherten Daten freigegeben sind und dass die Analysis Services-Instanz über Leseberechtigungen für den Inhalt verfügt.  
  
##  <a name="bkmk_vers"></a> Unterstützte Versionen und Modi von Analysis Services  
 In der folgenden Tabelle wird die Verfügbarkeit von Analysis Services PowerShell in unterschiedlichen Kontexten angezeigt.  
  
|Kontext|Verfügbarkeit der PowerShell-Funktion|  
|-------------|-------------------------------------|  
|Mehrdimensionale Instanzen und Datenbanken|Unterstützt für lokale und Remoteverwaltung.<br /><br /> Merge-Partition erfordert eine lokale Verbindung.|  
|Tabellarische Instanzen und Datenbanken|Unterstützt für die lokale und Remoteverwaltung bei allen Kompatibilitätsgraden.<br /><br /> SQLAS-Cmdlets für tabellarische Modelle mit dem Kompatibilitätsgrad 1200 unter Verwendung von TMSL (Tabular Model Scripting Language) in JSON anstatt XMLA.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint-Instanzen und Datenbanken|Eingeschränkte Unterstützung. Sie können Instanz- und Datenbankinformationen mithilfe von HTTP-Verbindungen und dem SQLAS-Anbieter anzeigen.<br /><br /> Die Verwendung der Cmdlets wird jedoch nicht unterstützt. Verwenden Sie Analysis Services PowerShell nicht, um eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenbank im Arbeitsspeicher zu sichern und wiederherzustellen, Rollen hinzuzufügen oder zu entfernen, Daten zu verarbeiten oder beliebige XMLA-Skripts auszuführen.<br /><br /> Zu Konfigurationszwecken verfügt [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint über integrierte PowerShell-Unterstützung, die getrennt bereitgestellt wird. Weitere Informationen finden Sie unter [PowerShell-Referenz für PowerPivot für SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).|  
|Systemeigene Verbindungen zu lokalen Cubes<br /><br /> “Data Source=c:\backup\test.cub”|Nicht unterstützt.|  
|HTTP-Verbindungen zu BI-Semantikmodell-Verbindungsdateien (.bism) in SharePoint<br /><br /> “Data Source=http://server/shared_docs/name.bism”|Nicht unterstützt.|  
|Eingebettete Verbindungen mit [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Datenbanken<br /><br /> “Data Source=$Embedded$”|Nicht unterstützt.|  
|Lokaler Serverkontext in gespeicherten Prozeduren für Analysis Services<br /><br /> “Data Source=*”|Nicht unterstützt.|  
  
## Beispiele für Serververwaltungsaufgaben mit PowerShell  
 **Auflisten der Servereigenschaften**  
  
 Servereigenschaften werden auf verschiedene Weise verfügbar gemacht.  Wenn Sie mit Eigenschaften vertraut sind, die in der Datei „msmdsrv. ini“ oder auf den Eigenschaftenseiten von Management Studio verfügbar gemacht werden, erkennen Sie in den nachstehenden Beispielen, dass die Eigenschaften tatsächlich von verschiedenen Objekten zurückgegeben werden.  
  
 Dieses Skript lädt ein AMO-Serverobjekt. Wenn Sie einen vollständig qualifizierten Eigenschaftsnamen benötigen, können Sie dieses Skript zum Zurückgeben der Liste ausführen.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$as.serverproperties  
  
```  
  
 Dieses Skript gibt die Eigenschaften und Methoden auf Instanzebene zurück. Aus dieser Liste können Sie Werte wie **ServerMode**, **Version**, **ProductName** oder **ProductLevel** lesen.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as | get-member  
  
```  
  
 **Abrufen des Servermodus**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.ServerMode  
```  
  
 **Abrufen des Standardkompatibilitätsgrads**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.DefaultCompatibilityLevel  
```  
  
 **Abrufen einer Datenbankliste**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.databases  
```  
  
 **Ändern der Portnummer**  
  
 Dieses Skript erstellt ein Objekt für eine benannte Instanz, deklariert den Port, legt den Port fest, aktualisiert die Serverinstanz, trennt das Objekt und startet den Dienst neu. Als Überprüfungsschritt können Sie eine neue Verbindung öffnen und den Port zurückgeben lassen.  
  
 Sie können den Port auch in der Datei „msmdsrv.ini“ oder auf der Eigenschaftenseite „Allgemein“ des Servers in Management Studio überprüfen.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$port = $as.serverproperties['Port']  
$port | select *  
$port.Value = [int]55555  
$as.Update()  
$as.Disconnect()  
restart-service 'MSOLAP$TABULAR'  
$as.connect("server-name\instance-name")  
$port | select *  
  
```  
  
## Siehe auch  
 [Erteilen von serverweiten Administratorrechten für eine Analysis Services-Instanz](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Installieren von SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)   
 [Verwalten von tabellarischen Modellen mit PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)   
 [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)  
  
  