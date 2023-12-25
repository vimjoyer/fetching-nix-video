## Fake hash

```nix
sha256-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=
```

## Nurl 
```nix
nix shell nixpkgs#nurl
nurl "https://github.com/vimjoyer/flake-starter-config"
```
or use nix run

## Fetching flake example
```nix
{
  description = "flake";

  inputs = {
    nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";

    somefile = {
      url = "https://somewebsite/somefile.png";
      flake = false;
    };
  };

  outputs = { ... }@inputs:
    let
      system = "x86_64-linux";
      pkgs = inputs.nixpkgs.legacyPackages.\${system};
    in
    {
      packages.${system}.default = pkgs.writeShellScriptBin "example" ''
        echo "${inputs.somefile}"
      '';
    };
}
```
