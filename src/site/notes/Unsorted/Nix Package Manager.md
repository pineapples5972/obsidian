---
{"dg-publish":true,"permalink":"/unsorted/nix-package-manager/"}
---

<h1 style="color: Pink"><img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fnixos.org%2Flogo%2Fnixos-logo-only-hires.png&f=1&nofb=1&ipt=883160bc005dc414d932d26eb43680388cf6614f22d56b5c4cc3f1341f9ee1cf&ipo=images&f=1&h=30" style="margin: 0"> Nix Package Manger Basics</h1>

#### Packages
search available packages
`nix --extra-experimental-features "nix-command flakes" search nixpkgs firefox`
`nix-env -qaP`

Install new package
`nix-env -iA nixpkgs.gimp`

delete package
`nix-env -e gimp`

list installed packages
`nix-env -q`
#### generations
list generations
`nix-env --list-generations`

switch generations
`nix-env --switch-generation 50`

delete generation
`nix-env --delete-generations old`

delete specific generations
 `nix-env --delete-generations 10 11 14`

delete generation older than specific number of days
`nix-env --delete-generations 14d`

#### Garbage Collection (cleanup)
After removing appropriate old generations you can run the garbage collector as follows:
 `nix-store --gc`

If you are feeling uncertain, you can also first view what files would be deleted:

 `nix-store --gc --print-dead`

Likewise, the option `--print-live` will show the paths that _won’t_ be deleted.

There is also a convenient little utility `nix-collect-garbage`, which when invoked with the `-d` (`--delete-old`) switch deletes all old generations of all profiles in `/nix/var/nix/profiles`. So

```console
 nix-collect-garbage -d
```

is a quick and easy way to clean up your system.

