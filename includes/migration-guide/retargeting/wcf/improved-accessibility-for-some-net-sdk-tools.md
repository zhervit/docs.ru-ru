---
ms.openlocfilehash: 79005f19ac31ba32e7e468ef61eb867a052eff40
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858982"
---
### <a name="improved-accessibility-for-some-net-sdk-tools"></a>Улучшенные специальные возможности для некоторых средств пакета SDK для .NET

|   |   |
|---|---|
|Подробные сведения|В пакете SDK .NET Framework 4.7.1 в средствах SvcConfigEditor.exe и SvcTraceViewer.exe были устранены различные проблемы со специальными возможностями. В основном это были незначительные проблемы, например не определялось имя или некорректно реализовывались шаблоны автоматизации пользовательского интерфейса. Многие пользователи могли не замечать неверные значения, но пользователям, использующим вспомогательные технологии, такие как средства чтения с экрана, будет проще использовать эти средства пакета SDK. Безусловно, эти исправления влияют на предыдущее поведение, например порядок фокуса клавиатуры. Чтобы получить все исправления специальных возможностей в этих средствах, выполните следующее в файле app.config:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.UseLegacyAccessibilityFeatures=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Область|Пограничный случай|
|Версия|4.7.1|
|Тип|Изменение целевой платформы|

