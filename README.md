## Fake hash

```nix
"sha256-AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA="
# or instead of learning it, use
pkgs.lib.fakeHash
```

## Nurl 

```bash
nix shell nixpkgs#nurl
nurl "https://github.com/vimjoyer/flake-starter-config"
# or use nix run
nix run nixpkgs#nurl -- "https://github.com/vimjoyer/flake-starter-config"
```

`nurl` will output:

```nix
fetchFromGitHub {
  owner = "vimjoyer";
  repo = "flake-starter-config";
  rev = "55521689415027356800947e91690271be4a1c10";
  hash = "sha256-SgQdHZMpqbC2k8ZQg0PvYY8OnsNRBYVgXS+dQX5pqkU=";
}
```

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
