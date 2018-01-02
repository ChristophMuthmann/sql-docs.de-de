---
title: "Aktualisiert: Integration Services für SQL Server-Dokumentation | Microsoft-Dokumentation"
description: "Sie können sich Ausschnitte der kürzlich aktualisierten Inhalte in der Dokumentation zu Integration Services für Microsoft SQL Server anzeigen lassen."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: integration-services
ms.openlocfilehash: 9660fa7239c14c3adc963cc75ceb98de8316734c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>Neu und kürzlich aktualisiert: Integration Services für SQL Server



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **28.09.2017** &nbsp; – bis – &nbsp; **02.12.2017**
- *Themenbereich:* &nbsp; **Integration Services für SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Speichern und Abrufen von Dateien auf lokalen Dateifreigaben und Dateifreigaben in Azure mit SSIS](lift-shift/ssis-azure-files-file-shares.md)
2. [Überprüfen von in Azure bereitgestellten SSIS-Paketen](lift-shift/ssis-azure-validate-packages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Hadoop-Verbindungs-Manager](#TitleNum_1)
2. [Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-hadoop-connection-managerconnection-managerhadoop-connection-managermd"></a>1. &nbsp; [Hadoop-Verbindungs-Manager](connection-manager/hadoop-connection-manager.md)

*Aktualisiert: 28.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 65.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2d68f4e884304f1a28045b42b680c15cc6a41ec5 fb2429466ea4d545682975d8dbea47451ce98ec7  (PR=4113  ,  Filename=hadoop-connection-manager.md  ,  Dirpath=docs\integration-services\connection-manager\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



**Herstellen einer Verbindung mit der Kerberos-Authentifizierung**

Es gibt zwei Möglichkeiten, um die lokale Umgebung so einzurichten, dass Sie die Kerberos-Authentifizierung mit dem Hadoop-Verbindungs-Manager verwenden können. Sie können die Option wählen, die besser auf Ihre Anforderungen zugeschnitten ist.
-   Option 1: [Einbinden des SSIS-Computers in den Kerberos-Bereich--#kerberos-join-realm)
-   Option 2: [Aktivieren von gegenseitiger Vertrauensstellung zwischen der Windows-Domäne und dem Kerberos-Bereich--#kerberos-mutual-trust)

**<a name="kerberos-join-realm"></a>Option 1: Einbinden des SSIS-Computers in den Kerberos-Bereich**


**Anforderungen:**


-   Der Gatewaycomputer muss in den Kerberos-Bereich eingebunden und kann nicht in Windows-Domänen eingebunden werden.

**Vorgehensweise zur Konfiguration:**


**Gehen Sie auf dem SSIS-Computer wie folgt vor:**

1.  Führen Sie das **Ksetup**-Hilfsprogramm aus, um den Kerberos-KDC-Server (Key Distribution Center) und -Bereich zu konfigurieren.

    Der Computer muss als Mitglied einer Arbeitsgruppe konfiguriert werden, da sich ein Kerberos-Bereich von einer Windows-Domäne unterscheidet. Legen Sie wie im folgenden Beispiel gezeigt den Kerberos-Bereich fest, und fügen Sie einen KDC-Server hinzu. Ersetzen Sie *REALM.COM* ggf. durch Ihren eigenen entsprechenden Bereich.

```
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
```

    Restart the computer after executing these two commands.

2.  Überprüfen Sie die Konfiguration mit dem **Ksetup**-Befehl. Die Ausgabe sollte wie im folgenden Beispiel aussehen:

```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
```

**<a name="kerberos-mutual-trust"></a>Option 2: Aktivieren von gegenseitiger Vertrauensstellung zwischen der Windows-Domäne und dem Kerberos-Bereich**


**Anforderungen:**

-   Der Gatewaycomputer muss in eine Windows-Domäne eingebunden werden.
-   Sie benötigen die Berechtigung zum Aktualisieren der Einstellungen des Domänencontrollers.

**Vorgehensweise zur Konfiguration:**


> [!NOTE]
> Ersetzen Sie REALM.COM und AD.COM im folgenden Tutorial ggf. durch Ihren eigenen Bereich und Domänencontroller.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authenticationlift-shiftssis-azure-connect-with-windows-authmd"></a>2. &nbsp; [Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung](lift-shift/ssis-azure-connect-with-windows-auth.md)

*Aktualisiert: 27.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_1))

<!-- Source markdown line 66.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 673386fca53cb60b983e0cb3cd4b9e2ee1dee0de 65458b4dceb92d01184c5e9c6f68ec0e8f16ba08  (PR=4104  ,  Filename=ssis-azure-connect-with-windows-auth.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=19e1c4067142d33e8485cb903a7a9beb7d894015) -->



**Herstellen einer Verbindung mit einem lokalem SQL Server**

Führen Sie folgende Schritte aus, um zu überprüfen, ob Sie eine Verbindung mit einem lokalen SQL Server herstellen können:

1.  Suchen Sie einen Computer, der nicht in eine Domäne eingebunden ist, um diesen Test auszuführen.

2.  Führen Sie auf dem Computer, der nicht in eine Domäne eingebunden ist, folgenden Befehl aus, um SQL Server Management Studio (SSMS) mit den Anmeldeinformationen für die Domäne zu starten, die Sie verwenden möchten:

```
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
```

3.  Überprüfen Sie über SSMS, ob Sie eine Verbindung mit dem lokalen SQL Server herstellen können, den Sie verwenden möchten.

**Herstellen einer Verbindung mit einer lokalen Dateifreigabe**

Führen Sie die folgenden Schritte durch, um zu überprüfen, ob Sie eine Verbindung mit einer lokalen Dateifreigabe herstellen können:

1.  Suchen Sie einen Computer, der nicht in eine Domäne eingebunden ist, um diesen Test auszuführen.

2.  Führen Sie den folgenden Befehl auf dem Computer aus, der nicht in eine Domäne eingebunden ist. Über diesen Befehl öffnen Sie zunächst ein Eingabeaufforderungsfenster mit den Anmeldeinformationen der Domäne, die Sie verwenden möchten, und testen dann die Konnektivität mit der Dateifreigabe, indem Sie eine Verzeichnisliste abrufen.

```
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
```

3.  Überprüfen Sie, ob die Verzeichnisliste für die lokale Dateifreigabe zurückgegeben wird, die Sie verwenden möchten.

**Herstellen einer Verbindung mit einer Dateifreigabe auf einer Azure-VM**

Führen Sie die folgenden Schritte durch, um eine Verbindung mit einer Dateifreigabe auf einer Azure-VM herzustellen:

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet.

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die gespeicherte Prozedur `catalog.set_execution_credential` aus, wie in den folgenden Optionen beschrieben:

```
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
```

**Herstellen einer Verbindung mit einer Dateifreigabe in Azure Files**

Weitere Informationen zu Azure Files finden Sie unter [Azure Files](https://azure.microsoft.com/services/storage/files/).







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neu + Aktualisiert (3+14): Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (1+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (1+0): Analysis Services für SQL-Dokumente)](../analysis-services/new-updated-analysis-services.md)
- [Neu + Aktualisiert (87+0): Dokumente zu **Analyseplattformsystem für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu + Aktualisiert (5+4): Dokumente zu **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu + Aktualisiert (0+1): Dokumente zum **Datenbankmodul für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu + Aktualisiert (2+2):Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu + Aktualisiert (10+9): Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu + Aktualisiert (2+4): Dokumente zu **Relationale Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu + Aktualisiert (4+2): Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu + Aktualisiert (0+1): Dokumente zu **Beispiele für SQL**](../sample/new-updated-sample.md)
- [Neu + Aktualisiert (21+0): Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu + Aktualisiert (5+1): Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+1): SQL Server Data Tools-Dokumente (SSDT))](../ssdt/new-updated-ssdt.md)
- [Neu + Aktualisiert (1+0): Dokumente zu **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): SQL Server Management Studio-Dokumente (SSMS))](../ssms/new-updated-ssms.md)
- [Neu + Aktualisiert (0+2): Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


