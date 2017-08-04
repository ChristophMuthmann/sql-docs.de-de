---
title: Herstellen einer Verbindung mit einer ODBC-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4d1a2374d480f2d6b886425a02cb590b00b3564a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer ODBC-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **ODBC** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten.

Möglicherweise wird den ODBC-Treiber zu laden, müssen von Microsoft oder von einem Drittanbieter stammen.

Möglicherweise müssen auch die erforderlichen Verbindungsinformationen zu suchen, die Sie bereitstellen. Diese Drittanbieter-Website - [der Zeichenfolgen-Verbindungsverweis](https://www.connectionstrings.com/) -enthält Beispiele für Verbindungszeichenfolgen und Weitere Informationen zu Datenanbietern und die Verbindungsinformationen, die sie benötigen.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Stellen Sie sicher, den Treiber gewünschten installiert ist
1.  Suchen, oder navigieren Sie zu der **ODBC-Datenquellen (64-Bit)** in der Systemsteuerung. Wenn Sie nur einen 32-Bit-Treiber, oder Sie wissen, dass Sie einen 32-Bit-Treiber verwenden, suchen, oder navigieren Sie zu **ODBC-Datenquellen (32-Bit)** stattdessen.
2.  Starten Sie das Applet ". Die **ODBC-Datenquellenadministrator** Fenster wird geöffnet.
3.  Auf der **Treiber** Registerkarte finden Sie eine Liste aller ODBC-Treiber, die auf Ihrem Computer installiert. (Die Namen einiger der Treiber können in mehreren Sprachen aufgelistet werden.)

    Hier ist ein Beispiel für die Liste der installierten 64-Bit-Treiber.

    ![64-Bit-ODBC-Treiber installiert](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Wenn Sie wissen, dass des Treibers installiert und nicht im 64-Bit-Applet wird angezeigt, suchen Sie in der 32-Bit-Applet stattdessen. Dies darüber hinaus erfahren Sie, ob Sie die 64-Bit oder 32-Bit SQL Server-Import / Export-Assistenten ausführen müssen.
    
## <a name="step-1---select-the-data-source"></a>Schritt 1: Wählen Sie die Datenquelle
Die ODBC-Treiber auf dem Computer installiert sind nicht in der Dropdown-Liste der Datenquellen aufgeführt. Um mit einem ODBC-Treiber eine Verbindung herzustellen, starten Sie dazu die **.NET Framework-Datenanbieter für ODBC** als Datenquelle für die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite des Assistenten. Dieser Anbieter dient als Wrapper um die ODBC-Treiber.

Hier ist die generische Bildschirm sofort nach der Auswahl der .NET Framework-Datenanbieter für ODBC.

![Herstellen einer Verbindung mit SQL mit ODBC vor](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Schritt 2: Geben Sie die Verbindungsinformationen
Der nächste Schritt ist der ODBC-Treiber und die Datenquelle die Verbindungsinformationen bereit. Hierfür stehen zwei Möglichkeiten zur Verfügung:
1.  Geben Sie eine **DSN** (Data Source Name), die bereits vorhanden ist, oder, die Sie erstellen, mit der **ODBC-Datenquellenadministrator** in der Systemsteuerung. Ein DSN ist die gespeicherte Auflistung von Einstellungen für die Verbindung mit einer ODBC-Datenquelle.

    Wenn Sie bereits den DSN-Namen kennen oder wissen, wie Sie einen neuen DSN jetzt erstellen, können Sie den Rest dieser Seite überspringen. Geben Sie den DSN-Namen in der **Dsn** Feld der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite, und klicken Sie dann mit dem nächsten Schritt des Assistenten fortfahren.

    [Geben Sie einen DSN](#odbc_dsn)
    
2.  Geben Sie einen **Verbindungszeichenfolge**, suchen Sie online, oder erstellen und Testen auf dem Computer mit der **ODBC-Datenquellen-Administrator** Applet ".

    Wenn Sie bereits die Verbindungszeichenfolge haben oder wissen, wie Sie es erstellen, können Sie den Rest dieser Seite überspringen. Geben Sie die Verbindungszeichenfolge in der **"ConnectionString"** Feld der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite, und klicken Sie dann mit dem nächsten Schritt des Assistenten fortfahren.

    [Geben Sie eine Verbindungszeichenfolge](#odbc_connstring)

Wenn Sie eine Verbindungszeichenfolge zur Verfügung stellen die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite zeigt alle Verbindungsinformationen, die der Assistent für die Verbindung zur Datenquelle, z. B. den Servernamen und den Authentifizierungsmodus für den Server und Datenbank Methode verwenden soll. Wenn Sie einen DSN angeben, ist diese Informationen nicht sichtbar.

## <a name="odbc_dsn"></a>Option 1: Bereitstellen von einem DSN
Wenn Sie die Verbindungsinformationen mit einem DSN (Data Source Name) bieten möchten, verwenden Sie die **ODBC-Datenquellenadministrator** Applet ", um den Namen des vorhandenen DSN finden oder einen neuen DSN erstellen.
1.  Suchen, oder navigieren Sie zu der **ODBC-Datenquellen (64-Bit)** in der Systemsteuerung. Wenn Sie nur einen 32-Bit-Treiber besitzen, oder einen 32-Bit-Treiber verwenden, suchen, oder navigieren Sie zu **ODBC-Datenquellen (32-Bit)** stattdessen.
2.  Starten Sie das Applet ". Die **ODBC-Datenquellenadministrator** Fenster wird geöffnet. Im folgenden wird das Applet "aussieht.

    ![Systemsteuerungs-Applets für ODBC-Administrator](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Nach Bedarf **verwenden Sie einen vorhandenen DSN** für Ihre Datenquelle anzuwenden, können Sie alle DSN, der auf die **Benutzer-DSN**, **System-DSN**, oder **Datei-DSN** Registerkarte. Überprüfen Sie den Namen, und klicken Sie dann zum Assistenten zurückkehren, und geben Sie ihn in die **Dsn** Feld der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Überspringen Sie den Rest dieser Seite, und mit dem nächsten Schritt des Assistenten fortfahren.
4.  Wenn Sie möchten **erstellen Sie einen neuen DSN**, entscheiden Sie, ob es sichtbar sein sollen nur für Sie (Benutzer-DSN) für alle Benutzer des Computers sichtbar einschließlich Windows-Dienste (System-DSN) oder in einer Datei (Datei-DSN) gespeichert. Dieses Beispiel erstellt ein neues System-DSN.
5. Auf der **System-DSN** auf **hinzufügen**.

    ![Fügen Sie einen neuen ODBC-System-DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  In der **erstellen Sie eine neue Datenquelle** (Dialogfeld), wählen Sie die Treiber für die Datenquelle aus, und klicken Sie auf **Fertig stellen**.

    ![Wählen Sie die Treiber für das neue System-DSN](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. Der Treiber zeigt jetzt ein oder mehrere Treiber-spezifische Bildschirme, in dem Sie die Verbindung mit Ihrer Datenquelle erforderliche Informationen eingeben. (Für den SQL Server-Treiber angenommen, es gibt vier Seiten des benutzerdefinierten Einstellungen.) Wenn Sie fertig sind, wird das neue System DSN in der Liste angezeigt.

    ![Neue System-DSN in Liste](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Wechseln Sie zurück zu den Assistenten, und geben Sie den DNS-Namen in der **Dsn** Feld der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Mit dem nächsten Schritt des Assistenten fortfahren.

## <a name="odbc_connstring"></a>Option 2: Geben Sie eine Verbindungszeichenfolge
Wenn Sie die Verbindungsinformationen mit einer Verbindungszeichenfolge angeben möchten, können Sie mithilfe von im weiteren Verlauf dieses Themas auf Abrufen der Verbindungszeichenfolge, die Sie benötigen.

In diesem Beispiel geht die folgende Verbindungszeichenfolge verwendet wird, die eine Verbindung mit Microsoft SQL Server herstellt.

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

Geben Sie die Verbindungszeichenfolge in der **"ConnectionString"** Feld der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite. Nachdem Sie die Verbindungszeichenfolge eingeben, wird der Assistent analysiert die Zeichenfolge und zeigt die einzelnen Eigenschaften und ihre Werte in der Liste.

Hier ist der Bildschirm, den nach dem Eingeben der Verbindungszeichenfolge angezeigt.

![Herstellen einer Verbindung mit SQL mit ODBC nach](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> Die Verbindungsoptionen für einen ODBC-Treiber sind identisch, ob Sie die Quelle oder Ziel konfigurieren. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

## <a name="get-the-connection-string-online"></a>Abrufen der Verbindungszeichenfolge online
Verbindungszeichenfolgen für die ODBC-Treiber online finden Sie unter [der Zeichenfolgen-Verbindungsverweis](https://www.connectionstrings.com/). Diese Site eines Drittanbieters enthält Beispiele für Verbindungszeichenfolgen und Weitere Informationen zu Datenanbietern und die Verbindungsinformationen, die sie benötigen.

## <a name="get-the-connection-string-with-an-app"></a>Hiermit rufen Sie die Verbindungszeichenfolge mit einer app
Zum Erstellen und testen die Verbindungszeichenfolge für die ODBC-Treiber auf dem lokalen Computer, können Sie die **ODBC-Datenquellenadministrator** in der Systemsteuerung. Erstellen Sie eine Datei-DSN für Ihre Verbindung, und kopieren Sie die Einstellungen aus der Datei-DSN, um die Verbindungszeichenfolge zu assemblieren. Dies sind mehrere Schritte erforderlich, jedoch können Sie sicherstellen, dass Sie eine gültige Verbindungszeichenfolge verfügen.

1.  Suchen, oder navigieren Sie zu der **ODBC-Datenquellen (64-Bit)** in der Systemsteuerung. Wenn Sie nur einen 32-Bit-Treiber besitzen, oder einen 32-Bit-Treiber verwenden, suchen, oder navigieren Sie zu **ODBC-Datenquellen (32-Bit)** stattdessen.
2.  Starten Sie das Applet ". Die **ODBC-Datenquellenadministrator** Fenster wird geöffnet.
3.  Lesen Sie jetzt die **Datei-DSN** des Applets an. Klicken Sie auf **Hinzufügen**.

    In diesem Beispiel erstellen Sie einen Datei-DSN anstelle einer Benutzer-DSN oder System-DSN, da die Datei-DSN, die Name-Wert-Paare in das Format der Verbindungszeichenfolge erforderlich speichert.

    ![Fügen Sie eine neue ODBC-Dateidatenquelle hinzu](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  In der **neue Datenquelle erstellen** (Dialogfeld), wählen Sie in der Liste den Treiber, und klicken Sie dann auf **Weiter**. In diesem Beispiel soll ein DSN zu erstellen, die den Argumenten für Verbindungszeichenfolgen enthält, die Verbindung mit Microsoft SQL Server erforderlich.

    ![Erstellen Sie neue ODBC-Datenquelle](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Wählen Sie einen Speicherort, und geben Sie einen Dateinamen für die neue Datei-DSN, und klicken Sie dann auf **Weiter**. Denken Sie daran, in dem Sie die Datei speichern, damit Sie ihn finden und öffnen Sie es in einem nachfolgenden Schritt können.

    ![Speichern Sie die neue Datei-DSN](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Überprüfen Sie die Zusammenfassung der Auswahl, und klicken Sie dann auf **Fertig stellen**.

7.  Nachdem Sie auf **Fertig stellen**, der Treiber, die Sie ausgewählt zeigt einen oder mehrere proprietären Bildschirme, um die Informationen zu sammeln, es eine Verbindung herstellen muss. In der Regel umfasst diese Infos Server, Anmeldeinformationen und Datenbank zum Server-basierten Datenquellen und Datei, Format und Version für einen dateibasierten Datenquellen.

8. Nachdem Sie Ihre Datenquelle konfigurieren, und klicken Sie auf **Fertig stellen**, in der Regel finden Sie eine Zusammenfassung der Auswahl und haben die Möglichkeit, die sie testen.

    ![Neuen Test-Datei-DSN](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Nachdem Sie Ihre Datenquelle testen, und schließen Sie die Dialogfelder, suchen Sie die Datei-DSN, wo Sie es im Dateisystem gespeichert. Wenn Sie nicht die Dateierweiterung geändert haben, ist die Standardeinstellung. DSN.

10. Öffnen Sie die gespeicherte Datei mit Editor oder einem anderen Texteditor. Folgen Sie den Inhalt der SQL Server-Beispiel.

        [ODBC]  
        DRIVER=ODBC Driver 13 for SQL Server  
        TrustServerCertificate=No  
        DATABASE=WideWorldImporters    
        WSID=<local computer name>  
        APP=Microsoft® Windows® Operating System  
        Trusted_Connection=Yes  
        SERVER=localhost   
        
11. Kopieren Sie die erforderlichen Werte in einer Verbindungszeichenfolge, in der die Name-Wert-Paare durch Semikolons getrennt sind.

    Nachdem Sie die erforderlichen Werte aus der Beispieldatei-DSN zusammentragen, müssen Sie die folgende Verbindungszeichenfolge.
    
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes

    In der Regel erforderlich nicht alle Einstellungen in einem DSN, der von ODBC-Datenquellen-Administrator um eine Verbindungszeichenfolge zu erstellen, die funktioniert erstellt.  
    -   Sie müssen immer die ODBC-Treiber angeben.
    -   Für eine serverbasierte Datenquelle wie SQL Server benötigen Sie in der Regel Server, Datenbank und Anmeldeinformationen. Im Beispiel DSN "TrustServerCertificate" WSID oder Anwendung erforderlich.
    -   Für eine dateibasierte Datenquelle müssen Sie mindestens die Namen und Speicherort einreichen.
    
12. Fügen Sie diese Verbindungszeichenfolge in der **"ConnectionString"** Feld der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite des Assistenten. Der Assistent analysiert die Zeichenfolge, und jetzt können Sie den Vorgang fortzusetzen.

    ![Herstellen einer Verbindung mit SQL mit ODBC nach](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



