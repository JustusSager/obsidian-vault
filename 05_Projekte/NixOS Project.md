Bei NixOS werden alle Änderungen am Basis OS über verschiedene Konfigurationsdateien gemacht. Das schließt z.B. auch das installieren von Software ein.

Die Basisdatei liegt unter:
`/etc/nixos/configuration.nix`

NixOS Configuration neu laden:
``` bash
// neu laden und direkt starten
nixos-rebuild switch --use-remote-sudo

// neu laden und als test starten
// reboot setzt configuration zurück
nixos-rebuild test --use-remote-sudo

// beim nächsten reboot neu laden
nixos-rebuild boot --use-remote-sudo
```

# Desktop Umgebung
Zu einer Desktop-Umgebung gehören viele Komponenten die man bei anderen Betriebssystemen gar nicht beachtet und als selbstverständlich wahrnimmt. Hier einmal aufgelistet welche Komponenten noch händisch mitinstalliert werden müssen und welche Alternativen es so gibt.

## Terminal
Als erstes Terminal (und standardmäßig auch vorkonfiguriert) habe ich `kitty` ausprobiert. Jedoch fanden meine ersten Versuche in einer VM statt (was ich mit NixOS und Hyprland nicht empfehlen kann) und dort gab es mit `kitty` Probleme mit den 3D-Graphiken die dabei verlangt werden. Daher habe ich mich als Grundlage erstmal für `foot` entschieden, da es bereits in der VM funktionierte und bisher alles erfüllt was ich von einer Konsole gerne hätte.
## Terminal Text Editor
Hier habe ich folgende installiert:
- nano (ist bei NixOS standardmäßig vorkonfiguriert)
- vim
## File Manager
Hier habe ich folgende ausprobiert:
- `dolphin` (ist bei NixOS standardmäßig vorkonfiguriert)
#TODO hier vervollständigen
## App-Launcher

## Task Bar
Als Task/Status-Bar verwende ich `waybar`.
## Copy-Paste

## Web Browser

## Logout / Shutdown GUI
#TODO noch konfigurieren
- `wlogout`
- 

## Notification Daemon
Manche Apps wie Discord stürzen ab, wenn kein (mit dieser App) kompatibler Notification Daemon installiert und aktiviert ist.

Hierfür verwende ich `mako`, jedoch muss sich noch zeigen, ob es den Zweck erfüllt.


# Hyprland nach der Anmeldung mit tty1 ausführen
https://www.youtube.com/watch?v=fmFjV3_iIn0&t=465s (9:00 Min)
``` bash
echo '[[ "$(tty)" == "/dev/tty1" ]] && exec Hyprland' >~.bash_profile
```

# Flakes 
#TODO Was sind Flakes und warum musste ich es aktivieren?
https://drakerossman.com/blog/how-to-convert-default-nixos-to-nixos-with-flakes

## Flakes aktivieren:
Eine neue Datei anlegen:
`/etc/nixos/flake.nix`
mit folgendem Inhalt:
``` bash
{
  description = "flake for yourHostNameGoesHere";

  inputs = {
    nixpkgs = {
      url = "github:NixOS/nixpkgs/nixos-unstable";
    };
  };

  outputs = { self, nixpkgs }: {
    nixosConfigurations = {
      yourHostNameGoesHere = nixpkgs.lib.nixosSystem {
        system = "x86_64-linux";
        modules = [
          ./configuration.nix
        ];
      };
    };
  };
}
```
`yourHostNameGoesHere` ersetzen durch den entsprechenden Hostname, zu finden unter `/etc/nixos/configuration.nix`

Oben in der `/etc/nixos/configuration.nix` folgendes einfügen (innerhalb der äußersten geschweiften Klammern)
``` bash
nix = {
  package = pkgs.nixFlakes;
  extraOptions = ''
    experimental-features = nix-command flakes
  '';
};
```

Mit folgendem neu laden (mit sudo, während man in `/etc/nixos` ist)
`nixos-rebuild --flake .#yourHostNameGoesHere switch`
Hier auf das `.#` vor dem `yourHostNameGoesHere` achten. `.#` muss stehen bleiben

## Flakes aktualisieren
``` bash
// Flakes aktualisieren
// muss in '/etc/nixos' ausgeführt werden
nix flake update
```