---
title: "Verwalten von Identit&#228;tsspalten | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Identitätswerte [SQL Server-Replikation]"
  - "Mergereplikation [SQL Server-Replikation], Verwaltung von Identitätsbereichen"
  - "Veröffentlichen [SQL Server-Replikation], Identitätsspalten"
  - "Transaktionsreplikation, Verwaltung von Identitätsbereichen"
  - "Identitätsspalten [SQL Server-Replikation], Replikation"
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Verwalten von Identit&#228;tsspalten
  In diesem Thema wird beschrieben, wie Identitätsspalten in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../../includes/tsql-md.md)] verwaltet werden. Wenn Einfügungen von Abonnenten zurück auf den Verleger repliziert werden, müssen Identitätsspalten verwaltet werden, um zu verhindern, dass der gleiche Identitätswert sowohl dem Abonnenten als auch dem Verleger zugewiesen wird. Die Replikation kann Identitätsbereiche automatisch verwalten, oder Sie können sich dafür entscheiden, Identitätsbereiche manuell zu verwalten.  Informationen über die Identität zur Verfügung gestellten Verwaltungsoptionen von der Replikation finden Sie unter [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
-   **So verwalten Sie Identitätsspalten mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   Wird eine Tabelle in mehr als einer Veröffentlichung veröffentlicht, müssen Sie für diese Veröffentlichungen die gleichen Verwaltungsoptionen für Identitätsbereiche angeben. Weitere Informationen finden Sie unter "Veröffentlichen von Tabellen in mehreren Veröffentlichungen" im [Veröffentlichen von Daten und Datenbankobjekten](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
-   Erstellen eine automatisch inkrementierten Nummer, die verwendet werden kann, in mehreren Tabellen oder von Anwendungen ohne Verweis auf eine Tabelle aufgerufen werden können, finden Sie unter [Sequenznummern](../../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
 Geben Sie eine Verwaltungsoption für die **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** im Dialogfeld des Assistenten für neue Veröffentlichung. Weitere Informationen zum Verwenden dieses Assistenten finden Sie unter [Erstellen einer Publikation](../../../relational-databases/replication/publish/create-a-publication.md). Führen Sie im Assistenten für neue Veröffentlichung folgende Aktionen aus:  
  
-   Bei Auswahl von **Mergepublikation** oder **Transaktionspublikation mit aktualisierbaren Abonnements** auf die **Veröffentlichungstyp** Seite, wählen Sie die automatische oder manuelle identitätsbereichsverwaltung (automatisch, der Standardwert wird empfohlen). Nach dem Veröffentlichen der Tabelle kann die Eigenschaft nicht geändert werden. Es können jedoch andere, verbundene Eigenschaften geändert werden.  
  
-   Wenn Sie andere Veröffentlichungstypen auswählen, legen Sie die manuelle Identitätsbereichsverwaltung fest.  
  
 Ändern Sie Identitätsbereiche und Schwellenwerte für die **Eigenschaften** auf der Registerkarte der **Artikeleigenschaften - \< Artikel>**, die in verfügbar ist die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld). Weitere Informationen zum Zugreifen auf dieses Dialogfeld finden Sie unter [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### So geben Sie eine Verwaltungsoption für Identitätsspalten an  
  
1.  Wenn der Verleger eine Version von ausgeführt wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], auf die **Veröffentlichungstyp** Seite des Assistenten für neue Veröffentlichung, wählen Sie **Mergepublikation** oder **Transaktionspublikation mit aktualisierbaren Abonnements**.  
  
2.  Auf der **Artikel** Seite, wählen Sie eine Tabelle mit einer Identitätsspalte.  
  
3.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Artikels festlegen**.  
  
4.  Auf der **Eigenschaften** auf der Registerkarte der **Artikeleigenschaften - \< Artikel>** im Feld der **Verwaltung von Identitätsbereichen** legen die **Identitätsbereiche automatisch verwalten** -Eigenschaft **automatische** oder **manuell** (für Verleger, auf denen [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] oder höher), oder **True** oder **False** (für Verleger, auf denen eine Version von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]).  
  
5.  Bei Auswahl von **automatische** oder **True** in Schritt 4, geben Sie Werte für die Optionen in der folgenden Tabelle. Weitere Informationen darüber, wie diese Einstellungen verwendet werden, finden Sie im Abschnitt "Zuweisen von Identität Bereiche" von [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
    |Option|Wert|Beschreibung|  
    |------------|-----------|-----------------|  
    |**Bereichsgröße auf dem Verleger**|Ganze Zahl für die Bereichsgröße (z. B. 20000).|Finden Sie im Abschnitt "Zuweisen von Identität Bereiche" [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Bereichsgröße auf dem Abonnenten**|Ganze Zahl für die Bereichsgröße (z. B. 10000).|Finden Sie im Abschnitt "Zuweisen von Identität Bereiche" [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Prozentsatz für Bereichsschwellenwert**|Ganze Zahl für Schwellenwert in Prozent (z. B. 90 entspricht 90 %)|Der Prozentsatz der Identitätswerte, die in einem Knoten insgesamt verwendet werden, bevor ein neuer Identitätsbereich zugewiesen wird.<br /><br /> <br /><br /> Hinweis: Dieser Wert muss angegeben werden, aber es wird nur von verwendet: Abonnenten mithilfe von Abonnements mit verzögerter Aktualisierung; und den Abonnenten zu Mergepublikationen mit [!INCLUDE[ssEW](../../../includes/ssew-md.md)] oder frühere Versionen von anderen SQL Server-Editionen. Weitere Informationen finden Sie im Abschnitt "Zuweisen von Identität Bereiche" [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Anfangswert des nächsten Bereichs**|Wert für ganze Zahl. Schreibgeschützt.|Der Wert, bei dem der nächste Bereich beginnt. Wenn der aktuelle Bereich z. B. 5001-6000 lautet, liegt dieser Wert bei 6001.|  
    |**Maximaler Identitätswert**|Wert für ganze Zahl. Schreibgeschützt.|Der größte Wert für die Identitätsspalte. Er wird durch den Basisdatentyp der Spalte bestimmt.|  
    |**Increment**|Wert für ganze Zahl. Schreibgeschützt.|Die Zahl, um die sich eine Identitätsspalte bei jeder Einfügung erhöhen oder verringern sollte: in der Regel auf 1 festgelegt.|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### So ändern Sie Identitätsbereiche und Schwellenwerte nach dem Veröffentlichen einer Tabelle  
  
1.  Auf der **Artikel** auf der Seite der **Veröffentlichungseigenschaften - \< Veröffentlichung>** Dialogfeld Wählen Sie eine Tabelle mit einer Identitätsspalte.  
  
2.  Klicken Sie auf **Artikeleigenschaften**und anschließend auf **Eigenschaften des hervorgehobenen Artikels festlegen**.  
  
3.  Auf der **Eigenschaften** Registerkarte der **Artikeleigenschaften - \< Artikel>** im Feld der **Verwaltung von Identitätsbereichen** Abschnitt, geben Sie Werte für eine oder mehrere der folgenden Eigenschaften: **Bereichsgröße auf dem Verleger**, **Bereichsgröße auf dem Abonnenten**, und **Schwellenwert in Prozent im Bereich**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Klicken Sie auf **OK** auf die **Veröffentlichungseigenschaften - \< Veröffentlichung>** (Dialogfeld).  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 Wenn ein Artikel erstellt wird, können Sie mithilfe gespeicherter Replikationsprozeduren Verwaltungsoptionen für Identitätsbereiche angeben.  
  
#### So aktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Wenn die zu veröffentlichende Quelltabelle eine Identitätsspalte verfügt, geben Sie den Wert **automatisch** für **@identityrangemanagementoption**, den Bereich von Identitätswerten zugewiesen, mit dem Verleger für **@pub_identity_range**, jedem Abonnenten zugewiesenen Bereich **@identity_range**, den Prozentsatz der gesamten Identitätswerte, die verwendet werden, bevor ein neuer Identitätsbereich zugewiesen ist **@threshold**. Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Vergewissern Sie sich, dass der Datentyp der Identitätsspalte groß genug ist, um den gesamten, allen Abonnenten zugewiesenen Identitätsbereich zu unterstützen.  
  
#### So deaktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Geben Sie den Wert **Manuelle** für **@identityrangemanagementoption**. Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Weisen Sie auf dem Abonnenten Identitätsartikelspalten Bereiche zu, um zu verhindern, dass für Updateabonnenten Konflikte auftreten. Weitere Informationen finden Sie im Abschnitt zum Zuweisen von Bereichen für die manuelle Verwaltung von Identitätsbereichen im Thema [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
#### So aktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Wenn die zu veröffentlichende Quelltabelle eine Identitätsspalte verfügt, geben Sie den Wert **automatisch** für **@identityrangemanagementoption**, Bereich von Identitätswerten für ein Serverabonnement **@pub_identity_range**, Bereich von Identitätswerten für den Verleger und jedem clientabonnement **@identity_range**, den Prozentsatz der gesamten Identitätswerte, die verwendet werden, bevor ein neuer Identitätsbereich zugewiesen ist **@threshold**. Weitere Informationen dazu, wann neue Identitätsbereiche zugewiesen werden, finden Sie unter Zuweisen von Identitätsbereichen im Thema [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md). Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Vergewissern Sie sich, dass der Datentyp der Identitätsspalte groß genug ist, um den gesamten, allen Abonnenten zugewiesenen Identitätsbereich zu unterstützen. Dies gilt besonders bei Abonnenten mit Serverabonnements.  
  
#### So deaktivieren Sie die automatische Identitätsbereichsverwaltung beim Definieren von Artikeln für eine Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Geben Sie einen der folgenden Werte für **@identityrangemanagementoption**:  
  
    -   **Manuelle** -Identitätsbereiche müssen manuell für Abonnenten mit Aktualisierung zugewiesen werden.  
  
    -   **keine** -Identity-Spalten auf dem Verleger werden nicht als Identitätsspalten auf dem Abonnenten definiert.  
  
     Weitere Informationen zum Definieren von Artikeln finden Sie unter [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Weisen Sie auf dem Abonnenten Identitätsartikelspalten Bereiche zu, um zu verhindern, dass für Updateabonnenten Konflikte auftreten.  
  
#### So ändern Sie die Einstellungen für die automatische Identitätsbereichsverwaltung für einen vorhandenen Artikel in einer Momentaufnahme- oder Transaktionsveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) und notieren Sie sich den Wert des **Identityrangemanagementoption** im Ergebnis festlegen. Wenn dieser Wert **0**, automatische identitätsbereichsverwaltung nicht aktiviert ist.  
  
2.  Wenn der Wert der **Identityrangemanagementoption** im Ergebnis ist **1**, ändern Sie die Einstellungen wie folgt:  
  
    -   Um die zugewiesenen Identitätsbereiche zu ändern, führen [Sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Identity_range** oder **Pub_identity_range** für **@property** und den neuen Bereichswert für **@value**.  
  
    -   Um den Schwellenwert ändern, an dem neue Identitätsbereiche zugewiesen werden, führen [Sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Schwellenwert** für **@property** und den neuen Schwellenwert für **@value**.  
  
#### So ändern Sie die Einstellungen für die automatische Identitätsbereichsverwaltung für einen vorhandenen Artikel in einer Mergeveröffentlichung  
  
1.  Führen Sie auf dem Verleger für die Veröffentlichungsdatenbank [Sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) und notieren Sie sich den Wert der **Identity_support** im Ergebnis festlegen. Wenn dieser Wert **0**, automatische identitätsbereichsverwaltung nicht aktiviert ist.  
  
2.  Wenn der Wert der **Identity_support** im Ergebnis ist **1**, ändern Sie die Einstellungen wie folgt:  
  
    -   Um die zugewiesenen Identitätsbereiche zu ändern, führen [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Identity_range** oder **Pub_identity_range** für **@property** und den neuen Bereichswert für **@value**.  
  
    -   Um den Schwellenwert ändern, an dem neue Identitätsbereiche zugewiesen werden, führen [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Schwellenwert** für **@property** und den neuen Schwellenwert für **@value**. Weitere Informationen dazu, wann neue Identitätsbereiche zugewiesen werden, finden Sie unter Zuweisen von Identitätsbereichen im Thema [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
    -   Führen Sie zum Deaktivieren der automatischen Verwaltung von Identitätsbereichen [Sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) auf dem Verleger für die Veröffentlichungsdatenbank. Geben Sie den Wert **Identityrangemanagementoption** für **@property** und entweder **Manuelle** oder **keine** für **@value**.  
  
## Siehe auch  
 [Peer-zu-Peer-Transaktionsreplikation](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Konzepte für gespeicherte Systemprozeduren für die Replikation](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Replizieren von Identitätsspalten](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  