---
title: Always Encrypted-Assistent | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/04/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.alwaysencryptedwizard.encryption.f1
- sql13.swb.alwaysencryptedwizard.f1
- sql.swb.alwaysencryptedwizard.masterkey.f1
helpviewer_keywords:
- Wizard, Always Encrypted
ms.assetid: 68daddc9-ce48-49aa-917f-6dec86ad5af5
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a4c51eabac1ed59fcda896e84aef7525a4271228
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="always-encrypted-wizard"></a>Always Encrypted-Assistent
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Verwenden Sie den **Always Encrypted-Assistent** zum Schutz sensibler Daten, die in einer SQL Server-Datenbank gespeichert sind. „Immer verschlüsselt“ ermöglicht es Clients, sensible Daten in Clientanwendungen zu verschlüsseln und die Verschlüsselungsschlüssel niemals an SQL Server weiterzugeben. Always Encrypted trennt daher zwischen denjenigen Benutzern, die die Daten besitzen (und sie ansehen können) und denjenigen, die die Daten verwalten, (aber keinen Zugriff haben sollten).  Eine vollständige Beschreibung des Features finden Sie unter [Always Encrypted &#40;Datenbankmodul&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).  
 
 - Eine exemplarische End-to-End-Vorgehensweise, die das Konfigurieren von Always Encrypted mit dem Assistenten sowie die Verwendung in einer Clientanwendung veranschaulicht, finden Sie unter [Tutorial zur SQL-Datenbank: Schützen von sensiblen Daten mit Always Encrypted](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/).  
 
 - Ein Video, das die Verwendung des Assistenten erläutert, finden Sie unter [Keeping Sensitive Data Secure with Always Encrypted](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)(Sensible Daten mit Always Encrypted schützen). Weitere Informationen finden Sie auch im [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Security-Teamblog [SSMS Encryption Wizard - Enabling Always Encrypted in a Few Easy Steps](http://blogs.msdn.com/b/sqlsecurity/archive/2015/11/01/ssms-encryption-wizard-enabling-always-encrypted-made-easy.aspx).  
 
 - **Berechtigungen:** Damit Sie mit diesem Assistenten verschlüsselte Spalten abfragen und Schlüssel auswählen können, müssen Sie die Berechtigungen `VIEW ANY COLUMN MASTER KEY DEFINITION` und `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` haben. Damit Sie neue Schlüssel erstellen können, müssen Sie auch die Berechtigungen `ALTER ANY COLUMN MASTER KEY` und `ALTER ANY COLUMN ENCRYPTION KEY` haben.  
 
 #### <a name="to-open-the-always-encrypted-wizard"></a>So öffnen Sie den Always Encrypted-Assistenten  
 
 1.  Stellen Sie eine Verbindung mit Ihrem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Objekt-Explorer-Komponente von [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]her.  
   
 2.  Klicken Sie mit der rechten Maustaste auf Ihre Datenbank, bewegen Sie den Mauszeiger zu **Aufgaben**, und klicken Sie dann auf **Spalten verschlüsseln**.  
   
 ## <a name="column-selection-page"></a>Die Seite „Spaltenauswahl“  
 - Suchen Sie eine Tabelle und eine Spalte, und wählen Sie dann einen Verschlüsselungstyp (deterministisch oder zufällig) und einen Verschlüsselungsschlüssel für die ausgewählte Spalte aus. Um eine verschlüsselte Spalte zu entschlüsseln, wählen Sie **Klartext**. Um einen Spaltenverschlüsselungsschlüssel zu wechseln, wählen Sie die Option „andere Verschlüsselungsschlüssel“ und der Assistent wird die Spalte entschlüsseln und dann wieder mit dem neuen Schlüssel verschlüsseln. (Das Verschlüsseln von temporalen und speicherinternen Tabellen wird von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt, kann jedoch nicht mit diesem Assistenten konfiguriert werden.)  
 
## <a name="master-key-configuration-page"></a>Die Seite „Konfigurieren des Hauptschlüssels“  
 - Erstellen Sie einen neuen Spaltenhauptschlüssel im Windows-Zertifikatspeicher oder in Azure Key Vault. Weitere Informationen finden Sie unter den Links unten unter „Schlüsselspeicher“.  
 
 - Wenn Sie einen automatisch generierter Spaltenverschlüsselungsschlüssel auf der Seite „Spaltenauswahl“ ausgewählt haben, müssen Sie ein Spaltenhauptschlüssel konfigurieren, mit dem der generierten Spaltenverschlüsselungsschlüssel verschlüsselt wird. Wenn Sie bereits einen Spaltenhauptschlüssel in Ihrer Datenbank definiert haben, können Sie diesen auswählen. (Um einen vorhandenen Spaltenhauptschlüssel zu verwenden, muss der Benutzer über die Zugriffsberechtigung auf den Schlüssel verfügen.) Sie können alternativ einen Spaltenhauptschlüssel in einem ausgewählten Schlüsselspeicher (Windows-Zertifikatspeicher oder Azure Key Vault) generieren und den Schlüssel in der Datenbank definieren.  
 
 ### <a name="key-storage"></a>**Schlüsselspeicher**  
 
 - Wählen Sie den Speicherort für den Spaltenhauptschlüssel.  
 
   - **Einen Hauptschlüssel im Windows-Zertifikatspeicher speichern** Weitere Informationen finden Sie unter [Using Certificate Stores](https://msdn.microsoft.com/library/windows/desktop/aa388160.aspx)  
 
   - **Einen Hauptschlüssel in AKV speichern** Weitere Informationen finden Sie unter [Erste Schritte mit dem Azure-Schlüsseltresor](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).  
 
 - Zum Generieren eines Spaltenhauptschlüssels im Azure Key Vault muss der Benutzer über die Berechtigungen **WrapKey**, **UnwrapKey**, **Verify**, und **Sign** für den Schlüsseltresor verfügen. Benutzer benötigen möglicherweise auch die Berechtigungen **Get**, **List**, **Create**, **Delete**, **Update**, **Import**, **Backup**, und **Restore** . Weitere Informationen finden Sie unter [Was ist der Azure-Schlüsseltresor?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) und   [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).  
 
 - Der Assistent hat nur zwei Optionen unterstützt. Hardwaresicherheitsmodule und Kundenspeicher müssen mithilfe von [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] konfiguriert werden.  
 
 ## <a name="always-encrypted-terms"></a>Begriffe zu Always Encrypted  
 
 - Die**deterministische Verschlüsselung** verwendet eine Methode, die immer denselben verschlüsselten Wert für jeden angegebenen Klartextwert generiert. Die Verwendung der deterministischen Verschlüsselung ermöglicht das Gruppieren, das Filtern nach Gleichheit und das Verknüpfen von Tabellen, basierend auf verschlüsselten Werten. Jedoch erlaubt sie nicht autorisierten Benutzern möglicherweise, Informationen zu verschlüsselten Werten zu erraten, indem sie die Muster in den verschlüsselten Spalten untersuchen. Diese Schwäche verschlimmert sich, wenn es sich um einen kleinen Satz möglicher verschlüsselter Werte handelt, beispielsweise TRUE/FALSE, oder die Regionen „Nord“/ „Süd“/ „Ost“/ „West“. Die deterministische Verschlüsselung muss eine Spaltensortierung mit einer binary2-Sortierreihenfolge für Zeichenspalten verwenden.  
 
 - Die**zufällige Verschlüsselung** verwendet eine Methode, die Daten in einer weniger vorhersagbaren Weise verschlüsselt. Die zufällige Verschlüsselung ist sicherer, verhindert aber die Gleichheitssuche, Gruppierung, Indizierung und Verknüpfung für verschlüsselte Spalten.  

 - **Spaltenhauptschlüssel** sind Schutzschlüssel, die zur Verschlüsselung von Spaltenverschlüsselungsschlüsseln verwendet werden. Spaltenhauptschlüssel müssen in einem vertrauenswürdigen Schlüsselspeicher gespeichert werden. Informationen zu Spaltenhauptschlüsseln, einschließlich ihres Speicherorts, werden in der Datenbank in Systemkatalogsichten gespeichert.  

 - **Spaltenverschlüsselungsschlüssel** werden verwendet, um sensible Daten zu verschlüsseln, die in Datenbankspalten gespeichert sind. Alle Werte in einer Spalte können mit einem einzelnen Spaltenverschlüsselungsschlüssel verschlüsselt werden. Verschlüsselte Werte der Spaltenverschlüsselungsschlüssel werden in der Datenbank in Systemkatalogsichten gespeichert. Sie sollten eine Sicherung der Spaltenverschlüsselungsschlüssel an einem sicheren/vertrauenswürdigen Ort speichern.  

 ## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 - [Always Encrypted &#40;Datenbankmodul&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
