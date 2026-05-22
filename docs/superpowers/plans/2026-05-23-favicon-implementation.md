# Внедрение Фавикона Софии Агачер Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Генерация и интеграция полноценного набора фавиконов на основе утвержденной монограммы «СА» для личного сайта писателя Софии Агачер.

**Architecture:** Использование встроенных .NET средств в Windows PowerShell для создания высококачественных ресайзов исходного изображения в 512x512, 180x180, 32x32 и 16x16 PNG файлы, а также добавление необходимых `<link>` метатегов в заголовок `index.html`.

**Tech Stack:** PowerShell, .NET (System.Drawing), HTML5.

---

### Task 1: Генерация файлов фавиконов различных размеров

**Files:**
- Create: `favicon.png` (512x512)
- Create: `apple-touch-icon.png` (180x180)
- Create: `favicon-32x32.png` (32x32)
- Create: `favicon-16x16.png` (16x16)

- [ ] **Step 1: Создать PowerShell-скрипт для генерации иконки**
  Создать временный скрипт генерации `generate-favicons.ps1` в директории `.superpowers/brainstorm/` с кодом высококачественного ресайза через .NET `System.Drawing.Graphics`.

  Код скрипта:
  ```powershell
  Add-Type -AssemblyName System.Drawing
  function Resize-Image {
      param (
          [string]$InputPath,
          [string]$OutputPath,
          [int]$Width,
          [int]$Height
      )
      $src = [System.Drawing.Image]::FromFile($InputPath)
      $dest = New-Object System.Drawing.Bitmap($Width, $Height)
      $g = [System.Drawing.Graphics]::FromImage($dest)
      $g.InterpolationMode = [System.Drawing.Drawing2D.InterpolationMode]::HighQualityBicubic
      $g.DrawImage($src, 0, 0, $Width, $Height)
      $dest.Save($OutputPath, [System.Drawing.Imaging.ImageFormat]::Png)
      $g.Dispose()
      $dest.Dispose()
      $src.Dispose()
  }

  $srcPath = "d:\myyan\Yandex.Disk\www-yandex\Сайт-визитка для писателя Софии Агачер\.superpowers\brainstorm\content\elegant_monogram_icon.png"
  $rootPath = "d:\myyan\Yandex.Disk\www-yandex\Сайт-визитка для писателя Софии Агачер"

  Resize-Image -InputPath $srcPath -OutputPath "$rootPath\favicon.png" -Width 512 -Height 512
  Resize-Image -InputPath $srcPath -OutputPath "$rootPath\apple-touch-icon.png" -Width 180 -Height 180
  Resize-Image -InputPath $srcPath -OutputPath "$rootPath\favicon-32x32.png" -Width 32 -Height 32
  Resize-Image -InputPath $srcPath -OutputPath "$rootPath\favicon-16x16.png" -Width 16 -Height 16
  Write-Host "Все фавиконы успешно сгенерированы!"
  ```

- [ ] **Step 2: Запустить скрипт генерации**
  Run: `powershell -File "d:\myyan\Yandex.Disk\www-yandex\Сайт-визитка для писателя Софии Агачер\.superpowers\brainstorm\generate-favicons.ps1"`
  Expected output: "Все фавиконы успешно сгенерированы!"

- [ ] **Step 3: Проверить физическое наличие файлов**
  Убедиться, что файлы `favicon.png`, `apple-touch-icon.png`, `favicon-32x32.png` и `favicon-16x16.png` созданы в корне сайта.
  Run: `Test-Path "d:\myyan\Yandex.Disk\www-yandex\Сайт-визитка для писателя Софии Агачер\favicon.png"` (должно вернуть True).

- [ ] **Step 4: Зафиксировать изменения в коммите**
  ```bash
  git add favicon.png apple-touch-icon.png favicon-32x32.png favicon-16x16.png
  git commit -m "feat: add generated favicon assets in multiple sizes"
  ```

---

### Task 2: Интеграция метатегов фавикона в index.html

**Files:**
- Modify: `index.html` (добавление `<link>` тегов в раздел `<head>`)

- [ ] **Step 1: Добавить метатеги в head секцию index.html**
  Внедрить в `index.html` (ориентировочно в районе строк 2-5, перед `<title>`) следующие строки:
  ```html
  <link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">
  <link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
  <link rel="icon" type="image/png" sizes="512x512" href="favicon.png">
  ```

- [ ] **Step 2: Проверить корректность форматирования HTML**
  Убедиться, что в `index.html` нет синтаксических ошибок, теги закрыты и не нарушена верстка.

- [ ] **Step 3: Зафиксировать изменения в коммите**
  ```bash
  git add index.html
  git commit -m "feat: link favicon files in index.html head"
  ```

---

### Task 3: Верификация работы фавикона

**Files:**
- Test: `index.html` в веб-интерфейсе

- [ ] **Step 1: Проверить локально в браузере**
  Открыть `index.html` напрямую в браузере или через локальный веб-сервер и убедиться, что вкладка отображает золотую монограмму «СА» на темно-синем фоне.

- [ ] **Step 2: Удалить временный скрипт генерации**
  Run: `Remove-Item "d:\myyan\Yandex.Disk\www-yandex\Сайт-визитка для писателя Софии Агачер\.superpowers\brainstorm\generate-favicons.ps1"`
