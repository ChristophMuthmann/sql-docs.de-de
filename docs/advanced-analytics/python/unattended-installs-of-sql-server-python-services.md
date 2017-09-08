---
title: Unbeaufsichtigte Installation von Python Machine Learning-Services (Datenbankintern) | Microsoft Docs
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
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b9156a3dc9dec21187eec8dc0b5a44059fb5e31
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-python-machine-learning-services-in-database"></a>Unbeaufsichtigte Installation von Python Machine Learning-Services (Datenbankintern)

Dieses Thema beschreibt, wie die Befehlszeilenargumente in 2017 von SQL Server-Setup zum Installieren von SQL Server-Datenbankmodul mit Machine Learning-Dienste und Python stillen Modus verwenden.

> [!NOTE]
> Vergessen Sie nicht die Befehlszeilenargumente für die Lizenzbedingungen, eine für Python und für SQL Server enthalten.

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie mit der Installation beginnen, beachten Sie folgende Voraussetzungen:

+ Der Python-Dienst kann nicht unabhängig von der 2017 von SQL Server-Datenbankmodul installiert werden. Sie müssen die SQL-Datenbankfunktion einschließen.
+ Falls Sie eine offline-Installation ausführen, müssen Sie die erforderlichen Python-Komponenten im Voraus herunterladen und in einen lokalen Ordner zu kopieren. Speicherorte für den Download, finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).
+ Es wird ein neuer Parameter */IACCEPTPYTHONLICENSETERMS*, Wert, der angibt, haben Sie die Lizenzbedingungen für die Verwendung der Python-Komponenten von Continuum Analytics bereitgestellten akzeptiert. Wenn Sie diesen Parameter nicht in der Befehlszeile verwenden, schlägt das Setup fehl.
+ Um Setup abzuschließen ohne Anforderungen reagieren, stellen Sie sicher, dass Sie alle erforderlichen Argumente, einschließlich derjenigen für Python und SQL Server-Lizenzierung und für andere Features, die Sie installieren möchten, möglicherweise identifiziert haben.
+  Authentifizierung im gemischten Modus wurde in einigen Vorabversionen von SQL Server 2016 erforderlich. Es ist nicht mehr erforderlich ist, obwohl es in Szenarien nützlich sein kann, in dem Datenanalysten entwickeln und Testen von Lösungen, die Remote mit SQL-Anmeldungen.

## <a name="perform-an-unattended-installation-of-python-machine-learning-services-in-database"></a>Ausführen einer unbeaufsichtigten Installations von Python Machine Learning-Services (Datenbankintern)

Das folgende Beispiel zeigt die **minimale** erforderlichen Funktionen in der Befehlszeile angeben, wenn Sie eine unbeaufsichtigte automatische Installation von Python und das Datenbankmodul die Standardinstanz durchführen.

> [!NOTE]
> Dieses Feature erfordert SQL Server-2017. Python wird in früheren Versionen von SQL Server nicht unterstützt.

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie den folgenden Befehl:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONLICENSETERMS
    ```

    > [!NOTE]
    > 
    > Es gibt neue Setup-Flags für Python: `SQL_INST_MPY` und`IACCEPTPYTHONLICENSETERMS`

2. Starten Sie den Server weitergeleitet.
3. Führen Sie die Schritte für die Konfiguration nach der Installation aus, wie in beschrieben [in diesem Abschnitt](#bkmk_PostInstall). Ein weiterer Neustart des SQL Server-Dienste werden benötigt.

## <a name = "bkmk_PostInstall"></a>Schritte nach der installation

1.  Nachdem die Installation abgeschlossen ist, öffnen Sie ein neues **Abfrage** Fenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie den folgenden Befehl zum Aktivieren der Funktion.

    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Die Funktion muss explizit aktiviert werden und Reconfigure; Andernfalls ist dies nicht möglich, externe Skripts zu aufrufen, auch wenn die Funktion installiert wurde.
  
3.  Starten Sie SQL Server-Diensts für den neu konfigurierten Instanz neu. Auf diese Weise wird automatisch neu gestartet den zugehörigen [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] als auch Service.

3. Möglicherweise sind weitere Schritte erforderlich, wenn Sie eine benutzerdefinierte Sicherheitskonfiguration verwenden, oder wenn Sie SQL Server einsetzen möchten, um Remoterechenkontexte zu unterstützen. Weitere Informationen finden Sie unter [Problembehandlung beim Machine Learning-Setup](../machine-learning-troubleshooting-faq.md).
