---
title: "Angeben der Weitergabemethode für Änderungen bei Transaktionsartikeln | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactional replication, propagation methods
ms.assetid: a10c5001-22cc-4667-8f0b-3d0818dca2e9
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 22e745406fe58c38e44e42395844a55efff3f57a
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="transactional-articles---specify-how-changes-are-propagated"></a>Transaktionsartikel – Angeben der Weitergabemethode für Änderungen
  Bei der Transaktionsreplikation können Sie angeben, wie Datenänderungen vom Verleger an den Abonnenten weitergegeben werden. Für jede veröffentlichte Tabelle können Sie eine von vier Methoden angeben, mit der jeder Vorgang (INSERT, UPDATE oder DELETE) an den Abonnenten weitergegeben werden soll:  
  
-   Angeben, dass die Transaktionsreplikation eine gespeicherte Prozedur zur Weitergabe von Änderungen an die Abonnenten ausgibt und anschließend aufruft (Standardeinstellung).  
  
-   Angeben, dass die Änderungen mithilfe einer INSERT-, UPDATE- oder DELETE-Anweisung weitergegeben werden sollen (Standardeinstellung bei Nicht-[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Abonnenten).  
  
-   Angeben, dass eine benutzerdefinierte gespeicherte Prozedur verwendet wird.  
  
-   Angeben, dass diese Aktion auf keinem Abonnenten ausgeführt wird. Transaktionen dieses Typs werden nicht repliziert.  
  
 Standardmäßig gibt die Transaktionsreplikation Änderungen an Abonnenten mithilfe einer Reihe gespeicherter Prozeduren weiter, die auf jedem Abonnenten gespeichert sind. Wenn eine Einfügung, ein Update oder eine Löschung an einer Tabelle auf dem Verleger vorgenommen wird, wird der Vorgang in einen Aufruf an eine gespeicherte Prozedur auf dem Abonnenten übersetzt. Die gespeicherte Prozedur akzeptiert Parameter, die den Spalten in der Tabelle zugeordnet sind, und lässt das Ändern dieser Spalten auf dem Abonnenten zu.  
  
 Informationen zum Festlegen der Propagierungsmethode für Datenänderungen an Transaktionsartikeln finden Sie unter [Festlegen der Propagierungsmethode für Datenänderungen an Transaktionsartikeln](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md).  
  
## <a name="default-and-custom-stored-procedures"></a>Standardmäßige und benutzerdefinierte gespeicherte Prozeduren  
 Die folgenden drei Prozeduren werden von der Replikation standardmäßig für jeden Tabellenartikel erstellt:  
  
-   **sp_MSins_\<** *Tabellenname* **>** behandelt Einfügungen.  
  
-   **sp_MSupd_\<** *Tabellenname* **>** behandelt Updates.  
  
-   **sp_MSdel_\<** *Tabellenname* **>** behandelt Löschvorgänge.  
  
 Der in der Prozedur verwendete **\<***Tabellenname***>** hängt davon ab, wie der Artikel der Veröffentlichung hinzugefügt wurde und ob die Abonnementdatenbank eine Tabelle mit demselben Namen und einem anderen Besitzer enthält.  
  
 Jede dieser Prozeduren kann durch eine benutzerdefinierte Prozedur ersetzt werden, die Sie beim Hinzufügen eines Artikels zur Veröffentlichung angeben. In einer Anwendung verwendete benutzerdefinierte Prozeduren erfordern eine benutzerdefinierte Logik: z. B. das Einfügen von Daten in eine Überwachungstabelle, wenn eine Zeile auf einem Abonnenten aktualisiert wird. Weitere Informationen zum Angeben von benutzerdefinierten gespeicherten Prozeduren finden Sie in den oben aufgeführten Themen.  
  
 Wenn Sie die Standardreplikationsprozeduren oder benutzerdefinierten Prozeduren angeben, geben Sie auch eine Aufrufsyntax für jede Prozedur an (bei Verwendung von Standardprozeduren werden diese Prozeduren von der Replikation ausgewählt). Die Aufrufsyntax legt die Struktur der für die Prozedur bereitgestellten Parameter fest und welche Informationen bei jeder Datenänderung an den Abonnenten gesendet werden. Weitere Informationen finden Sie im Abschnitt zur Aufrufsyntax für gespeicherte Prozeduren in diesem Thema.  
  
### <a name="considerations-for-using-custom-stored-procedures"></a>Überlegungen zum Verwenden benutzerdefinierter gespeicherter Prozeduren  
 Berücksichtigen Sie bei der Verwendung benutzerdefinierter gespeicherter Prozeduren die folgenden Überlegungen:  
  
-   Sie müssen den Support für die Logik der gespeicherten Prozedur selbst übernehmen. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] stellt für benutzerdefinierte Logik keinen Support bereit.  
  
-   Verwenden Sie keine expliziten Transaktionen in benutzerdefinierten Prozeduren, um Konflikte mit Transaktionen zu vermeiden, die von der Replikation verwendet werden.  
  
-   Das Schema auf dem Abonnenten ist in der Regel mit dem Schema auf dem Verleger identisch, kann bei Verwendung der Spaltenfilterung jedoch eine Teilmenge des Verlegerschemas sein. Wenn Sie jedoch beim Verschieben der Daten das Schema so transformieren, dass das Schema auf dem Abonnenten keine Teilmenge des Schemas auf dem Verleger darstellt, ist [!INCLUDE[ssISCurrent](../../../includes/ssiscurrent-md.md)] die empfohlene Lösung. Weitere Informationen finden Sie unter [SQL Server Integration Services](../../../integration-services/sql-server-integration-services.md).  
  
-   Wenn Sie Schemaänderungen an einer veröffentlichten Tabelle vornehmen, müssen die benutzerdefinierten Prozeduren neu generiert werden. Weitere Informationen finden Sie unter [Erneutes Generieren von Transaktionsprozeduren zur Erfassung von Schemaänderungen](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
-   Wenn Sie einen höheren Wert als 1 für den **-SubscriptionStreams** -Parameter des Verteilungs-Agent verwenden, müssen Sie sicherstellen, dass Updates an der Primärschlüsselspalte erfolgreich sind. Beispiel:  
  
    ```  
    update ... set pk = 2 where pk = 1 -- update 1  
    update ... set pk = 3 where pk = 2 -- update 2  
    ```  
  
     Wenn der Verteilungs-Agent mehrere Verbindungen verwendet, werden diese beiden Updates gegebenenfalls über verschiedene Verbindungen repliziert. Wird Update 1 zuerst angewendet, gibt es kein Problem. Wird Update 2 zuerst angewendet, wird '0 Zeilen betroffen' zurückgegeben, da Update 1 noch nicht stattgefunden hat. Diese Situation wird von den Standardprozeduren beantwortet. Dabei wird ein Fehler ausgelöst, wenn von einem Update keine Zeilen betroffen sind:  
  
    ```  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sys.sp_MSreplraiserror 20598  
    ```  
  
     Das Auslösen des Fehlers zwingt den Verteilungs-Agent, die Updates erneut über eine einzige Verbindung zu versuchen. Dieser Versuch ist dann erfolgreich. Benutzerdefinierte gespeicherte Prozeduren müssen eine ähnliche Logik einschließen.  
  
### <a name="call-syntax-for-stored-procedures"></a>Aufrufsyntax für gespeicherte Prozeduren  
 Es gibt fünf Optionen für die Syntax, mit der die von der Transaktionsreplikation verwendeten Prozeduren aufgerufen werden:  
  
-   CALL-Syntax. Diese Syntax kann für Einfügungen, Updates und Löschungen verwendet werden. Die Replikation verwendet diese Syntax standardmäßig für Einfügungen und Löschungen.  
  
-   SCALL-Syntax. Diese Syntax kann nur für Updates verwendet werden. Die Replikation verwendet diese Syntax standardmäßig für Updates.  
  
-   MCALL-Syntax. Diese Syntax kann nur für Updates verwendet werden.  
  
-   XCALL-Syntax. Diese Syntax kann für Updates und Löschungen verwendet werden.  
  
-   VCALL. Diese Syntax wird für aktualisierbare Abonnements verwendet. Nur interne Verwendung.  
  
 Die einzelnen Methoden unterscheiden sich in der Datenmenge, die an den Abonnenten weitergegeben wird. SCALL gibt z. B. Werte nur für die Spalten weiter, die tatsächlich von einem Update betroffen sind. XCALL dagegen erfordert alle Spalten (unabhängig davon, ob sie von einem Update betroffen sind) und alle alten Datenwerte für jede Spalte. In vielen Fällen eignet sich SCALL für Updates. Erfordert die Anwendung jedoch alle Datenwerte bei einem Update, empfiehlt sich die Verwendung von XCALL.  
  
#### <a name="call-syntax"></a>CALL-Syntax  
 Gespeicherte Prozeduren zu INSERT  
 Gespeicherte Prozeduren, die INSERT-Anweisungen verarbeiten, übergeben die in allen Spalten eingefügten Werte:  
  
```  
c1, c2, c3,... cn  
```  
  
 Gespeicherte Prozeduren zu UPDATE  
 Gespeicherte Prozeduren, die UPDATE-Anweisungen verarbeiten, übergeben die aktualisierten Werte für alle in dem Artikel definierten Spaltenwerte, gefolgt von den ursprünglichen Werten der Primärschlüsselspalten (es wird kein Versuch zur Bestimmung der geänderten Spalten unternommen):  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn  
```  
  
 Gespeicherte Prozeduren zu DELETE  
 Gespeicherte Prozeduren, die DELETE Anweisungen verarbeiten, übergeben die Werte der folgenden Primärschlüsselspalten:  
  
```  
pkc1, pkc2, pkc3,... pkcn  
```  
  
#### <a name="scall-syntax"></a>SCALL-Syntax  
 Gespeicherte Prozeduren zu UPDATE  
 Gespeicherte Prozeduren, die UPDATE-Anweisungen verarbeiten, übergeben die aktualisierten Werte nur für die geänderten Spalten, gefolgt von den ursprünglichen Werten der Primärschlüsselspalten, auf die wiederum ein Bitmaskenparameter (**binary(n)**) folgt, der die geänderten Spalten anzeigt. Im folgenden Beispiel wurde die Spalte 2 (c2) nicht geändert:  
  
```  
c1, , c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="mcall-syntax"></a>MCALL-Syntax  
 Gespeicherte Prozeduren zu UPDATE  
 Gespeicherte Prozeduren, die UPDATE-Anweisungen verarbeiten, übergeben die aktualisierten Werte für alle in dem Artikel definierten Spaltenwerte, gefolgt von den ursprünglichen Werten der Primärschlüsselspalten, auf die wiederum ein Bitmaskenparameter (**binary(n)**) folgt, der die geänderten Spalten anzeigt:  
  
```  
c1, c2, c3,... cn, pkc1, pkc2, pkc3,... pkcn, bitmask  
```  
  
#### <a name="xcall-syntax"></a>XCALL-Syntax  
 Gespeicherte Prozeduren zu UPDATE  
 Gespeicherte Prozeduren, die UPDATE-Anweisungen verarbeiten, übergeben die ursprünglichen Werte (das Anfangsimage) für alle in dem Artikel definierten Spalten, gefolgt von den aktualisierten Werten (das Endimage) für alle in dem Artikel definierten Spalten.  
  
```  
old-c1, old-c2, old-c3,... old-cn, c1, c2, c3,... cn,  
```  
  
 Gespeicherte Prozeduren zu DELETE  
 Gespeicherte Prozeduren, die DELETE-Anweisungen verarbeiten, übergeben die ursprünglichen Werte (das Anfangsimage) für alle in dem Artikel definierten Spalten:  
  
```  
old-c1, old-c2, old-c3,... old-cn  
```  
  
> [!NOTE]  
>  Beim Verwenden von XCALL wird erwartet, dass die Anfangsimagewerte für **text** - und **image** -Spalten NULL sind.  
  
## <a name="examples"></a>Beispiele  
 Bei den folgenden Prozeduren handelt es sich um Standardprozeduren, die für die `Vendor Table` in der [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] -Beispieldatenbank erstellt wurden.  
  
```  
--INSERT procedure using CALL syntax  
create procedure [sp_MSins_PurchasingVendor]   
  @c1 int,@c2 nvarchar(15),@c3 nvarchar(50),@c4 tinyint,@c5 bit,@c6 bit,@c7 nvarchar(1024),@c8 datetime  
as   
begin   
insert into [Purchasing].[Vendor]([VendorID]  
,[AccountNumber]  
,[Name]  
,[CreditRating]  
,[PreferredVendorStatus]  
,[ActiveFlag]  
,[PurchasingWebServiceURL]  
,[ModifiedDate])  
values (   
 @c1  
,@c2  
,@c3  
,@c4  
,@c5  
,@c6  
,@c7  
,@c8  
 )   
end  
go  
  
--UPDATE procedure using SCALL syntax  
create procedure [sp_MSupd_PurchasingVendor]   
 @c1 int = null,@c2 nvarchar(15) = null,@c3 nvarchar(50) = null,@c4 tinyint = null,@c5 bit = null,@c6 bit = null,@c7 nvarchar(1024) = null,@c8 datetime = null,@pkc1 int  
,@bitmap binary(2)  
as  
begin  
update [Purchasing].[Vendor] set   
 [AccountNumber] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [AccountNumber] end  
,[Name] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [Name] end  
,[CreditRating] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [CreditRating] end  
,[PreferredVendorStatus] = case substring(@bitmap,1,1) & 16 when 16 then @c5 else [PreferredVendorStatus] end  
,[ActiveFlag] = case substring(@bitmap,1,1) & 32 when 32 then @c6 else [ActiveFlag] end  
,[PurchasingWebServiceURL] = case substring(@bitmap,1,1) & 64 when 64 then @c7 else [PurchasingWebServiceURL] end  
,[ModifiedDate] = case substring(@bitmap,1,1) & 128 when 128 then @c8 else [ModifiedDate] end  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end  
go  
  
--DELETE procedure using CALL syntax  
create procedure [sp_MSdel_PurchasingVendor]   
  @pkc1 int  
as   
begin   
delete [Purchasing].[Vendor]  
where [VendorID] = @pkc1  
if @@rowcount = 0  
    if @@microsoftversion>0x07320000  
        exec sp_MSreplraiserror 20598  
end   
go  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  

