---
title: Konfigurieren von SQL Server zum Senden von Feedback an Microsoft | Microsoft-Dokumentation
description: 
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 07/12/2017
ms.topic: article
ms.prod: sql-server
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 89fa77ec8e95bfc1f6ea2b796e07a1a2266bbab4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="configure-sql-server-to-send-feedback-to-microsoft"></a>Konfigurieren von SQL Server zum Senden von Feedback an Microsoft
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="summary"></a>Zusammenfassung
Microsoft SQL Server erfasst standardmäßig Informationen darüber, wie Kunden die Anwendung verwenden. Dies bedeutet, dass SQL Server Informationen zur Installationserfahrung, Nutzung und Leistung sammelt. Mit diesen Informationen kann Microsoft besser an die Bedürfnisse der Kunden anpassen. Microsoft erfasst z.B. Informationen zu Fehlercodes von Kunden, sodass wir damit verknüpfte Probleme beheben, die Dokumentation zu SQL Server verbessern und bestimmen können, ob wir dem Produkt weitere Funktionen hinzufügen müssen, um die Benutzererfahrung zu optimieren.

Microsoft sendet nicht die folgenden Informationen mit diesem Mechanismus:
- Werte aus Benutzertabellen
- Anmeldeinformationen oder andere Authentifizierungsinformationen
- personenbezogene Informationen (PII)

Die folgenden Beispielszenarios beinhalten Informationen zur Nutzung von Funktionen, die zur Verbesserung des Produkts beitragen.

SQL Server 2017 unterstützt Columnstore-Indizes für Szenarios, in denen schnelle Analysen erforderlich sind. Columnstore-Indizes vereinen eine herkömmliche B-Baumindexstruktur für neu eingefügte Daten mit einer besonderen spaltenorientierten, komprimierten Struktur zur Komprimierung von Daten und Beschleunigung der Abfrageausführung. Das Produkt enthält Heuristik zum Migrieren von Daten aus der B-Baumstruktur zur komprimierten Struktur, was im Hintergrund durchgeführt wird. Dadurch werden zukünftige Abfrageergebnisse beschleunigt.

Wenn der Vorgang im Hintergrund nicht mit der Rate an eingefügten Daten mithalten kann, ist die Abfrageleistung möglicherweise langsamer als erwartet. Um das Produkt zu verbessern, erfasst Microsoft Informationen darüber, wie gut SQL Server mit dem automatischen Kompressionsprozess mithalten kann. Das Produktteam verwendet diese Informationen, um die Häufigkeit und Parallelität von Code zu optimieren, der die Kompression durchführt. Diese Abfrage wird gelegentlich ausgeführt, um diese Informationen zu erfassen, damit wir von Microsoft die Datenverschiebungsrate bewerten können. Damit können wir die Produktheuristik optimieren.  

```sql
SELECT object_id, type_desc, data_space_id, db_id() AS database_id FROM sys.indexes WITH(nolock) WHERE type = 5 or type = 6 
```

```sql
SELECT cntr_value as merge_policy_evaluation
FROM sys.dm_os_performance_counters WITH(nolock)
WHERE object_name LIKE '%columnstore%' 
AND counter_name ='Total Merge Policy Evaluations' 
AND instance_name = '_Total'
```

Beachten Sie, dass dieser Prozess auf den erforderlichen Mechanismus für die Lieferung von Werten an den Kunden konzentriert ist. Das Produktteam schaut sich die Daten im Index nicht an und sendet diese auch nicht an Microsoft. SQL Server 2017 erfasst und sammelt kontinuierlich Informationen zur Installationserfahrung des Einrichtungsvorgangs, damit wir schnell Installationsprobleme erkennen und beheben können, die der Kunde hat. SQL Server 2017 kann so konfiguriert werden, dass es keine Informationen (pro Serverinstanz) an Microsoft mit den folgenden Mechanismen sendet:
- Mit der Anwendung „Fehler- und Verwendungsberichterstellung“
- Mit dem Festlegen von Registrierungsunterschlüsseln auf dem Server

Schauen Sie sich [Kundenfeedback zu SQL Server unter Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-customer-feedback.md) an, um Informationen zu SQL Server unter Linux zu erhalten.

> [!NOTE]
> Sie können das Senden von Informationen an Microsoft nur in bezahlten Versionen von SQL Server deaktivieren.

## <a name="error-and-usage-reporting-application"></a>Anwendung „Fehler- und Verwendungsberichterstellung“ 

Nach dem Einrichten der Einstellung für das Erfassen von Nutzungsdaten für SQL Server können Komponenten und Instanzen über die Anwendung „Fehler- und Verwendungsberichterstellung“ geändert werden. Diese Anwendung ist mit der Installation von SQL Server erhältlich. Mit diesem Tool kann jede Instanz von System Center ihre eigene Einstellung zu Nutzungsdaten konfigurieren.

> [!NOTE]
> Die Anwendung „Fehler- und Verwendungsberichterstellung“ ist unter den Konfigurationstools von SQL Server aufgelistet. Sie können dieses Tool verwenden, um Ihre Einstellungen zur Erfassung de Daten für die Fehler- und Verwendungsberichterstellung genauso wie in SQL Server 2017 vorzunehmen. Die Fehlerberichterstellung ist unabhängig vom Erfassen der Nutzungsdaten. Deshalb können sie unabhängig voneinander aktiviert und deaktiviert werden. Bei der Fehlerberichterstattung werden Absturzabbilder erfasst, die an Microsoft gesendet werden, und die möglicherweise vertrauliche Informationen enthalten, wie in den Datenschutzbestimmungen erläutert.

Um die Fehler- und Verwendungsberichterstellung von SQL Server zu starten, klicken oder tippen Sie auf **Start**, und suchen Sie anschließend im Suchfeld nach „Fehler“. Das SQL-Server-Element „Fehler- und Verwendungsberichterstellung“ wird angezeigt. Nachdem Sie das Tool gestartet haben, können Sie die Nutzungsdaten und schwerwiegende Fehler verwalten, die für Instanzen und Komponenten gesammelt wurden, die auf diesem Computer installiert sind.

Verwenden Sie in bezahlten Versionen die Kontrollkästchen „Nutzungsberichte“, um zu bestimmen, welche Daten zur Nutzung an Microsoft gesendet wird.

Verwenden Sie für bezahlte oder kostenlose Versionen die Kontrollkästchen „Fehlerberichte“, um zu bestimmen, welche Daten zu schwerwiegenden Fehlern an Microsoft gesendet werden.

## <a name="set-registry-subkeys-on-the-server"></a>Festlegen von Registrierungsunterschlüsseln auf dem Server

Enterprise-Kunden können die Einstellungen für Gruppenrichtlinien konfigurieren, um die Nutzungsdatenerfassung zu aktivieren oder zu deaktivieren. Dies erfolgt mit dem Konfigurieren einer registrierungsbasierten Richtlinie. Der entsprechende Registrierungsunterschlüssel und die entsprechenden Einstellungen lauten wie folgt:

- Für Funktionen einer SQL-Server-Instanz:
    
    Unterschlüssel = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanzID}\CPE
    
    Name des Registrierungseintrags = CustomerFeedback
    
    Eingabetyp DWORD: 0 bedeutet deaktivieren; 1 bedeutet aktivieren
    
    {InstanzID} ist der Instanztyp und die Instanz, wie in folgendem Beispiel:

    - MSSQL14.CANBERRA für SQL Server 2017-Datenbankmodul mit dem Instanznamen „CANBERRA“
    - MSAS14.CANBERRA für SQL Server 2017-Analysis Services mit dem Instanznamen „CANBERRA“
    - MSRS14.CANBERRA für SQL Server 2017-Reporting Services mit dem Instanznamen „CANBERRA“

- Für alle freigegebenen Funktionen:
    
    Unterschlüssel = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Hauptversion}
    
    Name des Registrierungseintrags = CustomerFeedback
    
    Eingabetyp DWORD: 0 bedeutet deaktivieren; 1 bedeutet aktivieren

> [!NOTE]
> {Hauptversion} ist die Version von SQL Server, z.B. 140 für SQL Server 2017.

- Für SQL Server Management Studio:
  
    Unterschlüssel = HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\140

    Name des Registrierungseintrags = CustomerFeedback

    Eingabetyp DWORD: 0 bedeutet deaktivieren; 1 bedeutet aktivieren

Darüber hinaus könne Sie durch Festlegen des folgenden Registrierungsunterschlüssels und der folgenden Einstellungen die Fehler- und Verwendungsberichterstellung auf Ebene von Visual Studio deaktivieren:

-    Unterschlüssel = HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\Telemetry

-    Name des Registrierungseintrags = TurnOffSwitch

-    Eingabetyp DWORD: 0 bedeutet deaktivieren; 1 bedeutet aktivieren
 
Die registrierungsbasierte Gruppenrichtlinie dieses Registrierungsschlüssels wird von der Nutzungsdatenerfassung von SQL Server 2017 berücksichtigt.

## <a name="set-registry-subkeys-for-crash-dump-collection"></a>Festlegen des Registrierungsunterschlüssels für die Absturzabbilderfassung

Kunden von SQL Server 2017 Enterprise können, ähnlich zum Verhalten früherer Versionen von SQL Server, Einstellungen für Gruppenrichtlinien auf dem Server konfigurieren, um die Absturzabbilderfassung zu aktivieren oder zu deaktivieren. Dies erfolgt mit dem Konfigurieren einer registrierungsbasierten Richtlinie. Die entsprechenden Registrierungsschlüssel und Einstellungen lauten wie folgt: 

- Für Funktionen einer SQL-Server-Instanz:

    Unterschlüssel = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{InstanzID}\CPE

    Name des Registrierungseintrags = EnableErrorReporting

    Eingabetyp DWORD: 0 bedeutet deaktivieren; 1 bedeutet aktivieren
 
    {InstanzID} ist der Instanztyp und die Instanz, wie in folgendem Beispiel: 

    - MSSQL14.CANBERRA für SQL Server 2017-Datenbankmodul mit dem Instanznamen „CANBERRA“
    - MSAS14.CANBERRA für SQL Server 2017-Analysis Services mit dem Instanznamen „CANBERRA“
    - MSRS14.CANBERRA für SQL Server 2017-Reporting Services mit dem Instanznamen „CANBERRA“
 

- Für alle freigegebenen Funktionen:
    
    Unterschlüssel = HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\{Hauptversion}

    Name des Registrierungseintrags = EnableErrorReporting

    Eingabetyp DWORD: 0 bedeutet deaktivieren; 1 bedeutet aktivieren

> [!NOTE]
> {Hauptversion} ist die Version von SQL Server. „140“ ist z.B. SQL Server 2017.

Die registrierungsbasierte Gruppenrichtlinie dieses Registrierungsschlüssels wird von der Absturzabbilderfassung von SQL Server 2017 berücksichtigt. 

## <a name="crash-dump-collection-for-ssms"></a>Absturzabbilderfassung für SSMS
SSMS erfasst nicht seine eigenen Absturzabbilder. Jedes Absturzabbild, das mit SSMS in Verbindung steht, wird im Rahmen der Windows-Fehlerberichterstattung erfasst.

Wie Sie diese Funktion deaktivieren oder aktivieren können, hängt von der Version Ihres Betriebssystems ab. Halten Sie sich zum Aktivieren oder Deaktivieren dieser Funktion an die Schritte im entsprechenden Artikel für Ihr Betriebssystem.
 
- Windows Server 2016 und Windows 10

    [Konfigurieren der Windows-Telemetrie in Ihrem Unternehmen](https://technet.microsoft.com/en-us/itpro/windows/manage/configure-windows-telemetry-in-your-organization)
- Windows 2008 R2 und Windows Server 7

    [WER Settings (WER-Einstellungen)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb513638(v=vs.85).aspx)
 
## <a name="feedback-for-analysis-services"></a>Feedback zu Analysis Services

Während der Installation fügt SQL Server 2016 Analysis Services ein gesondertes Konto zu Ihrer Instanz von Analysis Services hinzu. Dieses Konto ist ein Member der Rolle „Administrator des Analysis Services-Server“. Das Konto wird dazu verwendet, Informationen für das Senden von Feedback für die Instanz von Analysis Services zu sammeln.  

Sie können Ihren Dienst so konfigurieren, dass keine Nutzungsdaten gesendet werden. Wie Sie dazu vorgehen müssen, ist im Abschnitt „Festlegen von Registrierungsunterschlüsseln auf dem Server“ beschrieben. Wenn Sie dies machen, wird das Dienstkonto jedoch nicht entfernt. 
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
