---
title: "&#220;berwachung von R Services mithilfe von benutzerdefinierten Berichten in Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "02/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# &#220;berwachung von R Services mithilfe von benutzerdefinierten Berichten in Management Studio
Um die Verwaltung von SQL Server R Services zu vereinfachen, hat das Produktteam eine Anzahl von benutzerdefinierten Berichten als Beispiele zur Verfügung gestellt, die Sie zu SQL Server Management Studios hinzufügen können. Dadurch können Sie Details für R Services anzeigen, z.B.:

- Eine Liste der aktiven R-Sitzungen
- Die R-Konfiguration der aktuellen Instanz
- Statistik über die Ausführung der R-Laufzeit
- Eine Liste der erweiterten Ereignisse bei R Services
- Eine Liste der R-Pakete, die auf der aktuellen Instanz installiert sind

In diesem Thema wird erklärt, wie Sie diese Berichte installieren und verwenden. Weitere Informationen über benutzerdefinierte Berichte in Management Studio finden Sie unter [Benutzerdefinierte Berichte in Management Studio](../../ssms/object/custom-reports-in-management-studio.md).

## <a name="how-to-install-the-reports"></a>So führen Sie die Installation von Berichten durch

Die Berichte wurden mithilfe von SQL Server Reporting Services erstellt, können aber direkt aus SQL Server Management Studio verwendet werden, selbst wenn Reporting Services nicht auf Ihrer Instanz installiert ist. 

So verwenden Sie die Berichte:

* Laden Sie die RDL-Dateien aus dem GitHub-Repository für SQL Server Produktbeispiele herunter.
* Fügen Sie die Dateien zum Ordner der benutzerdefinierten Berichten hinzu, der von SQL Server Management Studio verwendet wird.
* Öffnen Sie die Berichte in SQL Server Management Studio.


### <a name="step-1-download-the-reports"></a>Schritt 1: Herunterladen der Berichte

1. Öffnen Sie das GitHub-Repository, das Beispiele aller SQL Server-Produkte enthält, darunter auch Beispieldatenbanken. 
   + [Microsoft/sql-server-samples](https://github.com/Microsoft/sql-server-samples)
   + [SSMS Custom Reports](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/SSMS-Custom-Reports)
      
2. Sie können sich auch in GitHub anmelden, und eine lokale Verzweigung der Beispiele erstellen, um die Beispiele herunterzuladen. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>Schritt 2: Kopieren der Berichte in Management Studio

3. Suchen Sie den Ordner der benutzerdefinierten Berichte, der von SQL Server Management Studio verwendet wird. Standardmäßig werden benutzerdefinierte Berichte in diesem Ordner gespeichert:
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   Sie können jedoch einen anderen Ordner angeben, oder einen Unterordner erstellen.

4. Kopieren Sie die *.RDL-Dateien in den Ordner der benutzerdefinierten Berichte.


### <a name="step-3-run-the-reports"></a>Schritt 3: Ausführen der Berichte

5. Klicken Sie in Management Studio mit der rechten Maustaste auf den Knoten **Datenbanken** der Instanz, auf der Sie die Berichte ausführen möchten.
6. Klicken Sie auf **Berichte**, und klicken Sie dann auf **Benutzerdefinierte Berichte**. 
7. Suchen Sie im Dialogfeld **Datei öffnen** den Ordner mit den benutzerdefinierten Berichten.
8. Wählen Sie eine der RDL-Dateien aus, die Sie heruntergeladen haben, und klicken Sie dann auf **Öffnen**.

> [!IMPORTANT] Diese Berichte können bei manchen Remotedesktopsitzungen oder auf manchen Computern nicht verwendet werden, z.B. auf Computern mit Anzeigegeräten mit hohem DPI-Wert oder einer höheren Auflösung als 1080p. Es gibt einen Fehler im Berichtanzeige-Steuerelement in SSMS, der den Bericht abstürzen lässt.  


## <a name="report-list"></a>Berichtsliste

Das GitHub-Repository für Produktbeispiele enthält zur Zeit die folgenden Berichte für SQL Server R Services:

+ **R Services - Active Sessions** (R-Services – aktive Sitzungen)

  Verwenden Sie diesen Bericht, um die Benutzer anzuzeigen, die gerade mit der SQL-Instanz verbunden sind und R-Aufträge ausführen. 
  
+ **R Services - Configuration** (R-Services – Konfiguration)

  Verwenden Sie diesen Bericht, um die Eigenschaften der R-Laufzeit und der Konfiguration von R Services anzuzeigen. Dieser Bericht gibt an, ob ein Neustart erforderlich ist, und sucht nach erforderlichen Netzwerkprotokollen. 
  
  Die implizierte Authentifizierung ist für das Ausführen von R in einem SQL-Computekontext erforderlich. Der Bericht überprüft, ob eine Datenbankanmeldung für die Gruppe „SQLRUserGroup“ vorliegt, um das zu überprüfen.

  > [!NOTE] Weitere Informationen zu diesen Feldern finden Sie unter [Package metadata (Paketmetadaten)](http://r-pkgs.had.co.nz/description.html) von Hadley Wickam (in englischer Sprache). Zum Beispiel wurde das Feld *Spitzname* für die R-Laufzeit eingeführt, um die Unterscheidung zwischen den Releases zu vereinfachen. 

 + **R Services - Configure Instance** (R Services – Instanz konfigurieren) 

   Dieser Bericht soll Sie beim Konfigurieren von R Services nach der Installation unterstützen. Sie können ihn aus dem vorhergehenden Bericht ausführen, wenn R Services nicht korrekt konfiguriert ist.
 
+ **R Services - Execution Statistics** (R Services – Ausführungsstatistiken)

  Verwenden Sie diesen Bericht, um die Statistiken zur Ausführung von R Services anzuzeigen. Sie können z.B. die Gesamtzahl der R-Skripts, die ausgeführt wurden, die Anzahl der parallelen Ausführungen und die am häufigsten verwendeten RevoScaleR-Funktionen anzeigen lassen.
  Der Bericht überwacht derzeit nur die Statistiken für Funktionen aus dem RevoScaleR-Paket.
  Klicken Sie auf **View SQL Script (SQL-Skript anzeigen)**, um T-SQL-Code für diesen Bericht zu erhalten. 

+ **R Services - Extended Events** (R Services – Erweiterte Ereignisse)

  Verwenden Sie diesen Bericht, um eine Liste der erweiterten Ereignisse anzuzeigen, die für die Überwachung der Ausführung des R-Skripts verfügbar sind. 
  Klicken Sie auf **View SQL Script (SQL-Skript anzeigen)**, um T-SQL-Code für diesen Bericht zu erhalten.

+ **R Services - Packages** (R Services – Pakete)

  Verwenden Sie diesen Bericht zum Anzeigen einer Liste der R-Pakete, die auf der SQL Server-Instanz installiert sind. Derzeit enthält der Bericht diese Paketeigenschaften: 
  + Paket (Name)
  + Version 
  + Depends (Abhängig)
  + License (Lizenz)
  + Built (Erstellt)
  + Lib Path (Bibliothekspfad)

+ **R Services - Resource Usage** (R-Services – Ressourcenverwendung)

  Verwenden Sie diesen Bericht, um den Verbrauch von CPU, Arbeitsspeicher, und E/A-Ressourcen durch die Ausführung von SQL Server R-Skripts anzuzeigen. Sie können auch die Einstellung für den Speicher von externen Ressourcenpools anzeigen. 


## <a name="see-also"></a>Siehe auch

[Monitoring R Services (Überwachung von R-Diensten)](../../advanced-analytics/r-services/monitoring-r-services.md)

[Extended events for R Services (Erweiterte Ereignisse bei R Services)](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)