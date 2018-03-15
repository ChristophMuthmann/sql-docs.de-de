---
title: Bereitstellen und nutzen Sie Analysen mit Mrsdeploy | Microsoft Docs
ms.custom: 
ms.date: 08/20/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 4b439725c8c9e522ed500f717686b8a9cf7d972a
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="deploy-and-consume-analytics-using-mrsdeploy"></a>Bereitstellen Sie und nutzen Sie Analysen mit mrsdeploy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft R Server enthält eine Funktion, die operationalisierung **Mrsdeploy**, diese Aufgaben unterstützt:

+ Veröffentlichen und Verwalten von R und Python-Modellen und Code in Form von Webdiensten
+ Nutzen diese Dienste in Clientanwendungen

Dieses Thema enthält Informationen zum Aktivieren und konfigurieren die Funktion.

Allgemeine Informationen zu von unterstützten Szenarien **Mrsdeploy**, finden Sie unter [Operationalisierung mit R Server](https://docs.microsoft.com/r-server/what-is-operationalization).

## <a name="using-mrsdeploy-for-operationalization"></a>Verwenden von Mrsdeploy für operationalisierung

Das Wort *operationalisierung* kann bedeuten, dass viele Dinge sein:

+ Die Möglichkeit zum Veröffentlichen von Modellen an einen Webdienst für die Verwendung von Anwendungen
+ Unterstützung für die skalierbare oder verteilte Berechnung
+ Einmal entwickeln, oft bereitstellen
+ Schnelle Bewertung für beide einzeiliges und batchbewertung

Wenn Sie Machine Learning Services mit SQL Server installiert haben *operationalisierung* ist weiterhin den R oder Python-Code in einer gespeicherten Prozedur umschließen. Jede Anwendung kann dann zum Trainieren eines Modells, Generieren von Bewertungen oder Berichte erstellen, die gespeicherte Prozedur aufrufen. Sie können auch Aufträge mithilfe von vorhandenen Planungsmechanismen in SQL Server automatisieren.

Microsoft R Server bietet jedoch eine unterschiedliche Mechanismen für die Unterstützung für die Bereitstellung, mithilfe von Webdiensten, die Veröffentlichung von R-Aufträge, und ein-Verwaltungshilfsprogramm für die Ausführung von verteilten R-Aufträge unterstützen. Microsoft R Server verwendet die Funktionen in der **Mrsdeploy** Paket richten Sie eine Sitzung mit remote-Serverknoten, und führen Sie R-Code in einer Konsolenanwendung.

Diese Bereitstellungsfunktion von R Server bietet folgende Vorteile:

+ Mit der rollenbasierten Zugriffssteuerung mit analytischen Web services

    Bestimmen, wer veröffentlichen, aktualisieren und löschen ihre eigenen Webdienste, Personen können ebenfalls aktualisieren und Löschen von den Webdiensten von anderen Benutzern und wer kann nur Liste veröffentlicht, und Nutzen von Webdiensten.

+ Schneller Bewertung
  
  Echtzeit-batchbewertung mit unterstützten R Model-Objekts können zur Verbesserung der Geschwindigkeit der Bewertung der Vorgänge.

+ Asynchrones BatchUpdate Verbrauch

  Webdienste, die für große Eingabedaten aufrufen können jetzt über die Batchausführung asynchron verarbeitet werden.

+ Automatische Skalierung eines Rasters von Web- und Compute-Knoten

  Eine Vorlage für ein Skript wird bereitgestellt, Sie können problemlos einen Satz von R-Server-VMs in Azure bündelt und konfigurieren sie als Raster für Analysen und Remoteausführung operationalisieren. In diesem Raster kann nach unten Abhängigkeit CPU-Auslastung oder skaliert werden.

+ Asynchrone Remoteausführung

    Unterstützt jetzt die Verwendung der **Mrsdeploy** R-Paket. Führen Sie zum Fortsetzen des Vorgangs in der Entwicklungsumgebung arbeiten, während der Ausführung von Remoteskripts asynchron mit R-Skript die `async` Parameter. Dies ist besonders nützlich, wenn Sie Skripts ausführen, die langen Ausführungszeiten.

## <a name="requirements-and-configuration"></a>Anforderungen und Konfiguration

SQLServer 2017 CTP-Version 2.0 oder höher enthält dieses Feature, das zuvor gab es nur mit R-Server und mit SQL Server R Services nicht installiert. Die **Mrsdeploy** Paket ist auf dem SQL Server-Computer installiert, wenn Sie die Option zur Installation auswählen **Microsoft Machine Learning-Server**, aus der **gemeinsam genutzte Funktionen** Abschnitt der SQL Server-Setup.

In der Regel empfohlen nicht, dass Sie Machine Learning-Server auf demselben Computer installieren, auf dem SQL Server-Machine Learning-Services ausgeführt wird. Es wird empfohlen, die Installation von **Microsoft Machine Learning-Server** auf demselben Computer wie SQL Server, und klicken Sie dann die operationalisierung-Funktionen auf diesem Computer konfigurieren.

Sie müssen zusammen installiert werden, führen Sie diese zusätzlichen Schritte aus, um den Dienst zu konfigurieren Sie.

1. Installieren Sie DotNetCore 1.1

    Wenn .NET Core als Teil von SQL Server nicht installiert wurde, müssen Sie es vor dem R-Server-Setup installieren.

2. Installieren Sie Microsoft-Machine Learning-Server.

3. Nach Abschluss des Setups von **Microsoft Machine Learning-Server**manuell fügen Sie den folgenden Registrierungsschlüssel für **Mrsdeploy**, gibt den Basisordner für die R_SERVER-Dateien. 

    + Erstellen Sie einen neuen Registrierungsschlüssel `H_KEY_LOCAL_MACHINE\SOFTWARE\R Server\Path`
    + Legen Sie den Wert des Schlüssels, der `"C:\Program Files\Microsoft SQL Server\140\R_SERVER"`.

4. Öffnen Sie anschließend die [Administrator Utility](https://docs.microsoft.com/r-server/operationalize/configure-use-admin-utility).

5. So konfigurieren Sie weiterhin die **Mrsdeploy** service wie hier beschrieben: [Konfiguration für Administratoren](https://docs.microsoft.com/r-server/operationalize/configure-start-for-administrators)

6. Weitere Informationen finden Sie unter [Mrsdeploy Funktionen](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package).
