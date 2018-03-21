---
title: "Upgrade und Installation häufig gestellte Fragen zur SQL Server-Machine Learning | Microsoft Docs"
ms.date: 03/15/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 3cbb94081b2d056128fb4beda413c82cd4a20964
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>Upgrade und Installation häufig gestellte Fragen zur SQL Server-Machine Learning oder R-Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieses Thema enthält Antworten auf einige häufig gestellte Fragen zur Installation von Machine learning-Funktionen in SQL Server. Außerdem werden häufige gestellte Fragen zu Upgrades behandelt.

+ Einige Probleme auftreten, nur beim Upgrade älterer Versionen. Aus diesem Grund wird empfohlen, dass Sie die Version und-Edition zuerst identifizieren, bevor diese Hinweise zu lesen. Führen Sie zum Abrufen von Versionsinformationen `@@VERSION` in einer Abfrage in SQL Server Management Studio.
+ Aktualisieren Sie auf die neueste Version oder die Dienstversion so bald wie möglich, so beheben Sie alle Probleme, die in neueren Versionen behoben wurden.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Services (Datenbankintern)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>Anforderungen und Einschränkungen unter älteren Versionen von SQL Server 2016 

Abhängig von der Build von SQL Server, die installiert werden, kann die folgenden Einschränkungen gelten:

- In frühen Versionen von SQL Server 2016 R Services wurde 8.3-Notation auf dem Laufwerk erforderlich, die das Arbeitsverzeichnis enthält. Wenn Sie eine Vorabversion installiert haben, sollte ein Upgrade auf SQL Server 2016 Service Pack 1 dieses Problem beheben. Diese Anforderung gilt nicht für Versionen nach SP1.

- Seite-an-Seite-Installation eine andere Version von R oder mit anderen Versionen von Revolution Analytics, wird nicht unterstützt.

- Deaktivieren Sie vor dem Setup Virenscan. Wenn Setup abgeschlossen ist, sollten Sie bis zum Anhalten der Scan für die Ordner, in [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]. Vorzugsweise anhalten-Überprüfung wird auf die gesamte [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)] Struktur.

 - Installieren von Microsoft R Server in einer Instanz von SQL Server unter Windows Core installiert. In der RTM-Version von SQL Server 2016 lag ein bekanntes Problem beim Hinzufügen von Microsoft R Server für eine Instanz auf Windows Server Core-Edition. Dies wurde behoben. Wenn dieses Problem auftritt, können, wenden Sie das Update, die in beschriebenen [KB3164398](https://support.microsoft.com/kb/3164398) Feature "R" mit der vorhandenen Instanz unter Windows Server Core hinzu. Weitere Informationen finden Sie unter [Microsoft R Server (eigenständig) kann nicht auf einem Windows Server Core-System installiert werden](https://support.microsoft.com/kb/3168691).


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>Offline-Installation von Machine Learning-Komponenten für eine lokalisierte Version von SQL Server 2016

Frühe Version Versionen von SQL Server 2016 Fehler beim Installieren von gebietsschemaspezifische CAB-Dateien während der offline-Installation ohne eine Internetverbindung. Dieses Problem wurde in späteren Versionen behoben, aber wenn das Installationsprogramm eine Meldung, die besagt, dass es nicht die richtige Sprache installieren können gibt, können Sie einen Dateinamen, um das Setup fortgesetzt bearbeiten.

+ Manuell bearbeiten Sie, die Installationsdatei, um sicherzustellen, dass die richtige Sprache installiert ist. Angenommen, um die japanische Version von SQL Server zu installieren, ändern Sie den Namen der Datei aus SRS_8.0.3.0_**1033**CAB zum SRS_8.0.3.0_**1041**CAB.
+ Die Sprachen-ID, die für Machine learning-Komponenten verwendet, muss die Sprache der SQL Server-Setup identisch sein, oder Sie nicht Setup abgeschlossen.

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>Vorabversionen: unterstützen von Richtlinien, Aktualisierung und bekannte Probleme

Neue Installationen von alle Vorabversionen von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] wird nicht mehr unterstützt. Wenn Sie eine Vorabversion verwenden, aktualisieren Sie so bald wie möglich.

Dieser Abschnitt enthält detaillierte Anweisungen für bestimmte Szenarien für das Upgrade an.

### <a name="how-to-upgrade-sql-server"></a>Gewusst wie: upgrade von SQL Server

Sie können Ihre Version von SQL Server aktualisieren, indem Sie den Setup-Assistenten erneut ausführen.

+ [Aktualisieren von SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [Aktualisieren von SQLServer mithilfe des Installations-Assistenten](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

Sie können nur die computerlernverfahren Komponenten mithilfe des so genannten Bindung aktualisieren: 
+ [Verwenden Sie SqlBindR Upgrade Machine Learning-Komponenten](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>Ende des Supports für direkte Upgrades von Vorabversionen

Upgrades von Vorabversionen von SQL Server 2016 werden nicht mehr unterstützt. Hierzu zählen SQL Server 2016 CTP3, CTP3. 1, CTP3. 2, RC0 oder RC1.

Die folgenden Versionen wurden mit Vorabversionen von SQL Server 2016 installiert.

| Version | Erstellen         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

Wenn Sie nur die geringste Möglichkeit haben, welche Version Sie verwenden, führen Sie `@@VERSION` in einer Abfrage in SQL Server Management Studio.

Im Allgemeinen ist der Prozess für das Upgrade wie folgt ein:

1. Sichern Sie Skripts und Daten.
2. Deinstallieren Sie die Vorabversion.
3. Installieren Sie eine veröffentlichte Version.

Deinstallieren einer Vorabversion von SQL Server von Machine Learning-Komponenten können komplex sein und erfordert unter Umständen ein spezielles Skript ausführen. Technischen Support um Unterstützung zu erhalten.

###  <a name="bkmk_Uninstall"></a> Deinstallieren Sie vor dem Upgrade von einer älteren Version von Microsoft R Server

Wenn Sie eine Vorabversion von Microsoft R Server installiert haben, müssen Sie diese deinstallieren, bevor Sie auf eine neuere Version aktualisieren können.

1.  Klicken Sie in der **Systemsteuerung**auf **Programme hinzufügen/entfernen**, und wählen Sie `Microsoft SQL Server 2016 <version number>`aus.

2.  Wählen Sie im Dialogfeld mit den Optionen zum **Hinzufügen**, **Reparieren**oder **Entfernen** von Komponenten die Option **Entfernen**aus.
  
3.  Wählen Sie auf der Seite **Funktionen auswählen** unter **Freigegebene Funktionen**die Option **R Server (eigenständig)**aus. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen** , um nur die ausgewählten Komponenten zu deinstallieren.

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services und R-Server (eigenständig)-Seite-an-Seite-Fehler 

Beim Installieren von R Server (eigenständig) und R Services (Datenbankintern) zur gleichen Zeit manchmal in früheren Versionen von SQL Server 2016 verursacht Setup mit der Fehlermeldung "Zugriff verweigert" fehl. Dieses Problem wurde in Service Pack 1 für SQL Server 2016 behoben.

Wenn Sie diesen Fehler und diese Funktionen zu aktualisieren müssen, führen Sie eine Slipstream-Installation von SQL Server 2016 mit SP1. Es gibt zwei Möglichkeiten zum Beheben des Problems, die beides erforderlich, deinstallieren und neu installieren.

1. Deinstallieren Sie R Services (Datenbankintern), und stellen Sie sicher, dass die Benutzerkonten für SQLRUserGroup entfernt werden.

2. Starten Sie den Server neu, und installieren Sie R-Server (eigenständig).

3. Ausführen von SQL Server setup einmal, und wählen Sie dieses Mal **Hinzufügen von Funktionen zu einer vorhandenen SQL Server**.

4. Wählen Sie die Instanz, und wählen Sie dann die **R Services (Datenbankintern)** Option zum Hinzufügen.

Wenn diese Prozedur nicht das Problem zu beheben, versuchen Sie die folgende problemumgehung:

1. Deinstallieren Sie R Services (Datenbankintern) und R-Server (eigenständig) gleichzeitig aus.

2. Entfernen Sie die lokalen Benutzerkonten (SQLRUserGroup).

3. Starten Sie den Server neu.

4. Führen Sie SQL Server-Setup, und fügen Sie nur die R-Services (Datenbankintern)-Funktion. Aktivieren Sie nicht **R Server (eigenständig)**.

Im Allgemeinen wird empfohlen, dass Sie R Services (Datenbankintern) und R-Server (eigenständig) nicht installieren auf dem gleichen Computer. Vorausgesetzt, dass der Server über ausreichend Kapazität verfügt, können Sie jedoch feststellen, dass eigenständigen R-Server als ein Entwicklungstool von Nutzen sein kann. Eine andere besteht mögliche, müssen Sie die Funktionen operationalisierung von R-Server verwenden, aber auch SQL Server-Daten ohne Verschieben von Daten zugreifen möchten.

## <a name="incompatible-version-of-r-client-and-r-server"></a>Inkompatible Version von R Client und R Server

Wenn Sie Microsoft-R-Client installieren und sie zum Ausführen von R in einen remote SQL Server-computekontext verwenden, erhalten Sie möglicherweise einen Fehler wie folgt:

*Sie sind Version 9.0.0 von Microsoft R-Client auf Ihrem Computer ausführen, die mit dem Microsoft R Server 8.0.3-Version nicht kompatibel ist. Laden Sie eine kompatible Version herunter und installieren Sie sie.*

In SQL Server 2016 war es erforderlich, dass die Version von R, die in SQL Server R Services ausgeführt wurde wie die Microsoft-R-Client-Bibliotheken identisch sein. Diese Anforderung wurde in höheren Versionen entfernt. Wir empfehlen jedoch, dass Sie immer die neuesten Versionen des Machine learning-Komponenten erhalten, und installieren Sie alle Servicepacks. 

Wenn Sie eine frühere Version von Microsoft R Server aufweisen und Kompatibilität mit Microsoft R Client 9.0.0 sicherstellen müssen, installieren Sie die Updates, die beschrieben werden, in diesem [Support-Artikel](https://support.microsoft.com/kb/3210262).


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>Installation schlägt fehl mit dem Fehler „Es kann jeweils nur ein Revolution Enterprise-Produkt installiert werden.“

Dieser Fehler kann auftreten, wenn Sie eine ältere Installation von Revolution Analytics-Produkten oder eine Vorabversion von SQL Server R Services verwenden. Sie müssen alle früheren Versionen deinstallieren, bevor Sie eine neuere Version von Microsoft R Server installieren können. Eine parallele Installation mit anderen Versionen der Revolution Enterprise-Tools wird nicht unterstützt.

Parallele Installationen werden jedoch unterstützt, wenn R Server (eigenständig) mit [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] oder SQL Server 2016 verwendet wird.

## <a name="registry-cleanup-to-uninstall-older-components"></a>Registry-Bereinigung, um ältere Komponenten zu deinstallieren

Wenn Sie Probleme beim Entfernen einer älteren Version haben, müssen Sie unter Umständen die Registrierung bearbeiten, um betroffene Schlüssel zu entfernen.

> [!IMPORTANT]
> Dieses Problem tritt nur auf, wenn Sie eine Vorabversion von Microsoft R Server oder eine CTP-Version von SQL Server 2016 R Services installiert haben.
  
1. Öffnen Sie die Windows-Registrierung, und suchen Sie folgenden Schlüssel: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
2. Löschen Sie einen der folgenden Einträge, wenn er vorhanden ist und der Schlüssel nur den Wert `sEstimatedSize2`enthält:
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (für 8.0.2)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (für 8.0.1)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (für 8.0.0)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (für 7.5.0)

## <a name="see-also"></a>Siehe auch

 [SQL Server-Machine Learning-Services (Datenbankintern)](../r/sql-server-r-services.md)

 [SQL Server-Machine Learning-Server (eigenständig)](../r/r-server-standalone.md)
