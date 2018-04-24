---
title: Indexeigenschaften (F1-Hilfe) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.indexproperties.filter.f1
- sql13.swb.indexproperties.partitions.f1
- sql13.swb.indexproperties.general.f1
- sql13.swb.indexproperties.storage.f1
- sql13.swb.indexproperties.columns.f1
- sql13.swb.indexproperties.options.f1
- sql13.swb.indexproperties.spatial.f1
ms.assetid: 45efd81a-3796-4b04-b0cc-f3deec94c733
caps.latest.revision: 38
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d51449f61a3c324952946704c2df5bcfecf5cb84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="index-properties-f1-help"></a>Indexeigenschaften (F1-Hilfe)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In den Abschnitten dieses Themas werden verschiedene Indexeigenschaften beschrieben, die in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Dialogfeldern verfügbar sind.  
  
 **In diesem Thema:**  
  
 [Indexeigenschaften auf der Seite "Allgemein"](#General)  
  
 [(Index-)spalten auswählen (Dialogfeld)](#Columns)  
  
 [Indexeigenschaften auf der Seite "Speicher"](#Storage)  
  
 [Indexeigenschaften auf der Seite "Räumlich"](#Spatial)  
  
 [Indexeigenschaften auf der Seite "Filter"](#Filter)  
  
##  <a name="General"></a> Indexeigenschaften auf der Seite "Allgemein"  
 Auf der Seite Allgemein können Sie die Indexeigenschaften für die ausgewählte Tabelle oder Sicht anzeigen und ändern. Die Optionen für jede Seite ändern sich möglicherweise abhängig vom ausgewählten Indextyp.  
  
 **Tabellenname**  
 Zeigt den Namen der Tabelle oder Sicht an, für die der Index erstellt wurde. Dieses Feld ist schreibgeschützt. Um eine andere Tabelle auszuwählen, schließen Sie die Seite Indexeigenschaften, wählen Sie die richtige Tabelle aus, und öffnen Sie die Seite Indexeigenschaften erneut.  
  
 Räumliche Indizes können nicht für indizierte Sichten angegeben werden. Räumliche Indizes können nur für eine Tabelle definiert werden, die einen Primärschlüssel aufweist. Die maximale Anzahl von Primärschlüsselspalten in einer Tabelle beträgt 15. Die kombinierte Größe pro Zeile der Primärschlüsselspalten ist auf maximal 895 Bytes beschränkt.  
  
 **Indexname**  
 Zeigt den Namen des Indexes an. Dieses Feld ist bei einem vorhandenen Index schreibgeschützt. Wenn ein neuer Index erstellt wird, geben Sie den Namen des Indexes an.  
  
 **Indextyp**  
 Gibt den Indextyp an. Gibt bei neuen Indizes den Indextyp an, der beim Öffnen des Dialogfelds ausgewählt ist. Indizes können folgende Typen aufweisen: **Gruppiert**, **Nicht gruppiert**, **Primäre XML**, **Sekundäre XML**, **Räumlich**, **Gruppierter Columnstore**oder **Nicht gruppierter Columnstore**.  
  
 **Hinweis** Es ist nur ein gruppierter Index pro Tabelle zulässig. Pro Tabelle ist nur ein speicheroptimierter xVelocity-columnstore-Index zulässig.  
  
 **Eindeutig**  
 Durch Aktivierung dieses Kontrollkästchens wird der Index zu einem eindeutigen Index gemacht. Zwei Zeilen mit demselben Wert sind dann nicht zulässig. Standardmäßig ist dieses Kontrollkästchen deaktiviert. Wenn beim Ändern eines vorhandenen Indexes zwei Zeilen denselben Wert aufweisen, schlägt die Indexerstellung fehl. In Spalten, in denen NULL-Werte zulässig sind, ist bei einem eindeutigen Index ein NULL-Wert zulässig.  
  
 Wenn Sie im Feld **Indextyp** die Option **Räumlich** auswählen, ist das Kontrollkästchen **Eindeutig** abgeblendet.  
  
 **Indexschlüsselspalten**  
 Fügt die gewünschten Spalten dem Raster **Indexschlüsselspalten** hinzu. Wenn mehr als eine Spalte hinzugefügt wird, müssen die Spalten in der gewünschten Reihenfolge aufgeführt werden. Die Spaltenreihenfolge in einem Index kann einen großen Einfluss auf die Leistung des Indexes haben.  
  
 Es können nicht mehr als 16 Spalten an einem einzelnen zusammengesetzten Index beteiligt sein. Im Fall von mehr als 16 Spalten finden Sie weitere Informationen am Ende dieses Themas unter "Eingeschlossene Spalten".  
  
 Ein räumlicher Index kann nur für eine einzelne Spalte definiert werden, die einen räumlichen Datentyp aufweist (eine *räumliche Spalte*).  
  
 **Name**  
 Zeigt den Namen der Spalte an, die am Indexschlüssel beteiligt ist.  
  
 **Sortierreihenfolge**  
 Gibt die Sortierreihenfolge der ausgewählten Indexspalte an, entweder **Aufsteigend** oder **Absteigend**.  
  
> [!NOTE]  
>  Wenn der Indextyp **Primär-XML** oder **Räumlich**ist, wird diese Spalte nicht in der Tabelle aufgeführt.  
  
 **Datentyp**  
 Zeigt die Datentypinformationen an.  
  
> [!NOTE]  
>  Wenn die Tabellenspalte eine berechnete Spalte ist, wird unter **Datentyp** "berechnete Spalte" angezeigt.  
  
 **Größe**  
 Zeigt die maximale Anzahl von Bytes an, die für das Speichern der Spaltendatentypen benötigt wird. Zeigt eine Null (0) für eine räumliche oder XML-Spalte an.  
  
 **Identität**  
 Zeigt an, ob die am Indexschlüssel beteiligte Spalte eine Identitätsspalte ist.  
  
 **NULL-Werte zulassen**  
 Zeigt an, ob in der am Indexschlüssel beteiligten Spalte NULL-Werte in der Tabellen- oder Sichtspalte gespeichert werden dürfen.  
  
 **Hinzufügen**  
 Fügt dem Indexschlüssel eine Spalte hinzu. Wählen Sie im Dialogfeld **Select Columns from** (Spalten auswählen aus) *\<table name>* Tabellenspalten aus. Dieses Dialogfeld wird angezeigt, wenn Sie auf **Hinzufügen** klicken. Wenn Sie eine Spalte ausgewählt haben, ist diese Schaltfläche bei einem räumlichen Index abgeblendet.  
  
 **Entfernen**  
 Entfernt die ausgewählte Spalte aus der Beteiligung am Indexschlüssel.  
  
 **Nach oben**  
 Verschiebt die ausgewählte Spalte im Indexschlüsselraster nach oben.  
  
 **Nach unten**  
 Verschiebt die ausgewählte Spalte im Indexschlüsselraster nach unten.  
  
 **columnstore-Spalten**  
 Klicken Sie auf **Hinzufügen** , um Spalten für den columnstore-Index auszuwählen. Einschränkungen für einen Columnstore-Index finden Sie unter [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).  
  
 **Eingeschlossene Spalten**  
 Nimmt Nichtschlüsselspalten in den nicht gruppierten Index auf. Mit dieser Option können Sie die aktuellen Indexgrenzwerte hinsichtlich der Gesamtgröße eines Indexschlüssels und der maximalen Anzahl der Spalten in einem Indexschlüssel umgehen, indem Sie Spalten auf Blattebene eines nicht gruppierten Indexes als Nichtschlüsselspalten hinzufügen. Weitere Informationen finden Sie unter [Erstellen von Indizes mit eingeschlossenen Spalten](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
##  <a name="Columns"></a> (Index-)spalten auswählen (Dialogfeld)  
 Mithilfe dieser Seite können Sie der Seite **Indexeigenschaften, Allgemein** beim Erstellen oder Ändern eines Indexes Spalten hinzufügen.  
  
 **Kontrollkästchen**  
 Aktivieren Sie diese Option, um Spalten hinzuzufügen.  
  
 **Name**  
 Der Name der Spalte.  
  
 **Datentyp**  
 Der Datentyp der Spalte.  
  
 **Byte**  
 Die Größe der Spalte in Bytes.  
  
 **Identität**  
 Zeigt bei Identitätsspalten **Ja** an. Wenn die Spalte keine Identitätsspalte ist, wird **Nein** angezeigt.  
  
 **Allow Nulls**  
 Zeigt **Ja** an, wenn die Tabellendefinition für die Spalte NULL-Werte zulässt. Zeigt **Nein** an, wenn die Tabellendefinition für die Spalte keine NULL-Werte zulässt.  
  
##  <a name="Storage"></a> Optionen auf der Seite "Speicher"  
 Auf dieser Seite können Sie Dateigruppen- bzw. Partitionsschemaeigenschaften für den ausgewählten Index anzeigen und ändern. Zeigt nur Optionen in Zusammenhang mit dem Indextyp an.  
  
 **Dateigruppe**  
 Speichert den Index in der angegebenen Dateigruppe. Diese Liste enthält nur Standarddateigruppen (ROW). Die Standardauswahl in der Liste ist die PRIMARY-Dateigruppe der Datenbank. Weitere Informationen finden Sie unter [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 **FILESTREAM-Dateigruppe**  
 Gibt die Dateigruppe für FILESTREAM-Daten an. Diese Liste zeigt nur FILESTREAM-Dateigruppen an. Die Standardlistenauswahl ist die Dateigruppe PRIMARY FILESTREAM. Weitere Informationen finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 **Partitionsschema**  
 Speichert den Index in einem Partitionsschema. Wenn Sie auf **Partitionsschema** klicken, wird das unten stehende Raster aktiviert. Die Standardlistenauswahl ist das für das Speichern der Tabellendaten verwendete Partitionsschema. Bei Auswahl eines anderen Partitionsschemas in der Liste werden die im Raster angezeigten Informationen aktualisiert. Weitere Informationen finden Sie unter [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 Die Option Partitionsschema ist nicht verfügbar, wenn in der Datenbank keine Partitionsschemas vorhanden sind.  
  
 **Dateidatenstrom-Partitionsschema**  
 Gibt das Partitionsschema für FILESTREAM-Daten an. Das Partitionsschema muss mit dem Schema symmetrisch sein, das in der Option **Partitionsschema** angegeben wird.  
  
 Wenn die Tabelle nicht partitioniert ist, ist das Feld leer.  
  
 **Partitionsschemaparameter**  
 Zeigt den Namen der Spalte an, die Teil des Partitionsschemas ist.  
  
 **Tabellenspalte**  
 Wählt die Tabelle oder Sicht aus, die dem Partitionsschema zugeordnet werden soll.  
  
 **Datentyp der Spalte**  
 Zeigt Datentypinformationen zu der Spalte an.  
  
> [!NOTE]  
>  Wenn die Tabellenspalte eine berechnete Spalte ist, wird unter **Spaltendatentyp** „berechnete Spalte“ angezeigt.  
  
 **Onlineverarbeitung von DML-Anweisungen während der Indexverschiebung zulassen**  
 Ermöglicht Benutzern während des Indexvorgangs den Zugriff auf die zugrunde liegenden Tabellen- bzw. gruppierten Indexdaten und zugehörigen nicht gruppierten Indizes. Weitere Informationen finden Sie unter [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
> [!NOTE]  
>  Diese Option ist für XML-Indizes nicht verfügbar. Das gilt auch, wenn der Index ein deaktivierter gruppierter Index ist.  
  
 **Maximalen Grad an Parallelität festlegen**  
 Begrenzt die Anzahl der bei der Ausführung paralleler Pläne einzusetzenden Prozessoren. Der Standardwert ist 0; bei diesem Wert wird die tatsächliche Anzahl der verfügbaren CPUs verwendet. Wenn Sie den Wert auf 1 setzen, wird die Ausführung paralleler Pläne unterdrückt; bei einem Wert von größer als 1 wird die maximale Anzahl der bei der Ausführung einer einzelnen Abfrage zu verwendenden Prozessoren begrenzt. Diese Option ist nur verfügbar, wenn sich das Dialogfeld im Status **Neu organisieren** oder **Neu erstellen** befindet. Weitere Informationen finden Sie unter [Set the Max Degree of Parallelism Option for Optimal Performance](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md).  
  
> [!NOTE]  
>  Wird ein Wert angegeben, der über der Anzahl der verfügbaren CPUs liegt, wird die tatsächliche Anzahl der CPUs verwendet.  
  
##  <a name="Spatial"></a> Indexoptionen auf der Seite "Räumlich"  
 Auf der Seite **Räumlich** können Sie die Werte der räumlichen Eigenschaften anzeigen oder angeben. Weitere Informationen finden Sie unter [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
### <a name="bounding-box"></a>Umgebendes Feld  
 Das *umgebende Feld* ist der Umkreis des Rasters der höchsten Ebene einer geometrischen Ebene. Die Parameter für das umgebende Feld sind nur im Geometrierastermosaik vorhanden. Diese Parameter sind nicht verfügbar, wenn das **Mosaikschema** auf **Geografieraster**festgelegt ist.  
  
 In dem Bereich werden die Koordinaten **(***X-min***, ***Y-min***)** und **(***X-max***, ***Y-max***)** des umgebenden Felds angezeigt. Es gibt keine Standardkoordinatenwerte. Daher müssen Sie die Koordinatenwerte angeben, wenn Sie einen neuen räumlichen Index für eine Spalte vom Typ **geometry** erstellen.  
  
 **X-min**  
 Die X-Koordinate der unteren linken Ecke des umgebenden Felds.  
  
 **Y-min**  
 Die Y-Koordinate der unteren linken Ecke des umgebenden Felds.  
  
 **X-max**  
 Die X-Koordinate der oberen rechten Ecke des umgebenden Felds.  
  
 **Y-max**  
 Die Y-Koordinate der oberen rechten Ecke des umgebenden Felds.  
  
### <a name="general"></a>Allgemein  
 **Mosaikschema**  
 Gibt das Mosaikschema für den Index an. Folgende Mosaikschemas werden unterstützt.  
  
 **Geometrieraster**  
 Gibt das Mosaikschema für das Geometrieraster an, das für eine Spalte mit dem Datentyp **geometry** gilt.  
  
 **Automatisches Geometrieraster**  
 Diese Option wird für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert, wenn der Datenbank-Kompatibilitätsgrad auf 110 oder höher festgelegt wird.  
  
 **Geografieraster**  
 Gibt das Mosaikschema für das Geografieraster an, das für eine Spalte mit dem Datentyp **geography** gilt.  
  
 **Automatisches Geografieraster**  
 Diese Option wird für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert, wenn der Datenbank-Kompatibilitätsgrad auf 110 oder höher festgelegt wird.  
  
 Informationen darüber, wie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Mosaik implementiert wird, finden Sie unter [Räumliche Daten &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
 **Zellen pro Objekt**  
 Gibt die Anzahl von Zellen pro Objekt für das Mosaik an, die für ein einzelnes räumliches Objekt im Index verwendet werden können. Bei dieser Zahl kann es sich um jede ganze Zahl von 1 bis 8192 handeln. Der Standardwert ist 16. Der Wert lautet 8 für frühere Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , wenn der Datenbank-Kompatibilitätsgrad auf 110 oder höher festgelegt wird.  
  
 Auf höchster Ebene verwendet die Indizierung die Anzahl von Zellen, die zum Bereitstellen eines vollständigen Mosaiks der höchsten Ebene erforderlich sind, wenn ein Objekt mehr Zellen abdeckt, als durch *n*angegeben sind. In solchen Fällen ist es möglich, dass ein Objekt mehr als die angegebene Anzahl von Zellen erhält. Die maximale Anzahl ist dann die Anzahl von Zellen, die von dem Raster der höchsten Ebene generiert wird, welche von der Dichte der **Ebene 1** abhängt.  
  
### <a name="grids"></a>Raster  
 In diesem Bereich wird die Dichte des Rasters auf jeder Ebene des Mosaikschemas angezeigt. Die Dichte wird als **Niedrig**, **Mittel**oder **Hoch**angegeben. Der Standardwert ist **Mittel**. **Niedrig** stellt ein Raster aus 4x4, also 16 Zellen, **Mittel** ein Raster aus 8x8, also 64 Zellen, und **Hoch** ein Raster aus 16x16, also 256 Zellen, dar. Diese Optionen sind nicht verfügbar, wenn die Mosaikoptionen **Automatisches Geometrieraster** oder **Automatisches Geografieraster** nicht ausgewählt sind.  
  
 **Ebene 1**  
 Die Dichte des Rasters der obersten (höchsten) Ebene.  
  
 **Ebene 2**  
 Die Dichte des Rasters der zweiten Ebene.  
  
 **Ebene 3**  
 Die Dichte des Rasters der dritten Ebene.  
  
 **Ebene 4**  
 Die Dichte des Rasters der vierten Ebene.  
  
##  <a name="Filter"></a> Seite "Filter"  
 Auf dieser Seite können Sie das Filterprädikat für einen gefilterten Index eingeben. Weitere Informationen finden Sie unter [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 **Filterausdruck**  
 Definiert, welche Datenzeilen in den gefilterten Index eingeschlossen werden sollen. Beispiel: `StartDate > '20000101' AND EndDate IS NOT NULL'.`  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Festlegen von Indexoptionen](../../relational-databases/indexes/set-index-options.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
