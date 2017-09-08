---
title: Machine Learning-Komponenten in SQL Server-Instanz aktualisieren | Microsoft Docs
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9d7ddd95bdbcf6efca98ed94bc305924902b98
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>Aktualisieren des Machine Learning-Komponenten in SQL Server-Instanz

Microsoft Machine Learning-Server für Windows enthält ein Tool, das Sie zum Aktualisieren der R-Komponenten mit einer Instanz von SQL Server verwenden können. Es gibt zwei Versionen des Tools: Assistenten, und ein Befehlszeilen-Hilfsprogramm.

In diesem Artikel wird beschrieben, wie Sie diese Tools verwenden, um eine kompatible Instanz von SQL Server zu aktualisieren, und wie eine Instanz wiederherstellen, die zuvor ein Upgrade ausgeführt wurde.

Sie müssen nicht durch diesen Prozess zu verwenden, wenn Upgrades als Teil von SQL Server-Updates abgerufen werden soll. Wenn Sie ein neues Servicepack oder Service Version installieren, werden die Machine Learning-Komponenten immer automatisch auf die neueste Version aktualisiert. Verwenden Sie nur diese Proess auf, wenn Sie Komponenten mit einer schnellere Geschwindigkeit als Affored von SQL Server Service Releases ist aktualisieren möchten.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

> [!NOTE]
> Zum Zeitpunkt der Verfassung dieses Artikels gelten Upgrades nur für kompatible SQL Server 2016-Instanzen.  Upgrade für SQL Server-2017 wird zwar unterstützt, wurde eine neue Version des Microsoft Machine Learning-Server zur Verwendung für Upgrades nicht freigegeben.

## <a name="upgrade-an-instance"></a>Aktualisieren einer Instanz

Im Rahmen des Upgradeprozesses die Verfügbarkeitsklasse **Bindung**, da sie das Modell Unterstützung für SQL Server Machine Learning Komponenten, die neue moderne Lifecycle-Richtlinie ändert. Das Upgrade ändert sich jedoch nicht auf das Modell Unterstützung für SQL Server-Datenbank aus.

Dieses Lizenzierungssystem stellt allgemein sicher, dass Ihre Datenanalysten stets die neueste Version von R verwenden. Weitere Informationen über die Bedingungen der Modern Lifecycle-Richtlinie finden Sie unter [Support Timeline for Microsoft R Server (Zeitachse für die Unterstützung für Microsoft R Server)](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support).

Wenn Sie eine Instanz binden, passieren mehrere Dinge:

+ Das Supportmodell geändert wird. Anstatt auf SQL Server-Dienst-Versionen, basiert die Unterstützung auf die neue moderne Lifecycle-Richtlinie.
+ Machine learning-Komponenten, mit der Instanz wird automatisch mit jedem Release, im Gleichschritt mit der Version aktualisiert werden, die unter der neuen, modernen Lifecycle-Richtlinie aktuell ist. 
+ Neue R oder Python-Pakete können hinzugefügt werden. Z. B. vorherige Updates von Microsoft R Server hinzugefügt neue R-Pakete, z. B. [MicrosoftML](../using-the-microsoftml-package.md), [OlapR](../r/how-to-create-mdx-queries-using-olapr.md), und [Sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md).
+ Die Instanz kann nicht mehr manuell aktualisiert werden, außer wenn Sie neue Pakete hinzufügen.
+ Sie haben die Möglichkeit vortrainierte Modelle hinzufügen.

Wenn Sie später entscheiden, dass Sie beenden die Instanz mit jeder neuen Version aktualisieren möchten, müssen Sie **Bindung** der Instanz, wie in beschrieben [in diesem Abschnitt](#bkmk_Unbind), und deinstallieren Sie Machine learning Upgrades, wie beschrieben In diesem Artikel: [führen Microsoft R Server für Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows). Wenn der Prozess abgeschlossen ist, werden zukünftige Machine learning-Upgrades, die basierend auf Machine Learning-Server nicht mehr auf die Instanz angewendet.

### <a name="bkmk_prereqs"></a>Voraussetzungen für das upgrade

1. Identifizieren von Instanzen, die für ein Upgrade in Frage kommen.
    + SQL Server 2016 mit installiertem R Services
    + Mindestens Service Pack 1 plus CU3

2. Abrufen **Microsoft R Server**, durch die separate Windows Installer herunterladen.

    [So installieren Sie R Server 9.0.1 unter Windows mithilfe des eigenständigen Windows Installers](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)

> [!TIP]
> 
> Gefunden SqlBindR.exe wurde nicht? Sie haben wahrscheinlich R Server noch nicht heruntergeladen. Dieses Dienstprogramm ist nur mit Windows Installer für Microsoft R Server verfügbar.

### <a name="bkmk_BindWizard"></a>Aktualisieren Sie mit dem Setup-Assistenten

1. Starten Sie mit dem neuen Installer für R-Server, auf dem Computer mit der Instanz, die Sie aktualisieren möchten.
  ![Microsoft R Server-Setup-Assistenten](media/r-server-installer-01.PNG)
2. Akzeptieren Sie den Lizenzvertrag für Microsoft R Server 9.1.0, und klicken Sie auf **Weiter**.
3. Akzeptieren Sie die Lizenzierung Bedingungen für die open-Source-R-Komponenten, und klicken Sie auf **Weiter**.
4. Auf **Installationsordner auswählen**, akzeptieren Sie die Standardeinstellungen, oder geben Sie einen anderen Speicherort, in dem R-Bibliotheken installiert werden soll. 
5. Das Installationsprogramm wird jede lokalen Instanzen identifizieren, Kandidaten für die Bindung. Wenn keine Instanzen angezeigt werden, bedeutet dies, dass keine gültigen Instanzen gefunden wurden. Sie müssen möglicherweise Patch für den Server, oder Überprüfen Sie, ob die R-Services installiert wurde.
6. Wählen Sie das Kontrollkästchen neben einer beliebigen Instanz, die Sie verwenden möchten, aktualisieren, und klicken Sie auf **Weiter**.
7. Der Prozess kann eine Weile dauern.
    
    Während der Installation werden von SQL Server R Services verwendete R-Bibliotheken mit den Bibliotheken für Microsoft R Server 9.1.0 ersetzt.
    
    Launchpad wird durch den Prozess nicht betroffen, aber die Bibliotheken im Ordner "R_SERVICES" entfernt werden und die Eigenschaften für den Dienst werden geändert, um die Bibliotheken in `C:\Program Files\Microsoft\R Server\R_SERVER`.

### <a name="bkmk_BindCmd"></a>Aktualisierung über die Befehlszeile

Nach der Installation von Microsoft R Server können Sie nur die SqlBindR.exe-Tool über die Befehlszeile ausführen.

1. Öffnen Sie als Administrator eine Eingabeaufforderung und navigieren Sie zum Ordner, der „sqlbindr.exe“ enthält. Der Standardspeicherort ist`C:\Program Files\Microsoft\R Server\Setup`
2. Geben Sie den folgenden Befehl ein, um eine Liste der verfügbaren Instanzen anzuzeigen: `SqlBindR.exe /list`
  
   Merken Sie sich den vollständigen aufgelisteten Namen der Instanz. Der Instanzname kann z. B., `MSSQL13.MSSQLSERVER` für die Standardinstanz oder etwa `SERVERNAME.MYNAMEDINSTANCE`.
3. Führen Sie den Befehl **SqlBindR.exe** mit dem */bind*-Argument aus, und geben Sie den Namen der zu aktualisierenden Instanz an, wie er im vorherigen Schritt zurückgegeben wurde.

   Um die Standardinstanz zu aktualisieren, z. B. Folgendes ein:`SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
4. Wenn das Upgrade abgeschlossen ist, starten Sie den Launchpad-Dienst neu, der mit einer beliebigen aktualisierten Instanz verknüpft ist.


## <a name="bkmk_Unbind"></a>REVERT oder Aufheben der Bindung einer Instanz

Zum Wiederherstellen von einer Instanz von SQL Server verwendet die ursprünglichen Bibliotheken, die von SQL Server installiert, müssen Sie die Ausführen einer **Bindung** Vorgang. Sie können entweder durch erneute Ausführung des Setup-Assistenten für Microsoft R Server oder durch Ausführen des Hilfsprogramms SqlBindR über die Befehlszeile erfolgen.

Beim Aufheben der Bindung ist abgeschlossen, die Bibliotheken für Microsoft R Server 9.1.0 werden entfernt und der ursprünglichen R-Bibliotheken, die von SQL Server R Services verwendete wiederhergestellt werden.

Die Eigenschaften des SQL Server-LaunchPads R_SERVICES, in der R-Bibliotheken im Ordner "Standard" verwenden bearbeitet werden `C:\Program Files\Microsoft\R Server\R_SERVER`.

### <a name="unbind-using-the-wizard"></a>Aufheben der Bindung mithilfe des Assistenten

1. Mit dem neuen Installer für Microsoft R Server 9.1.0 herunterladen
2. Führen Sie das Installationsprogramm auf dem Computer mit der Instanz, die Sie Bindung aufheben möchten.
2. Das Installationsprogramm wird lokale Instanzen identifiziert, die für die Bindung aufgehoben werden.
3. Deaktivieren Sie das Kontrollkästchen neben der Instanz, die die ursprüngliche SQL Server R Services-Konfiguration wiederhergestellt werden soll.
4. Akzeptieren Sie den Lizenzvertrag für Microsoft R Server 9.1.0. Auch wenn Sie R-Server entfernen möchten, müssen Sie den Lizenzvertrag akzeptieren.
5. Klicken Sie auf **Fertig stellen**. Der Vorgang dauert eine Weile.

### <a name="unbind-using-the-command-line"></a>Aufheben der Bindung über die Befehlszeile

1. Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zu dem Ordner, der **sqlbindr.exe** enthält, wie im vorherigen Abschnitt beschrieben.

2. Führen Sie den Befehl **SqlBindR.exe** mit dem */unbind*-Argument aus, und geben Sie die Instanz an.

   Der folgende Befehl stellt z. B. die Standardinstanz wieder her:
   
    `SqlBindR.exe /unbind MSSQL13.MSSQLSERVER`

## <a name="known-issues"></a>Bekannte Probleme

Dieser Abschnitt enthält bekannte Probleme im Zusammenhang Verwendung des Hilfsprogramms SqlBindR.exe oder für Upgrades mit dem Microsoft R Server-Setup-Hilfsprogramm, die SQL Server-Instanzen zu beeinflussen.

### <a name="restoring-packages-that-were-previously-installed"></a>Wiederherstellen von Paketen, die zuvor installiert wurden

In den Upgrade-Dienstprogramm, das mit Microsoft R Server 9.0.1 enthalten ist, das Hilfsprogramm die ursprünglichen Pakete nicht wiederhergestellt oder R-Komponenten vollständig zu erfordern, dass der Benutzer eine Reparatur an der Instanz ausführen Anwenden aller Service Releases, und klicken Sie dann die Instanz neu gestartet.

Allerdings wird die neueste Version des Hilfsprogramms Upgrade für Microsoft R Server 9.1.0, die ursprüngliche R-Funktionen automatisch wiederhergestellt. Aus diesem Grund sollten Sie nicht müssen R-Komponenten zu installieren oder ein patch installiert den Server neu. Allerdings müssen Sie dennoch alle R-Pakete installieren, die nach der Erstinstallation hinzugefügt wurden.

Wenn Sie zum Installieren und Freigeben von Paket die Paket-Verwaltungsrollen verwendet haben, ist diese Aufgabe sehr viel einfacher: Sie können R-Befehle verwenden, mit dem installierten Pakete im Dateisystem verwenden die Datensätze in der Datenbank synchronisiert und umgekehrt. Weitere Informationen finden Sie unter [installieren und Verwalten von R-Paketen](installing-and-managing-r-packages.md)

### <a name="cannot-perform-upgrade-from-901"></a>Upgrade kann nicht von 9.0.1 ausgeführt werden.

Wenn Sie beim Ausführen von mit dem neuen Installers für Microsoft R Server 9.1.0 zuvor eine Instanz von SQL Server 2016 R Services zu 9.0.1 aktualisiert haben, werden eine Liste aller gültigen Instanzen anzeigen und wählen Sie dann in der Standardeinstellung bereits gebundene Instanzen. Wenn Sie den Vorgang fortsetzen, sind die zuvor gebundenen Instanzen aufgehoben. Als Ergebnis der früheren 9.0.1 Installation entfernt wird, einschließlich aller Pakete verknüpft, aber die neue Version von Microsoft R Server (9.1.0) ist nicht installiert.

Dieses Problem zu umgehen können Sie die vorhandene Installation von R-Server wie folgt ändern:
1. Öffnen Sie in der Systemsteuerung **Software**.
2. Suchen von Microsoft R Server, und klicken Sie auf **ändern "/" ändern**.
3. Wenn das Installationsprogramm gestartet wird, wählen Sie die Instanzen, die Sie an 9.1.0 binden möchten.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>Binden oder Aufheben der Bindung bewirkt, dass mehrere temporären Ordner

Treten ggf. Fehler bei der Bindung und Aufheben der Bindung Vorgänge zum Bereinigen von temporären Ordner.
Wenn Sie den Ordner mit einem Namen wie folgt finden, können Sie es nach der Installation entfernen:`R_SERVICES_<guid>`

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

+ [Was ist neu in R-Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [R-Server, die bekannte Probleme](https://docs.microsoft.com/r-server/resources-known-issues)

