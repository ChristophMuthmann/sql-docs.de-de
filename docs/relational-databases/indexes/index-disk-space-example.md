---
title: "Beispiel für den zum Speichern eines Indexes belegten Speicherplatz | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- online index disk space
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- offline index disk space [SQL Server]
ms.assetid: e5c71f55-0be3-4c93-97e9-7b3455c8f581
caps.latest.revision: "30"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a9fb062940b786528ea4e0f19395391a2b84b19
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="index-disk-space-example"></a>Beispiel für den zum Speichern eines Indexes belegten Speicherplatz
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Für jeden Erstellungs-, Neuerstellungs- oder Löschvorgang eines Indexes ist Speicherplatz für die alten (Quellindex) und neuen (Zielindex) Strukturen in den entsprechenden Dateien und Dateigruppen erforderlich. Die Zuordnung der alten Struktur wird erst aufgehoben, nachdem die Indexerstellungstransaktion den Commitvorgang ausgeführt hat. Außerdem ist möglicherweise weiterer temporärer Speicherplatz auf dem Datenträger für Sortiervorgänge erforderlich. Weitere Informationen finden Sie unter [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
 Im folgenden Beispiel werden die Speicherplatzanforderungen beim Erstellen eines gruppierten Indexes ermittelt.  
  
 Nehmen Sie an, dass die folgenden Bedingungen zutreffen, bevor Sie den gruppierten Index erstellen:  
  
-   Die vorhandene Tabelle (Heap) enthält 1 Millionen Zeilen. Jede Zeile ist 200 Byte lang.  
  
-   Der nicht gruppierte Index A enthält 1 Million Zeilen. Jede Zeile ist 50 Byte lang.  
  
-   Der nicht gruppierte Index B enthält 1 Million Zeilen. Jede Zeile ist 80 Byte lang.  
  
-   Die Option 'Speicher für Indexerstellung' wird auf 2 MB festgelegt.  
  
-   Ein Füllfaktorwert von 80 wird für alle vorhandenen und neuen Indizes verwendet. Dies bedeutet, dass die Seiten zu 80 Prozent gefüllt sind.  
  
    > [!NOTE]  
    >  Als Ergebnis der Erstellung eines gruppierten Indexes müssen die beiden nicht gruppierten Indizes neu erstellt werden, um den Zeilenindikator durch den neuen Schlüssel des gruppierten Indexes zu ersetzen.  
  
## <a name="disk-space-calculations-for-an-offline-index-operation"></a>Speicherplatzberechnungen für einen Offlineindexvorgang  
 In den folgenden Schritten werden der temporäre Speicherplatz, der während des Indexvorgangs verwendet werden soll, sowie der dauerhafte Speicherplatz berechnet, der für das Speichern neuer Indizes erforderlich ist. Die gezeigten Berechnungen geben Näherungswerte an. Die Ergebnisse werden aufgerundet, und es wird nur die Größe der Indexblattebene berücksichtigt. Die Tilde (~) wird zum Angeben von Näherungswerten verwendet.  
  
1.  Ermitteln der Größe der Quellstrukturen  
  
     Heap: 1 Million * 200 Byte ~ 200 MB  
  
     Nicht gruppierter Index A: 1 Million * 50 Byte / 80% ~ 63 MB  
  
     Nicht gruppierter Index B: 1 Million * 80 Byte / 80% ~ 100 MB  
  
     Gesamtgröße der vorhandenen Strukturen: 363 MB  
  
2.  Ermitteln der Größe der Indexstrukturen (Zielstrukturen) Nehmen Sie an, dass der neue Schlüssel des gruppierten Indexes 24 Byte lang ist (einschließlich Uniqueifier). Der Zeilenindikator (Länge von 8 Byte) in beiden nicht gruppierten Indizes wird durch diesen gruppierten Schlüssel ersetzt.  
  
     Gruppierter Index: 1 Million * 200 Byte / 80% ~ 250 MB  
  
     Nicht gruppierter Index A: 1 Million * (50 – 8 + 24) Byte / 80% ~ 83 MB  
  
     Nicht gruppierter Index B: 1 Million * (80 – 8 + 24) Byte / 80% ~ 120 MB  
  
     Gesamtgröße der neuen Strukturen: 453 MB  
  
     Der Gesamtspeicherplatz, der zum Unterstützen der Quell- und Zielstrukturen für die Dauer des Indexvorgangs erforderlich ist, beträgt 816 MB (363 + 453). Die Zuordnung des Speicherplatzes, der den Quellstrukturen aktuell zugeordnet ist, wird aufgehoben, nachdem ein Commit für den Indexvorgang ausgeführt wurde.  
  
3.  Ermitteln des zusätzlichen temporären Speicherplatzes für die Sortierung.  
  
     Im Folgenden werden die Speicherplatzanforderungen für das Sortieren in **tempdb** (wobei SORT_IN_TEMPDB auf ON festgelegt wurde) sowie das Sortieren am Zielspeicherort gezeigt (wobei SORT_IN_TEMPDB auf OFF festgelegt wurde).  
  
    1.  Wenn SORT_IN_TEMPDB auf ON festgelegt wurde, muss für **tempdb** ausreichend Speicherplatz zum Speichern des größten Indexes vorhanden sein (1 Million * 200 Byte ~ 200 MB). Der Füllfaktor wird bei der Sortieroperation nicht berücksichtigt.  
  
         Zusätzlicher Speicherplatz (am Speicherort von **tempdb** ), der dem Wert von [Konfigurieren der Serverkonfigurationsoption „Speicher für Indexerstellung“](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) entspricht (= 2 MB).  
  
         Gesamtgröße des temporären Speicherplatzes, wenn SORT_IN_TEMPDB auf ON festgelegt wurde ~ 202 MB.  
  
    2.  Wenn SORT_IN_TEMPDB auf OFF festgelegt wird (Standardeinstellung), werden die für den neuen Index in Schritt 2 berücksichtigten 250 MB Speicherplatz zum Sortieren verwendet.  
  
         Zusätzlicher Speicherplatz (am Zielspeicherort), der dem Wert von [Konfigurieren der Serverkonfigurationsoption „Speicher für Indexerstellung“](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) entspricht (= 2 MB).  
  
         Gesamtgröße des temporären Speicherplatzes, wenn SORT_IN_TEMPDB auf OFF festgelegt wurde = 2 MB.  
  
 Wenn **tempdb**verwendet wird, sind insgesamt 1018 MB (816 + 202) zum Erstellen des gruppierten Indexes und der nicht gruppierten Indizes erforderlich. Obwohl durch die Verwendung von **tempdb** die Menge des temporären Speicherplatzes erhöht wird, die zur Indexerstellung verwendet wird, kann sich die Zeitspanne verringern, die zum Erstellen eines Indexes erforderlich ist, wenn **tempdb** auf einer anderen Gruppe von Datenträgern gespeichert ist als die Benutzerdatenbank. Weitere Informationen zur Verwendung von **tempdb**, finden Sie unter [SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).  
  
 Wenn **tempdb**nicht verwendet wird, sind insgesamt 818 MB (816 + 2) zum Erstellen des gruppierten Indexes und der nicht gruppierten Indizes erforderlich.  
  
## <a name="disk-space-calculations-for-an-online-clustered-index-operation"></a>Speicherplatzberechnungen für eine Onlineoperation mit einem gruppierten Index  
 Wenn Sie einen gruppierten Index online erstellen, löschen oder neu erstellen, ist zusätzlicher Speicherplatz zum Erstellen und Verwalten eines temporären Zuordnungsindexes erforderlich. Dieser temporäre Zuordnungsindex enthält einen Datensatz für jede Zeile in der Tabelle, und sein Inhalt ist die Vereinigung der alten und der neuen Lesezeichenspalten.  
  
 Wenn Sie den erforderlichen Speicherplatz für eine Onlineoperation mit einem gruppierten Index berechnen möchten, verwenden Sie die für einen Offlineindexvorgang beschriebenen Schritte und addieren dann diese Ergebnisse zu den Ergebnissen des folgenden Schritts.  
  
-   Ermitteln des Speicherplatzes für den temporären Zuordnungsindex  
  
     In diesem Beispiel ist das alte Lesezeichen die Zeilen-ID (Row ID, RID) des Heaps (8 Byte), und das neue Lesezeichen ist der Gruppierungsschlüssel (24 Byte einschließlich eines **Uniqueifier**). Es sind keine überlappenden Spalten zwischen den alten und neuen Lesezeichen vorhanden.  
  
     Größe des temporären Zuordnungsindexes = 1 Million * (8 Byte + 24 Byte) / 80% ~ 40 MB.  
  
     Dieser Speicherplatz muss zum erforderlichen Speicherplatz am Zielspeicherort addiert werden, wenn SORT_IN_TEMPDB auf OFF festgelegt ist, oder zu **tempdb** , wenn SORT_IN_TEMPDB auf ON festgelegt ist.  
  
 Weitere Informationen finden Sie unter [Speicherplatzanforderungen für Index-DDL-Vorgänge](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md).  
  
## <a name="disk-space-summary"></a>Zusammenfassung der Speicherplatzüberlegungen  
 Die folgende Tabelle fasst die Ergebnisse der Speicherplatzberechnungen zusammen.  
  
|Indexvorgang|Speicherplatzanforderungen für die Speicherorte der folgenden Strukturen|  
|---------------------|---------------------------------------------------------------------------|  
|Offlineindexvorgang mit SORT_IN_TEMPDB = ON|Gesamtspeicherplatz während des Vorgangs: 1018 MB<br /><br /> – Vorhandene Tabelle und Indizes: 363 MB\*<br /><br /> -<br />                    **tempdb**: 202 MB*<br /><br /> – Neue Indizes: 453 MB<br /><br /> Erforderlicher Gesamtspeicherplatz nach der Operation: 453 MB|  
|Offlineindexvorgang mit SORT_IN_TEMPDB = OFF|Gesamtspeicherplatz während des Vorgangs: 816 MB<br /><br /> – Vorhandene Tabelle und Indizes: 363 MB*<br /><br /> – Neue Indizes: 453 MB<br /><br /> Erforderlicher Gesamtspeicherplatz nach der Operation: 453 MB|  
|Onlineindexvorgang mit SORT_IN_TEMPDB = ON|Gesamtspeicherplatz während des Vorgangs: 1058 MB<br /><br /> – Vorhandene Tabelle und Indizes: 363 MB\*<br /><br /> -<br />                    **tempdb** (einschließlich Zuordnungsindex): 242 MB*<br /><br /> – Neue Indizes: 453 MB<br /><br /> Erforderlicher Gesamtspeicherplatz nach der Operation: 453 MB|  
|Onlineindexvorgang mit SORT_IN_TEMPDB = OFF|Gesamtspeicherplatz während der Operation: 856 MB<br /><br /> – Vorhandene Tabelle und Indizes: 363 MB*<br /><br /> – Temporärer Zuordnungsindex: 40 MB\*<br /><br /> – Neue Indizes: 453 MB<br /><br /> Erforderlicher Gesamtspeicherplatz nach der Operation: 453 MB|  
  
 *Die Zuordnung dieses Speicherplatzes wird aufgehoben, nachdem ein Commit für den Indexvorgang ausgeführt wurde.  
  
 Dieses Beispiel berücksichtigt keinen zusätzlichen temporären Speicherplatz, der in **tempdb** für Versionsdatensätze erforderlich ist, die durch gleichzeitige Update- und Löschvorgänge von Benutzern erstellt werden.  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Transaktionsprotokollspeicherplatz für Indexvorgänge](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)  
  
  
