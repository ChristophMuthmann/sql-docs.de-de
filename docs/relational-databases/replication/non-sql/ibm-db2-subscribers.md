---
title: IMB DB2-Abonnenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-SQL Server Subscribers, IBM DB2
- data types [SQL Server replication], non-SQL Server Subscribers
- IBM DB2 Subscribers
- mapping data types [SQL Server replication]
- heterogeneous Subscribers, IBM DB2
ms.assetid: a1a27b1e-45dd-4d7d-b6c0-2b608ed175f6
caps.latest.revision: 74
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6fa91235b6de818646673afd4e637083c5a6660c
ms.lasthandoff: 04/11/2017

---
# <a name="ibm-db2-subscribers"></a>IBM DB2-Abonnenten
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt Pushabonnements für IBM DB2/AS 400, DB2/MVS und DB2/Universal Database über die OLE DB-Anbieter, die mit [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host Integration-Server bereitgestellt werden.  
  
## <a name="configuring-an-ibm-db2-subscriber"></a>Konfigurieren eines IBM DB2-Abonnenten  
 Führen Sie zum Konfigurieren eines IBM DB2-Abonnenten die folgenden Schritte aus:  
  
1.  Installieren Sie die neueste Version des [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB-Anbieters für DB2 auf dem Verteiler:  
  
    -   Wenn Sie [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition verwenden, klicken Sie auf der Webseite [SQL Server Downloads](http://go.microsoft.com/fwlink/?LinkId=149256) (in Englisch) im Abschnitt **Verwandte Downloads** auf den Link zur aktuellen Version des Microsoft SQL Server Feature Packs. Suchen Sie auf der Webseite **Microsoft SQL Server Feature Pack** nach **Microsoft OLE DB-Anbieter für DB2**.  
  
    -   Wenn Sie [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Standard Edition verwenden, installieren Sie die aktuelle Version von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Host [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Server (HIS). Der Anbieter ist in diesem Produkt enthalten.  
  
     Zusätzlich zum Anbieter sollten Sie das Data Access Tool installieren, das im nächsten Schritt verwendet wird (es wird standardmäßig mit dem Download für [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] Enterprise Edition installiert). Weitere Informationen zum Installieren und Verwenden des Data Access Tools finden Sie in der Anbieter- oder der HIS-Dokumentation.  
  
2.  Erstellen Sie eine Verbindungszeichenfolge für den Abonnenten. Die Verbindungszeichenfolge kann in einem beliebigen Text-Editor erstellt werden, Sie sollten jedoch das Data Access Tool verwenden. So erstellen Sie die Zeichenfolge im Data Access Tool  
  
    1.  Zeigen Sie im Menü **Start**auf **Programme**, dann auf **Microsoft OLE DB-Anbieter für DB2**, und klicken Sie dann auf **Data Access Tool**.  
  
    2.  Folgen Sie im Data Access Tool ****den Anweisungen, um die Informationen zum DB2-Server anzugeben. Wenn Sie das Tool abgeschlossen haben, wird ein universeller Datenlink (Universal Data Link, UDL) mit einer zugeordneten Verbindungszeichenfolge erstellt (die UDL wird nicht tatsächlich von der Replikation verwendet, sondern die Verbindungszeichenfolge).  
  
    3.  Greifen Sie auf die Verbindungszeichenfolge zu: Klicken Sie mit der rechten Maustaste auf die UDL im Data Access Tool, und wählen Sie **Verbindungszeichenfolge anzeigen**aus.  
  
     Die Verbindungszeichenfolge ähnelt dem Folgenden (der Zeilenumbruch dient der besseren Lesbarkeit):  
  
    ```  
    Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
    PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
    Default Schema=MY_SCHEMA;Process Binary as Character=False;Derive Parameters=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
    Persist Security Info=False;Connection Pooling=True;  
    ```  
  
     Die meisten Optionen in der Zeichenfolge beziehen sich speziell auf den DB2-Server, den Sie konfigurieren. Die Optionen `Process Binary as Character` und `Derive Parameters` sollten jedoch immer auf `False` festgelegt sein. Für die Option `Initial Catalog` ist ein Wert erforderlich, um die Abonnementdatenbank identifizieren zu können. Die Verbindungszeichenfolge wird beim Erstellen des Abonnements in Assistenten für neue Abonnements eingegeben.  
  
3.  Erstellen Sie eine Momentaufnahme- oder Transaktionsveröffentlichung, aktivieren Sie sie für Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten, und erstellen Sie dann ein Pushabonnement für den Abonnenten. Weitere Informationen finden Sie unter [Create a Subscription for a Non-SQL Server Subscriber](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
4.  Sie können auch ein benutzerdefiniertes Erstellungsskript für einen oder mehrere Artikel angeben. Beim Veröffentlichen einer Tabelle wird ein `CREATE TABLE`-Skript für diese Tabelle erstellt. Bei Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten wird das Skript im [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Dialekt erstellt und dann vom Verteilungs-Agent in einen allgemeineren SQL-Dialekt übersetzt, bevor es auf dem Abonnenten angewendet wird. Um ein benutzerdefiniertes Erstellungsskript anzugeben, ändern Sie entweder das vorhandene [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript, oder erstellen Sie ein vollständiges Skript, das den DB2 SQL-Dialekt verwendet. Wenn Sie ein DB2-Skript erstellen, verwenden Sie die **bypass_translation** -Direktive, damit der Verteilungs-Agent das Skript ohne Übersetzung auf dem Abonnenten anwendet.  
  
     Skripts können aus verschiedenen Gründen geändert werden, der häufigste Grund ist jedoch das Ändern von Datentypzuordnungen. Weitere Informationen dazu finden Sie unter den Überlegungen zu Datentypänderungen in diesem Thema. Wenn Sie das [!INCLUDE[tsql](../../../includes/tsql-md.md)] -Skript ändern, sollten sich Änderungen ausschließlich auf Datentypzuordnungen beziehen (und das Skript darf keine Kommentare enthalten). Wenn weit reichendere Änderungen erforderlich sind, erstellen Sie ein DB2-Skript.  
  
     **So ändern Sie ein Artikelskript und stellen Sie es als benutzerdefiniertes Erstellungsskript bereit**  
  
    1.  Nachdem die Momentaufnahme für die Veröffentlichung generiert wurde, wechseln Sie in den Momentaufnahmeordner für die Veröffentlichung.  
  
    2.  Suchen Sie die Datei `.sch`, die denselben Namen wie der Artikel trägt, z.B. `MyArticle.sch`.  
  
    3.  Öffnen Sie diese Datei im Editor oder einem anderen Text-Editor.  
  
    4.  Ändern Sie die Datei, und speichern Sie sie in einem anderen Verzeichnis.  
  
    5.  Führen Sie `sp_changearticle`aus, und geben Sie dabei den Dateipfad und den Namen für die *creation_script* -Eigenschaft an. Weitere Informationen finden Sie unter [sp_changearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md).  
  
     **So erstellen Sie ein Artikelskript und stellen Sie es als benutzerdefiniertes Erstellungsskript bereit**  
  
    1.  Erstellen Sie mit dem DB2 SQL-Dialekt ein Artikelskript. Stellen Sie sicher, dass **bypass_translation**die erste Zeile in der Datei ist und nichts sonst in der Zeile steht.  
  
    2.  Führen Sie sp_changearticle aus, wobei Sie den Dateipfad und den Namen für die Eigenschaft *creation_script* angeben.  
  
## <a name="considerations-for-ibm-db2-subscribers"></a>Überlegungen zu IBM DB2-Abonnenten  
 Berücksichtigen Sie beim Replizieren auf DB2-Abonnenten neben den Überlegungen im Thema [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)die folgenden Aspekte:  
  
-   Die Daten und Indizes für jede replizierte Tabelle werden einem DB2-Tabellenbereich zugewiesen. Die Seitengröße eines DB2-Tabellenbereichs steuert die maximale Spaltenzahl und die maximale Zeilengröße der zum Tabellenbereich gehörenden Tabellen. Stellen Sie sicher, dass sich der Tabellenbereich, der replizierten Tabellen zugeordnet ist, hinsichtlich der Zahl der replizierten Spalten und der maximalen Zeilengröße der Tabellen eignet.  
  
-   Veröffentlichen Sie Tabellen nicht mithilfe der Transaktionsreplikation auf DB2-Abonnenten, wenn eine oder mehrere Fremdschlüsselspalten in der Tabelle den DECIMAL(32-38, 0-38)- oder NUMERIC(32-38, 0-38)-Datentyp aufweist. Bei der Transaktionsreplikation werden Zeilen anhand des Primärschlüssels identifiziert. Das kann zu Fehlern führen, weil diese Datentypen VARCHAR(41) auf dem Abonnenten zugeordnet sind. Tabellen mit Primärschlüsseln, die diesen Datentyp verwenden, können mithilfe der Momentaufnahmereplikation veröffentlicht werden.  
  
-   Wenn Sie Tabellen auf dem Abonnenten im Voraus erstellen möchten statt später durch die Replikation, verwenden Sie die Option replication support only. Weitere Informationen finden Sie unter [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
-   In[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] werden längere Tabellen- und Spaltennamen als DB2 unterstützt:  
  
    -   Wenn die Veröffentlichungsdatenbank Tabellen mit längeren Namen enthält, als von der DB2-Version auf dem Abonnenten unterstützt werden, geben Sie einen alternativen Namen für die destination_table-Artikeleigenschaft an. Weitere Informationen zum Festlegen von Eigenschaften beim Erstellen einer Veröffentlichung finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
    -   Es können keine alternativen Spaltennamen angegeben werden. Stellen Sie sicher, dass veröffentlichte Tabellen keine längeren Spaltennamen enthalten, als von der DB2-Version auf dem Abonnenten unterstützt werden.  
  
## <a name="mapping-data-types-from-sql-server-to-ibm-db2"></a>Zuordnung zwischen Datentypen von SQL Server und IBM DB2  
 Die folgende Tabelle zeigt die Datentypzuordnungen, die beim Replizieren von Daten auf einen Abonnenten mit IBM DB2 verwendet werden.  
  
|SQL Server-Datentyp|IBM DB2-Datentyp|  
|--------------------------|-----------------------|  
|**bigint**|DECIMAL(19,0)|  
|**binary(1-254)**|CHAR(1-254) FOR BIT DATA|  
|**binary(255-8000)**|VARCHAR(255-8000) FOR BIT DATA|  
|**bit**|SMALLINT|  
|**char(1-254)**|CHAR(1-254)|  
|**char(255-8000)**|VARCHAR(255-8000)|  
|**date**|DATE|  
|**datetime**|TIMESTAMP|  
|**datetime2(0-7)**|VARCHAR(27)|  
|**datetimeoffset(0-7)**|VARCHAR(34)|  
|**decimal(1-31, 0-31)**|DECIMAL(1-31, 0-31)|  
|**decimal(32-38, 0-38)**|VARCHAR(41)|  
|**float(53)**|DOUBLE|  
|**float**|GLEITKOMMAZAHL|  
|**geography**|IMAGE|  
|**Geometrie**|IMAGE|  
|**hierarchyid**|IMAGE|  
|**image**|VARCHAR(0) FOR BIT DATA*|  
|**into**|INT|  
|**money**|DECIMAL(19,4)|  
|**nchar(1-4000)**|VARCHAR(1-4000)|  
|**ntext**|VARCHAR(0)*|  
|**numeric(1-31, 0-31)**|DECIMAL(1-31,0-31)|  
|**numeric(32-38, 0-38)**|VARCHAR(41)|  
|**nvarchar(1-4000)**|VARCHAR(1-4000)|  
|**nvarchar(max)**|VARCHAR(0)*|  
|**real**|real|  
|**smalldatetime**|TIMESTAMP|  
|**smallint**|SMALLINT|  
|**smallmoney**|DECIMAL(10,4)|  
|**sql_variant**|–|  
|**sysname**|VARCHAR(128)|  
|**text**|VARCHAR(0)*|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|CHAR(8) FOR BIT DATA|  
|**tinyint**|SMALLINT|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-8000)**|VARCHAR(1-8000) FOR BIT DATA|  
|**varchar(1-8000)**|VARCHAR(1-8000)|  
|**varbinary(max)**|VARCHAR(0) FOR BIT DATA*|  
|**varchar(max)**|VARCHAR(0)*|  
|**xml**|VARCHAR(0)*|  
  
* Im nächsten Abschnitt finden Sie weitere Informationen zu den Zuordnungen zu VARCHAR(0).  
  
### <a name="data-type-mapping-considerations"></a>Überlegungen zur Datentypzuordnung  
 Berücksichtigen Sie die folgenden Überlegungen zur Datentypzuordnung beim Replizieren auf DB2-Abonnenten:  
  
-   Beim Zuordnen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**auf **varchar**auf **binary** und **varbinary** zu den DB2-Datentypen CHAR, VARCHAR, CHAR FOR BIT DATA bzw. VARCHAR FOR BIT DATA wird bei der Replikation die Länge des DB2-Datentyps auf die Länge des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Typs festgelegt.  
  
     Dadurch kann die Tabelle erfolgreich auf dem Abonnenten erstellt werden, sofern die Einschränkung der DB2-Seitengröße die maximale Größe der Zeile zulässt. Stellen Sie sicher, dass die für den Zugriff auf die DB2 verwendete Anmeldung über die Berechtigungen verfügt, um auf Tabellenbereiche von ausreichender Größe für die auf DB2 zu replizierenden Tabellen zugreifen zu können.  
  
-   DB2 unterstützt VARCHAR-Spalten bis zu 32 KB. Deshalb können einige LOB-Spalten (Large Object) von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ordnungsgemäß VARCHAR-Spalten von DB2 zugeordnet werden. Der von der Replikation für DB2 verwendete OLE DB-Anbieter unterstützt jedoch keine Zuordnung von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -LOB zu DB2-LOB. Deshalb werden die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **text**auf **varchar(max)**auf **ntext**und **nvarchar(max)** in den generierten Erstellungsskripts VARCHAR(0) zugeordnet. Der Längenwert 0 muss in einen ordnungsgemäßen Wert geändert werden, bevor das Skript auf den Abonnenten angewendet wird. Wird die Länge des Datentyps nicht geändert, löst DB2 Fehler 604 bei dem Versuch der Tabellenerstellung auf dem DB2-Abonnenten aus (Fehler 604 bedeutet, dass das Genauigkeits- oder Längenattribut des Datentyps ungültig ist).  
  
     Bestimmen Sie basierend auf Ihrer Kenntnis der von Ihnen replizierten Quelltabelle, ob es angemessen ist, einen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -LOB einem DB2-Objekt variabler Länge zuzuordnen, und geben Sie eine angemessene maximale Länge in einem benutzerdefinierten Erstellungsskript an. Informationen zum Angeben eines benutzerdefinierten Erstellungsskripts finden Sie in Schritt 5 im Abschnitt zum Konfigurieren eines IBM DB2-Abonnenten in diesem Thema.  
  
    > [!NOTE]  
    >  Die angegebene Länge für den DB2-Typ kann beim Kombinieren mit anderen Spaltenlängen die maximale Zeilengröße nicht überschreiten, die auf dem DB2-Tabellenbereich basiert, dem die Tabellendaten zugewiesen sind.  
  
     Wenn keine geeignete Zuordnung für eine LOB-Spalte vorhanden ist, verwenden Sie die Spaltenfilterung für die Artikel, sodass die Spalte nicht repliziert wird. Weitere Informationen finden Sie unter [Filtern von veröffentlichten Daten](../../../relational-databases/replication/publish/filter-published-data.md).  
  
-   Beim Replizieren der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **nchar** und **nvarchar** auf die DB2-Datentypen CHAR und VARCHAR werden dieselben Längenbezeichner für den DB2-Typ wie für den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Typs festgelegt. Die Datentyplänge ist jedoch möglicherweise zu gering für die generierte DB2-Tabelle  
  
     In einigen DB2-Umgebungen ist ein [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char** nicht auf Ein-Byte-Zeichen beschränkt. Bei der Länge eines CHAR- oder VARCHAR-Elements muss dies berücksichtigt werden. Sie müssen auch *Rückschaltungs* - und *Dauerumschaltungs* zeichen berücksichtigen, wenn diese benötigt werden. Wenn Sie Tabellen mit **nchar** - und **nvarchar** -Spalten replizieren, müssen Sie gegebenenfalls eine größere maximale Länge für die Datentypen in einem benutzerdefinierten Erstellungsskript angeben. Informationen zum Angeben eines benutzerdefinierten Erstellungsskripts finden Sie in Schritt 5 im Abschnitt zum Konfigurieren eines IBM DB2-Abonnenten in diesem Thema.  
  
## <a name="see-also"></a>Siehe auch  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Abonnieren von Veröffentlichungen](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  

