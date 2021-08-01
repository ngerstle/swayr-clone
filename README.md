# Nix flake for Swayr (a window switcher (and more) for sway)

See  [https://todo.sr.ht/~tsdh/swayr](https://todo.sr.ht/~tsdh/swayr).

This is a flake to provide the package for nixos systems using flakes.

To use with nixos system flake, add the following to /etc/nixos/flake.nix:
`    swayr.url = "github:ngerstle/swayr-clone";` to `inputs`;
define an overlay in the output section, after adding `swayr` as an input: 
```
    let
      swayr-overlay = (final: prev: { swayr = swayr.packages.${prev.system}.swayr; });
    in
```
then apply the overlay in your system:
```
    nixosConfigurations.SOMEHOST = nixpkgs.lib.nixosSystem {
   
      modules = [
        { nixpkgs.overlays = [ swayr-overlay ]; }
        ./configuration.nix
```

It can then be accessed in configuration.nix/home-manger/etc using the standard `pkgs.swayr`
