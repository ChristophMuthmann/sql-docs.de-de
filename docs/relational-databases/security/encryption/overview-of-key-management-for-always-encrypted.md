---
title: "Übersicht über die Schlüsselverwaltung für Always Encrypted | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-security
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 07a305b1-4110-42f0-b7aa-28a4e32e912a
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 8333a497795ae7968b5d297b62aba83944f1b3ba
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="overview-of-key-management-for-always-encrypted"></a>Übersicht über die Schlüsselverwaltung für Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) verwendet zwei Typen von kryptografischen Schlüsseln zum Schützen Ihrer Daten – einen Schlüssel zum Verschlüsseln Ihrer Daten und einen anderen Schlüssel zum Verschlüsseln des Schlüssels, der Ihre Daten verschlüsselt. Der Spaltenverschlüsselungsschlüssel verschlüsselt Ihre Daten, der Spaltenhauptschlüssel verschlüsselt den Spaltenverschlüsselungsschlüssel. Dieser Artikel enthält eine ausführliche Übersicht über die Verwaltung dieser Verschlüsselungsschlüssel.

Wenn es um Always Encrypted-Schlüssel und Schlüsselmanagement geht, ist es wichtig, den Unterschied zwischen den tatsächlichen kryptografischen Schlüsseln und den Metadatenobjekten zu verstehen, die die Schlüssel *beschreiben* . Die Begriffe **Spaltenverschlüsselungsschlüssel** und **Spaltenhauptschlüssel** beziehen sich auf die tatsächlichen kryptografischen Schlüssel, während sich die Begriffe **Spaltenverschlüsselungsschlüssel-Metadaten** und **Spaltenhauptschlüssel-Metadaten** auf die *Beschreibungen* der Always Encrypted-Schlüssel in der Datenbank beziehen.

- ***Spaltenverschlüsselungsschlüssel*** sind Inhaltsverschlüsselungsschlüssel, die zum Verschlüsseln von Daten verwendet werden. Wie der Name schon sagt, verwenden Sie die Spaltenverschlüsselungsschlüssel zum Verschlüsseln von Daten in Datenbankspalten. Je nach den Anforderungen Ihrer Anwendung können Sie eine oder mehrere Spalten mit demselben Spaltenverschlüsselungsschlüssel verschlüsseln oder mehrere Spaltenverschlüsselungsschlüssel verwenden. Die Spaltenverschlüsselungsschlüssel sind selbst verschlüsselt, und nur die verschlüsselten Werte der Spaltenverschlüsselungsschlüssel werden in der Datenbank gespeichert (als Teil der Spaltenverschlüsselungsschlüssel-Metadaten). Die Spaltenverschlüsselungsschlüssel-Metadaten werden in den Katalogsichten [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) und [sys.column_encryption_key_values (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) gespeichert. Spaltenverschlüsselungsschlüssel, die mit dem AES-256-Algorithmus verwendet werden, sind 256 Bit lang.


- ***Spaltenhauptschlüssel*** sind Schlüsselschutzschlüssel, die zur Verschlüsselung von Spaltenverschlüsselungsschlüsseln verwendet werden. Spaltenhauptschlüssel müssen in einem vertrauenswürdigen Schlüsselspeicher, wie z.B. Windows-Zertifikatspeicher, Azure Key Vault oder einem Hardwaresicherheitsmodul gespeichert werden. Die Datenbank enthält nur Metadaten zu Spaltenhauptschlüsseln (der Schlüsselspeichertyp und -ort). Die Spaltenhauptschlüssel-Metadaten befinden sich in der Katalogsicht [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md) .  

Es ist wichtig zu beachten, dass die Schlüsselmetadaten im Datenbanksystem keine Nur-Text-Spaltenhauptschlüssel oder Nur-Text-Spaltenverschlüsselungsschlüssel enthalten. Die Datenbank enthält nur Informationen über den Typ und den Speicherort von Spaltenhauptschlüsseln sowie verschlüsselte Werte von Spaltenverschlüsselungsschlüsseln. Dies bedeutet, dass Nur-Text-Schlüssel dem Datenbanksystem niemals zur Verfügung gestellt werden, wodurch sichergestellt wird, dass das Schützen von Daten mithilfe von Always Encrypted sicher ist, selbst wenn das Datenbanksystem kompromittiert wird. Achten Sie darauf, Ihre Schlüsselverwaltungstools auf einem anderen Computer als dem Computer auszuführen, der Ihre Datenbank hostet, um sicherzustellen, dass das Datenbanksystem keinen Zugriff auf die Nur-Text-Schlüssel erhält. Weitere Informationen hierzu finden Sie im Abschnitt [Sicherheitsüberlegungen für die Schlüsselverwaltung](#SecurityForKeyManagement) weiter unten.

Da die Datenbank nur verschlüsselte Daten (in Always Encrypted geschützte Spalten) enthält und nicht auf die Nur-Text-Schlüssel zugreifen kann, können die Daten nicht entschlüsselt werden. Dies bedeutet, dass beim Abfragen von Always Encrypted-Spalten einfach nur verschlüsselte Werte zurückgegeben werden. Clientanwendungen, die geschützte Daten ver- oder entschlüsseln müssen, benötigen Zugriff auf den Spaltenhauptschlüssel und die verknüpften Spaltenverschlüsselungsschlüssel. Weitere Informationen finden Sie unter [Always Encrypted (client development)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)(Always Encrypted (Cliententwicklung))



## <a name="key-management-tasks"></a>Schlüsselverwaltungs-Tasks

Der Prozess der Schlüsselverwaltung kann in die folgenden grundlegenden Tasks unterteilt werden:

- **Schlüsselbereitstellung** – Erstellen des physischen Schlüssels in einem vertrauenswürdigen Schlüsselspeicher (z.B. im Windows-Zertifikatspeicher, Azure Key Vault oder einem Hardwaresicherheitsmodul), Verschlüsseln von Spaltenverschlüsselungsschlüsseln mithilfe von Spaltenhauptschlüsseln und Erstellen von Metadaten für beide Schlüsseltypen in der Datenbank

- **Schlüsselrotation** – Ersetzen eines vorhandenen Schlüssels mit einem neuen Schlüssel in regelmäßigen Abständen Sie müssen einen Schlüssel möglicherweise drehen, wenn er kompromittiert wurde, oder um die Richtlinien und Kompatibilitätsbestimmungen Ihrer Organisation einzuhalten, die die Rotation kryptografischer Schlüssel vorschreiben. 


## <a name="KeyManagementRoles"></a> Schlüsselverwaltungsrollen

Es gibt zwei unterschiedliche Rollen von Benutzern, die Always Encrypted-Schlüssel verwalten, und zwar Sicherheits- und Datenbankadministratoren (DBAs):

- **Sicherheitsadministrator** : generiert Spaltenverschlüsselungsschlüssel und Spaltenhauptschlüssel und verwaltet die Schlüsselspeicher, die die Spaltenhauptschlüssel enthalten. Ein Sicherheitsadministrator benötigt zum Durchführen dieser Aufgaben Zugriff auf die Schlüssel und den Schlüsselspeicher, jedoch nicht auf die Datenbank.
- **DBA** : verwaltet die Metadaten zu den Schlüsseln in der Datenbank. Ein DBA muss zum Durchführen von Schlüsselverwaltungsaufgaben in der Lage sein, Schlüsselmetadaten in der Datenbank zu verwalten, benötigt jedoch keinen Zugriff auf die Schlüssel oder den Schlüsselspeicher, der die Spaltenhauptschlüssel enthält.

Unter Berücksichtigung der oben erwähnten Rollen gibt es zwei unterschiedliche Arten, Verwaltungsaufgaben für Always Encrypted durchzuführen: *per Rollentrennung*und *ohne Rollentrennung*. Je nach den Bedürfnissen Ihrer Organisation können Sie den Schlüsselverwaltungsprozess auswählen, der sich für Ihre Anforderungen am besten eignet.

## <a name="managing-keys-with-role-separation"></a>Verwalten von Schlüsseln per Rollentrennung
Wenn Always Encrypted-Schlüssel per Rollentrennung verwaltet werden, übernehmen verschiedene Personen in einer Organisation die Rollen des Sicherheits- und Datenbankadministrators. Ein Schlüsselverwaltungsprozess mit Rollentrennung gewährleistet, dass DBAs keinen Zugriff auf den Schlüssel oder die Schlüsselspeicher haben, die die tatsächlichen Schlüssel enthalten, und dass Sicherheitsadministratoren keinen Zugriff auf die Datenbank haben, die sensible Daten enthält. Die Schlüsselverwaltung per Rollentrennung wird empfohlen, wenn Sie erreichen möchten, dass DBAs in Ihrer Organisation keinen Zugriff auf sensible Daten haben. 

**Hinweis:** Sicherheitsadministratoren generieren die Nur-Text-Schlüssel und arbeiten mit ihnen. Daher sollten sie ihre Aufgaben nie auf den gleichen Computern ausführen, auf denen auch ein Datenbanksystem gehostet wird, oder auf die von Datenbankadministratoren oder anderen Personen zugegriffen werden kann, die potenziell gefährlich sein könnten. 

## <a name="managing-keys-without-role-separation"></a>Verwalten von Schlüsseln ohne Rollentrennung
Wenn Always Encrypted-Schlüssel ohne Rollentrennung verwaltet werden, kann eine einzelne Person sowohl die Sicherheitsadministratorrolle als auch die DBA-Rolle übernehmen. Diese Person muss also sowohl auf die Schlüssel/Schlüsselspeicher als auch auf die Schlüsselmetadaten zugreifen und diese verwalten können. Die Schlüsselverwaltung ohne Rollentrennung wird für Organisationen empfohlen, die das DevOps-Modell verwenden, oder für Fälle, in denen die Datenbank in der Cloud gehostet wird und das primäre Ziel ist, Cloudadministratoren (nicht jedoch lokalen DBAs) den Zugriff auf sensible Daten zu verweigern.



## <a name="tools-for-managing-always-encrypted-keys"></a>Tools zum Verwalten von Always Encrypted-Schlüsseln

Always Encrypted-Schlüssel können mithilfe von [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms174173.aspx) und [PowerShell](../../scripting/sql-server-powershell.md)verwaltet werden:

- **SQL Server Management Studio (SSMS)** stellt die Dialogfelder und Assistenten bereit, die Aufgaben im Zusammenhang mit dem Zugriff auf den Schlüsselspeicher und die Datenbank kombinieren. SSMS unterstützt die Rollentrennung daher nicht, vereinfacht jedoch das Konfigurieren Ihrer Schlüssel. Weitere Informationen zum Verwalten von Schlüsseln mithilfe von SSMS finden Sie hier:
    - [Bereitstellen von Spaltenhauptschlüsseln](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncmk)
    - [Bereitstellen von Spaltenverschlüsselungsschlüsseln](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#provisioncek)
    - [Rotieren von Spaltenhauptschlüsseln](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecmk)
    - [Rotieren von Spaltenverschlüsselungsschlüsseln](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md#rotatecek)


- **SQL Server PowerShell** enthält Cmdlets zum Verwalten von Always Encrypted-Schlüsseln mit und ohne Rollentrennung. Weitere Informationen finden Sie in den folgenden Themen:
    - [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
    - [Rotieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)


## <a name="SecurityForKeyManagement"></a> Sicherheitsüberlegungen für die Schlüsselverwaltung

Das primäre Ziel von Always Encrypted ist es, zu gewährleisten, dass in einer Datenbank gespeicherte sensible Daten sicher sind, selbst wenn das Datenbanksystem oder seine Hostumgebung kompromittiert werden. Beispiele für Sicherheitsangriffe, bei denen Always Encrypted dabei helfen kann, den Verlust von sensiblen Daten zu verhindern, sind u.a. folgende:

- Ein böswilliger Datenbankbenutzer mit erhöhten Rechten, wie z.B. ein DBA, der Spalten mit sensiblen Daten abfragt.
- Ein nicht autorisierter Administrator eines Computers, der eine SQL Server-Instanz hostet, der den Arbeitsspeicher oder Abbilddateien eines SQL Server-Prozesses scannt.
- Ein böswilliger Rechenzentrumsoperator, der eine Kundendatenbank abfragt, SQL Server-Dumpdateien oder den Arbeitsspeicher eines Computers liest, der Kundendaten in der Cloud hostet.
- Schadsoftware, die auf einem Computer ausgeführt wird, auf dem die Datenbank gehostet wird.

Ihr Schlüsselverwaltungsprozess muss sicherstellen, dass die Spaltenhauptschlüssel und die Spaltenverschlüsselungsschlüssel sowie die Anmeldeinformationen für einen Schlüsselspeicher, der die Spaltenhauptschlüssel enthält, niemals einem potenziellen Angreifer angezeigt werden, um zu gewährleisten, dass Always Encrypted diese Arten von Angriffen effektiv verhindert. Im Folgenden finden Sie einige Richtlinien, die Sie befolgen sollten:

- Generieren Sie niemals Spaltenhauptschlüssel oder Spaltenverschlüsselungsschlüssel auf einem Computer, der Ihre Datenbank hostet. Generieren Sie die Schlüssel stattdessen auf einem separaten Computer, der entweder für die Schlüsselverwaltung vorgesehen ist oder auf dem Anwendungen gehostet werden, die ohnehin Zugriff auf die Schlüssel benötigen. Dies bedeutet, dass Sie **niemals Tools ausführen sollten, die für das Generieren der Schlüssel auf dem Computer verwendet werden, der die Datenbank hostet** . Wenn nämlich ein Angreifer auf einen Computer zugreift, der für die Bereitstellung oder Verwaltung Ihrer Always Encrypted-Schlüssel verwendet wird, kann er Ihre Schlüssel möglicherweise abrufen, selbst wenn die Schlüssel nur für kurze Zeit im Arbeitsspeicher des Tools angezeigt werden.
- Es ist wichtig, potenzielle Angreifer und Sicherheitsbedrohungen zu identifizieren, bevor ein Schlüsselverwaltungprozess definiert und implementiert wird, um sicherzustellen, dass ihr Schlüsselverwaltungsprozess nicht aus Versehen Spaltenhauptschlüssel oder Spaltenverschlüsselungsschlüssel offenlegt. Wenn Sie z.B. möchten, dass DBAs keinen Zugriff auf sensible Daten haben, darf ein DBA nicht für das Generieren von Schlüsseln verantwortlich sein. Ein DBA *kann* jedoch Schlüsselmetadaten in der Datenbank verwalten, da die Nur-Text-Schlüssel in den Metadaten nicht enthalten sind.

## <a name="next-steps"></a>Nächste Schritte

- [Create and Store Column Master Keys (Always Encrypted) (Erstellen und Speichern von Spaltenhauptschlüsseln (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Konfigurieren von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [Rotation von Always Encrypted-Schlüsseln mithilfe von PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Konfigurieren von Always Encrypted mithilfe von SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [„Immer verschlüsselt“ (Datenbankmodul)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted (Client Development)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Tutorial zum Always Encrypted-Assistenten (Azure Key Vault)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/)
- [Tutorial zum Always Encrypted-Assistenten (Windows-Zertifikatspeicher)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)





