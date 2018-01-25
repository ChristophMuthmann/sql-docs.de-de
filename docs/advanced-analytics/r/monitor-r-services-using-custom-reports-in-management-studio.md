---
title: "Überwachung von R Services mithilfe von benutzerdefinierten Berichten in Management Studio | Microsoft-Dokumentation"
ms.custom: 
ms.date: 10/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 141d0e3114a59a9b280ceee6d599f97ef16919c7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>Überwachen von Machine Learning Services mithilfe benutzerdefinierter Berichte in Management Studio

Zum Verwalten von für Machine learning verwendeten Instanz zu vereinfachen, wurde das Produktteam hat eine Reihe von benutzerdefinierten Beispielberichten bereitgestellt, die Sie für SQL Server Management Studio hinzufügen können. In diesen Berichten können Sie Details wie z. B. anzeigen:

- Aktive R oder Python-Sitzungen
- Konfigurationseinstellungen für die Instanz
- Ausführungsstatistiken für Machine Learning-Aufträge
- Erweiterte Ereignisse für R Services
- R oder Python-Pakete, die auf die aktuelle Instanz installiert

In diesem Artikel wird erläutert, wie zum Installieren und verwenden die benutzerdefinierten Berichte, die speziell für Computer Leaerning bereitgestellt wird. 

Eine allgemeine Einführung in die Berichte in Management Studio finden Sie unter [benutzerdefinierte Berichte in Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>So führen Sie die Installation von Berichten durch

Die Berichte wurden mithilfe von SQL Server Reporting Services erstellt, können aber direkt aus SQL Server Management Studio verwendet werden, selbst wenn Reporting Services nicht auf Ihrer Instanz installiert ist. 

So verwenden Sie die Berichte:

* Laden Sie die RDL-Dateien aus dem GitHub-Repository für SQL Server Produktbeispiele herunter.
* Fügen Sie die Dateien zum Ordner der benutzerdefinierten Berichten hinzu, der von SQL Server Management Studio verwendet wird.
* Öffnen Sie die Berichte in SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Schritt 1: Herunterladen der Berichte

1. Öffnen Sie die GitHub-Repository, enthält [SQL Server Product Samples](https://github.com/Microsoft/sql-server-samples), und zum Herunterladen von Beispielberichten. 

    + [Benutzerdefinierte Berichte von SSMS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > Die Berichte können mit SQL Server 2017 Machiine Learning Services oder SQL Server 2016-R-Services verwendet werden.

2. Sie können sich auch in GitHub anmelden, und eine lokale Verzweigung der Beispiele erstellen, um die Beispiele herunterzuladen. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>Schritt 2: Kopieren der Berichte in Management Studio

3. Suchen Sie den Ordner der benutzerdefinierten Berichte, der von SQL Server Management Studio verwendet wird. Standardmäßig werden benutzerdefinierte Berichte in diesem Ordner gespeichert:
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   Sie können jedoch einen anderen Ordner angeben, oder einen Unterordner erstellen.

4. Kopieren Sie die *.RDL-Dateien in den Ordner der benutzerdefinierten Berichte.


### <a name="step-3-run-the-reports"></a>Schritt 3: Ausführen der Berichte

5. Klicken Sie in Management Studio mit der rechten Maustaste auf den Knoten **Datenbanken** der Instanz, auf der Sie die Berichte ausführen möchten.
6. Klicken Sie auf **Berichte**, und klicken Sie dann auf **Benutzerdefinierte Berichte**.
7. Suchen Sie im Dialogfeld **Datei öffnen** den Ordner mit den benutzerdefinierten Berichten.
8. Wählen Sie eine der RDL-Dateien aus, die Sie heruntergeladen haben, und klicken Sie dann auf **Öffnen**.

> [!IMPORTANT]
> Diese Berichte können bei manchen Remotedesktopsitzungen oder auf manchen Computern nicht verwendet werden, z.B. auf Computern mit Anzeigegeräten mit hohem DPI-Wert oder einer höheren Auflösung als 1080p. Es gibt einen Fehler im Berichtanzeige-Steuerelement in SSMS, der den Bericht abstürzen lässt.

## <a name="report-list"></a>Berichtliste

Der Product Samples-Repository in GitHub enthält zurzeit die folgenden Berichte:

+ **R Services - Active Sessions**

  Verwenden Sie diesen Bericht, um die Benutzer anzuzeigen, die aktuell ausgeführten Machine learning-Aufträge und SQL Server-Instanz verbunden sind. 
  
+ **R Services - Configuration**

  Verwenden Sie diesen Bericht, um die Konfiguration des externen Skriptlaufzeit und zugehöriger Dienste anzuzeigen. Dieser Bericht gibt an, ob ein Neustart erforderlich ist, und sucht nach erforderlichen Netzwerkprotokollen. 
  
  Implizite Authentifizierung ist erforderlich für Machine Learning-Aufgaben, die in SQL Server als computekontext ausgeführt. Um zu überprüfen, dass die implizite Authentifizierung konfiguriert ist, überprüft der Bericht an, ob eine Datenbank-Anmeldung für die Gruppe SQLRUserGroup vorhanden ist.

 + **R Services - Configure Instance** 

   Dieser Bericht ist vorgesehen, helfen Ihnen beim Machine Learning zu konfigurieren. Sie können diesen Bericht zum Beheben von Konfigurationsfehlern in den vorangehenden Bericht gefunden auch ausführen.
 
+ **R Services - Execution Statistics**

  Mithilfe dieses Berichts Ausführungsstatistiken für Machine Learning-Aufträge anzeigen. Sie können z.B. die Gesamtzahl der R-Skripts, die ausgeführt wurden, die Anzahl der parallelen Ausführungen und die am häufigsten verwendeten RevoScaleR-Funktionen anzeigen lassen. Klicken Sie auf **SQL-Skript anzeigen** den vollständigen T-SQL-Code hinter diesen Bericht abgerufen.

  Der Bericht überwacht derzeit nur die Statistiken für Funktionen aus dem RevoScaleR-Paket.

+ **R Services - Extended Events**

  Verwenden Sie diesen Bericht, um eine Liste der erweiterten Ereignisse anzuzeigen, die für die Überwachung von Aufgaben im Zusammenhang mit externen Skript Laufzeiten verfügbar sind. Klicken Sie auf **SQL-Skript anzeigen** den vollständigen T-SQL-Code hinter diesen Bericht abgerufen.

+ **R Services - Packages**

  Verwenden Sie diesen Bericht zum Anzeigen einer Liste der R oder Python-Pakete, die auf SQL Server-Instanz installiert.

+ **R Services - Resource Usage**

  Mithilfe dieses Berichts Verbrauch von CPU, Arbeitsspeicher und e/a-Ressourcen durch Ausführen des externen Skripts anzuzeigen. Sie können auch die Einstellung für den Speicher von externen Ressourcenpools anzeigen.

## <a name="see-also"></a>Siehe auch

[Monitoring R Services (Überwachung von R-Diensten)](../../advanced-analytics/r-services/monitoring-r-services.md)

[Extended events for R Services (Erweiterte Ereignisse bei R Services)](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)
