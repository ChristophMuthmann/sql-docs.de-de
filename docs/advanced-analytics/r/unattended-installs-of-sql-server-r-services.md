---
title: Unbeaufsichtigte Installation von Machine Learning Services | Microsoft Docs
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 801a29c07d55b9388d5be0edab33690399f2dde9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>Unbeaufsichtigte Installation von Machine Learning-Services (Datenbankintern)

Dieser Artikel beschreibt die Befehlszeilenargumente mit SQL Server-Setup zu verwenden, um die Machine learning-Komponenten zu installieren.

Für die unbeaufsichtigte Installation bedeutet, dass Sie nicht die interaktiven Features des Setup-Assistenten verwenden, und geben Sie stattdessen alle Argumente, die erforderlich sind, um die Installation abzuschließen, einschließlich von Lizenzverträgen für SQL Server und für Machine Learning-Komponenten auf einem über die Befehlszeile oder als Teil eines Skripts, in der Regel im stillen Modus.

+ [SQL Server 2016 R Services](#bkmk_OldInstall)
+ [SQL Server 2017 Machine Learning-Services](#bkmk_NewInstall) mit R oder Python
+ [Microsoft R Server "oder" Machine Learning-Server](../r/install-microsoft-r-server-from-the-command-line.md)

**Gilt für: SQL Server 2017 Machine Learning Services (Datenbankintern), SQL Server 2016 R Services**

## <a name="prerequisites"></a>Voraussetzungen

+ Sie müssen das Datenbankmodul für jede Instanz installieren, in dem Sie Machine Learning verwenden möchten.

+ Wenn der Computer nicht über Internetzugriff verfügt, achten Sie darauf, dass Sie die Installationsprogramme für Machine learning von Komponenten im Voraus herunterladen. Finden Sie unter [Machine Learning-Komponenten ohne Internetzugang installieren](../r/installing-ml-components-without-internet-access.md).

+ Es gibt separate Parameter für die open-Source-Komponenten für R und Python-Lizenzierung. SQL Server 2016 unterstützt nur R; SQL Server-2017 unterstützt R und Python. Sie müssen die Lizenzbedingungen für jede Sprache zustimmen, die Sie installieren. Setup schlägt fehl, wenn Sie diesen Parameter nicht in der Befehlszeile aufnehmen.

+ Um Setup abzuschließen ohne Anforderungen reagieren, stellen Sie sicher, dass Sie alle erforderlichen Argumente, einschließlich der für die Lizenzierung und für andere Features, die Sie installieren möchten, möglicherweise identifiziert haben.

+ Die **gemischt** Sicherheitsmodus, der SQL-Anmeldungen unterstützt war in frühen Versionen erforderlich. Obwohl es nicht mehr benötigt wird, sollten Sie erwägen, aktivieren die Authentifizierung im gemischten Modus Lösungsentwicklung von datenspezialisten unterstützt werden, die eine SQL-Anmeldung verwenden.

> [!IMPORTANT]
> 
> Nachdem Setup abgeschlossen ist, um das Feature zu aktivieren, sind zusätzliche Schritte erforderlich. Diese umfassen eine Neukonfiguration und Neustart der Instanz. Sie sicher, dass alle Elemente im Abschnitt [Schritte nach der Installation] überprüfen (#Bkmk_PostInstall), um zu bestimmen, Aktionen erforderlich nach Abschluss des Setups.

## <a name="bkmk_NewInstall"></a>Installation für SQL Server-2017 über die Befehlszeile

Im folgenden Beispiel enthalten die **minimale** erforderlichen Funktionen.

> [!IMPORTANT]
> Achten Sie darauf, dass alle Befehle in einer Eingabeaufforderung mit erhöhten Rechten ausgeführt werden.
> 
> Nachdem die Installation abgeschlossen ist, sind einige zusätzliche Schritte erforderlich. Finden Sie unter [in diesem Abschnitt](#bkmk_PostInstall). 
> Ein weiterer Neustart des SQL Server-Dienste werden benötigt, nachdem die Konfiguration abgeschlossen ist.

### <a name="install-r-only"></a>Nur Installieren von R

Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2017 Machine Services (Datenbankintern) installieren, mit der Sprache "R" hinzugefügt.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

Beachten Sie die Flags, die für R in SQL Server-2017 erforderlich:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MR`
+ `IACCEPTROPENLICENSETERMS`installiert haben.

### <a name="install-python-only"></a>Installieren Sie Python nur

Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2017 Machine Services (Datenbankintern) mit der Python-Programmiersprache hinzugefügt installieren.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

Beachten Sie die Flags für Python in SQL Server-2017 erforderlich:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

### <a name="install-both-r-and-python-on-a-named-instance"></a>Installieren von R und Python auf einer benannten Instanz

Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2017 Machine Services (In-Database) installieren, auf einer benannten Instanz. R und Python-Sprachen werden hinzugefügt.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

## <a name="OldInstall"></a>Installation für SQL Server 2016 über die Befehlszeile
 
Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2016 installieren, mit der Sprache "R" hinzugefügt.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

Beachten Sie die Flags für 2016 R Services erforderlich sind:

+ `ADVANCEDANALYTICS`
+ `IACCEPTROPENLICENSETERMS`

## <a name = "bkmk_PostInstall"></a>Zusätzliche Schritte nach der Installation

Sie müssen die folgenden Schritte ausführen, nachdem SQL Server-Setup abgeschlossen ist, unabhängig davon, welche Version ist, die Sie installiert. Machine Learning-Funktionen sind nicht standardmäßig aktiviert und müssen explizit aktiviert werden.

1.  Nachdem die Installation abgeschlossen ist, öffnen Sie ein neues **Abfrage** Fenster in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und führen Sie den folgenden Befehl zum Aktivieren der Funktion.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Die Funktion muss explizit aktiviert werden und Reconfigure; Andernfalls ist dies nicht möglich, externe Skripts zu aufrufen, auch wenn die Funktion installiert wurde.
  
2.  Starten Sie SQL Server-Diensts für den neu konfigurierten Instanz neu. Auf diese Weise wird automatisch neu gestartet den zugehörigen [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] als auch Service.

> [!IMPORTANT]
> 
> Einige zusätzliche Schritte können erforderlich sein, wenn Sie eine benutzerdefinierte Sicherheitskonfiguration haben oder wenn Sie die SQL Server als computekontext verwenden beim Ausführen von R oder Python-Code von einem Remoteclient aus. 
> 
> Weitere Informationen finden Sie unter [häufig gestellte Fragen zu Upgrade und Installation](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md).
