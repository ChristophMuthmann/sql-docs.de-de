---
title: "Erweiterbare Schl&#252;sselverwaltung mit Azure Key Vault (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Erweiterbare Schlüsselverwaltung mit Schlüsseltresor"
  - "Transparente Datenverschlüsselung mit EKM und wichtiger Schlüsseltresor"
  - "EKM, mit Schlüsseltresor"
  - "TDE, EKM und Schlüsseltresor"
  - "Schlüsselverwaltung mit Schlüsseltresor"
  - "SQL Server Connector, Info"
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 66
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 66
---
# Erweiterbare Schl&#252;sselverwaltung mit Azure Key Vault (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault ermöglicht der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verschlüsselung die Verwendung des Azure Key Vault-Diensts als Anbieter für die [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) zum Schutz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verschlüsselungsschlüsseln.  
  
 In diesem Thema wird der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector beschrieben. Weitere Informationen finden Sie unter [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md), [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md) und [SQL Server Connector Maintenance & Troubleshooting](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) (SQL Server Connector Wartung & Problembehandlung).  
  
##  <a name="Uses"></a> Was ist die erweiterbare Schlüsselverwaltung (EKM, Extensible Key Management) und warum sollte sie verwendet werden?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt verschiedene Arten von Verschlüsselung bereit, die beim Verschlüsseln von sensiblen Daten nützlich sind, einschließlich [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption-tde.md), [Verschlüsselung auf Spaltenebene](../../../t-sql/functions/cryptographic-functions-transact-sql.md) (CLE) und [Sicherungsverschlüsselung](../../../relational-databases/backup-restore/backup-encryption.md). In all diesen Fällen werden die Daten in dieser traditionellen Schlüsselhierarchie mit einem symmetrischen Datenverschlüsselungsschlüssel (DEK, Data Encrpytion Key) verschlüsselt. Der symmetrische Datenverschlüsselungsschlüssel wird außerdem geschützt durch Verschlüsselung mit einer Hierarchie von Schlüsseln, die in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gespeichert sind. Die Alternative zu diesem Modell ist das EKM-Anbietermodell. Die Verwendung der EKM-Anbieterarchitektur ermöglicht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], die Datenverschlüsselungsschlüssel mithilfe eines asymmetrischen Schlüssels zu schützen, der außerhalb von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in einem externen Kryptografieanbieter gespeichert ist. Dieses Modell fügt eine zusätzliche Sicherheitsschicht hinzu und trennt die Verwaltung von Schlüsseln und Daten.  
   
 Das folgende Bild stellt die traditionelle Hierarchie zur Dienst-/Schlüsselverwaltung dem Azure Key Vault-System gegenüber.  
  
 ![ekm-key-hierarchy-traditional](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector dient als Brücke zwischen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und Azure Key Vault, sodass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] von der Skalierbarkeit, hohen Leistung und hohen Verfügbarkeit des Azure Key Vault-Diensts profitieren kann. In der folgenden Abbildung ist dargestellt, wie die Schlüsselhierarchie in der EKM-Anbieterarchitektur mit Azure Key Vault und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector funktioniert.  
  
  Azure Key Vault kann mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Installationen auf virtuellen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure-Computern und für lokale Server verwendet werden. Der Schlüsseltresordienst bietet auch die Option, genau gesteuerte und stark überwachte Hardwaresicherheitsmodule (HSMs) für ein höheres Maß an Schutz für asymmetrische Schlüssel zu verwenden. Weitere Informationen zum Schlüsseltresor finden Sie unter [Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521401).  
  
 Die folgende Grafik enthält eine Zusammenfassung des Prozessablaufs der erweiterbaren Schlüsselverwaltung mit Schlüsseltresor. (Die Nummern der Prozessschritte in der Grafik stimmen nicht mit den Nummern der Einrichtungsschritte, die auf die Grafik folgen, überein.)  
  
 ![SQL Server EKM using the Azure Key Vault](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "SQL Server EKM using the Azure Key Vault")  

> [!NOTE]  
>  Die Versionen 1.0.0.440 und älter wurden ersetzt und werden nicht länger in Produktionsumgebungen unterstützt. Führen Sie ein Upgrade auf Version 1.0.1.0 oder höher durch, indem Sie das [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45344) besuchen und die Anweisungen auf der Seite [SQL Server Connector Maintenance & Troubleshooting](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) (SQL Server Connector Wartung & Problembehandlung) unter „Upgrade des SQL Server-Connectors“ ausführen.
  
 Die nächsten Schritte erläutert [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md).  
  
 Eine Beschreibung von Nutzungsszenarien finden Sie unter [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
## Siehe auch  
 [SQL Server-Connector Wartung & Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  