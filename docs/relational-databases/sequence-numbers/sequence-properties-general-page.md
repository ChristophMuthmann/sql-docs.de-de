---
title: "Sequenzeigenschaften (Seite &quot;Allgemein&quot;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.sequence.general.f1"
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
caps.latest.revision: 10
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# Sequenzeigenschaften (Seite &quot;Allgemein&quot;)
  Erstellt ein Sequenzobjekt und gibt dessen Eigenschaften an. Als Sequenz wird ein benutzerdefiniertes schemagebundenes Objekt bezeichnet, das eine Sequenz numerischer Werte anhand der Spezifikation generiert, mit der die Sequenz erstellt wurde. Die Sequenz numerischer Werte wird in aufsteigender oder absteigender Reihenfolge in einem definierten Intervall generiert und kann so konfiguriert werden, dass sie beim Erreichen des Endes neu gestartet wird (Zyklus). Sequenzen werden anders als Identitätsspalten keinen bestimmten Tabellen zugeordnet. Anwendungen verweisen auf ein Sequenzobjekt, um dessen nächsten Wert abzurufen. Die Beziehung zwischen Sequenzen und Tabellen wird von der Anwendung gesteuert. Benutzeranwendungen können auf ein Sequenzobjekt verweisen und die Werte in mehreren Zeilen und Tabellen koordinieren.  
  
 Anders als Identitätsspaltenwerte, die beim Einfügen generiert werden, kann eine Anwendung durch Aufrufen der [NEXT VALUE FOR-Funktion](../../t-sql/functions/next-value-for-transact-sql.md)die nächste Sequenznummer abrufen, ohne die Zeile einzufügen. Mit [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) können Sie mehrere Sequenznummern gleichzeitig abrufen.  
  
 Informationen und Szenarien, in denen die **CREATE SEQUENCE**-Funktion und die **NEXT VALUE FOR**-Funktion verwendet werden, finden Sie unter [Sequenznummern](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 Auf diese Seite kann auf zwei Arten zugegriffen werden: Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf **Sequenzen** und anschließend auf **Neue Sequenz**, oder klicken Sie mit der rechten Maustaste auf eine vorhandene Sequenz und anschließend auf **Eigenschaften**. Wenn Sie mit der rechten Maustaste auf eine vorhandene Sequenz und anschließend auf **Eigenschaften** klicken, können Sie die Optionen nicht bearbeiten. Zum Ändern der Sequenzoptionen verwenden Sie die [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)-Anweisung, oder erstellen Sie das Sequenzobjekt durch Ziehen erneut.  
  
## Optionen  
 **Sequenzname**  
 Geben Sie hier den Sequenznamen ein.  
  
 **Sequenzschema**  
 Geben Sie das Schema an, das Besitzer dieser Sequenz ist.  
  
 **Datentyp**  
 Eine Sequenz kann als beliebiger ganzzahliger Typ definiert werden. Dies schließt Folgendes ein:  
  
|Datentyp|Bereich|  
|---------------|-----------|  
|**tinyint**|0 bis 255|  
|**smallint**|-32.768 bis 32.767|  
|**int**|-2.147.483.648 bis 2.147.483.647|  
|**bigint**|-9.223.372.036.854.775.808 bis 9.223.372.036.854.775.807|  
  
-   **decimal** oder **numeric** mit einer Skalierung von 0.  
  
-   Ein beliebiger benutzerdefinierter Datentyp (Aliastyp), der auf einem dieser Typen basiert.  
  
 **Genauigkeit**  
 Geben Sie für **decimal** oder **numeric** die Genauigkeit an. (Die Skalierung ist stets 0.)  
  
 **Startwert**  
 Der erste Wert, der vom Sequenzobjekt zurückgegeben wird. Der **START** -Wert muss kleiner oder gleich dem maximalen und größer oder gleich dem minimalen Wert des Sequenzobjekts sein. Der Standardstartwert eines neuen Sequenzobjekts ist gleich dem minimalen Wert eines aufsteigenden Sequenzobjekts und dem maximalen Wert eines absteigenden Sequenzobjekts.  
  
 **Erhöhen um**  
 Der Wert, um den der Wert des Sequenzobjekts bei jedem Aufruf der **NEXT VALUE FOR**-Funktion inkrementiert (oder bei negativem Wert dekrementiert) wird. Wenn als Inkrement ein negativer Wert verwendet wird, ist der Wert des Sequenzobjekts absteigend, andernfalls ist er aufsteigend. Das Inkrement kann nicht 0 sein.  
  
 **Mindestwert**  
 Gibt die Grenzen für das Sequenzobjekt an. Der minimale Standardwert eines neuen Sequenzobjekts ist gleich dem minimalen Wert für den Datentyp des Sequenzobjekts. Dieser ist für den **tinyint** -Datentyp 0 und für alle anderen Datentypen eine negative Zahl.  
  
 **Höchstwert**  
 Gibt die Grenzen für das Sequenzobjekt an. Der maximale Standardwert eines neuen Sequenzobjekts ist gleich dem maximalen Wert für den Datentyp des Sequenzobjekts.  
  
 **Zyklus – Sequenz wird bei Erreichen des Grenzwerts neu gestartet**  
 Wählen Sie aus, ob das Sequenzobjekt ab dem Mindestwert (oder, bei Sequenzobjekten mit absteigendem Wert, ab dem Maximalwert) erneut gestartet wird, wenn der jeweilige Mindest- bzw. Maximalwert überschritten wurde.  
  
> [!NOTE]  
>  Der Zyklus wird nicht ab dem Startwert erneut gestartet, sondern ab dem Mindest-/Maximalwert.  
  
 **Cacheoptionen**  
 Durch Erstellen eines Caches von Sequenzwerten können Sie die Leistung von Anwendungen erhöhen, von denen Sequenzobjekte verwendet werden, da Sie so die Anzahl der zum Erstellen von Sequenznummern erforderlichen Datenträger-E/As senken.  
  
-   Standardgröße – [!INCLUDE[ssDE](../../includes/ssde-md.md)] wählt eine Größe aus, Benutzer sollten sich jedoch nicht auf die Konsistenz der Auswahl verlassen. [!INCLUDE[msCoName](../../includes/msconame-md.md)] könnte die Methode zur Berechnung der Cachegröße ohne vorherige Ankündigung ändern.  
  
-   Kein Cache – Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden keine Sequenznummern zwischengespeichert.  
  
-   Cachegröße – Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Sequenzwerte zwischengespeichert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichert lediglich den aktuellen Wert und die Anzahl der im Cache verbleibenden Werte. Daher ist der zum Speichern des Caches erforderliche Arbeitsspeicher immer doppelt so groß wie zwei Instanzen des Sequenzobjekt-Datentyps.  
  
 Bei Erstellung mit der CACHE-Option können die Sequenznummern im Cache durch unerwartetes Herunterfahren, z. B. bei einem Stromausfall, verloren gehen.  
  
 Weitere Informationen zum Erstellen von Sequenzoptionen finden Sie unter [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## Berechtigungen  
 Erfordert die Berechtigung **CREATE SEQUENCE**, **ALTER**oder **CONTROL** für das SCHEMA.  
  
## Siehe auch  
 [sys.sequences &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)  
  
  