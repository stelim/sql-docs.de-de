---
title: Verbindung mit Server herstellen (Datenbank-Engine) (Datenbank-Engine) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 563366020c125cb798b45e3a7db16e36f934c79a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784778"
---
# <a name="connect-to-server-database-engine"></a>Verbindung mit Server herstellen (Datenbank-Engine)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Verwenden Sie dieses Dialogfeld, um Optionen für Verbindungen mit Computern mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]anzuzeigen oder anzugeben. In den meisten Fällen können Sie eine Verbindung herstellen, indem Sie im Feld **Servername** den Computernamen des Datenbankservers eingeben und dann auf **Verbinden**klicken. Wenn Sie eine Verbindung mit einer benannte Instanz herstellen, verwenden Sie den Computernamen, gefolgt von einem umgekehrten Schrägstrich und dem Namen der Instanz. Beispiel: `mycomputer\myinstance`. Geben Sie beim Herstellen der Verbindung mit [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]den Computernamen gefolgt von **\sqlexpress**an.  
  
Viele Faktoren können Auswirkungen auf die Fähigkeit zum Herstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]haben. Hilfe finden Sie in den folgenden Artikeln:  
- [Lektion 1: Herstellen einer Verbindung mit der Datenbank-Engine](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [Beheben von Verbindungsfehlern mit der SQL Server-Datenbank-Engine](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [Solving Connectivity errors to SQL Server (Lösen von Verbindungsproblemen in SQL Server)](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)   
  
## <a name="options"></a>Tastatur  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem die Verbindung hergestellt werden soll: [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]oder [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über „Registrierte Server“ registrieren, ist das Feld **Servertyp** schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente „Registrierte Server“ angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste Registrierte Server [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)]oder [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] aus, bevor Sie mit der Registrierung eines neuen Servers beginnen.  
  
**Servername**  
Wählen Sie die Serverinstanz aus, mit der eine Verbindung hergestellt werden soll. Standardmäßig wird die Serverinstanz angezeigt, mit der zuletzt eine Verbindung bestanden hat.  
  
> [!NOTE]  
> Um eine Verbindung mit einer aktiven Benutzerinstanz von [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] mit dem Named Pipes-Protokoll herzustellen, geben Sie den Pipenamen an, z.B. `np:\\.\pipe\3C3DF6B1-2262-47\tsql\query`. Weitere Informationen finden Sie in der Dokumentation zu [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].  
  
**Authentifizierung**  
Die aktuelle Version von SSMS stellt fünf verschiedene Authentifizierungsmodi beim Verbinden mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde_md.md)] bereit. Wenn das Authentifizierungsdialogfeld nicht mit der folgenden Liste übereinstimmt, laden Sie die aktuellste Version von SSMS unter [Herunterladen von SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) herunter.  

  
  > **Windows-Authentifizierung**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Der Windows Authentifizierungsmodus ermöglicht Benutzern die Verbindung über ein Windows-Benutzerkonto.  
  
  > **SQL Server-Authentifizierung**  
  > Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Authentifizierung durch, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn kein Anmeldekonto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingerichtet wurde, schlägt die Authentifizierung fehl, und der Benutzer erhält eine Fehlermeldung. Verwenden Sie nach Möglichkeit die Windows-Authentifizierung oder die Active Directory-Kennwortauthentifizierung.  

  > **Active Directory: Universell mit MFA-Unterstützung**  
Universelle Active Directory-Authentifizierung mit MFA ist ein interaktiver Workflow, in dem Azure Multi-Factor Authentication (MFA) unterstützt wird. Azure MFA bietet Schutz für den Zugriff auf Daten sowie Anwendungen und erfüllt gleichzeitig Benutzeranforderungen nach einem einfachen Anmeldevorgang. MFA stellt strenge Authentifizierung mit einigen einfachen Überprüfungsoptionen bereit (Telefonanruf, SMS, Smartcards mit PIN oder eine Benachrichtigung über mobile App), sodass Benutzer die von ihnen bevorzugte Methode auswählen können. Ist ein Benutzerkonto für MFA konfiguriert, ist für den interaktiven Authentifizierungswokflow eine zusätzliche Benutzerinteraktion über Popupdialogfelder, Verwenden von Smartcards usw. erforderlich. Ist ein Benutzerkonto für MFA konfiguriert, muss der Benutzer die Option für universelle Azure-Authentifizierung auswählen, um eine Verbindung herzustellen. Erfordert das Benutzerkonto keine MFA, kann der Benutzer weiterhin die beiden anderen Azure Active Directory-Authentifizierungsoptionen verwenden. Weitere Informationen hierzu finden Sie unter [SSMS-Unterstützung für Azure AD MFA mit SQL-Datenbank und SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Falls nötig können Sie die Domäne ändern, die die Anmeldung authentifiziert, indem Sie auf **Optionen** und dann auf die Registerkarte **Verbindungseigenschaften** klicken und anschließend das Feld **AD-Domänenname oder Mandanten-ID** ausfüllen.  

  > **Active Directory: Kennwort**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden.  Verwenden Sie diese Methode zum Herstellen von Verbindungen mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)], wenn Sie bei Windows mit Anmeldeinformationen aus einer Domäne angemeldet sind, die nicht mit Azure verbunden ist, oder wenn die Azure AD-Authentifizierung mithilfe von Azure AD auf Basis der ursprünglichen oder der Clientdomäne verwendet wird. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
  > **Active Directory – Integriert**  
Azure Active Directory-Authentifizierung ist ein Mechanismus zum Herstellen einer Verbindung mit [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] , wozu Identitäten in Azure Active Directory (Azure AD) verwendet werden. Verwenden Sie die Methode zum Verbinden mit [!INCLUDE[ssSDS](../../includes/sssds-md.md)], wenn Sie bei Windows mit Ihren Azure AD-Anmeldeinformationen aus einer Verbunddomäne angemeldet sind. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL-Datenbank unter Verwendung der Azure Active Directory-Authentifizierung](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**User name**  
Der Windows-Benutzername zum Herstellen der Verbindung. Diese Option ist nur verfügbar, wenn Sie **Active Directory-Kennwortauthentifizierung**ausgewählt haben, um eine Verbindung herzustellen. Sie ist schreibgeschützt, wenn Sie die Authentifizierungen **Windows-Authentifizierung** oder **Active Directory – Integriert** auswählen.  
  
**Anmeldename**  
Geben Sie den Anmeldenamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung oder die Active Directory-Kennwortauthentifizierung ausgewählt haben, um eine Verbindung herzustellen.  
  
**Kennwort**  
Geben Sie das Kennwort für die Anmeldung ein. Diese Option ist nur bearbeitbar, wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung oder die Active Directory-Kennwortauthentifizierung ausgewählt haben, um eine Verbindung herzustellen.  
  
**Verbinden**  
Klicken Sie darauf, um eine Verbindung mit dem Server herzustellen.  
  
**Optionen**  
Klicken Sie darauf, um die **Verbindungseigenschaften** und die Registerkarte **Zusätzliche Verbindungsparameter** anzuzeigen.  
  
