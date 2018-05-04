---
title: Auswählen einer Datenquelle oder Treiber | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], selecting driver
- connecting to data source [ODBC], selecting data source
- data sources [ODBC], selecting
- ODBC drivers [ODBC], selecting
ms.assetid: 10aaf570-01ab-4478-8339-bdde2a5e3dd1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3e9c5964d529fa70bd82c3aec7d25a42cb10c08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="choosing-a-data-source-or-driver"></a>Auswählen einer Datenquelle oder Treiber
Die Datenquelle oder von einer Anwendung verwendeten Treiber ist in einigen Fällen in der Anwendung hartcodiert. Z. B. eine benutzerdefinierte Anwendung ein MIS abteilungsweise zu übertragenden Daten aus einer Datenquelle in eine andere enthält die Namen dieser Datenquellen – die Anwendung einfach funktioniert nicht mit allen anderen Datenquellen. Ein weiteres Beispiel ist eine vertikale Anwendung, wie z. B. nach Auftragseingabe eines verwendet. Eine solche Anwendung immer verwendet die gleiche Datenquelle, mit einem vordefinierten Schema, das von der Anwendung bezeichnet.  
  
 Andere Anwendungen Auswählen der Datenquelle oder Treiber zur Laufzeit. In der Regel sind dies allgemeiner Anwendungen, die ad-hoc-Abfragen, z. B. als Kalkulationstabelle, die ODBC verwendet, um Daten zu importieren. Solche Anwendungen in der Regel Auflisten der verfügbaren Datenquellen oder Treiber und Benutzer entscheiden lassen möchten diejenigen, denen sie verwenden möchten. Gibt an, ob eine allgemeine Anwendung Datenquellen oder Treiber häufig enthält, hängt davon ab, gibt an, ob die Anwendung die DBMS-basierten oder einem dateibasierten Treibern verwendet.  
  
 DBMS-basierten Treibern erfordern i. d. r. einen komplexen Satz von Verbindungsinformationen, z. B. die Netzwerkadresse, Netzwerkprotokoll, Datenbankname und So weiter. Der Zweck einer Datenquelle ist, dass all diese Informationen ausgeblendet. Aus diesem Grund ist für das Data Source-Paradigma selbst für die Verwendung mit DBMS-basierten Treibern geeignet. Eine Anwendung kann eine Liste der Datenquellen für den Benutzer auf zwei Arten anzeigen. Aufrufen **SQLDriverConnect** mit der **DSN** (Data Source Name)-Schlüsselwort und keinen zugeordneten Wert; der Treiber-Manager zeigt eine Liste der Datenquellennamen. Wenn die Anwendung die Kontrolle über die Darstellung der Liste möchte, ruft es **SQLDataSources** zum Abrufen einer Liste verfügbarer Datenquellen und erstellt ein eigenes Dialogfeld. Diese Funktion wird vom Treiber-Manager implementiert und kann aufgerufen werden, bevor der Treiber geladen werden. Die Anwendung dann eine Verbindungsfunktion aufgerufen und übergibt den Namen der ausgewählten Datenquelle.  
  
 Wenn eine Datenquelle nicht angegeben ist, wird die Standarddatenquelle, angegeben durch die Systeminformationen verwendet. (Weitere Informationen finden Sie unter [Standard Unterschlüssel](../../../odbc/reference/install/default-subkey.md).) Wenn **SQLConnect** aufgerufen wird, mithilfe einer *ServerName* Argument, das nicht gefunden werden kann, wird ein null-Zeiger oder lautet "DEFAULT", der Treiber-Manager wird mit den Standard-Datenquelle verbunden. Der Standard-Datenquelle auch verwendet wird, wenn die Verbindungszeichenfolge wird verwendet, in einem Aufruf von **SQLDriverConnect** oder **SQLBrowseConnect** enthält die **DSN** Schlüsselwort "DEFAULT festgelegt "oder wenn die angegebene Datenquelle nicht gefunden wird. Darüber hinaus wird der Standard-Datenquelle verwendet wird, wenn die Verbindungszeichenfolge, die in einem Aufruf verwendet **SQLDriverConnect** enthält nicht die **DSN** Schlüsselwort.  
  
 Mit einem dateibasierten Treibern ist es möglich, ein Datei-Paradigma zu verwenden. Für Daten, die auf dem lokalen Computer gespeichert werden informieren Sie Benutzer häufig, dass ihre Daten in eine bestimmte Datei, z. B. nützlich ist. Anstatt eine unbekannten Datenquelle auswählen, ist es einfacher für solche Benutzer aus, um die Datei auszuwählen, die sie kennen. Dies ruft die Anwendung zuerst implementiert **SQLDrivers**. Diese Funktion wird vom Treiber-Manager implementiert und kann aufgerufen werden, bevor der Treiber geladen werden. **SQLDrivers** gibt eine Liste der verfügbaren Treiber; sie gibt überdies die Werte für die **FileUsage** und **FileExtns** Schlüsselwörter. Die **FileUsage** Schlüsselwort erläutert, ob dateibasierten Treibern Dateien wie Tabellen behandelt, als Xbase verfügt, werden als Datenbanken, wie Microsoft® Access. Die **FileExtns** Schlüsselwort Listet die Dateinamenerweiterungen der Treiber, z. B. für einen Treiber Xbase DBF erkennt. Mithilfe dieser Informationen erstellt die Anwendung ein Dialogfeld, das über die der Benutzer eine Datei auswählt. Basierend auf der Erweiterung der ausgewählten Datei, klicken Sie dann die Anwendung verbindet sich mit dem Treiber aufrufen **SQLDriverConnect** mit der **Treiber** Schlüsselwort.  
  
 Es ist nichts zum Beenden einer Anwendung mithilfe einer Datenquelle mit einem dateibasierten Treiber oder zum Aufrufen von **SQLDriverConnect** mit der **Treiber** Schlüsselwort zur Verbindung mit eines DBMS-basierten Treibers. Hier werden einige häufige Verwendungsmöglichkeiten von der **Treiber** für DBMS-basierten Treibern-Schlüsselwort:  
  
-   **Erstellen keine Datenquellen.** Eine benutzerdefinierte Anwendung kann z. B. einen bestimmten Treiber und die Datenbank verwenden. Wenn der Treibername und alle Informationen, der erforderlich sind, für die Verbindung mit der Datenbank ist in der Anwendung fest programmiert, verfügen Benutzer nicht auf ihrem Computer zum Ausführen der Anwendung eine Datenquelle erstellen. Alles, was sie tun müssen, ist die Anwendung und die Treiber zu installieren.  
  
     Ein Nachteil dieser Methode ist, dass die Anwendung neu kompiliert und verteilt werden, wenn die Verbindungsinformationen geändert werden muss. Wenn ein Datenquellennamen in der Anwendung anstelle der vollständigen Verbindungsinformationen hartcodiert ist, muss jeder Benutzer nur die Informationen in der Datenquelle ändern.  
  
-   **Beim Zugriff auf ein bestimmtes DBMS ein einziges Mal.** Angenommen, eine Tabelle, die Daten abruft, durch Aufrufen von ODBC-Funktionen enthält die **Treiber** Schlüsselwort, um einen bestimmten Treiber zu identifizieren. Da der Treibername für alle Benutzer sinnvoll, die diesen Treiber haben ist, kann das Arbeitsblatt für diesen Benutzer übergeben werden. Wenn das Arbeitsblatt einen Datenquellennamen enthalten, müssten jeden Benutzer erstellen Sie die gleiche Datenquelle, um das Arbeitsblatt zu verwenden.  
  
-   **Durchsuchen das System für alle Datenbanken auf einen bestimmten Treiber zugegriffen werden kann.** Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)weiter unten in diesem Abschnitt.
