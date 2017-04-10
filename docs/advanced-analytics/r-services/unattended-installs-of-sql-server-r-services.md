---
title: "Unbeaufsichtigte Installationen von SQL Server R Services | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 14
---
# Unbeaufsichtigte Installationen von SQL Server R Services
    
Beachten Sie vor der Installation beginnen, diese Anforderungen:

+ Installieren Sie das Datenbankmodul für jede Instanz, in denen Sie R-Services (In der Datenbank) verwenden, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
+ Wenn Sie eine offline-Installation durchführen, müssen Sie die erforderlichen Komponenten von R im Voraus herunterladen und in einen lokalen Ordner kopieren. Speicherorte für den Download, finden Sie unter [R-Komponenten installieren, ohne Zugriff auf das Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).   
+ Es wird ein neuer Parameter */IACCEPTROPENLICENSETERMS*, die Sie für die Verwendung der open-Source-R-Komponenten dem Lizenzvertrag zugestimmt haben angibt. Wenn Sie diesen Parameter nicht in der Befehlszeile einfügen, schlägt Setup fehl.  
  
## Ausführen einer unbeaufsichtigten Installation von R Services (In-Datenbank)  
 Das folgende Beispiel zeigt die mindestens erforderlichen Features in der Befehlszeile angeben, bei der Durchführung einer unbeaufsichtigte automatische Installation von R-Dienste in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
###  <a name="bkmk_Unattended"></a>  
  
1.  Führen Sie den folgenden Befehl in einem Eingabeaufforderungsfenster mit erhöhten Rechten aus:  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
  
2.  Nach der Installation vollständig in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], führen Sie den folgenden Befehl aus, um die Funktion zu aktivieren.  
  
    ```  
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with  override  
  
    ```  
  
    > [!NOTE]  
    >  Sie müssen die Modulfunktion explizit aktivieren. Andernfalls ist es nicht möglich, R-Skripts aufzurufen, auch wenn die Funktion als konfiguriert durch das Setup installiert wurde.  
  
3.  Starten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz. Dies wird automatisch neu gestartet verknüpften [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] -Dienst.  
  
## Siehe auch  
 [Problembehebung des R Services-Setups](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  