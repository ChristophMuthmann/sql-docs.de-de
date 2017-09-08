---
title: "Konvertieren von R-Code für die Verwendung in R Services| Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed5f9052467492fe4bbbfb4ac0682c08a7ba8062
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="converting-r-code-for-use-in-r-services"></a>Konvertieren von R-Code für die Verwendung in R Services

Wenn Sie R-Code von R Studio oder eine andere Umgebung mit SQL Server verschieben, häufig der Code funktioniert ohne weitere Änderung bei hinzugefügt der  *@script*  Parameter [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Dies ist insbesondere dann, wenn Sie die Projektmappe mit entwickelt haben die **"revoscaler"** Funktionen, sodass relativ einfach, Ausführungskontexte ändern.

In der Regel sollten Sie jedoch den R-Code für die Verwendung mit SQL Servern ändern, um sowohl von einer stärkeren Integration mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu profitieren als auch teure Übertragungen von Daten zu vermeiden.

Beispiele dafür, wie sich R-Code in SQL Server ausführen lässt, finden Sie in den folgenden Anleitungen:

+ [In der Datenbank Analytics für den SQL-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md) veranschaulicht, wie Sie R-Code modularer können durch Einbinden in gespeicherten Prozeduren

+ [End-to-End Data Science-Lösung](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) enthält einen Vergleich der namens Feature Engineering in R und T-SQL

## <a name="how-the-data-science-process-changes-in-sql-server"></a>Wie ändert sich die Data Science-Prozess in SQL Server

Wenn Sie arbeiten in einer dedizierten R-Entwicklungsumgebung wie z. B. [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] oder RStudio, der typische Arbeitsablauf umfasst, zum Abrufen von Daten auf Ihrem Computer, die Daten analysieren, iterativ, und klicken Sie dann auszuschreiben oder zeigen die Ergebnisse. Jedoch wenn eigenständigen R-Code zu SQL Server migriert wird, kann Großteil dieser Prozess werden vereinfacht oder automatisiert an andere SQL Server-Tools zu delegieren. Darüber hinaus können damit Leistung in vielen Fällen verbessert.

| Externer Code | R in SQL Server |
|-------|-------|
| Erfassen von Daten| Definieren Sie Eingabedaten als eine SQL-Abfrage an. Vermeiden Sie die datenverschiebung an. |
| Zusammenfassen und Visualisieren von Daten| Darstellungen können als Bilder exportiert oder an einer Remotearbeitsstation gesendet werden.|
|Featureentwicklung| Verwenden Sie in der Datenbank R, wenn Sie nicht möchten, ändern Sie den Code, aber betrachten Sie die Abfragen optimiert werden. Überprüfen Sie, ob es möglicherweise effizienter, T-SQL-Funktionen oder benutzerdefinierte UDFs aufzurufen.|
|Datenbereinigung als Teil des Analysevorgangs| Führen Sie namens Feature Engineering merkmalsextraktion und DatenBereinigung als Teil des Datenworkflows im voraus.|
|Ausgabevorhersagen in eine Datei| Ausgabe von Vorhersagen mit einer Tabelle zum Verschieben von Daten zu vermeiden. Wrap Vorhersagen Funktionen in gespeicherten Prozeduren für den direkten Zugriff von Anwendungen.|

## <a name="best-practices"></a>Bewährte Methoden

+ Notieren Sie sich Abhängigkeiten im Vorfeld wie z.B. die erforderlichen Pakete. In einer Entwicklungs- und Testumgebung lassen sich Pakete als Teil des Codes durchaus installieren. In einer Produktionsumgebung empfiehlt sich diese Vorgehensweise jedoch nicht. Benachrichtigen Sie den Administrator, damit Pakete installiert und im Voraus getestet werden, bevor Sie Ihren Code bereitstellen.

+ Stellen Sie eine Prüfliste der möglichen Probleme bei Datentypen zusammen. Dokumentieren Sie das Schema der Ergebnisse in jedem Abschnitt des Codes erwartet.

+ Identifizieren Sie primäre Datenquellen wie Modelltrainingsdaten oder Eingabedaten für Vorhersagen im Vergleich zu sekundären Quellen wie z.B. Faktoren, weitere Gruppierungsvariablen usw. Ordnen Sie dem Eingabeparameter [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Ihr größtes DataSet zu.

+ Ändern Sie Ihre Eingabedaten-Anweisungen, um direkt in der Datenbank arbeiten zu können. Anstatt das Verschieben von Daten in eine lokale CSV-Datei oder das ODBC-Aufrufe wiederholt wird, erhalten Sie eine bessere Leistung mithilfe von SQL-Abfragen oder Sichten, die direkt gegen die Datenbank ausgeführt werden können datenverschiebungen zu vermeiden.

+ Verwenden Sie SQL Server-Abfragepläne, um Aufgaben zu identifizieren, die parallel ausgeführt werden können. Wenn die Eingabeabfrage parallelisiert werden kann, legen Sie `@parallel=1` als Teil Ihrer Argumente [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Eine Parallelverarbeitung mit diesem Flag ist in der Regel jedes Mal möglich, wenn SQL Server mit partitionierten Tabellen arbeiten oder eine Abfrage zwischen mehreren Prozessen verteilen kann und die Ergebnisse am Ende aggregiert.

  Eine Parallelverarbeitung mit diesem Flag ist nicht möglich, wenn Sie Modelle mithilfe von Algorithmen trainieren, die ein Lesen aller Daten voraussetzen, oder wenn Sie Aggregate erstellen müssen.

+ Ersetzen Sie nach Möglichkeit konventionelle R-Funktionen mit **ScaleR**-Funktionen, die verteilte Ausführung unterstützen. Weitere Informationen finden Sie unter [Vergleich der Base R und R-Funktionen für Skalierung](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Überprüfen Sie Ihren R-Code, um Schritte zu identifizieren, die unabhängig oder effizienter ausgeführt werden können, und verwenden Sie dazu einen separat gespeicherten Prozeduraufruf. Sie können beispielsweise Featureengineering oder Featureextraktion voneinander getrennt ausführen und die Werte in einer neuer Spalte hinzufügen. 

  Verwenden Sie T-SQL anstelle von R-Code für satzbasierte Berechnungen. Ein Beispiel für R-Lösungen, die benutzerdefinierte Funktionen und R für Feature engineering-Aufgaben vergleicht, finden Sie unter [Data Science-End-to-End-Exemplarische Vorgehensweise](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Verwenden Sie das R-Paket **Sqlrutils** konvertieren Sie den Code für eine Funktion mit klar definierten Eingaben und Ausgaben, die leicht Parameter gespeicherter Prozeduren zugeordnet werden können. Weitere Informationen und Beispiele finden Sie unter [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).


## <a name="restrictions"></a>Einschränkungen

 Beachten Sie die folgenden Einschränkungen bei der Konvertierung von R-Code:

### <a name="data-types"></a>Datentypen

-   Alle R-Datentypen werden unterstützt. Allerdings unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine größere Vielfalt von Datentypen als R. Daher sind einige implizite Datentypkonvertierungen erforderlich, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Daten nach bzw. von R gesendet werden. Sie müssen auch explizit umgewandelt oder einige Daten zu konvertieren.

- NULL-Werte werden unterstützt. R verwendet die `na` Data-Konstrukts einen fehlenden Wert darstellen, also ein NULL-Wert ähnelt.

Weitere Informationen finden Sie unter [R-Bibliotheken und Datentypen](../r/r-libraries-and-data-types.md).

### <a name="inputs-and-outputs"></a>Eingaben und Ausgaben

+ Sie können nur ein Eingabe-DataSet als Teil der Parameter der gespeicherten Prozedur definieren. Diese Eingabeabfrage für die gespeicherte Prozedur kann eine beliebige gültige einzelne SELECT-Anweisung sein. Es wird empfohlen, dass Sie diese Eingabe für das größte Dataset verwenden und kleinere Datasets aufteilen nach Bedarf über Aufrufe RODBC abrufen.

+ Vor dem Ausführen der Aufrufe von gespeicherten Prozeduren können nicht verwendet werden, als Eingabe für [Sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Alle Spalten im Eingabe-DataSet müssen Variablen im R-Skript zugeordnet werden. Variablen werden automatisch nach Namen zugeordnet. Nehmen wir beispielsweise an, dass Ihre R-Skript enthält eine Formel wie diese:
    
    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
     Ein Fehler wird ausgelöst, wenn die Eingabedatasets keine Spalten mit den entsprechenden Namen ArrDelay, CRSDepTime DayOfWeek, CRSDepHour und DayOfWeek enthält.

+ Sie können auch mehrere skalare Parametern als Eingabe bereitstellen. Allerdings müssen alle Variablen, die Sie als Parameter der gespeicherten Prozedur [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) übergeben, Variablen im R-Code zugeordnet werden. Standardmäßig werden die Variablen nach Namen zugeordnet.

+ Um skalare Variablen in der Ausgabe des R-Codes einzuschließen, fügen Sie einfach das **OUTPUT**-Schlüsselwort an, wenn Sie die Variable definieren.

+ In [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] kann Ihr R-Code nur ein einzelnes DataSet als Datenrahmenobjekt ausgeben. Sie können jedoch auch mehrere skalare Ausgaben ausgeben, darunter Elemente im Binärformat und Modelle im Varbinary-Format.

+ Sie können in der Regel das DataSet, das vom R-Skript zurückgegeben wird, ohne die Namen der Ausgabespalten ausgeben, indem Sie die Option RESULT SETS UNDEFINED verwenden. Allerdings müssen alle Variablen im R-Skript, das Sie ausgeben möchten, SQL Ausgabeparametern zugeordnet werden.

+ Wenn Ihr R-Skript das `@parallel=1`-Argument verwendet, müssen Sie das Ausgabeschema definieren. Grund hierfür ist, dass mehrere Prozesse von SQL Server zum Ausführen der Abfrage möglicherweise parallel erstellt und die Ergebnisse am Ende gesammelten werden. Aus diesem Grund muss Ausgabeschema definiert werden, bevor die parallele Prozesse erstellt werden können.

### <a name="dependencies"></a>Abhängigkeiten

 + Vermeiden Sie die Installation von Paketen aus R-Code. Auf SQL Server sollten im Voraus Pakete installiert werden.
 
  Achten Sie darauf, dass Pakete in die Standardbibliothek von Machine Learning Services verwendete Paket zu installieren. Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server](../r/r-package-management-for-sql-server-r-services.md)

