---
title: Migrieren der Konfiguration
author: ardalis
description: 
keywords: ASP.NET Core
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 8468d859-ff32-4a92-9e62-08c4a9e36594
ms.technology: aspnet
ms.prod: asp.net-core
uid: migration/configuration
ms.openlocfilehash: 62660f7e58467a69f540966df188747b6fde57fe
ms.sourcegitcommit: 9cdbfd0d670d70b9c354216aabee260c52dad5ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2017
---
# <a name="migrating-configuration"></a>Migrieren der Konfiguration

Durch [Steve Smith](https://ardalis.com/) und [Scott Addie](https://scottaddie.com)

In der vorherigen Artikel wir begann [Migrieren eines ASP.NET MVC-Projekts zu ASP.NET Core MVC](mvc.md). In diesem Artikel wir die Konfiguration migrieren.

[Anzeigen oder Herunterladen von Beispielcode](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples)

## <a name="setup-configuration"></a>Setup-Konfiguration

ASP.NET Core wird nicht mehr verwendet, die *"Global.asax"* und *"Web.config"* Dateien, die frühere Versionen von ASP.NET verwendet. In früheren Versionen von ASP.NET Startlogik für die Anwendung im positioniert wurde ein `Application_StartUp` Methode innerhalb *"Global.asax"*. Später werden Sie in ASP.NET MVC eine *Startup.cs* Datei im Stammverzeichnis des Projekts; enthalten war, und es wurde aufgerufen, wenn die Anwendung gestartet. ASP.NET Core hat dieser Ansatz vollständig von übernommen platzieren Startlogik für alle in der *Startup.cs* Datei.

Die *"Web.config"* Datei auch in ASP.NET Core ersetzt wurde. Konfiguration selbst kann nun konfiguriert werden, und als Teil der Schritte beim Starten einer Anwendung in beschriebenen *Startup.cs*. Konfiguration kann XML-Dateien weiterhin nutzen, sondern in der Regel ASP.NET Core Projekte werden platzieren Konfigurationswerte in einer JSON-formatierten Datei wie z. B. *appsettings.json*. ASP.NET-Core-Konfigurationssystem kann leicht Umgebungsvariablen, zugreifen, die einen Speicherort im sicheren und stabilen für umgebungsspezifische Werte angeben können. Dies gilt insbesondere für geheime Schlüssel, wie z. B. Verbindungszeichenfolgen und API-Schlüssel, die nicht in die quellcodeverwaltung überprüft werden sollen. Finden Sie unter [Konfiguration](../fundamentals/configuration.md) Weitere Informationen zur Konfiguration in ASP.NET Core.

Für diesen Artikel beginnen wir mit dem teilweise migriert ASP.NET Core-Projekt aus [vorherigen Artikel](mvc.md). Zum Einrichten des Konfiguration fügen die folgenden Konstruktor und die Eigenschaft, um die *Startup.cs* Datei befindet sich im Stammverzeichnis des Projekts:

[!code-csharp[Main](configuration/samples/WebApp1/src/WebApp1/Startup.cs?range=11-21)]

Beachten Sie, dass an diesem Punkt der *Startup.cs* Datei wird nicht kompiliert werden, da wir benötigen Sie Folgendes hinzufügen `using` Anweisung:

```csharp
using Microsoft.Extensions.Configuration;
```

Hinzufügen einer *appsettings.json* Datei im Stammverzeichnis des Projekts mit der entsprechenden Elementvorlage:

![Hinzufügen von "appSettings" JSON](configuration/_static/add-appsettings-json.png)

## <a name="migrate-configuration-settings-from-webconfig"></a>Migrieren von Konfigurationseinstellungen aus der Datei "Web.config"

Unsere ASP.NET MVC-Projekt enthielt, die erforderliche Datenbank-Verbindungszeichenfolge in *"Web.config"*in die `<connectionStrings>` Element. In unserem Projekt ASP.NET Core Kegel zum Speichern dieser Informationen in den *appsettings.json* Datei. Open *appsettings.json*, und beachten Sie, dass sie bereits die Folgendes umfasst:

[!code-json[Main](../migration/configuration/samples/WebApp1/src/WebApp1/appsettings.json?highlight=4)]


In der markierten Zeile in der oben dargestellten, ändern Sie den Namen der Datenbank von **_CHANGE_ME** auf den Namen der Datenbank.

## <a name="summary"></a>Zusammenfassung

ASP.NET Core setzt alle Startlogik für die Anwendung in eine einzelne Datei, in der die erforderlichen Dienste und Abhängigkeiten definiert und konfiguriert werden können. Er ersetzt die *"Web.config"* Datei in eine flexible Konfiguration-Funktion, die eine Vielzahl von Dateiformaten wie JSON sowie Umgebungsvariablen nutzen können.
