---
title: "Migrieren von durch Always Encrypted geschützten sensiblen Daten | Microsoft-Dokumentation"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/04/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: da73d0d20404f513e22dcdf0340e24fe85dc3184
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>Migrieren von durch Always Encrypted geschützten sensiblen Daten
  Erstellen Sie den Benutzer mit der Option **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** , um verschlüsselte Daten zu laden, ohne während Massenkopiervorgängen auf dem Server Metadatenüberprüfungen durchzuführen. Diese Option soll von Legacytools von älteren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Versionen als [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] (wie z.B. bcp.exe) oder von Drittanbieter-ETL-Workflows (Extract-Transform-Load; Extrahieren, Transformieren und Laden) verwendet werden, die Always Encrypted nicht verwenden können. Dadurch kann der Benutzer verschlüsselte Daten sicher von einem Tabellensatz mit verschlüsselten Spalten zu einem anderen Tabellensatz mit verschlüsselten Spalten (innerhalb derselben oder zu einer anderen Datenbank) verschieben.  
  
## <a name="the-allowencryptedvaluemodifications-option"></a>Die Option ALLOW_ENCRYPTED_VALUE_MODIFICATIONS  
 Sowohl [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) als auch [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) verfügen über eine Option ALLOW_ENCRYPTED_VALUE_MODIFICATIONS. Wenn diese Option auf ON festgelegt wird (der Standardwert ist OFF), unterdrückt sie kryptografische Metadatenüberprüfungen bei Massenkopiervorgängen auf dem Server, wodurch der Benutzer verschlüsselte Daten zwischen Tabellen oder Datenbanken massenkopieren kann, ohne die Daten zu entschlüsseln.  
  
## <a name="data-migration-scenarios"></a>Datenmigrationsszenarien  
 Die folgende Tabelle zeigt die empfohlenen Einstellungen für mehrere Migrationsszenarien.  
  
 ![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  
  
## <a name="bulk-loading-of-encrypted-data"></a>Massenladen von verschlüsselten Daten  
 Verwenden Sie das folgende Verfahren, um verschlüsselte Daten zu laden.  
  
1.  Legen Sie die Option für den Benutzer in der Datenbank auf ON fest, der das Ziel für den Massenkopiervorgang darstellt. Beispiel:  
  
    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
    ```  
  
2.  Führen Sie Ihre Massenkopieranwendung oder Ihr Massenkopiertool aus, indem Sie als dieser Benutzer eine Verbindung herstellen. (Wenn Ihre Anwendung einen durch Always Encrypted aktivierten Clienttreiber verwendet, achten Sie darauf, dass die Verbindungszeichenfolge für die Datenquelle nicht **column encryption setting=enabled** enthält. Dadurch stellen Sie sicher, dass die von verschlüsselten Spalten abgerufenen Daten verschlüsselt bleiben. Weitere Informationen finden Sie unter [Always Encrypted &#40;Cliententwicklung&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md).)  
  
3.  Legen Sie die Option ALLOW_ENCRYPTED_VALUE_MODIFICATIONS wieder auf OFF fest. Beispiel:  
  
    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  
  
## <a name="potential-for-data-corruption"></a>Risiko der Datenbeschädigung  
 Die falsche Verwendung dieser Option kann zur Datenbeschädigung führen. Die Option **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** ermöglicht es dem Benutzer, beliebige Daten in verschlüsselte Spalten in der Datenbank einzufügen. Dazu zählen auch Daten, die mit verschiedenen Schlüsseln, falsch oder überhaupt nicht verschlüsselt wurden. Wenn der Benutzer aus Versehen Daten kopiert, die mithilfe des für die Zielspalte festgelegten Verschlüsselungsschemas (Spaltenverschlüsselungsschlüssel, Algorithmus, Verschlüsselungstyp) nicht richtig verschlüsselt wurden, können Sie diese Daten nicht entschlüsseln (die Daten sind beschädigt). Diese Option muss mit Vorsicht verwendet werden, da sie zur Datenbeschädigung in der Datenbank führen kann.  
  
 Das folgende Szenario zeigt, wie nicht ordnungsgemäß importierte Daten zur Datenbeschädigung führen können:  
  
1.  Die Option ist für einen Benutzer auf ON festgelegt.  
  
2.  Der Benutzer führt die Anwendung aus, die mit der Datenbank verbunden ist. Die Anwendung verwendet Massen-APIs zum Einfügen von Klartextwerten in verschlüsselte Spalten. Die Anwendung erwartet von einem durch Always Encrypted aktivierten Clienttreiber die Verschlüsselung der Daten beim Einfügen. Die Anwendung ist jedoch falsch konfiguriert, sodass sie entweder einen Treiber verwendet, der Always Encrypted nicht unterstützt, oder die Verbindungszeichenfolge **column encryption setting=enabled**nicht enthält.  
  
3.  Die Anwendung sendet Klartextwerte an den Server. Da kryptografische Metadatenüberprüfungen auf dem Server für den Benutzer deaktiviert sind, lässt der Server zu, dass falsche Daten (Klartext statt richtig verschlüsselter Chiffretext) in eine verschlüsselte Spalte eingefügt werden.  
  
4.  Die gleiche oder eine andere Anwendung stellt mithilfe eines durch Always Encrypted aktivierten Treibers und mit **column encryption setting=enabled** in der Verbindungszeichenfolge eine Verbindung mit der Datenbank her und ruft die Daten ab. Die Anwendung erwartet, dass die Daten transparent entschlüsselt werden. Der Treiber kann die Daten jedoch nicht entschlüsseln, da es sich dabei um falschen Chiffretext handelt.  
  
## <a name="best-practice"></a>Bewährte Methoden  
  
-   Verwenden Sie vorgesehene Benutzerkonten für Workloads mit langer Ausführungszeit, die diese Option verwenden.  
  
-   Legen Sie die Option bei Massenkopieranwendungen oder -tools, die verschlüsselte Daten ohne Entschlüsseln verschieben müssen, direkt vor dem Ausführen der Anwendung auf ON fest. Setzen Sie die Option sofort nach der Ausführung des Vorgangs auf OFF zurück.  
  
-   Verwenden Sie diese Option nicht zum Entwickeln neuer Anwendungen. Verwenden Sie stattdessen einen Clienttreiber (z.B. ADO 4.6.1), der eine API zum Unterdrücken kryptografischer Metadatenüberprüfungen für eine einzelne Sitzung bietet.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
 [Always Encrypted &#40;Datenbankmodul&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted-Assistent](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
 [Always Encrypted &#40;Cliententwicklung&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  

