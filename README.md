# SoftwareInstaller - instalacja programów jednym poleceniem

Skrypt PowerShell do przygotowania komputera dla nowego pracownika.
Zamiast ręcznie pobierać i klikać instalatory, technik wybiera **zestaw programów**
(np. dla biura albo działu IT) i uruchamia jedną komendę. Instalacja odbywa się
w tle przez **winget**, oficjalny menedżer pakietów Windows.

## Funkcje

- Zestawy programów zdefiniowane w pliku [`apps.json`](apps.json): **Podstawowy**, **Biuro**, **IT**
- Pomijanie programów, które są już zainstalowane
- Cicha instalacja (bez okien i klikania „Dalej”)
- Pasek postępu i podsumowanie w tabeli
- Log instalacji do analizy błędów (`logs\`)
- Tryb `-WhatIf`: pokazuje, co zostałoby zainstalowane

## Użycie

```powershell
# Lista dostępnych zestawów
.\Install-Software.ps1 -ListPresets

# Podgląd: co zostanie zainstalowane
.\Install-Software.ps1 -Preset Biuro -WhatIf

# Instalacja zestawu
.\Install-Software.ps1 -Preset IT
```

## Własny zestaw

Wystarczy dopisać zestaw do `apps.json`. Identyfikator programu można znaleźć poleceniem:

```powershell
winget search "nazwa programu"
```

```json
"Grafika": [
  { "name": "GIMP", "id": "GIMP.GIMP" },
  { "name": "Paint.NET", "id": "dotPDN.PaintDotNet" }
]
```

## Przykładowy wynik

```
=== Instalacja zestawu 'Podstawowy' (programów: 4) ===

[1/4] Google Chrome               Już zainstalowany
[2/4] 7-Zip                       Zainstalowano (18 s)
[3/4] Adobe Acrobat Reader        Zainstalowano (74 s)
[4/4] VLC media player            Zainstalowano (22 s)
```

## Wymagania

- Windows 10 (1809+) / 11 z zainstalowanym **winget** (App Installer)
- Niektóre programy wymagają uprawnień administratora (pojawi się okno UAC)

## Wykorzystane umiejętności

- Automatyzacja wdrażania stanowisk pracy (onboarding pracownika)
- Menedżer pakietów `winget` i obsługa kodów wyjścia programów zewnętrznych
- Konfiguracja w JSON oddzielona od logiki skryptu
