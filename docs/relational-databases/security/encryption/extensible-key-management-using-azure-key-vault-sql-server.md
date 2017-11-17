---
title: "Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/22/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Extensible Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
- EKM, with key vault
- TDE, EKM and key vault
- Key Management with key vault
- SQL Server Connector, about
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
caps.latest.revision: 66
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 7b4f037616e0559ac62bbae5dbe04aeffe529b06
ms.openlocfilehash: 24d344d6dc7f42ed57c53442f7fada245d25c65a
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault ermöglicht der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verschlüsselung die Verwendung des Azure Key Vault-Diensts als Anbieter für die [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md) zum Schutz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verschlüsselungsschlüsseln.  
  
 In diesem Thema wird der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Connector beschrieben. Weitere Informationen finden Sie unter [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md), [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)und [SQL Server-Connector Wartung &amp; Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)(SQL Server Connector Wartung &amp; Problembehandlung).  
  
##  <a name="Uses"></a> Was ist die erweiterbare Schlüsselverwaltung (EKM, Extensible Key Management) und warum sollte sie verwendet werden?  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt verschiedene Arten von Verschlüsselung bereit, die beim Verschlüsseln von sensiblen Daten nützlich sind, einschließlich [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md), [Verschlüsselung auf Spaltenebene](../../../t-sql/functions/cryptographic-functions-transact-sql.md) (CLE) und [Sicherungsverschlüsselung](../../../relational-databases/backup-restore/backup-encryption.md). In all diesen Fällen werden die Daten in dieser traditionellen Schlüsselhierarchie mit einem symmetrischen Datenverschlüsselungsschlüssel (DEK, Data Encrpytion Key) verschlüsselt. Der symmetrische Datenverschlüsselungsschlüssel wird außerdem geschützt durch Verschlüsselung mit einer Hierarchie von Schlüsseln, die in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gespeichert sind. Die Alternative zu diesem Modell ist das EKM-Anbietermodell. Die Verwendung der EKM-Anbieterarchitektur ermöglicht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die Datenverschlüsselungsschlüssel mithilfe eines asymmetrischen Schlüssels zu schützen, der außerhalb von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in einem externen Kryptografieanbieter gespeichert ist. Dieses Modell fügt eine zusätzliche Sicherheitsschicht hinzu und trennt die Verwaltung von Schlüsseln und Daten.  
   
 Das folgende Bild stellt die traditionelle Hierarchie zur Dienst-/Schlüsselverwaltung dem Azure Key Vault-System gegenüber.  
  
 ![EKM-Schlüssel-Hierarchie-traditionell](../../../relational-databases/security/encryption/media/ekm-key-hierarchy-traditional.png "ekm-key-hierarchy-traditional")  
  
   
 Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector dient als Brücke zwischen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und Azure Key Vault, sodass [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] von der Skalierbarkeit, hohen Leistung und hohen Verfügbarkeit des Azure Key Vault-Diensts profitieren kann. In der folgenden Abbildung ist dargestellt, wie die Schlüsselhierarchie in der EKM-Anbieterarchitektur mit Azure Key Vault und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector funktioniert.  
  
  Azure Key Vault kann mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Installationen auf virtuellen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure-Computern und für lokale Server verwendet werden. Der Schlüsseltresordienst bietet auch die Option, genau gesteuerte und stark überwachte Hardwaresicherheitsmodule (HSMs) für ein höheres Maß an Schutz für asymmetrische Schlüssel zu verwenden. Weitere Informationen zum Schlüsseltresor finden Sie unter [Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521401).  
  
 Die folgende Grafik enthält eine Zusammenfassung des Prozessablaufs der erweiterbaren Schlüsselverwaltung mit Schlüsseltresor. (Die Nummern der Prozessschritte in der Grafik stimmen nicht mit den Nummern der Einrichtungsschritte, die auf die Grafik folgen, überein.)  
  
 ![SQL Server-EKM mit Azure Key Vault](../../../relational-databases/security/encryption/media/ekm-using-azure-key-vault.png "SQL Server EKM using the Azure Key Vault")  

> [!NOTE]  
>  Die Versionen 1.0.0.440 und älter wurden ersetzt und werden in Produktionsumgebungen nicht mehr unterstützt. Führen Sie ein Upgrade auf Version 1.0.1.0 oder höher durch, indem Sie das [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=45344) besuchen und die Anweisungen auf der Seite [SQL Server-Connector Wartung &amp; Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) (SQL Server Connector Wartung &amp; Problembehandlung) unter „Upgrade des SQL Server-Connectors“ ausführen.
  
 Die nächsten Schritte erläutert [Installationsschritte für die Erweiterbare Schlüsselverwaltung mit Azure Key Vault](../../../relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault.md).  
  
 Eine Beschreibung von Nutzungsszenarien finden Sie unter [Verwenden von SQL Server-Connector mit SQL-Verschlüsselungsfunktionen](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Connector Wartung & Problembehandlung](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)  
  
  

