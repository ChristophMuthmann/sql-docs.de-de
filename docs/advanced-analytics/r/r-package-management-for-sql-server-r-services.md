---
title: Installieren und Verwalten von Machine Learning-Paketen in SQL Server | Microsoft Docs
ms.custom: 
ms.date: 02/19/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 0fd96240581203d9f948372dfbe98cac80a3b906
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/28/2018
---
# <a name="installing-and-managing-machine-learning-packages-in-sql-server"></a>Installieren und Verwalten von Machine Learning-Paketen in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

In diesem Artikel wird beschrieben, wie Sie neue R oder Python-Pakete in SQL Server-2017 und SQL Server 2016 installieren können. Es beschreibt auch Einschränkungen auf die Pakete, die Sie auf SQL Server installieren können.

## <a name="overview-of-package-management-methods-and-requirements"></a>Übersicht über die Paket-Verwaltungsmethoden und Anforderungen

Im Gegensatz zu einer typischen R oder Python-Entwicklung müssen die Pakete, die von SQL Server verwendete in einen Ordner unter administrative Kontrolle installiert sein. Es gibt zahlreiche Vorteile für die Speicherung der Pakete in einem zentralen Ort aus:

+ Der Serveradministrator kann das Hinzufügen neuer Dateien und Bibliotheken, auf dem Server zu überwachen und Steuern der Vergrößerung von Dateien, die von Paket-Bibliotheken verwendet. 
+ Pakete können einfacher mehrere Datenbankbenutzer, im Gegensatz zum Installieren von mehreren Kopien desselben Pakets in benutzerbibliotheken freigegeben werden.
+ Nur sichere, genehmigter Pakete können zum Schützen von Server und seine Vorgänge installiert werden.

Diese Einschränkung bedeutet jedoch unbedingt einige Änderungen bei der Datenerfassung, die Datenanalysten und Analytiker arbeiten:

+ Im Allgemeinen ist Administratorzugriff auf dem Server erforderlich. In SQL Server-2017 kann der Datenbankadministrator Rollen verwenden, um bestimmten Benutzern die Möglichkeit zum Installieren der Pakete zur privaten Verwendung, aber der Administrator kann weiterhin auf diese Funktion zu aktivieren.
+ Anzahl der Server keine Zugang zum Internet. Installieren von Paketen auf diesen Computern erfordert einige zusätzliche Vorbereitung.
+ Pakete werden in einer Bibliothek Instanz installiert. Pakete können nicht über Instanzen freigegeben werden.
+ Benutzer können keine Pakete ausführen, die in einer Benutzerbibliothek installiert wurde.

## <a name="package-installation-guides-for-r-or-python"></a>Paket-Installationshandbücher für R oder Python

Finden Sie unter den folgenden Artikeln Ausführliche Schritte zum Installieren neuer R oder Python-Pakete ein. 

### <a name="install-new-r-packages"></a>Installieren Sie neue R-Pakete

+ [Installieren Sie zusätzliche R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md)

    Sie können R-Pakete auf SQL Server 2016 oder 2017 als Administrator, die mit R-Tools installieren.

    Sie können auch R-Pakete installieren, von einem Remoteclient von R, R Server 9.0.2 oder höher installiert ist.

    Sie können auch R-Pakete in SQL Server-2017 mithilfe von DDL-Anweisungen installieren.

### <a name="install-new-python-packages"></a>Installieren neuer Python-Pakete

+ [Installieren neuer Python-Pakete unter SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="prerequisites"></a>Erforderliche Komponenten

Bevor Sie versuchen, herunterladen oder installieren ein neues Paket, überprüfen Sie die Anforderungen:

+ Stellen Sie sicher, dass eine Windows-Version des Pakets vorhanden ist: [abrufen, die richtige Paketversion und Format](#packageVersion)

+ Identifizieren Sie alle Abhängigkeiten des Pakets und ermitteln Sie deren Kompatibilität mit SQL Server-Umgebung zu.

+ Überprüfen Sie R-Version oder Python Versionen Kompatibilität. Das Paket muss kompatibel mit der Version von R oder Python, die in SQL Server ausgeführt wird.

+ Berechtigungen. Bestimmen Sie, ob Sie berechtigt ist, das Paket zu installieren. Um die Instanz-Bibliothek zu installieren, ist Administratorzugriff auf dem Computer mit SQL Server erforderlich. Wenn Sie administrativen Zugriff auf die SQL Server-Computer besitzen, finden Sie ein Datenbankadministrator, Paketinstallation verwenden können.

    In SQL Server 2017 können Sie R-Pakete von einem Remoteclient aus installieren, wenn paketverwaltung auf dem Server aktiviert wurde und Sie, Datenbankbesitzer oder Mitglied einer Rolle der Paket-Management sind.

+ Betrachten Sie die Risiken und die Vorteile ein bestimmtes Pakets in SQL Server-Umgebung zu installieren. Überprüfen Sie, ob das Paket (oder sämtliche Pakete, die dafür) Funktionen enthält, die von SQL Server oder von der Richtlinie blockiert werden würde. Viele R und Python-Pakete sind für eine gesicherte SQL Server-Umgebung eine sehr schlecht geeignet. Probleme können Folgendes umfassen:

    - Pakete, die den Netzwerkzugriff
    - Pakete, die Java oder andere Frameworks, die üblicherweise nicht in einer SQL Server-Umgebung verwendet erfordern
    - Pakete, die mit erhöhten Rechten Dateisystemzugriff erfordern
    - Paket wird für die Webentwicklung oder andere Aufgaben, die durch die Ausführung innerhalb von SQL Server profitieren nicht verwendet.

## <a name="installation-on-servers-with-no-internet-access"></a>Installation auf Servern ohne Internetzugang

Im Allgemeinen gestatten auf Servern, Produktionsdatenbanken hosten, keine Verbindung mit dem Internet. Installieren von neuen R oder Python-Pakete in solchen Umgebungen erfordert, dass Sie alle Pakete und deren Abhängigkeiten rechtzeitig vorbereiten, und kopieren Sie die Dateien in einen Ordner auf dem Server für die Verwendung in der Installation.

1. Identifizieren Sie alle Abhängigkeiten des Pakets an. 
2. Überprüfen Sie, ob alle erforderlichen Pakete auf dem Server bereits installiert sind. Wenn das Paket installiert ist, stellen Sie sicher, dass die Version richtig ist.
3. Laden Sie das Paket und alle Abhängigkeiten auf einen separaten Computer herunter.
4. Verschieben Sie die Dateien vom Server in einen Ordner zugegriffen werden kann.
5. Führen Sie eine unterstützte Installationsbefehl oder DDL-Anweisung, zum Installieren des Pakets in die Bibliothek für die Instanz.

Identifizieren alle Abhängigkeiten kann kompliziert sein. Für R, empfehlen wir die Verwendung [MiniCRAN](create-a-local-package-repository-using-minicran.md) um ein Repository Offlinepaket vorzubereiten.

Auf ähnliche Weise müssen Sie für Python bereiten Sie alle Abhängigkeiten vor und lokal speichern. Achten Sie darauf, um ein Windows-kompatiblen Binärdateien und den WHL Format verwenden.
