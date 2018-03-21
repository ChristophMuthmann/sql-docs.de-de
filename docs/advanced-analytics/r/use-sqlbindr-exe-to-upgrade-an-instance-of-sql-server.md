---
title: Binden von Machine Learning-Komponenten auf SQL Server auf Microsoft Machine Learning-Server | Microsoft Docs
ms.custom: 
ms.date: 03/15/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 7c67d0accb7ac7be46105e5148028fac3f67aa0f
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="bind-machine-learning-components-on-sql-server-to-microsoft-machine-learning-server"></a>Binden von Machine Learning-Komponenten auf SQL Server auf Microsoft Machine Learning-Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel erläutert, wie der _Bindung_, die Sie verwenden können, zum Aktualisieren des Machine learning in SQL Server verwendete Komponenten. Der Prozess der Bindung sperrt die Server in einer Update-Rhythmus basierend auf Versionen von Machine Learning-Server, Version anstelle von SQL Server und Zeitplan aktualisieren.

> [!IMPORTANT]
> Sie müssen nicht durch diesen Prozess zu verwenden, wenn Upgrades als Teil von SQL Server-Updates abgerufen werden soll. Wenn Sie ein neues Servicepack oder Service Version installieren, werden die Machine Learning-Komponenten immer automatisch auf die neueste Version aktualisiert. Verwenden Sie nur die _Bindung_ verarbeiten, wenn Sie Komponenten mit einer schnellere Geschwindigkeit als von SQL Server Service Releases Authentifizierungsprozesses wird ein Upgrade ausführen möchten.

Wenn zu einem beliebigen Zeitpunkt Sie gemäß dem Zeitplan Machine Learning-Server beenden aktualisieren möchten, Sie müssen _Bindung_ der Instanz, wie in beschrieben [in diesem Abschnitt](#bkmk_Unbind), und Deinstallieren von Machine Learning-Server.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="binding-vs-upgrading"></a>Die Bindung im Vergleich zu aktualisieren

Der Prozess des Upgrades von Machine learning-Komponenten wird als bezeichnet **Bindung**, da sie das Modell Unterstützung für SQL Server Machine Learning Komponenten, die neue moderne Software Lifecycle-Richtlinie ändert. 

Wechseln mit dem neuen Wartungsmodell wird im Allgemeinen sichergestellt, dass auf die Datenanalysten immer die neueste Version von R oder Python verwenden können. Weitere Informationen zu den Begriffen der moderne Lifecycle-Richtlinie finden Sie unter [Unterstützungszeitraum für Microsoft R Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support).

> [!NOTE]
> Das Upgrade ändert sich nicht auf das Modell Unterstützung für SQL Server-Datenbank und die Version von SQL Server nicht geändert.

Wenn Sie eine Instanz binden, passieren mehrere Dinge:

+ Das Supportmodell geändert wird. Anstatt auf SQL Server-Dienst-Versionen, basiert die Unterstützung auf die neue moderne Lifecycle-Richtlinie.
+ Die Machine Learning-Komponenten, die der Instanz zugeordnet werden mit jedem Release, im Gleichschritt mit der Version, die unter der neuen, modernen Lifecycle-Richtlinie aktuell ist, automatisch aktualisiert. 
+ Neue R oder Python-Pakete können hinzugefügt werden. Z. B. vorherige Updates basierend auf Microsoft R Server 9.1 hinzugefügt neue R-Pakete, z. B. [MicrosoftML](../using-the-microsoftml-package.md), [OlapR](../r/how-to-create-mdx-queries-using-olapr.md), und [Sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).
+ Die Instanz kann nicht mehr manuell aktualisiert werden, außer wenn Sie neue Pakete hinzufügen.
+ Sie erhalten die Option zum Installieren von vortrainierte Modelle, die von Microsoft bereitgestellt.

## <a name="bkmk_prereqs"></a>Prerequisites

Durch das Identifizieren von Instanzen, die als für ein Upgrade Kandidaten beginnen. Wenn Sie das Installationsprogramm ausführen und wählen Sie die Bindungsoption, wird eine Liste der Instanzen, die kompatibel mit dem Upgrade werden zurückgegeben.

Finden Sie in der folgenden Tabelle eine Liste der unterstützten Upgrades und Anforderungen.

| SQL Server-Version| Unterstützte Upgrades| Hinweise|
|-----|-----|------|
| SQL Server 2016| Machine Learning Server 9.2.1| Erfordert mindestens Service Pack 1 plus CU3. R Services muss installiert und aktiviert werden.|
| SQL Server 2017| Machine Learning Server 9.2.1| Machine Learning-Services (Datenbankintern) muss installiert und aktiviert werden. |

## <a name="bind-or-upgrade-an-instance"></a>Binden oder Aktualisieren einer Instanz

Machine Learning-Server für Windows enthält ein Tool, das Sie verwenden können, so aktualisieren Sie die Machine learning-Sprachen und Tools, die einer Instanz von SQL Server zugeordnet. Es gibt zwei Versionen des Tools: Assistenten, und ein Befehlszeilen-Hilfsprogramm.

Bevor Sie den Assistenten oder das Befehlszeilentool ausführen können, müssen Sie die neueste Version des eigenständigen Installationsprogramms für den Machine learning-Komponenten herunterladen.

+ [Installieren Sie Machine Learning-Server 9.2.1 für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ [Herunterladen Sie für offline-Installation erforderlichen Komponenten](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="bkmk_BindWizard"></a>Aktualisieren Sie mit dem Setup-Assistenten

1. Beginnen Sie mit dem neuen Installer für Machine Learning-Server. Achten Sie darauf, dass Sie das Installationsprogramm auf dem Computer ausführen, die der Instanz verfügt, die Sie aktualisieren möchten.

    ![Microsoft Machine Learning-Server-Setup-Assistenten](media/mls-921-installer-start.PNG)

2. Auf der Seite **konfigurieren Sie die Installation**, bestätigen Sie die Komponenten aktualisieren, und überprüfen Sie die Liste der kompatiblen Instanzen. Wenn keine Instanzen angezeigt werden, überprüfen Sie die [Voraussetzungen](#bkmk_prereqs).

    Aktivieren Sie das Kontrollkästchen neben dem Instanznamen, um eine Instanz zu aktualisieren. Wenn Sie keine Instanz auswählen, wird eine separate Installation von Machine Learning-Server erstellt, und die SQL Server-Bibliotheken sind dieselben wie.

    ![Microsoft Machine Learning-Server-Setup-Assistenten](media/configure-the-installation.PNG)

3. Auf der **Lizenzvertrag** Seite **ich akzeptiere diese Lizenzbedingungen** für Machine Learning-Server die Lizenzbedingungen akzeptieren. 

4. Geben Sie auf den nachfolgenden Seiten seine Zustimmung zur weiteren Lizenzierung Bedingungen für open-Source-Komponenten, die Sie ausgewählt haben, z. B. Microsoft R Open oder die Python-Anaconda-Verteilung.

5. Auf der **beinahe** Seite, notieren Sie sich den Installationsordner. Der Standardordner ist `~\Program Files\Microsoft\ML Server`.

    Wenn Sie den Installationsordner nicht ändern möchten, klicken Sie auf **erweitert** um zur ersten Seite des Assistenten zurückzukehren. Allerdings müssen Sie alle vorherigen Auswahl wiederholen.

6. Wenn Sie die offline-Komponenten installieren, können Sie für den Speicherort der erforderlichen Machine Learning Komponenten wie Microsoft R Open, Python-Server und Python-Open aufgefordert.

Klicken Sie während der Installation alle R oder Python-Bibliotheken, die von SQL Server verwendeten ersetzt werden, und Launchpad wird aktualisiert, um die neueren Komponenten verwenden. Daher werden, wenn die Instanz zuvor Bibliotheken im Standardordner R_SERVICES verwendet, nach dem Upgrade werden diese Bibliotheken entfernt, und die Eigenschaften für den Launchpad-Dienst geändert werden, um die Bibliotheken in den neuen Speicherort zu verwenden.

### <a name="bkmk_BindCmd"></a>Aktualisierung über die Befehlszeile

Wenn Sie nicht, um den Assistenten verwenden möchten, können Sie Machine Learning-Server installieren, und führen Sie das Tool SqlBindR.exe über die Befehlszeile zum Aktualisieren der Instanz.

> [!TIP]
> 
> Gefunden SqlBindR.exe wurde nicht? Sie haben wahrscheinlich nicht die oben aufgelisteten Komponenten heruntergeladen. Dieses Dienstprogramm ist nur mit Windows Installer für Machine Learning-Server verfügbar.

1. Öffnen Sie als Administrator eine Eingabeaufforderung und navigieren Sie zum Ordner, der „sqlbindr.exe“ enthält. Der Standardspeicherort ist `C:\Program Files\Microsoft\MLServer\Setup`

2. Geben Sie den folgenden Befehl ein, um eine Liste der verfügbaren Instanzen anzuzeigen: `SqlBindR.exe /list`
  
   Merken Sie sich den vollständigen aufgelisteten Namen der Instanz. Der Instanzname kann z. B., `MSSQL14.MSSQLSERVER` für eine Standardinstanz oder etwa `SERVERNAME.MYNAMEDINSTANCE`.

3. Führen Sie die **SqlBindR.exe** -Befehl mit der */bind* Argument, und geben Sie den Namen der Instanz für ein upgrade auf die Verwendung des Instanznamens, die im vorherigen Schritt zurückgegeben wurde.

   Um die Standardinstanz zu aktualisieren, z. B. Folgendes ein:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Starten Sie nach Abschluss des Upgrades den Launchpad-Dienst verknüpft sind mit jeder Instanz, die geändert wurde.

## <a name="bkmk_Unbind"></a>REVERT oder Aufheben der Bindung einer Instanz

Wenn Sie sich entscheiden, dass Sie nicht mehr Machine learning-Komponenten mithilfe von Machine Learning-Server aktualisieren möchten, müssen Sie zuerst _Bindung_ der Instanz und Machine Learning-Server deinstallieren.

+ Heben Sie die Bindung der Instanz

    Heben Sie die Bindung der Instanz und kehren Sie zu der ursprünglichen Bibliotheken, die von SQL Server installiert werden, mithilfe einer dieser beiden Methoden möglich:

    + [Verwenden Sie den Setupassistenten](#bkmk_wizunbind) für Machine Learning-Server, und deaktivieren Sie alle Funktionen auf der Instanz
    + [Verwenden Sie das Dienstprogramm SqlBindR](#bkmk_cmdunbind) mit der `/unbind` Argument, gefolgt vom Instanznamen.

    Beim Aufheben der Bindung Prozess abgeschlossen ist, werden zukünftige Machine learning-Upgrades, die basierend auf Machine Learning-Server nicht mehr auf die Instanz angewendet werden.

+ Deinstallieren Sie Machine Learning-Server

    Anweisungen hierzu finden Sie unter [deinstallieren Machine Learning-Server für Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-uninstall). 

### <a name="bkmk_wizunbind"></a> Aufheben der Bindung mithilfe des Assistenten

1. Suchen Sie das Installationsprogramm für Machine Learning-Server. Wenn Sie das Installationsprogramm entfernt haben, müssen Sie möglicherweise erneut herunterladen oder von einem anderen Computer zu kopieren.
2. Achten Sie darauf, dass Sie das Installationsprogramm auf dem Computer ausführen, der die Instanz verfügt, die Bindung aufgehoben werden soll.
2. Der Installer gibt die lokale Instanzen, die für die Bindung aufgehoben werden.
3. Deaktivieren Sie das Kontrollkästchen neben der Instanz, die die ursprüngliche Konfiguration wiederhergestellt werden soll.
4. Akzeptieren Sie den Lizenzvertrag. Sie müssen die Annahme der Lizenzbedingungen auch angeben, bei der Installation.
5. Klicken Sie auf **Fertig stellen**. Der Vorgang dauert eine Weile.

### <a name="bkmk_cmdunbind"></a> Aufheben der Bindung über die Befehlszeile

1. Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zu dem Ordner, der **sqlbindr.exe** enthält, wie im vorherigen Abschnitt beschrieben.

2. Führen Sie den Befehl **SqlBindR.exe** mit dem */unbind*-Argument aus, und geben Sie die Instanz an.

   Der folgende Befehl stellt z. B. die Standardinstanz wieder her:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

## <a name="known-issues"></a>Bekannte Probleme

Dieser Abschnitt enthält bekannte Probleme im Zusammenhang Verwendung des Hilfsprogramms SqlBindR.exe oder für Upgrades von Machine Learning-Server, die SQL Server-Instanzen beeinträchtigen können.

### <a name="restoring-packages-that-were-previously-installed"></a>Wiederherstellen von Paketen, die zuvor installiert wurden

In den Upgrade-Dienstprogramm, das mit Microsoft R Server 9.0.1 enthalten ist, das Hilfsprogramm die ursprünglichen Pakete nicht wiederhergestellt oder R-Komponenten vollständig zu erfordern, dass der Benutzer eine Reparatur an der Instanz ausführen Anwenden aller Service Releases, und klicken Sie dann die Instanz neu gestartet.

Die neueste Version des Hilfsprogramms Upgrade wird jedoch automatisch die ursprüngliche R-Funktionen wiederhergestellt. Aus diesem Grund sollten Sie nicht müssen R-Komponenten zu installieren oder ein patch installiert den Server neu. Allerdings müssen Sie alle R-Pakete installieren, die nach der Erstinstallation hinzugefügt wurden.

Wenn Sie zum Installieren und Freigeben von Paket die Paket-Verwaltungsrollen verwendet haben, ist diese Aufgabe sehr viel einfacher: Sie können R-Befehle verwenden, mit dem installierten Pakete im Dateisystem verwenden die Datensätze in der Datenbank synchronisiert und umgekehrt. Weitere Informationen finden Sie unter [paketverwaltung für SQL Server R](r-package-management-for-sql-server-r-services.md).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Probleme bei mehreren Upgrades von SQL Server

Wenn Sie beim Ausführen von mit dem neuen Installers für Microsoft R Server 9.1.0 zuvor eine Instanz von SQL Server 2016 R Services zu 9.0.1 aktualisiert haben, zeigt eine Liste aller gültigen Instanzen und wählt dann standardmäßig bereits gebundenen Instanzen aus. Wenn Sie den Vorgang fortsetzen, sind die zuvor gebundenen Instanzen aufgehoben. Als Ergebnis der früheren 9.0.1 Installation entfernt wird, einschließlich aller Pakete verknüpft, aber die neue Version von Microsoft R Server (9.1.0) ist nicht installiert.

Dieses Problem zu umgehen können Sie die vorhandene Installation von R-Server wie folgt ändern:
1. Öffnen Sie in der Systemsteuerung **Software**.
2. Suchen von Microsoft R Server, und klicken Sie auf **ändern "/" ändern**.
3. Wenn das Installationsprogramm gestartet wird, wählen Sie die Instanzen, die Sie an 9.1.0 binden möchten.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Binden oder Aufheben der Bindung bewirkt, dass mehrere temporären Ordner

Treten ggf. Fehler bei der Bindung und Aufheben der Bindung Vorgänge zum Bereinigen von temporären Ordner.
Wenn Sie den Ordner mit einem Namen wie folgt finden, können Sie es nach der Installation entfernen: `R_SERVICES_<guid>`

> [!NOTE]
> Achten Sie darauf warten, bis die Installation abgeschlossen ist. Es dauert sehr lange zum Entfernen von R-Bibliotheken, die eine Version zugeordnet, und fügen Sie dann die neuen R-Bibliotheken. Wenn der Vorgang abgeschlossen ist, werden temporäre Ordner entfernt.

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe-Befehlssyntax

### <a name="usage"></a>Verwendung

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameter

|Name|Description|
|------|------|
|*list*| Zeigt eine Liste aller SQL-Datenbankinstanz-IDs auf dem aktuellen Computer an|
|*bind*| Aktualisiert die angegebene SQL-Datenbankinstanz auf die neueste Version von R Server und stellt sicher, dass die Instanz automatisch zukünftige Upgrades von R Server erhält|
|*unbind*|Die neueste Version von R Server wird auf der angegebenen SQL-Datenbankinstanz deinstalliert, und es wird verhindert, dass zukünftige R Server-Upgrades auf die Instanz angewandt werden|

### <a name="errors"></a>Fehler

Die Abfrage gibt die folgenden Fehlermeldungen zurück:

|Fehler|Lösung|
|------|------|
|Fehler beim Binden der Instanz| Die Instanz konnte nicht gebunden werden. Wenden Sie sich an den Support, um Unterstützung zu erhalten.|
|Die Instanz ist bereits gebunden| Sie haben den *bind* -Befehl ausgeführt, die angegebene Instanz ist aber bereits gebunden. Wählen Sie eine andere Instanz.|
|Die Instanz ist nicht gebunden| Sie haben den *unbind* -Befehl ausgeführt, die angegebene Instanz ist aber nicht gebunden. Wählen Sie eine andere, kompatible Instanz aus.|
|Keine gültige SQL-Instanz-ID| Möglicherweise haben Sie den Namen der Instanz falsch eingegeben. Führen Sie den Befehl erneut mit dem *list* -Argument aus, um die verfügbaren Instanz-IDs zu sehen.|
|Keine Instanzen gefunden| Auf diesem Computer befindet sich keine Instanz von SQL Server R Services.|
|In der Instanz muss eine kompatible Version von SQL R Services (In-Database) installiert sein.| Weitere Informationen finden Sie unter den Kompatibilitätsanforderungen in diesem Thema.|
|Fehler beim Aufheben der Bindung der Instanz| Die Bindung der Instanz konnte nicht aufgehoben werden. Wenden Sie sich an den Support, um Unterstützung zu erhalten.|
|Unerwarteter Fehler aufgetreten| Andere Fehler. Wenden Sie sich an den Support, um Unterstützung zu erhalten.  |
|Keine SQL-Instanzen gefunden| Auf diesem Computer befindet sich keine Instanz von SQL Server. |

Weitere Informationen finden Sie unter den Anmerkungen zur Version für Microsoft R Server:

+ [Bekannte Probleme in Machine Learning-Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)

+ [Ankündigungen von Funktionen aus der vorherigen Version von R-Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [Als veraltet markierte oder geänderten nicht mehr unterstützte Funktionen](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
