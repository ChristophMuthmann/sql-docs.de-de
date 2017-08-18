---
title: "Konfigurieren der Serverkonfigurationsoption „Benutzeroptionen“ | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- global default for all users [SQL Server]
- users [SQL Server], global defaults
- user options option [SQL Server]
ms.assetid: cfed8f86-6bcf-4b90-88eb-9656e22d5dc5
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a801f77059d2aa6bacd89901c63f80dcc91bf84a
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-user-options-server-configuration-option"></a>Konfigurieren der Serverkonfigurationsoption Benutzeroptionen
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  In diesem Thema wird beschrieben, wie die Serverkonfigurationsoption **Benutzeroptionen** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]konfiguriert wird. Die Option **Benutzeroptionen** gibt globale Standardwerte für alle Benutzer an. Es wird eine Liste der Standardoptionen der Abfrageverarbeitung für die Dauer der Sitzung eines Benutzers erstellt. Mit der Option **Benutzeroptionen** können Sie die Standardwerte der SET-Optionen ändern (wenn die Standardeinstellungen des Servers nicht verwendet werden können).  
  
 Ein Benutzer kann diese Standardeinstellungen mithilfe der SET-Anweisung überschreiben. Für neue Anmeldungen können Sie **Benutzeroptionen** dynamisch konfigurieren. Nach dem Ändern der Einstellung von **Benutzeroptionen**wird diese von neuen Anmeldesitzungen verwendet. Aktuelle Anmeldesitzungen sind davon nicht betroffen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Empfehlungen](#Recommendations)  
  
     [Sicherheit](#Security)  
  
-   **So konfigurieren Sie die Konfigurationsoption "Benutzeroptionen" mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Nachbereitung:**  [Nach dem Konfigurieren der Konfigurationsoption „Benutzeroptionen“](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Recommendations"></a> Empfehlungen  
  
-   In der folgenden Tabelle werden die Konfigurationswerte für **Benutzeroptionen**aufgeführt und beschrieben. Nicht alle Konfigurationswerte sind miteinander kompatibel. ANSI_NULL_DFLT_ON und ANSI_NULL_DFLT_OFF können beispielsweise nicht gleichzeitig festgelegt werden.  
  
    |Wert|Konfiguration|Beschreibung|  
    |-----------|-------------------|-----------------|  
    |1|DISABLE_DEF_CNST_CHK|Steuert die zwischenzeitliche oder verzögerte Einschränkungsüberprüfung.|  
    |2|IMPLICIT_TRANSACTIONS|Steuert bei Verbindungen zu dblib-Netzwerkbibliotheken, ob bei Ausführung einer Anweisung implizit eine Transaktion gestartet wird. Die Einstellung IMPLICIT_TRANSACTIONS wirkt sich weder auf ODBC- noch auf OLE DB-Verbindungen aus.|  
    |4|CURSOR_CLOSE_ON_COMMIT|Steuert das Cursorverhalten nach einem Commitvorgang.|  
    |8|ANSI_WARNINGS|Steuert das Abschneiden und NULL in Aggregatwarnungen.|  
    |16|ANSI_PADDING|Steuert die Auffüllung bei Variablen fester Länge.|  
    |32|ANSI_NULLS|Steuert die Behandlung von NULL bei der Verwendung von Gleichheitsoperatoren.|  
    |64|ARITHABORT|Beendet eine Abfrage, wenn während der Abfrage ein Überlauffehler oder ein Fehler aufgrund einer Division durch Null auftritt.|  
    |128|ARITHIGNORE|Gibt NULL zurück, wenn während der Abfrage ein Überlauffehler oder ein Fehler aufgrund einer Division durch null auftritt.|  
    |256|QUOTED_IDENTIFIER|Unterscheidet beim Auswerten eines Ausdrucks zwischen einfachen und doppelten Anführungszeichen.|  
    |512|NOCOUNT|Deaktiviert die Meldung über die Anzahl der betroffenen Zeilen, die am Ende jeder Anweisung zurückgegeben wird.|  
    |1024|ANSI_NULL_DFLT_ON|Ändert das Sitzungsverhalten so, dass bei der NULL-Zulässigkeit die ANSI-Kompatibilität verwendet wird. Neue Spalten ohne ausdrückliche NULL-Zulässigkeit werden dann so definiert, dass sie NULL-Werte zulassen.|  
    |2048|ANSI_NULL_DFLT_OFF|Ändert das Sitzungsverhalten so, dass bei der NULL-Zulässigkeit keine ANSI-Kompatibilität verwendet wird. Bei neuen Spalten, für die die NULL-Zulässigkeit nicht explizit definiert ist, sind Nullen nicht zulässig.|  
    |4096|CONCAT_NULL_YIELDS_NULL|Gibt NULL zurück, wenn ein NULL-Wert mit einer Zeichenfolge verkettet wird.|  
    |8192|NUMERIC_ROUNDABORT|Generiert einen Fehler, wenn in einem Ausdruck ein Genauigkeitsverlust auftritt.|  
    |16384|XACT_ABORT|Führt ein Rollback für eine Transaktion aus, wenn eine Transact-SQL-Anweisung einen Laufzeitfehler auslöst.|  
  
-   Die Bitpositionen in **Benutzeroptionen** sind mit den Positionen in @@OPTIONS identisch. Jede Verbindung verfügt über eine eigene @@OPTIONS-Funktion, die die Konfigurationsumgebung darstellt. Bei der Anmeldung bei einer Instanz von \ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erhält ein Benutzer eine Standardumgebung, die @@OPTIONS den aktuellen Wert von **Benutzeroptionen** zuweist. Das Ausführen von SET-Anweisungen für **Benutzeroptionen** wirkt sich ausschließlich auf den entsprechenden Wert in der @@OPTIONS-Funktion der Sitzung aus. Alle Verbindungen, die nach der Änderung dieser Einstellung erstellt werden, erhalten den neuen Wert.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Die Ausführungsberechtigungen für **sp_configure** ohne Parameter oder nur mit dem ersten Parameter werden standardmäßig allen Benutzern erteilt. Zum Ausführen von **sp_configure** mit beiden Parametern zum Ändern einer Konfigurationsoption oder zum Ausführen der RECONFIGURE-Anweisung muss einem Benutzer die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>So konfigurieren Sie die Konfigurationsoption "Benutzeroptionen"  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und wählen Sie **Eigenschaften**aus.  
  
2.  Klicken Sie auf den Knoten **Verbindungen** .  
  
3.  Wählen Sie im Feld **Standardverbindungsoptionen** mindestens ein Attribut aus, um die Standardoptionen zur Abfrageverarbeitung für alle verbundenen Benutzer zu konfigurieren.  
  
     Standardmäßig sind keine Benutzeroptionen konfiguriert.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>So konfigurieren Sie die Konfigurationsoption "Benutzeroptionen"  
  
1.  Stellen Sie eine Verbindung mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)]her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**. In diesem Beispiel wird gezeigt, wie [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) zum Konfigurieren der `user options` verwendet wird, um die Einstellung für die ANSI_WARNINGS-Serveroption zu ändern.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'user options', 8 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren der Konfigurationsoption "Benutzeroptionen"  
 Die Einstellung tritt ohne Neustarten des Servers sofort in Kraft.  
  
## <a name="see-also"></a>Siehe auch  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

