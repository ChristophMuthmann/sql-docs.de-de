---
title: Unbeaufsichtigte Installation von Machine Learning Services | Microsoft Docs
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: babb74aa866404853cfef83e1d30159354f385e7
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>Unbeaufsichtigte Installation von Machine Learning-Services (Datenbankintern)

Dieses Thema beschreibt, wie Befehlszeilenargumente mit SQL Server-Setup zum Installieren von Machine Learning in einer Instanz des Datenbankmoduls im stillen Modus. Bei einer unbeaufsichtigten Installation verwenden Sie keine die interaktiven Features des Setup-Assistenten, und müssen alle Argumente, die erforderlich sind, um die Installation abzuschließen, einschließlich von Lizenzverträgen für SQL Server und für Machine Learning-Komponenten bereitstellen.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Services (Datenbankintern)

> [!IMPORTANT]
> 
> In SQL Server 2016 und SQL Server-2017 sind zusätzliche Schritte erforderlich, nachdem Setup abgeschlossen ist, um das Feature zu aktivieren. Diese umfassen eine Neukonfiguration und Neustart der Instanz. Achten Sie darauf, dass Sie alle Schritte zu überprüfen.

## <a name="prerequisites"></a>Erforderliche Komponenten

+ Sie müssen das Datenbankmodul für jede Instanz installieren, in dem Sie Machine Learning verwenden möchten.

+ Wenn der Computer nicht über Internetzugriff verfügt, achten Sie darauf, dass Sie die Installationsprogramme für Machine learning von Komponenten im Voraus zu installieren. Speicherorte für den Download, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](../../advanced-analytics/r/installing-ml-components-without-internet-access.md).

+ Es sind neue Parameter, die im Zusammenhang mit der open-Source-Komponenten für R und Python-Lizenzierung. Sie müssen die Lizenzbedingungen für ein separates Argument für jede Sprache zustimmen, die Sie installieren. Wenn Sie diesen Parameter nicht in der Befehlszeile verwenden, schlägt das Setup fehl.

+ Um Setup abzuschließen ohne Anforderungen reagieren, stellen Sie sicher, dass Sie alle erforderlichen Argumente, einschließlich der für die Lizenzierung und für andere Features, die Sie installieren möchten, möglicherweise identifiziert haben.

> [!NOTE] 
> In frühen Versionen war der gemischten Sicherheitsmodus, der SQL-Anmeldungen unterstützt erforderlich. Allerdings sollten Sie erwägen, die Authentifizierung im gemischten Modus zur Unterstützung der Entwicklung von datenspezialisten unter Verwendung einer SQL-Anmeldung aktivieren.

## <a name="bkmk_NewInstall"></a>Unbeaufsichtigte Installation von Machine Learning-Dienste mit R

Das folgende Beispiel zeigt die **minimale** erforderlichen Features, die in der Befehlszeile angeben, wenn eine automatische, für die unbeaufsichtigte Ausführung der Installation von SQL Server 2017 Machines-Diensten (In-Database).

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie den folgenden Befehl:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    
    Beachten Sie die Flags, die für R in SQL Server-2017 erforderlich: `ADVANCEDANALYTICS`, `SQL_INST_MR`, und `IACCEPTROPENLICENSETERMS`.
2. Starten Sie den Server neu.
3. Führen Sie die Schritte für die Konfiguration nach der Installation aus, wie in beschrieben [in diesem Abschnitt](#bkmk_PostInstall). Ein weiterer Neustart des SQL Server-Dienste werden benötigt.

## <a name="OldInstall"></a>Für die unbeaufsichtigte Installation von R Services (Datenbankintern)
 
 Das folgende Beispiel zeigt die **minimale** erforderlichen Features, die in der Befehlszeile angeben, wenn eine automatische, für die unbeaufsichtigte Ausführung von SQL Server 2016 R Services zu installieren.

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie den folgenden Befehl:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    Beachten Sie die Flags für 2016 R SERVICES erforderlich sind: `ADVANCEDANALYTICS` und `IACCEPTROPENLICENSETERMS`.
2. Starten Sie den Server neu.
3. Führen Sie die Schritte für die Konfiguration nach der Installation aus, wie in beschrieben [in diesem Abschnitt](#bkmk_PostInstall). Ein weiterer Neustart des SQL Server-Dienste werden benötigt.

## <a name = "bkmk_PostInstall"></a>Zusätzliche Schritte nach der Installation

1.  Nachdem die Installation abgeschlossen ist, öffnen Sie ein neues **Abfrage** Fenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie den folgenden Befehl zum Aktivieren der Funktion.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Die Funktion muss explizit aktiviert werden und Reconfigure; Andernfalls ist dies nicht möglich, externe Skripts zu aufrufen, auch wenn die Funktion installiert wurde.
  
2.  Starten Sie SQL Server-Diensts für den neu konfigurierten Instanz neu. Auf diese Weise wird automatisch neu gestartet den zugehörigen [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] als auch Service.

3. Möglicherweise sind weitere Schritte erforderlich, wenn Sie eine benutzerdefinierte Sicherheitskonfiguration verwenden, oder wenn Sie SQL Server einsetzen möchten, um Remoterechenkontexte zu unterstützen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Upgrade und Installation](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md).

