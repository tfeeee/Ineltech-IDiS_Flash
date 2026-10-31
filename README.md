# Ineltech IDiS Flash

Windows x64 releases of Ineltech IDiS Flash. This repository distributes installers only; application source code is maintained in a separate repository.

## Slovenčina

### Inštalácia

1. Otvor [najnovší release](https://github.com/tfeeee/Ineltech-IDiS_Flash/releases/latest).
2. Stiahni `IDiS_Flash_Setup_<verzia>_x64.exe` a zodpovedajúci `.sha256` súbor.
3. Pred spustením over SHA-256 v PowerShelli:

   ```powershell
   $installer = '.\IDiS_Flash_Setup_<verzia>_x64.exe'
   $expected = (Get-Content "$installer.sha256").Split(' ')[0]
   $actual = (Get-FileHash $installer -Algorithm SHA256).Hash.ToLowerInvariant()
   if ($actual -ne $expected) { throw 'SHA-256 nesúhlasí' }
   ```

4. Spusti inštalátor. Windows môže vyžiadať potvrdenie UAC, pretože aplikácia sa inštaluje do `Program Files`.

### Aktualizácie

Aplikácia kontroluje GitHub Releases pri štarte a umožňuje kontrolu aj cez tlačidlo **Aktualizácie**. Pred inštaláciou zobrazí poznámky k vydaniu; používateľ aktualizáciu potvrdí. Stiahnutý inštalátor sa overí podľa SHA-256 digestu z GitHub API a nespustí sa, ak kontrola zlyhá. Aktualizácia môže vyžiadať UAC.

Používateľské konfigurácie, logy a výsledky v AppData zostávajú pri aktualizácii zachované.

## English

### Installation

1. Open the [latest release](https://github.com/tfeeee/Ineltech-IDiS_Flash/releases/latest).
2. Download `IDiS_Flash_Setup_<version>_x64.exe` and its matching `.sha256` file.
3. Verify the SHA-256 checksum in PowerShell before running the installer:

   ```powershell
   $installer = '.\IDiS_Flash_Setup_<version>_x64.exe'
   $expected = (Get-Content "$installer.sha256").Split(' ')[0]
   $actual = (Get-FileHash $installer -Algorithm SHA256).Hash.ToLowerInvariant()
   if ($actual -ne $expected) { throw 'SHA-256 mismatch' }
   ```

4. Run the installer. Windows may request UAC approval because the application installs under `Program Files`.

### Updates

The application checks GitHub Releases at startup and also provides a manual **Updates** action. It displays the release notes and asks before installing. The downloaded installer is verified against the SHA-256 digest from the GitHub API and is not launched if verification fails. UAC approval may be required.

User configurations, logs, and results stored in AppData are preserved during updates.