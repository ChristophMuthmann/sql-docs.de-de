---
title: Herstellen einer Verbindung mit einer ODBC-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9a7692c229728e97bc830020d6ec2cdc35843af4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer ODBC-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **ODBC**-Datenquelle von den Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen.

Möglicherweise müssen Sie den ODBC-Treiber bei Microsoft oder einem Drittanbieter herunterladen.

Außerdem müssen Sie gegebenenfalls nachsehen, welche Verbindungsinformationen erforderlich sind. Auf der Website [The Connection Strings Reference (Verweis auf Verbindungszeichenfolgen)](https://www.connectionstrings.com/) eines Drittanbieters sind Beispielverbindungszeichenfolgen aufgelistet, und es werden Informationen zu Datenanbietern und den erforderlichen Verbindungsinformationen gegeben.

## <a name="make-sure-the-driver-you-want-is-installed"></a>Sicherstellen, dass der gewünschte Treiber installiert ist
1.  Suchen Sie in den Einstellungen nach, oder navigieren Sie zu dem Applet **ODBC-Datenquellen (64-Bit)**. Wenn Sie nur über einen 32-Bit-Treiber verfügen, oder Sie wissen, dass Sie einen 32-Bit-Treiber verwenden müssen, suchen Sie stattdessen nach, oder navigieren Sie zu **ODBC-Datenquellen (32-Bit)**.
2.  Starten Sie das Applet. Das Fenster **ODBC-Datenquellen-Administrator** wird geöffnet.
3.  Auf der Registerkarte **Treiber** finden Sie eine Liste aller auf Ihrem Computer installierten ODBC-Treiber. (Die Namen einiger Treiber werden möglicherweise in mehreren Sprachen aufgeführt.)

    In der folgenden Abbildung ist ein Beispiel für eine Liste mit installierten 64-Bit-Treibern dargestellt.

    ![Installierte 64-Bit-ODBC-Treiber](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> Wenn Sie sicher sind, dass ein bestimmter Treiber installiert wurde, er aber im 64-Bit-Applet nicht angezeigt wird, prüfen Sie stattdessen das 32-Bit-Applet. Mithilfe dieses Applets erfahren Sie, ob Sie die 64-Bit- oder die 32-Bit-Version des SQL Server-Import/Export-Assistenten ausführen müssen.
>
> Sie müssen SQL Server installieren, um die 64-Bit-Version des SQL Server-Import/Export-Assistenten verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.
    
## <a name="step-1---select-the-data-source"></a>Schritt 1: Auswählen der Datenquelle
Die auf Ihrem Computer installierten ODBC-Treiber werden in der Dropdownliste der Datenquellen nicht aufgeführt. Wählen Sie zunächst **.NET Framework-Datenanbieter für ODBC** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten als Datenquelle aus, um eine Verbindung mit einem ODBC-Treiber herzustellen. Dieser Anbieter dient als Wrapper für den ODBC-Treiber.

In der folgenden Abbildung wird die generische Anzeige dargestellt, die Ihnen unmittelbar angezeigt wird, nachdem Sie „.NET Framework-Datenanbieter für ODBC“ ausgewählt haben.

![Herstellen einer Verbindung mit SQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>Schritt 2: Bereitstellen der Verbindungsinformationen
Im nächsten Schritt stellen Sie die Verbindungsinformationen für Ihren ODBC-Treiber und die Datenquelle bereit. Hierfür stehen zwei Möglichkeiten zur Verfügung:
1.  Geben Sie einen **DSN** (Datenquellennamen) ein, der bereits vorhanden ist, oder den Sie in den Einstellungen mithilfe des Applets **ODBC-Datenquellen-Administrator** erstellen. Ein Datenquellenname ist eine gespeicherte Auflistung von Einstellungen, die zum Herstellen einer Verbindung mit einer ODBC-Datenquelle erforderlich sind.

    Wenn Sie den DSN-Namen bereits kennen, oder Sie wissen, wie man einen neuen DSN erstellt, können Sie die restliche Seite überspringen. Geben Sie in das Feld **DSN** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** einen DSN ein, und fahren Sie dann im Assistenten mit dem nächsten Schritt fort.

    [Bereitstellen eines DSN](#odbc_dsn)
    
2.  Geben Sie eine **Verbindungszeichenfolge** ein, die Sie online suchen, oder auf Ihrem Computer mit dem Applet **ODBC-Datenquellen-Administrator** erstellen und testen können.

    Wenn Sie bereits über eine Verbindungszeichenfolge verfügen, oder Sie wissen, wie Sie eine erstellen, können Sie die restliche Seite überspringen. Geben Sie in das Feld **ConnectionString** auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** die Verbindungszeichenfolge ein, und gehen Sie dann im Assistenten zum nächsten Schritt.

    [Bereitstellen einer Verbindungszeichenfolge](#odbc_connstring)

Wenn Sie eine Verbindungszeichenfolge eingegeben haben, werden auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** sämtliche Verbindungsinformationen angezeigt, die der Assistent zum Herstellen einer Verbindung mit der Datenquelle verwenden wird, z.B. Server- und Datenbankname und Authentifizierungsmethode. Wenn Sie einen DSN eingeben, werden diese Informationen nicht angezeigt.

## <a name="odbc_dsn"></a> Option 1: Bereitstellen eines DSN
Wenn Sie die Verbindungsinformationen über einen Datenquellennamen bereitstellen möchten, verwenden Sie das Applet **ODBC-Datenquellen-Administrator**, um den Namen des bestehenden DSN zu finden oder einen neuen zu erstellen.
1.  Suchen Sie in den Einstellungen nach, oder navigieren Sie zu dem Applet **ODBC-Datenquellen (64-Bit)**. Wenn Sie nur über einen 32-Bit-Treiber verfügen oder Sie einen 32-Bit-Treiber verwenden müssen, suchen Sie stattdessen nach, oder navigieren Sie zu **ODBC-Datenquellen (32-Bit)**.
2.  Starten Sie das Applet. Das Fenster **ODBC-Datenquellen-Administrator** wird geöffnet. Das Applet sieht wie folgt aus.

    ![Applet „ODBC-Administratoreinstellungen“](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  Wenn Sie für Ihre Datenquelle einen **bereits vorhandenen DSN** verwenden möchten, können Sie jeden DSN verwenden, der in den Registerkarten **Benutzer-DSN**, **System-DSN** oder **Datei-DSN** angezeigt wird. Überprüfen Sie den Namen, wechseln Sie dann zurück zum Assistenten, und geben Sie diesen in das Feld **DSN** oder auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** ein. Überspringen Sie die restliche Seite, und fahren Sie mit dem nächsten Schritt des Assistenten fort.
4.  Wenn Sie einen **neuen DSN erstellen** möchten, wählen Sie aus, ob dieser nur für Sie (Benutzer-DSN) oder alle Benutzer des Computers, einschließlich Windows-Diensten, (System-DSN) sichtbar sein oder in einer Datei gespeichert sein soll (Datei-DSN). In diesem Beispiel wird ein neuer System-DSN erstellt.
5. Klicken Sie auf der Registerkarte **System-DSN** auf **Hinzufügen**.

    ![Hinzufügen einer neuen ODBC-System-DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  Wählen Sie im Dialogfeld **Neue Datenquelle erstellen** den Treiber für Ihre Datenquelle aus, und klicken Sie anschließend auf **Fertig stellen**.

    ![Auswählen des Treibers für einen neuen System-DSN](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. Der Treiber zeigt mindestens eine treiberspezifische Ansicht an, in der Sie die Informationen eingeben, die zum Herstellen einer Verbindung mit der Datenquelle erforderlich sind. (Für den SQL Server-Treiber sind beispielsweise vier Seiten mit benutzerdefinierten Einstellungen verfügbar.) Nachdem Sie den Vorgang fertig gestellt haben, wird der neue System-DSN in der Liste angezeigt.

    ![Neuer System-DSN in der Liste](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  Gehen Sie zurück zum Assistenten, und geben Sie den Datenquellennamen in das Feld **DSN** oder auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** ein. Fahren Sie mit dem nächsten Schritt des Assistenten fort.

## <a name="odbc_connstring"></a> Option 2: Bereitstellen einer Verbindungszeichenfolge
Wenn Sie die Verbindungsinformationen über eine Verbindungszeichenfolge bereitstellen möchten, lesen Sie diesem Artikel, um zu erfahren, wie Sie die notwendige Verbindungzeichenfolge abrufen.

In diesem Beispiel wir die folgende Verbindungszeichenfolge verwendet, die eine Verbindung mit Microsoft SQL Server herstellt.

    ```
    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
    ```

Geben Sie die Verbindungszeichenfolge in das **ConnectionString**-Feld auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** ein. Nach der Eingabe der Verbindungszeichenfolge analysiert der Assistent die Zeichenfolge und zeigt die einzelnen Eigenschaften und deren Werte in der Liste an.

In der folgenden Abbildung wird die Ansicht dargestellt, die Ihnen angezeigt wird, nachdem Sie die Verbindungszeichenfolge eingegeben haben.

![Herstellen einer Verbindung mit SQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> Die Verbindungsoptionen für einen OBCD-Treiber bleiben stets unverändert – egal, ob Sie die Quelle oder das Ziel konfigurieren. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

## <a name="get-the-connection-string-online"></a>Abrufen der Verbindungszeichenfolge online
Auf der Website [The Connection Strings Reference (Verweis auf Verbindungszeichenfolgen)](https://www.connectionstrings.com/) finden Sie online Verbindungszeichenfolgen für den ODBC-Treiber. Auf dieser Website eines Drittanbieters sind Beispielverbindungszeichenfolgen aufgelistet, und es werden Angaben zu Datenanbietern und den erforderlichen Verbindungsinformationen bereitgestellt.

## <a name="get-the-connection-string-with-an-app"></a>Abrufen der Verbindungszeichenfolge über eine App
Sie können das Applet **ODBC-Datenquellen-Administrator** in den Einstellungen verwenden, um eine Verbindungszeichenfolge für Ihren ODBC-Treiber auf Ihrem Computer zu erstellen und zu testen. Erstellen Sie einen Datei-DSN für Ihre Verbindung, und kopieren Sie die Einstellungen des Datei-DSN anschließend, um die Verbindungszeichenfolge zu assemblieren. Dafür müssen Sie zwar mehrere Schritte ausführen, aber dieser Vorgang hilft Ihnen dabei, eine gültige Verbindungszeichenfolge zu erstellen.

1.  Suchen Sie in den Einstellungen nach, oder navigieren Sie zu dem Applet **ODBC-Datenquellen (64-Bit)**. Wenn Sie nur über einen 32-Bit-Treiber verfügen oder Sie einen 32-Bit-Treiber verwenden müssen, suchen Sie stattdessen nach, oder navigieren Sie zu **ODBC-Datenquellen (32-Bit)**.
2.  Starten Sie das Applet. Das Fenster **ODBC-Datenquellen-Administrator** wird geöffnet.
3.  Gehen Sie jetzt zur Registerkarte **Datei-DSN** des Applets. Klicken Sie auf **Hinzufügen**.

    Erstellen Sie für dieses Beispiel besser einen Datei-DSN als einen Benutzer-DSN oder einen System-DSN, da der Datei-DSN dieselben Name/Wert-Paare in dem für die Verbindungszeichenfolge erforderlichen Format speichert.

    ![Hinzufügen eines neuen ODBC-Datei-DSN](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  Wählen Sie im Dialogfeld **Neue Datenquelle erstellen** den Treiber aus der Liste aus, und klicken Sie anschließend auf **Weiter**. In diesem Beispiel wird ein DSN erstellt, der die Verbindungszeichenargumente enthält, die zum Herstellen einer Verbindung mit Microsoft SQL Server benötigt werden.

    ![Erstellen einer neuen ODBC-Standarddatenquelle](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  Wählen Sie einen Speicherort aus, geben Sie einen Dateinamen für den neuen Datei-DSN ein, und klicken Sie anschließend auf **Weiter**. Merken Sie sich den Speicherort der Datei, damit Sie diese später wiederfinden können, und öffnen Sie sie in einem nachfolgenden Schritt.

    ![Speichern eines neuen Datei-DSN](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  Lesen Sie sich die Zusammenfassung für Ihre Auswahl durch, und klicken Sie anschließend auf **Fertig stellen**.

7.  Nachdem Sie auf **Fertig stellen** geklickt haben, zeigt der von Ihnen ausgewählte Treiber mindestens eine proprietäre Ansicht an, um die Informationen zu erfassen, die für das Herstellen einer Verbindung benötigt werden. In der Regel umfassen diese Informationen Server- und Anmeldeinformationen sowie die Datenbank für serverbasierte Datenquellen und die Datei, das Format und die Version für dateibasierte Datenquellen.

8. Nach dem Konfigurieren Ihrer Datenquelle, und nachdem Sie auf **Fertig stellen** geklickt haben, wird Ihnen in der Regel eine Zusammenfassung Ihrer Auswahl angezeigt, und es wird Ihnen die Möglichkeit geboten, diese zu testen.

    ![Speichern eines neuen Datei-DSN](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. Nachdem Sie die Datenquellen getestet und die Dialogfelder geschlossen haben, gehen Sie zum Speicherort der Datei-DSN auf dem Dateisystem. Wenn Sie die Dateierweiterungen nicht geändert haben, lautet die Standarderweiterung „.dsn“.

10. Öffnen Sie die gespeicherte Datei im Editor oder einem anderen Text-Editor. Im Folgenden werden die Inhalte des SQL Server-Beispiels angezeigt.

    ```   
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=Microsoft® Windows® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. Kopieren Sie die nötigen Werte, und fügen Sie sie in eine Verbindungszeichenfolge ein, in der die Name/Wert-Paare durch Semikolons getrennt werden.

    Nachdem Sie die benötigten Werte aus der Beispiel-DSN-Datei assembliert haben, verfügen Sie über die folgende Verbindungszeichenfolge.
    
        ```
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
        ```

    Sie benötigen nicht alle Einstellungen in einem DSN, der vom ODBC-Datenquellen-Administrator erstellt wurde, um eine funktionierende Verbindungszeichenfolge zu erstellen.  
    -   Sie müssen stets den ODBC-Treiber angeben.
    -   Für eine serverbasierte Datenquelle wie SQL Server benötigen Sie in der Regel Server-, Datenbank- und Anmeldeinformationen. Das heißt, Sie benötigen im Beispiel-DSN weder TrustServerCertificate noch WSID noch APP.
    -   Für eine dateibasierte Datenquelle benötigen Sie mindestens den Dateinamen und den -speicherort.
    
12. Fügen Sie die Verbindungszeichenfolge in das **ConnectionString**-Feld auf den Seiten **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten ein. Der Assistent analysiert die Zeichenfolge. Damit ist der Vorgang abgeschlossen, und Sie können fortfahren.

    ![Herstellen einer Verbindung mit SQL mithilfe von ODBC](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


