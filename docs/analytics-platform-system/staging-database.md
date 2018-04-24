---
title: Verwendung einer Stagingdatenbank - Parallel Data Warehouse | Microsoft Docs
description: SQL Server Parallel Data Warehouse (PDW) verwendet eine staging-Datenbank zum Speichern von Daten vorübergehend während des Ladevorgangs.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 73822c1495fa5f83d9a8ba37325a025999f94530
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>Verwendung einer Stagingdatenbank in Parallel Data Warehouse (PDW)
SQL Server Parallel Data Warehouse (PDW) verwendet eine staging-Datenbank zum Speichern von Daten vorübergehend während des Ladevorgangs. Standardmäßig verwendet SQL Server PDW die Zieldatenbank als Stagingdatenbank, die Tabellenfragmentierung verursachen kann. Um die Tabellenfragmentierung zu reduzieren, können Sie eine benutzerdefinierte staging-Datenbank erstellen. Oder, wenn Rollback von eines Ladefehlers nicht relevant ist, können Sie den Fastappend-Lademodus um Leistung zu verbessern, indem Sie die temporäre Tabelle überspringen und direkt in die Zieltabelle geladen.  
  
## <a name="StagingDatabase"></a>Grundlagen der Staging-Datenbank  
Ein *Stagingdatenbank* ist eine vom Benutzer erstellten PDW-Datenbank, die Daten gespeichert werden, vorübergehend, während sie in der Anwendung geladen wird. Wenn eine Stagingdatenbank für ein Auslastungstestergebnis angegeben wird, wird die Appliance zuerst die Daten in der Stagingdatenbank kopiert und kopiert dann die Daten von temporären Tabellen in der Stagingdatenbank in dauerhaften Tabellen in der Zieldatenbank.  
  
Wenn eine Stagingdatenbank für eine Last nicht angegeben ist, wird SQL ServerPDW die temporären Tabellen in der Zieldatenbank erstellt und verwendet sie zum die geladenen Daten zu speichern, bevor die geladenen Daten in die Zieltabellen permanente eingefügt.  
  
Wenn ein Auslastungstest verwendet die *Fastappend-Modus*, SQL ServerPDW lässt die Verwendung temporärer Tabellen vollständig und fügt die Daten direkt an die Zieltabelle. Der Fastappend-Modus verbessert die Leistung der Last für ELT-Szenarien, in denen Daten in eine Tabelle geladen werden, die eine temporäre Tabelle aus der Sicht der Anwendung ist. Beispielsweise konnte ein ELT-Prozess Laden von Daten in eine temporäre Tabelle verarbeiten die Daten durch DatenBereinigung und Deduplizierung Informationen und fügen Sie dann die Daten in der Faktentabelle Ziel. In diesem Fall ist es nicht erforderlich für PDW zum ersten Laden der Daten in eine interne temporäre Tabelle vor dem Einfügen der Daten in der Anwendung temporäre Tabelle. Der Fastappend-Modus wird vermieden, die zusätzliche Last Schritt, durch der die Leistung deutlich verbessert wird. Um den Fastappend-Modus verwenden zu können, müssen Sie mit mehreren Transaktionsmodus befindet, verwenden was bedeutet, dass die Wiederherstellung aus einer fehlerhaften oder abgebrochenen Last vom Auslastungstest-Prozess verarbeitet werden muss.  
  
**Vorteile der Staging-Datenbank**  
  
Der Hauptvorteil einer Stagingdatenbank wird um die Tabellenfragmentierung zu reduzieren. Wenn eine Stagingdatenbank nicht verwendet wird, werden die Daten in temporäre Tabellen in der Zieldatenbank geladen. Wenn temporäre Tabellen erstellt und in der Zieldatenbank gelöscht, werden die Seiten für die temporären Tabellen und dauerhaften Tabellen überlappenden. Im Laufe der Zeit Tabellenfragmentierung tritt auf, und beeinträchtigt die Leistung. Im Gegensatz dazu wird sichergestellt, dass eine Stagingdatenbank, temporäre Tabellen erstellt und in eine separate Datei-Speicherplatz als der dauerhaften Tabellen gelöscht werden.  
  
**Staging-Tabelle Datenbankstrukturen**  
  
Die Speicherstruktur für jede Datenbanktabelle hängt von der Zieltabelle ab.  
  
-   Für das Laden in einen Heap oder gruppierten columnstore-Index ist die staging-Tabelle ein Heap.  
  
-   Für das Laden in einen gruppierten Rowstore-Index ist die staging-Tabelle einen gruppierten Rowstore-Index.  
  
## <a name="Permissions"></a>Berechtigungen  
Erfordert die Berechtigung "erstellen" (für das Erstellen einer temporären Tabelle) für die staging-Datenbank. 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>Bewährte Methoden zum Erstellen einer Stagingdatenbank  
  
1.  Es darf nur eine Stagingdatenbank pro Anwendung vorhanden sein. Die Stagingdatenbank kann alle Lade-Aufträgen für alle Zieldatenbanken freigegeben werden.  
  
2.  Die Größe der Stagingdatenbank wird kundenspezifische. Zu Beginn sollten beim ersten Auffüllen die Appliance die Stagingdatenbank groß genug für die anfängliche Lade-Aufträgen sein. Diese Aufträge laden tendenziell groß sein, da mehrere Ladevorgänge gleichzeitig ausgeführt werden können. Nach dem anfänglich geladenen Aufträge abgeschlossen wurden, und das System in der Produktion ist, wird der Größe der einzelnen Ladeauftrag tendenziell kleiner sein. Wenn Ladevorgänge klein sind, können Sie Verkleinern der Stagingdatenbank um kleineren Load-Größen zu berücksichtigen. Zum Reduzieren der Größe können Sie die staging-Datenbank löschen und erstellen Sie es erneut mit kleinen Größe zuteilungen, oder Sie können die [ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md) Anweisung.  
  
    Wenn Sie die staging-Datenbank zu erstellen, verwenden Sie die folgenden Richtlinien.  
  
    -   Die Größe der replizierten Tabelle muss die geschätzte Größe pro Compute-Knoten, der die replizierten Tabellen, die gleichzeitig geladen werden. Die Größe wird in der Regel 25-30 GB.  
  
    -   Die verteilte Tabellengröße sollte die geschätzte Größe pro Anwendung, der verteilte Tabellen, die gleichzeitig geladen werden.  
  
    -   Die Protokollgröße ähnelt in der Regel die Größe der replizierten Tabelle.  
  
## <a name="Examples"></a>Beispiele für  
  
### <a name="a-create-a-staging-database"></a>A. Erstellen Sie eine staging-Datenbank 
Das folgende Beispiel erstellt eine staging-Datenbank, Stagedb, für die Verwendung mit allen laden, auf dem Gerät. Angenommen, Sie schätzen, dass fünf Tabellen Größe repliziert werden 5 GB gleichzeitig geladen werden. Diese Parallelität führt zu mindestens 25 GB für die replizierte Größe zuordnen. Angenommen, Sie schätzen, dass sechs Tabellen Größe 100 verteilt, werden 200, 400, 500, 500 und 550 GB gleichzeitig geladen werden. Diese Parallelität führt zu mindestens mit 2250 GB für die verteilte Tabellengröße belegen.  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
